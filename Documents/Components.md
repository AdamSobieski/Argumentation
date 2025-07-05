## Introduction

Given a formalized argument markup language which can be transformed via [RDF Mapping Language (RML)](https://rml.io/specs/rml/) into knowledge graphs using the [Argument Interchange Format (AIF)](https://en.wikipedia.org/wiki/Argument_Interchange_Format) model, the idea, here, is to allow software developers and artificial-intelligence agents to be able to create, define, and reuse markup components such that resultant content could also be transformed into such knowledge graphs.

## Component Models

Extensible markup-based components occur across user-interface design technologies. Using markup and programming languages, developers can define and subsequently reuse interactive user-interface components. Examples of [user-interface markup languages](https://en.wikipedia.org/wiki/Comparison_of_user_interface_markup_languages) include: [XAML](https://en.wikipedia.org/wiki/Extensible_Application_Markup_Language), [EMML](https://en.wikipedia.org/wiki/Enterprise_Mashup_Markup_Language), [FXML](https://en.wikipedia.org/wiki/FXML), [MXML](https://en.wikipedia.org/wiki/MXML), [XUL](https://en.wikipedia.org/wiki/XUL), and [ZUML](https://en.wikipedia.org/wiki/ZUML). With [Web Components](https://en.wikipedia.org/wiki/Web_Components), [HTML5](https://en.wikipedia.org/wiki/HTML5) documents can utilize extensible markup components.

## XML Schema Languages

Examples of [XML schema languages](https://en.wikipedia.org/wiki/XML_schema#Languages) include: [CLiX](https://en.wikipedia.org/wiki/CLiX_(markup)), [RelaxNG](https://en.wikipedia.org/wiki/RELAX_NG), [Schematron](https://en.wikipedia.org/wiki/Schematron), [SOX](https://www.w3.org/TR/NOTE-SOX/), and [XSD](https://en.wikipedia.org/wiki/XML_Schema_(W3C)). Useful features for defining components in schema will include type derivation and substitution groups.

## Component Definitions

As envisioned, components' definitions include XML schema and RML. Components' definitions and their parts could reference resources on the Web or as MIME message parts at the determination of serialization algorithms. For clarity, as possible, MIME messages will be shown here so that the various interrelated parts can be observed simultaneously.

> [!TIP]
> What would it look like for an argument markup language resource to reference an extension component's definition?
>
> Perhaps, resembling XML schemas, one could utilize attributes to indicate the locations of RML mappings?
> 
> ```xml
> <argument xmlns="..."
>           xmlns:ext="http://www.extension.org/#"
>           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>           xsi:schemaLocation="cid:part1 cid:part2"
>           xmlns:rmi="http://www.example.org/2025/RML-instance"
>           rmi:mappingLocation="cid:part3 cid:part4">
>   <conclusions>
>     <conclusion>This is an example showing how extensible markup-based components could be used.</conclusion>
>   </conclusions>
>   <rules>
>     <rule href="cid:part5" />
>   </rules>
>   <premises>
>     <ext:assertion ext:agent="cid:part6#agent">This is an extensible markup-based component.</ext:assertion>
>   </premises>
> </argument>
> ```
