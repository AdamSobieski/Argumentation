## Introduction

Given a formalized argument markup language which can be transformed via [RDF Mapping Language (RML)](https://kg-construct.github.io/rml-resources/portal/) into knowledge graphs, the idea, here, is to allow software developers and artificial-intelligence agents to be able to create, define, and subsequently reuse markup elements such that resultant content could also be transformed into knowledge graphs.

## Component Models

Extensible markup-based component models occur across user-interface design technologies. Using combinations of markup and programming languages, developers can define and subsequently reuse interactive user-interface components. Examples of [user-interface markup languages](https://en.wikipedia.org/wiki/Comparison_of_user_interface_markup_languages) include: [XAML](https://en.wikipedia.org/wiki/Extensible_Application_Markup_Language), [EMML](https://en.wikipedia.org/wiki/Enterprise_Mashup_Markup_Language), [FXML](https://en.wikipedia.org/wiki/FXML), [MXML](https://en.wikipedia.org/wiki/MXML), [XUL](https://en.wikipedia.org/wiki/XUL), and [ZUML](https://en.wikipedia.org/wiki/ZUML). With [Web Components](https://en.wikipedia.org/wiki/Web_Components), [HTML5](https://en.wikipedia.org/wiki/HTML5) documents can utilize extensible markup components.

## Referencing Component Definitions

What could it resemble for an argument markup language resource to reference extension components' definitions?

> [!TIP]
> Resembling XML schemas, one could utilize attributes to indicate the locations of RML mappings.
> 
> ```xml
> <argument xmlns="..."
>           xmlns:ext="http://www.extension.org/#"
>           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>           xsi:schemaLocation="https://www.example.org/argument.xsd https://www.extension.org/assertion.xsd"
>           xmlns:rmi="http://www.example.org/2025/RML-instance"
>           rmi:mappingLocation="https://www.example.org/argument.rml https://www.extension.org/assertion.rml">
>   <conclusions>
>     <conclusion id="c1">This is an example showing how extensible markup-based components could be used.</conclusion>
>   </conclusions>
>   <rules>
>     <rule href="cid:part1" />
>   </rules>
>   <premises>
>     <ext:assertion id="p1" ext:agent="cid:part2#agent">This is an extensible markup-based component.</ext:assertion>
>   </premises>
> </argument>
> ```
