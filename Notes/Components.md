## Introduction

Given a formalized argument markup language which can be transformed via RML into knowledge graphs using the AIF model, the idea here is to allow developers and artificial-intelligence agents to be able to create and utilize extension components to allow markup including the extension components to similarly be transformed into knowledge graphs based on AIF.

Components' definitions (these involving XML, XML schemas, and RML) and their parts could reference their parts as Web resources or as parts included in MIME messages at the determination of serialization algorithms. For clarity, as possible, MIME messages will be shown here so that the various interrelated parts can be observed simultaneously.

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
