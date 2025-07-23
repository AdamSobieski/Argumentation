## Introduction

Using multipart MIME and RFC 2392, one could create messages which include or refer to function definitions and which also include invocations of defined functions using a variety of included or referenced arguments in a variety of formats.

```xml
<invocation xmlns="...">
  <function href="cid:part1" />
  <arguments>
    <argument href="cid:part2" />
    <argument href="cid:part3" />
  </arguments>
</invocation>
```

## See Also

* [The Function Ontology](https://fno.io/spec/)
