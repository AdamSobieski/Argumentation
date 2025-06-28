## Introduction

This project is an argumentation framework designed for interoperability with a large number of artificial-intelligence models and services. This project will enable and explore agentic approaches to the creation, analysis, validation, and evaluation of argumentation and debate.

This project will utilize [Semantic Kernel](https://github.com/microsoft/semantic-kernel) to enable developers to more readily explore argumentation-related scenarios using their choice of models and services, e.g.: [OpenAI](https://platform.openai.com/docs/introduction), [Azure OpenAI](https://azure.microsoft.com/en-us/products/ai-services/openai-service), [HuggingFace](https://huggingface.co/), [NVidia](https://www.nvidia.com/en-us/ai-data-science/products/nim-microservices/), or [Ollama](https://ollama.com/).

## The Computational Representation of Argument

### Multipurpose Internet Mail Extensions (MIME)

[Multipurpose Internet Mail Extensions (MIME)](https://en.wikipedia.org/wiki/MIME) can be utilized as a format to serialize arguments to, to deserialize arguments from, to store arguments in filesystems, and to transmit arguments between machines and between artificial-intelligence agents in multi-agent systems.

See also: [MHTML](https://en.wikipedia.org/wiki/MHTML), [MAFF](https://en.wikipedia.org/wiki/Mozilla_Archive_Format), [Web Archive](https://en.wikipedia.org/wiki/Web_Archive_(file_format)), [WARC](https://en.wikipedia.org/wiki/WARC_(file_format)), [HAR](https://en.wikipedia.org/wiki/HAR_(file_format)), [EPUB](https://en.wikipedia.org/wiki/EPUB).

#### Example 1

In this example, one can observe that argument representation formats can use the Content-ID (`cid:`) URL scheme [[RFC 2392](https://datatracker.ietf.org/doc/rfc2392/)] to refer to other parts of multipart messages.

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

TG9yZW0gaXBzdW0gZG9sb3Igc2l0IGFtZXQsIGNvbnNlY3RldHVyIGFkaXBpc2NpbmcgZWxpdC4g
U2VkIGRvIGVpdXNtb2QgdGVtcG9yIGluY2lkaWR1bnQgdXQgbGFib3JlIGV0IGRvbG9yZSBtYWdu
YSBhbGlxdWEuIFV0IGVuaW0gYWQgbWluaW0gdmVuaWFtLCBxdWlzIG5vc3RydWQgZXhlcmNpdGF0
aW9uIHVsbGFtY28gbGFib3JpcyBuaXNpIHV0IGFsaXF1aXAgZXggZWEgY29tbW9kbyBjb25zZXF1
YXQuCg==

--boundary-example-1

Content-ID: <item3>
Content-Type: application/pdf
Content-Language: en
Content-Disposition: attachment; filename="birth_certificate.pdf"
Content-Transfer-Encoding: base64

TG9yZW0gaXBzdW0gZG9sb3Igc2l0IGFtZXQsIGNvbnNlY3RldHVyIGFkaXBpc2NpbmcgZWxpdC4g
U2VkIGRvIGVpdXNtb2QgdGVtcG9yIGluY2lkaWR1bnQgdXQgbGFib3JlIGV0IGRvbG9yZSBtYWdu
YSBhbGlxdWEuIFV0IGVuaW0gYWQgbWluaW0gdmVuaWFtLCBxdWlzIG5vc3RydWQgZXhlcmNpdGF0
aW9uIHVsbGFtY28gbGFib3JpcyBuaXNpIHV0IGFsaXF1aXAgZXggZWEgY29tbW9kbyBjb25zZXF1
YXQuCg==

--boundary-example-1

Content-ID: <item4>
Content-Type: application/octet-stream
Content-Transfer-Encoding: base64

TG9yZW0gaXBzdW0gZG9sb3Igc2l0IGFtZXQsIGNvbnNlY3RldHVyIGFkaXBpc2NpbmcgZWxpdC4g
U2VkIGRvIGVpdXNtb2QgdGVtcG9yIGluY2lkaWR1bnQgdXQgbGFib3JlIGV0IGRvbG9yZSBtYWdu
YSBhbGlxdWEuIFV0IGVuaW0gYWQgbWluaW0gdmVuaWFtLCBxdWlzIG5vc3RydWQgZXhlcmNpdGF0
aW9uIHVsbGFtY28gbGFib3JpcyBuaXNpIHV0IGFsaXF1aXAgZXggZWEgY29tbW9kbyBjb25zZXF1
YXQuCg==

--boundary-example-1

Content-ID: <item5>
Content-Type: application/octet-stream
Content-Transfer-Encoding: base64

TG9yZW0gaXBzdW0gZG9sb3Igc2l0IGFtZXQsIGNvbnNlY3RldHVyIGFkaXBpc2NpbmcgZWxpdC4g
U2VkIGRvIGVpdXNtb2QgdGVtcG9yIGluY2lkaWR1bnQgdXQgbGFib3JlIGV0IGRvbG9yZSBtYWdu
YSBhbGlxdWEuIFV0IGVuaW0gYWQgbWluaW0gdmVuaWFtLCBxdWlzIG5vc3RydWQgZXhlcmNpdGF0
aW9uIHVsbGFtY28gbGFib3JpcyBuaXNpIHV0IGFsaXF1aXAgZXggZWEgY29tbW9kbyBjb25zZXF1
YXQuCg==

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

#### Example 2

In addition to a new markup language, existing formats such as the [Argument Interchange Format (AIF)](https://en.wikipedia.org/wiki/Argument_Interchange_Format) could be of use for expressing and representing both arguments and argument templates in MIME messages.

```email
Mime-Version: 1.0
Content-Type: multipart/related; boundary="boundary-example-2"

--boundary-example-2

Content-Type: text/plain
Content-Language: en

Climate change is caused by human activities. Therefore, we should reduce carbon emissions.

--boundary-example-2

Content-Type: application/argument+n3
Content-Language: en

@prefix aif: <http://www.arg.dundee.ac.uk/aif#> .
@prefix ex: <http://example.org/> .

ex:Node1 a aif:I-node ;
    aif:claimText "Climate change is caused by human activities." .

ex:Node2 a aif:RA-node ;
    aif:hasPremise ex:Node1 ;
    aif:hasConclusion ex:Node3 .

ex:Node3 a aif:I-node ;
    aif:claimText "We should reduce carbon emissions." .

--boundary-example-2--
```

#### Example 3

The following example shows a simple approach to extend knowledge graphs using AIF to support attaching evidence and citing scholarly and scientific publications.

```email
Mime-Version: 1.0
Content-Type: multipart/related; boundary="boundary-example-3"

--boundary-example-3

Content-Type: text/plain
Content-Language: en

Climate change is caused by human activities. Therefore, we should reduce carbon emissions.

--boundary-example-3

Content-Type: application/argument+n3
Content-Language: en

@prefix aif: <http://www.arg.dundee.ac.uk/aif#> .
@prefix ex: <http://example.org/> .
@prefix ext: <http://extension.org/> .

ex:Node1 a aif:I-node ;
    aif:claimText "Climate change is caused by human activities." .
    ext:hasEvidence <cid:item1> .
    ext:cites <cid:item2> .

ex:Node2 a aif:RA-node ;
    aif:hasPremise ex:Node1 ;
    aif:hasConclusion ex:Node3 .

ex:Node3 a aif:I-node ;
    aif:claimText "We should reduce carbon emissions." .

--boundary-example-3

Content-ID: <item1>
Content-Type: application/pdf
Content-Language: en
Content-Disposition: attachment; filename="evidence.pdf"
Content-Transfer-Encoding: base64

TG9yZW0gaXBzdW0gZG9sb3Igc2l0IGFtZXQsIGNvbnNlY3RldHVyIGFkaXBpc2NpbmcgZWxpdC4g
U2VkIGRvIGVpdXNtb2QgdGVtcG9yIGluY2lkaWR1bnQgdXQgbGFib3JlIGV0IGRvbG9yZSBtYWdu
YSBhbGlxdWEuIFV0IGVuaW0gYWQgbWluaW0gdmVuaWFtLCBxdWlzIG5vc3RydWQgZXhlcmNpdGF0
aW9uIHVsbGFtY28gbGFib3JpcyBuaXNpIHV0IGFsaXF1aXAgZXggZWEgY29tbW9kbyBjb25zZXF1
YXQuCg==

--boundary-example-3

Content-ID: <item2>
Content-Type: text/x-bibtex

@article{Brown2023,
  author = {Charles Brown},
  title = {An Interesting Article},
  journal = {Journal of Interesting Articles},
  year = {2023}
}

--boundary-example-3--
```

### Templating Systems

[Semantic Kernel](https://github.com/microsoft/semantic-kernel) is interoperable with a number of templating systems, e.g., [Handlebars](https://handlebarsjs.com/), [Liquid](https://liquidjs.com/), and [Jinja](https://jinja.palletsprojects.com/en/stable/). These systems could be explored instead of, in addition to, or in combination with those markup-based templating approaches indicated above. Handlebars templates have a content type of `text/x-handlebars-template`, Liquid templates `application/liquid`, and Jinja templates `text/jinja`.

With solutions for knowledge-graph templating, the expressiveness of knowledge-graph approaches to representing argument, examples 2 and 3, could equal the expressiveness of the markup approach indicated, example 1. Knowledge-graph representations of argument would be able to refer to those reusable argument templates used to generate them (see also: [Reasonable Ontology Templates (OTTR)](https://www.ottr.xyz/)).

### Extensibility and Components

Inspired by [Web Components](https://en.wikipedia.org/wiki/Web_Components), where custom markup elements can be defined and subsequently reused, new argument markup languages could be extensible with respect to expressiveness for higher-level components. These components would, as envisioned, be defined not in terms of presentation and interactivity, but in terms of semantics. That is, one could define custom components in terms of mappings and transformations between them and knowledge graphs (see also: [R2RML](https://www.w3.org/TR/r2rml/) and [RML](https://kg-construct.github.io/rml-resources/portal/)).

### Knowledge Graphs

[Knowledge graphs](https://en.wikipedia.org/wiki/Knowledge_graph) are also of use for representing argument templates, arguments, and networks of interrelated arguments. As shown in example 3, above, knowledge graphs could similarly be parts of MIME messages and utilize [RFC 2392](https://datatracker.ietf.org/doc/rfc2392/), the `cid:` URL scheme, to refer to other parts of those MIME messages containing them.

### Metadata

[Knowledge graphs](https://en.wikipedia.org/wiki/Knowledge_graph) could also be of use in MIME messages to provide [metadata](https://en.wikipedia.org/wiki/Metadata) about other parts in messages.

There exists a `Content-Description` header for providing text descriptions of parts. In particular for content of type `multipart/related`, parts could use a new header, perhaps named `Content-Metadata`, to refer to other parts which serve as metadata for them. Additionally or instead, those parts providing metadata could use a new header, perhaps named `Content-About`, to refer to those parts which they describe.

### Hypertext

While it may suffice to include text and argument-related data together in MIME messages for artificial-intelligence agents, human end-users might tend to prefer the addition of hypertext, `text/html` or `application/xhtml+xml`.

These formats could provide end-users with enhanced presentational, interactional, and navigational features as well as other features made possible from the availability of argument-related data elsewhere in MIME messages.

Static hypertext could be automatically generated from argument-related data. In addition to algorithms producing static argument-specific hypertext from argument-related data, developers might want to explore providing reusable and general-purpose dynamic hypertext which would vary, at runtime, based upon loaded argument-related data.

How would embedded HTML content in MIME messages access argument-related data from other parts of MIME messages? As HTML content can use [RFC 2392](https://datatracker.ietf.org/doc/rfc2392/), the `cid:` URL scheme, to enable inlined images in email messages, so too could HTML content in other kinds of MIME messages use this URL scheme in [data blocks](https://html.spec.whatwg.org/multipage/scripting.html#data-block). This might resemble:

```html
<script id="argument1" type="application/argument+xml" src="cid:part1" />
```

Algorithms should be able to process and to verify that MIME messages' parts expressing arguments in a variety of ways, for a variety of purposes, were variations of the same content.

### Security

[Secure Multipurpose Internet Mail Extensions (S/MIME)](https://en.wikipedia.org/wiki/S/MIME) enables security features for MIME messages including [digitally signing](https://en.wikipedia.org/wiki/Digital_signature) messages.

New MIME `Content` headers could be designed for granting permissions and authorizations to and between parts of complex MIME messages, resembling [permissions policies](https://w3c.github.io/webappsec-permissions-policy/) for `<iframe>` nested content and involving HTTP headers.

### Serialization

Traditional approaches to [serializing](https://en.wikipedia.org/wiki/Serialization) objects have tended to involve transforming object graphs into and from single formats, e.g., binary data, JSON, YAML, XML, or RDF.

Objects could, additionally, be serialized into and be deserialized from MIME messages. During serialization, algorithms could add parts to MIME messages, each part expressed using a format. During deserialization, interrelated message parts would be processed back into objects.

With support for `multipart/alternative` parts and subparts, serialization algorithms would be able to add multiple alternatives into MIME messages and deserialization algorithms would be able to contextually choose from or select from these. Uses for this include [internationalization and localization](https://en.wikipedia.org/wiki/Internationalization_and_localization); alternatives could differ in terms of language.

## The Comparison of Message Models

Contemporary artificial-intelligence APIs, frameworks, and protocols include models of messages for exchange between end-users and agents. Components of message models include: message identifiers, timestamps, content parts, roles, annotations, attachments, and metadata.

Artificial-intelligence message models include: [Anthropic](https://docs.anthropic.com/en/api/messages), [Azure AI](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/responses?tabs=python-secure), [Google](https://ai.google.dev/gemini-api/docs/text-generation), [HuggingFace](https://huggingface.co/docs/text-generation-inference/main/en/messages_api), [Ollama](https://ollama.readthedocs.io/en/api/#generate-a-chat-completion), and [OpenAI](https://platform.openai.com/docs/api-reference/messages). Message models in agentic frameworks include: [AutoGen](https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/tutorial/messages.html) and [LangChain](https://python.langchain.com/api_reference/core/messages.html). Message models in multi-agent protocols include: [A2A](https://a2aproject.github.io/A2A/latest/specification/#64-message-object) and [ACP](https://agentcommunicationprotocol.dev/core-concepts/message-structure).

As one can observe, [JavaScript Object Notation (JSON)](https://en.wikipedia.org/wiki/JSON) and related [Remote Procedure Calls (JSON-RPC)](https://en.wikipedia.org/wiki/JSON-RPC) are very popular among artificial-intelligence APIs, frameworks, and protocols. JSON is also utilized by new [AIF libraries](https://github.com/arg-tech/xaif) and forthcoming standards for [representing conversation data](https://docs.vcons.org/en/current-draft).

Will artificial-intelligence APIs, frameworks, and protocols one day support the expressiveness for multipart messages having [`multipart/mixed`](https://en.wikipedia.org/wiki/MIME#mixed), [`multipart/related`](https://en.wikipedia.org/wiki/MIME#related), or [`multipart/alternative`](https://en.wikipedia.org/wiki/MIME#alternative) semantics? Will this expressiveness one day come to include that of the full hierarchical nature of MIME messages, where messages' parts can each have multiple parts?

Today, artificial-intelligence message models include support for multiple message content parts.

Today, in [Semantic Kernel](https://github.com/microsoft/semantic-kernel), messages are represented using the [`ChatMessageContent`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.semantickernel.chatmessagecontent?view=semantic-kernel-dotnet) class and derived classes. The `ChatMessageContent` class has a property, `MimeType`, for the content type of the message. The `ChatMessageContent` class also supports multiple content items using a [`ChatMessageContentItemCollection`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.semantickernel.chatcompletion.chatmessagecontentitemcollection?view=semantic-kernel-dotnet) collection.

So, it's possible.

Advantages from supporting MIME's multipart semantics would include, but not be limited to:

1. a well-defined hierarchical structure for message parts would simplify algorithmic processing,
2. the capability to provide one or more message attachments, e.g., documents, images, audio, video, and data,
3. the capability to provide content alternatives, enabling [content negotiation](https://en.wikipedia.org/wiki/Content_negotiation),
4. interoperability with URL schemes like [RFC 2392](https://datatracker.ietf.org/doc/rfc2392/),
5. the capability to provide complex data involving multiple related parts in multiple formats,
6. useful formats for communication channels and scenarios beyond agentic chat, e.g., agentic forums,
7. the capability to provide parallel forms of content for simultaneous consumption, e.g., natural-language text and structured-knowledge argumentation, could allow for the verification and validation of content and reasoning.
