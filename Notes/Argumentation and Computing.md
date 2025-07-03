## Introduction

Bindings are utilized throughout computing. They are utilized for [function invocations](https://en.wikipedia.org/wiki/Function_(computer_programming)), [remote procedure calls](https://en.wikipedia.org/wiki/Remote_procedure_call), [input forms](https://en.wikipedia.org/wiki/HTML_form), [templates](https://en.wikipedia.org/wiki/Template_processor), and [inference rules](https://en.wikipedia.org/wiki/Rule_of_inference).

Beyond [type systems](https://en.wikipedia.org/wiki/Type_system), [guard clauses](https://en.wikipedia.org/wiki/Guard_(computer_science)), and [design by contract](https://en.wikipedia.org/wiki/Design_by_contract) approaches, these assuring that provided values meet certain constraints and criteria, what if the binding of values to parameters could be justified, could be argued, to convince one or more artificial-intelligence agents that the values were valid?

This would enable a new level of expressiveness when declaring functions and their parameters, remote procedures and their parameters, input forms and their fields, templates and their parameters, and inference rules. Software developers and artificial-intelligence agents would be able to justify, or to argue, that values were valid and other artificial-intelligence agents would be able to evaluate these arguments.

## A Model

```cs
public interface IBinding
{
    Parameter Parameter { get; }

    object Value { get; }
}

public interface IGenerator<out TGENERATED>
{
    IReadOnlyList<Parameter> Parameters { get; }

    IBinding Bind(Parameter parameter, object value);

    TGENERATED Apply(IEnumerable<IBinding> bindings);
}

public interface IGenerated<out TGENERATOR>
{
    TGENERATOR Generator { get; }

    IReadOnlyList<IBinding> Bindings { get; }
}

public interface IJustifiableGenerator<out TGENERATED> : IGenerator<TGENERATED>
{
    IReadOnlyList<IArgumentGenerator> Preconditions { get; }

    TGENERATED Apply(IEnumerable<IBinding> bindings, IEnumerable<IArgument> justifications);
}

public interface IJustifiableGenerated<out TGENERATOR> : IGenerated<TGENERATOR>
{
    IReadOnlyList<IArgument> Arguments { get; }
}

public interface IArgument : IJustifiableGenerated<IArgumentGenerator>
{
    object Claim { get; }
}

public interface IArgumentGenerator : IJustifiableGenerator<IArgument> { }

public interface IExecutable : IGenerated<IFunction>
{
    public Task<IEnumerable<IBinding>> Execute();
}

public interface IJustifiableExecutable : IJustifiableGenerated<IJustifiableFunction>
{
    public Task<(IEnumerable<IBinding> Bindings, IEnumerable<IArgument> Justifications)> Execute();
}

public interface IFunction : IGenerator<IExecutable>
{
    IReadOnlyList<Parameter> OutputParameters { get; }

    public string Name { get; }
}

public interface IJustifiableFunction : IJustifiableGenerator<IJustifiableExecutable>
{
    IReadOnlyList<Parameter> OutputParameters { get; }

    public string Name { get; }
}
```

## Extension Methods Utilizing the Model

```cs
public static class Extensions
{
    public static async Task<IEnumerable<IBinding>> Invoke(this IFunction function, object[] args)
    {
        int n = args.Length;

        if (n != function.Parameters.Count)
        {
            throw new ArgumentException($"The number of arguments when invoking {function.Name} must be {function.Parameters.Count} but {n} were provided.");
        }

        List<IBinding> bindings = new List<IBinding>();

        for (int index = 0; index < n; ++index)
        {
            bindings.Add(function.Bind(function.Parameters[index], args[index]));
        }

        return await function.Apply(bindings).Execute();
    }
    public static async Task<(IEnumerable<IBinding> Bindings, IEnumerable<IArgument> Justifications)> Invoke(this IJustifiableFunction function, object[] args, bool auto = true)
    {
        int n = args.Length;

        if (n != function.Parameters.Count)
        {
            throw new ArgumentException($"The number of arguments when invoking {function.Name} must be {function.Parameters.Count} but {n} were provided.");
        }

        List<IBinding> bindings = new List<IBinding>();
        List<IArgument> justifications = new List<IArgument>();

        for (int index = 0; index < n; ++index)
        {
            bindings.Add(function.Bind(function.Parameters[index], args[index]));
        }

        if (auto)
        {
            foreach (var precondition in function.Preconditions)
            {
                if (!precondition.Parameters.All(x => function.Parameters.Contains(x)))
                {
                    throw new Exception("Could not auto-create justifications for parameter value bindings, at least one of the function's preconditions involves a parameter not in the function's signature.");
                }
                justifications.Add(precondition.Apply(bindings));
            }

            return await function.Apply(bindings, justifications).Execute();
        }
        else
        {
            return await function.Apply(bindings).Execute();
        }
    }
    public static async Task<(IEnumerable<IBinding> Bindings, IEnumerable<IArgument> Justifications)> Invoke(this IJustifiableFunction function, object[] args, IArgument[] justifications)
    {
        int n = args.Length;

        if (n != function.Parameters.Count)
        {
            throw new ArgumentException($"The number of arguments when invoking {function.Name} must be {function.Parameters.Count} but {n} were provided.");
        }

        List<IBinding> bindings = new List<IBinding>();

        for (int index = 0; index < n; ++index)
        {
            bindings.Add(function.Bind(function.Parameters[index], args[index]));
        }

        return await function.Apply(bindings, justifications).Execute();
    }
}
```

## Conclusion

Bindings are utilized throughout computing. They are utilized for function invocations, remote procedure calls, input forms, templates, and inference rules. As was shown above, the validity of values can be argued by software developers and artificial-intelligence agents, these arguments evaluated by artificial-intelligence agents.
