## Introduction

This project is an argumentation framework designed for interoperability with a large number of artificial-intelligence models and services. This project will enable and explore agentic approaches to the creation, analysis, validation, and evaluation of argumentation and debate.

This project will utilize [Semantic Kernel](https://github.com/microsoft/semantic-kernel) to enable developers to more readily explore argumentation-related scenarios using their choice of models and services, e.g.: [OpenAI](https://platform.openai.com/docs/introduction), [Azure OpenAI](https://azure.microsoft.com/en-us/products/ai-services/openai-service), [HuggingFace](https://huggingface.co/), [NVidia](https://www.nvidia.com/en-us/ai-data-science/products/nim-microservices/), or [Ollama](https://ollama.com/).

## Multipurpose Internet Mail Extensions (MIME)

[Multipurpose Internet Mail Extensions (MIME)](https://en.wikipedia.org/wiki/MIME) can be utilized as a format to serialize arguments to, to deserialize arguments from, to store arguments in filesystems, and to transmit arguments between machines and between artificial-intelligence agents in multi-agent systems.

In addition to existing formats such as the [Argument Interchange Format (AIF)](https://en.wikipedia.org/wiki/Argument_Interchange_Format), a new markup language could be of use for expressing and representing both arguments and argument templates.

In the example below, one can observe that argument representation formats can use the Content-ID (`cid:`) URL scheme [[RFC 2392](https://datatracker.ietf.org/doc/rfc2392/)] to refer to other objects (e.g., text, JSON, markup, or binary) elsewhere in the multipart message.

```email
Mime-Version: 1.0
Content-Type: multipart/related; boundary="boundary-example-1"

--boundary-example-1

Content-Type: text/plain
Content-Language: en

Bob Smith is a British citizen. Bob Smith was born in Bermuda. Attached is a copy of the birth certificate. People born in Bermuda are British citizens.

--boundary-example-1

Content-Type: application/argument+xml
Content-Language: en

<argument template="cid:item1">
  <conclusion><object href="cid:item2">Bob Smith</object> is a British citizen.</conclusion>
  <premises>
    <argument>
      <conclusion><object href="cid:item2">Bob Smith</object> was born in Bermuda.</conclusion>
      <evidence href="cid:item3">Attached is a copy of the birth certificate.</evidence>
    </argument>
    <argument>
      <conclusion><cite href="cid:item6" selection="cid:item7">People born in Bermuda are British citizens.</cite></conclusion>
    </argument>
  </premises>
</argument>

--boundary-example-1

Content-ID: <item1>
Content-Type: application/argument+xml
Content-Language: en

<argument>
  <conclusion><parameter href="cid:item4">The person</parameter> is a British citizen.</conclusion>
  <premises>
    <argument>
      <conclusion><parameter href="cid:item4">The person</parameter> was born in Bermuda.</conclusion>
      <evidence-parameter href="cid:item5">Attached is a copy of the birth certificate.</evidence-parameter>
    </argument>
    <argument>
      <conclusion><cite href="cid:item6" selection="cid:item7">People born in Bermuda are British citizens.</cite></conclusion>
    </argument>
  </premises>
</argument>

--boundary-example-1

Content-ID: <item2>
Content-Type: application/octet-stream
Content-Transfer-Encoding: base64

R0lGODlhGAGgAPEAAP/////ZRaCgoAAAACH+PUNvcHlyaWdodCAoQykgMTk5NSBJRVRGLiBVbmF1dGhvcml6ZWQgZHVwbGljYXRpb24gcHJvaGliaXRlZC4A...

--boundary-example-1

Content-ID: <item3>
Content-Type: application/pdf
Content-Language: en
Content-Disposition: attachment; filename="birth_certificate.pdf"
Content-Transfer-Encoding: base64

R0lGODlhGAGgAPEAAP/////ZRaCgoAAAACH+PUNvcHlyaWdodCAoQykgMTk5NSBJRVRGLiBVbmF1dGhvcml6ZWQgZHVwbGljYXRpb24gcHJvaGliaXRlZC4A...

--boundary-example-1

Content-ID: <item4>
Content-Type: application/octet-stream
Content-Transfer-Encoding: base64

R0lGODlhGAGgAPEAAP/////ZRaCgoAAAACH+PUNvcHlyaWdodCAoQykgMTk5NSBJRVRGLiBVbmF1dGhvcml6ZWQgZHVwbGljYXRpb24gcHJvaGliaXRlZC4A...

--boundary-example-1

Content-ID: <item5>
Content-Type: application/octet-stream
Content-Transfer-Encoding: base64

R0lGODlhGAGgAPEAAP/////ZRaCgoAAAACH+PUNvcHlyaWdodCAoQykgMTk5NSBJRVRGLiBVbmF1dGhvcml6ZWQgZHVwbGljYXRpb24gcHJvaGliaXRlZC4A...

--boundary-example-1

Content-ID: <item6>
Content-Type: text/x-bibtex

@article{Brown2023,
  author = {Charles Brown},
  title = {An Interesting Article},
  journal = {Journal of Interesting Articles},
  year = {2023}
}

--boundary-example-1

Content-ID: <item7>
Content-Type: application/ld+json; profile="http://www.w3.org/ns/anno.jsonld"

{
  "source": "cid:item6",
  "selector": {
    "type": "FragmentSelector",
    "value": "page=10",
    "refinedBy": {
      "type": "TextQuoteSelector",
      "prefix": "preceding text",
      "suffix": "subsequent text"
    }
  }
}

--boundary-example-1--
```

## Serialization and Deserialization

Traditional approaches to [serialization](https://en.wikipedia.org/wiki/Serialization) have typically involved transforming object graphs to or from single formats, e.g., binary data, JSON, YAML, XML, or RDF.

Objects could, additionally, serialize to and be deserialized from MIME messages. During serialization, objects could add parts to MIME messages, each part having its own format, and, during deserialization, these message parts could be processed back into objects.

Additional intricacy would arise from supporting `multipart/alternative` within MIME messages. With `multipart/alternative` support, deserialization algorithms would be able to choose from or to select from multiple available alternative parts. Use cases for this would include [internationalization and localization](https://en.wikipedia.org/wiki/Internationalization_and_localization).

## Templating

[Semantic Kernel](https://github.com/microsoft/semantic-kernel) is interoperable with a number of templating systems and interesting possiblities include exploring these systems, e.g., [Handlebars](https://handlebarsjs.com/) or [Jinja](https://jinja.palletsprojects.com/en/stable/), instead of, in addition to, or in combination with those markup-based templating approaches indicated above. Handlebars templates have a content type of `text/x-handlebars-template` and Jinja templates `text/jinja`.

## Knowledge Graphs

[Knowledge graphs](https://en.wikipedia.org/wiki/Knowledge_graph) are also of use for representing argument templates, arguments, and networks of interrelated arguments. Knowledge graphs could similarly utilize [RFC 2392](https://datatracker.ietf.org/doc/rfc2392/), the `cid:` URL scheme, to reference other parts of those MIME messages containing them.
