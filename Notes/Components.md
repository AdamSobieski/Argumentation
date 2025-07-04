## Introduction

Given a formalized argument markup language which can be transformed via RML into knowledge graphs using the AIF model, the idea here is to allow developers and artificial-intelligence agents to be able to create and utilize extension components to allow markup including the extension components to similarly be transformed into knowledge graphs based on AIF.

Components' definitions (these envisioned as involving XML, XML schemas, and RML) and their parts could reference their parts as Web resources or as parts included in MIME messages at the determination of serialization algorithms. For clarity, as possible, MIME messages will be shown here so that the various interrelated parts can be observed simultaneously.

## A Comparison of Component Models

Extensible markup-based components occur across user-interface design technologies. Using markup and programming languages, developers can define and subsequently reuse interactive user-interface components. Examples of [user-interface markup languages](https://en.wikipedia.org/wiki/Comparison_of_user_interface_markup_languages) include: [XAML](https://en.wikipedia.org/wiki/Extensible_Application_Markup_Language), [EMML](https://en.wikipedia.org/wiki/Enterprise_Mashup_Markup_Language), [FXML](https://en.wikipedia.org/wiki/FXML), [MXML](https://en.wikipedia.org/wiki/MXML), [XUL](https://en.wikipedia.org/wiki/XUL), and [ZUML](https://en.wikipedia.org/wiki/ZUML). With [Web Components](https://en.wikipedia.org/wiki/Web_Components), [HTML5](https://en.wikipedia.org/wiki/HTML5) documents can utilize extensible markup components.

## Including Components

What would it look like for an argument markup language resource to reference an extension component's definition? Perhaps using an `<include>` element, the markup-based resource could refer to a component definition.

```xml
<argument xmlns:ext="http://otherxmlns.org/extension1/#">
  <head>
    <include src="cid:part1" />
  </head>
  <body>
    <conclusion>This is an example showing how markup-based extensions could be used.</conclusion>
    <premises>
      <ext:assertion ext:agent="cid:part3#agent">This is an assertion.</ext:assertion>
    </premises>
  </body>
</argument>
```
