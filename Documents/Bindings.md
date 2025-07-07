## Introduction

Bindings are utilized throughout computing. They are utilized for [function invocations](https://en.wikipedia.org/wiki/Function_(computer_programming)), [remote procedure calls](https://en.wikipedia.org/wiki/Remote_procedure_call), [input forms](https://en.wikipedia.org/wiki/HTML_form), [templates](https://en.wikipedia.org/wiki/Template_processor), and [inference rules](https://en.wikipedia.org/wiki/Rule_of_inference).

Beyond [type systems](https://en.wikipedia.org/wiki/Type_system), [guard clauses](https://en.wikipedia.org/wiki/Guard_(computer_science)), and related [design by contract](https://en.wikipedia.org/wiki/Design_by_contract) approaches, these assuring that provided values meet specified constraints and criteria, what if the binding of values to parameters could be justified, could be argued, to convince one or more artificial-intelligence agents that the values were valid?

This would enable new levels of expressiveness for declaring functions and their parameters, remote procedures and their parameters, input forms and their fields, templates and their parameters, and inference rules. Software developers and artificial-intelligence agents would be able to justify, to argue, that values were valid and other artificial-intelligence agents would be able to evaluate these arguments.

## A Simple Argument Model

> [!TIP]
> For illustration purposes, here is a simple argument model.
> 
> ```cs
> public interface IArgumentGenerator : IJustifiableGenerator<IArgument> { }
> 
> public interface IArgument : IJustifiableGenerated<IArgumentGenerator>
> {
>     IEnumerable<object> Conclusions { get; }
>     IEnumerable<object> Rules { get; }
>     IEnumerable<IArgument> Premises { get; }
> }
> ```

## A Supporting Model

> [!TIP]
> Here is a supporting model that can work with many argument models.
> 
> ```cs
> public interface IBinding
> {
>     Parameter Parameter { get; }
> 
>     object Value { get; }
> }
> 
> public interface IGenerator<out TGENERATED>
> {
>     IReadOnlyList<Parameter> Parameters { get; }
> 
>     IBinding Bind(Parameter parameter, object value);
> 
>     TGENERATED Apply(IEnumerable<IBinding> bindings);
> }
> 
> public interface IGenerated<out TGENERATOR>
> {
>     TGENERATOR Generator { get; }
> 
>     IReadOnlyList<IBinding> Bindings { get; }
> }
> 
> public interface IJustifiableGenerator<out TGENERATED> : IGenerator<TGENERATED>
> {
>     IReadOnlyList<IArgumentGenerator> Preconditions { get; }
> 
>     TGENERATED Apply(IEnumerable<IBinding> bindings, IEnumerable<IArgument> justifications);
> }
> 
> public interface IJustifiableGenerated<out TGENERATOR> : IGenerated<TGENERATOR>
> {
>     IReadOnlyList<IArgument> Justifications { get; }
> }
> ```

## A Function Model

> [!TIP]
> Here is a function model utilizing that supporting model indicated above.
> 
> ```cs
> public interface IFunction : IGenerator<IExecutable>
> {
>     IReadOnlyList<Parameter> OutputParameters { get; }
> 
>     public string Name { get; }
> 
>     public string Description { get; }
> 
>     public IEnumerable<string> Tags { get; }
> 
>     public IEnumerable<string> Examples { get; }
> }
> 
> public interface IExecutable : IGenerated<IFunction>
> {
>     public Task<IEnumerable<IBinding>> Execute();
> }
> 
> public interface IJustifiableFunction : IJustifiableGenerator<IJustifiableExecutable>
> {
>     IReadOnlyList<Parameter> OutputParameters { get; }
> 
>     IReadOnlyList<IArgumentGenerator> Postconditions { get; }
> 
>     public string Name { get; }
> 
>     public string Description { get; }
> 
>     public IEnumerable<string> Tags { get; }
> 
>     public IEnumerable<string> Examples { get; }
> }
> 
> public interface IJustifiableExecutable : IJustifiableGenerated<IJustifiableFunction>
> {
>     public Task<(IEnumerable<IBinding> Bindings, IEnumerable<IArgument> Justifications)> Execute();
> }
> ```

## Extension Methods Utilizing The Function Model

> [!TIP]
> Here are some extension methods utilizing the function model. An `Invoke()` extension method is provided for `IFunction` and `IJustifiableFunction`.
> 
> ```cs
> public static class Extensions
> {
>     public static async Task<IEnumerable<IBinding>> Invoke(this IFunction function, object[] args)
>     {
>         int n = args.Length;
> 
>         if (n != function.Parameters.Count)
>         {
>             throw new ArgumentException($"The number of arguments when invoking {function.Name} must be {function.Parameters.Count} but {n} were provided.");
>         }
> 
>         List<IBinding> bindings = new List<IBinding>();
> 
>         for (int index = 0; index < n; ++index)
>         {
>             bindings.Add(function.Bind(function.Parameters[index], args[index]));
>         }
> 
>         return await function.Apply(bindings).Execute();
>     }
> 
>     public static async Task<(IEnumerable<IBinding> Bindings, IEnumerable<IArgument> Justifications)> Invoke(this IJustifiableFunction function, object[] args, bool auto = true)
>     {
>         int n = args.Length;
> 
>         if (n != function.Parameters.Count)
>         {
>             throw new ArgumentException($"The number of arguments when invoking {function.Name} must be {function.Parameters.Count} but {n} were provided.");
>         }
> 
>         List<IBinding> bindings = new List<IBinding>();
>         List<IArgument> justifications = new List<IArgument>();
> 
>         for (int index = 0; index < n; ++index)
>         {
>             bindings.Add(function.Bind(function.Parameters[index], args[index]));
>         }
> 
>         if (auto)
>         {
>             foreach (var precondition in function.Preconditions)
>             {
>                 if (!precondition.Parameters.All(x => function.Parameters.Contains(x)))
>                 {
>                     throw new Exception("Could not auto-create justifications for parameter value bindings. At least one of the function's preconditions involves a parameter not in the function's signature.");
>                 }
>                 justifications.Add(precondition.Apply(bindings));
>             }
> 
>             return await function.Apply(bindings, justifications).Execute();
>         }
>         else
>         {
>             return await function.Apply(bindings).Execute();
>         }
>     }
> 
>     public static async Task<(IEnumerable<IBinding> Bindings, IEnumerable<IArgument> Justifications)> Invoke(this IJustifiableFunction function, object[] args, IArgument[] justifications)
>     {
>         int n = args.Length;
> 
>         if (n != function.Parameters.Count)
>         {
>             throw new ArgumentException($"The number of arguments when invoking {function.Name} must be {function.Parameters.Count} but {n} were provided.");
>         }
> 
>         List<IBinding> bindings = new List<IBinding>();
> 
>         for (int index = 0; index < n; ++index)
>         {
>             bindings.Add(function.Bind(function.Parameters[index], args[index]));
>         }
> 
>         return await function.Apply(bindings, justifications).Execute();
>     }
> }
> ```

## Conclusion

Bindings are utilized throughout computing. They are utilized for function invocations, remote procedure calls, input forms, templates, and inference rules. As was shown above, the validity of values can be argued by software developers and artificial-intelligence agents and these arguments could be evaluated by artificial-intelligence agents.
