## The Computational Representation of Argument

### Multipurpose Internet Mail Extensions (MIME)

[Multipurpose Internet Mail Extensions (MIME)](https://en.wikipedia.org/wiki/MIME) can be utilized as a format to serialize arguments to, to deserialize arguments from, to store arguments in filesystems, and to transmit arguments between machines and between artificial-intelligence agents in multi-agent systems.

See also: [MHTML](https://en.wikipedia.org/wiki/MHTML), [MAFF](https://en.wikipedia.org/wiki/Mozilla_Archive_Format), [Web Archive](https://en.wikipedia.org/wiki/Web_Archive_(file_format)), [WARC](https://en.wikipedia.org/wiki/WARC_(file_format)), [HAR](https://en.wikipedia.org/wiki/HAR_(file_format)), [EPUB](https://en.wikipedia.org/wiki/EPUB).

#### Example 1

In this example, one can observe that argument representation formats can use the Content-ID (`cid:`) URL scheme from [RFC 2392](https://datatracker.ietf.org/doc/rfc2392/) to refer to other parts of multipart messages.

<details>
<summary>Click here to toggle the visibility of Example 1.</summary>
<br>
  
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
  <conclusion><parameter kind="object" href="cid:item4">The person</parameter> is a British citizen.</conclusion>
  <premises>
    <argument>
      <conclusion><parameter kind="object" href="cid:item4">The person</parameter> was born in Bermuda.</conclusion>
      <parameter kind="evidence" href="cid:item5">Attached is a copy of the birth certificate.</parameter>
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
</details>

#### Example 2

In addition to a new markup language, existing models such as the [Argument Interchange Format (AIF)](https://en.wikipedia.org/wiki/Argument_Interchange_Format) could be of use for representing arguments in MIME messages.

<details>
<summary>Click here to toggle the visibility of Example 2.</summary>
<br>

```email
Mime-Version: 1.0
Content-Type: multipart/related; boundary="boundary-example-2"

--boundary-example-2

Content-Type: text/plain
Content-Language: en

Climate change is caused by human activities. Therefore, we should reduce carbon emissions.

--boundary-example-2

Content-Type: application/argument+turtle
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
</details>

#### Example 3

This example shows a simple approach to extending knowledge graphs using the AIF model to support attaching evidence and citing scholarly and scientific publications.

<details>
<summary>Click here to toggle the visibility of Example 3.</summary>
<br>

```email
Mime-Version: 1.0
Content-Type: multipart/related; boundary="boundary-example-3"

--boundary-example-3

Content-Type: text/plain
Content-Language: en

Climate change is caused by human activities. Therefore, we should reduce carbon emissions.

--boundary-example-3

Content-Type: application/argument+turtle
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
</details>

#### Example 4

This example shows a more intricate approach to extending knowledge graphs using the AIF model to support attaching evidence and citing scholarly and scientific publications.

<details>
<summary>Click here to toggle the visibility of Example 4.</summary>
<br>

```email
Mime-Version: 1.0
Content-Type: multipart/related; boundary="boundary-example-4"

--boundary-example-4

Content-Type: text/plain
Content-Language: en

Climate change is caused by human activities. Therefore, we should reduce carbon emissions.

--boundary-example-4

Content-Type: application/argument+turtle
Content-Language: en

@prefix aif: <http://www.arg.dundee.ac.uk/aif#> .
@prefix ex: <http://example.org/> .
@prefix ext: <http://extension.org/> .

ex:Node1 a aif:I-node ;
    aif:claimText "Climate change is caused by human activities." .

ex:Node2 a aif:RA-node ;
    aif:hasPremise ex:Node1 ;
    aif:hasConclusion ex:Node3 .

ex:Node3 a aif:I-node ;
    aif:claimText "We should reduce carbon emissions." .

ex:Node4 a ext:E-node ;
    ext:hasEvidence <cid:item1> .

ex:Node5 a ext:ES-node ;
    ext:supported ex:Node1 ;
    ext:supportedBy ex:Node4 .

ex:Node6 a ext:C-node ;
    ext:cites <cid:item2> .

ex:Node7 a ext:CS-node ;
    ext:supported ex:Node1 ;
    ext:supportedBy ex:Node6 .

--boundary-example-4

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

--boundary-example-4

Content-ID: <item2>
Content-Type: text/x-bibtex

@article{Brown2023,
  author = {Charles Brown},
  title = {An Interesting Article},
  journal = {Journal of Interesting Articles},
  year = {2023}
}

--boundary-example-4--
```
</details>

#### Example 5

This example shows that arguments could be represented using the AIF model expressed using JSON in a MIME message.

<details>
<summary>Click here to toggle the visibility of Example 5.</summary>
<br>

```email
Mime-Version: 1.0
Content-Type: multipart/related; boundary="boundary-example-5"

--boundary-example-5

Content-Type: text/plain
Content-Language: en

Speaker 1: Disagreements between party members are entirely to be expected.
Speaker 2: The SNP has disagreements.
Speaker 1: It's not uncommon for there to be disagreements between party members.

--boundary-example-5

Content-Type: application/argument+json
Content-Language: en

{
  "AIF": {
    "descriptorfulfillments": null,
    "edges": [
      {
        "edgeID": 0,
        "fromID": 0,
        "toID": 4
      },
      {
        "edgeID": 1,
        "fromID": 4,
        "toID": 3
      },
      {
        "edgeID": 2,
        "fromID": 1,
        "toID": 6
      },
      {
        "edgeID": 3,
        "fromID": 6,
        "toID": 5
      },
      {
        "edgeID": 4,
        "fromID": 2,
        "toID": 8
      },
      {
        "edgeID": 5,
        "fromID": 8,
        "toID": 7
      },
      {
        "edgeID": 6,
        "fromID": 3,
        "toID": 9
      },
      {
        "edgeID": 7,
        "fromID": 9,
        "toID": 7
      }
    ],
    "locutions": [
      {
        "nodeID": 0,
        "personID": 0
      },
      {
        "nodeID": 1,
        "personID": 1
      },
      {
        "nodeID": 2,
        "personID": 2
      }
    ],
    "nodes": [
      {
        "nodeID": 0,
        "text": "disagreements between party members are entirely to be expected.",
        "type": "L"
      },
      {
        "nodeID": 1,
        "text": "the SNP has disagreements.",
        "type": "L"
      },
      {
        "nodeID": 2,
        "text": "it's not uncommon for there to be disagreements between party members.",
        "type": "L"
      },
      {
        "nodeID": 3,
        "text": "disagreements between party members are entirely to be expected.",
        "type": "I"
      },
      {
        "nodeID": 4,
        "text": "Default Illocuting",
        "type": "YA"
      },
      {
        "nodeID": 5,
        "text": "the SNP has disagreements.",
        "type": "I"
      },
      {
        "nodeID": 6,
        "text": "Default Illocuting",
        "type": "YA"
      },
      {
        "nodeID": 7,
        "text": "it's not uncommon for there to be disagreements between party members.",
        "type": "I"
      },
      {
        "nodeID": 8,
        "text": "Default Illocuting",
        "type": "YA"
      },
      {
        "nodeID": 9,
        "text": "Default Inference",
        "type": "RA"
      }
    ],
    "participants": [
      {
        "firstname": "Speaker",
        "participantID": 0,
        "surname": "1"
      },
      {
        "firstname": "Speaker",
        "participantID": 1,
        "surname": "2"
      }
    ],
    "schemefulfillments": null
  },
  "dialog": true,
  "ova": [],
  "text": {
    "txt": " Speaker 1 <span class=\"highlighted\" id=\"0\">disagreements between party members are entirely to be expected.</span>.<br><br> Speaker 2 <span class=\"highlighted\" id=\"1\">the SNP has disagreements.</span>.<br><br> Speaker 1 <span class=\"highlighted\" id=\"2\">it's not uncommon for there to be disagreements between party members.</span>.<br><br>"
  }
}

--boundary-example-5--
```
</details>

### Argument Templating

[Semantic Kernel](https://github.com/microsoft/semantic-kernel) is interoperable with a number of templating systems, e.g., [Handlebars](https://handlebarsjs.com/), [Liquid](https://liquidjs.com/), and [Jinja](https://jinja.palletsprojects.com/en/stable/). These systems could be explored instead of, in addition to, or in combination with those markup-based templating approaches indicated above. Handlebars templates have a content type of `text/x-handlebars-template`, Liquid templates `application/liquid`, and Jinja templates `text/jinja`.

With solutions for knowledge-graph templating, the expressiveness of knowledge-graph-based approaches to representing argument could equal the expressiveness of the markup-based approach indicated in example 1. Knowledge-graph-based representations of argument would be able to refer to those reusable argument templates used to generate them (see also: [Reasonable Ontology Templates (OTTR)](https://www.ottr.xyz/)).

Advanced topics in argument templating include interactive templates and agentic templates. Interactive templates are templates with accompanying forms or questionnaires which end-users or artificial-intelligence agents would complete to produce output, in this case arguments. Agentic templates would resemble scripts, including [prompts](https://en.wikipedia.org/wiki/Prompt_engineering), for artificial-intelligence systems to contextually produce natural-language arguments with accompanying structured knowledge.

### Hypertext

While it may suffice to include text and argument-related data together in MIME messages for artificial-intelligence agents, human end-users might tend to prefer the addition of hypertext.

This format could provide end-users with enhanced presentational, interactional, and navigational features. This format could provide end-users with other features from accessing argument-related data available elsewhere in MIME messages.

Static hypertext could be automatically generated from argument-related data. In addition to algorithms producing static argument-specific hypertext from argument-related data, developers might want to explore providing reusable and general-purpose dynamic hypertext which would vary, at runtime, based upon loaded argument-related data.

How would embedded HTML content in MIME messages access argument-related data from other parts of MIME messages? HTML content can use [RFC 2392](https://datatracker.ietf.org/doc/rfc2392/), the `cid:` URL scheme, to enable inlined images in email messages. HTML content in other kinds of MIME messages could use this scheme to enable [data blocks](https://html.spec.whatwg.org/multipage/scripting.html#data-block) to refer to other message parts.

### Extensible Markup and Components

Inspired by [Web Components](https://en.wikipedia.org/wiki/Web_Components), where custom markup elements can be defined and subsequently reused, new argument markup languages could be extensible with respect to an expressiveness for higher-level components. These markup components would be defined not in terms of their presentation and interaction, but in terms of their semantics. That is, one could define custom components in terms of mappings and transformations between them and knowledge graphs (see also: [R2RML](https://www.w3.org/TR/r2rml/) and [RML](https://kg-construct.github.io/rml-resources/portal/)).

### Knowledge Graphs

[Knowledge graphs](https://en.wikipedia.org/wiki/Knowledge_graph) are also of use for representing argument templates, arguments, and networks of interrelated arguments. As shown in examples 3 and 4, above, knowledge graphs can be parts of MIME messages and utilize [RFC 2392](https://datatracker.ietf.org/doc/rfc2392/), the `cid:` URL scheme, to refer to other parts of those MIME messages containing them.

### Metadata

[Knowledge graphs](https://en.wikipedia.org/wiki/Knowledge_graph) could also be of use in MIME messages to provide [metadata](https://en.wikipedia.org/wiki/Metadata) about other parts in messages.

There exists a `Content-Description` header for providing text descriptions of parts. There could, in particular for content of type `multipart/related`, be a new MIME header, perhaps named `Content-Metadata`, to refer to other parts which serve as metadata for them. Additionally or instead, those parts providing metadata could use a new header, perhaps named `Content-About`, to refer to those parts which they describe.

#### Example 6

This example shows how one could include metadata in one MIME message part to describe content in another part.

<details>
<summary>Click here to toggle the visibility of Example 6.</summary>
<br>

```email
Mime-Version: 1.0
Content-Type: multipart/related; boundary="boundary-example-6"

--boundary-example-6

Content-Type: text/turtle
Content-About: <part1>

@prefix dc: <http://purl.org/dc/terms/> .
@prefix foaf: <http://xmlns.com/foaf/0.1/> .

<cid:part1> dc:created "2025-06-29 20:00:00.000" ;
    dc:creator [ a foaf:Person ;
            foaf:name "Bob Smith" ] .

--boundary-example-6

Content-ID: <part1>
Content-Type: text/plain
Content-Language: en

Climate change is caused by human activities. Therefore, we should reduce carbon emissions.

--boundary-example-6--
```
</details>

### Content Negotiation

Agent-driven or reactive [content negotiation](https://en.wikipedia.org/wiki/Content_negotiation) is performed by algorithms in user-agents which choose among the possible variant representations. This is commonly performed using a server-provided list of representations and metadata about them.

One could provide these functionalities using MIME messages. Senders could indicate the availability of content in various formats and languages and online locations without having to include the content in MIME messages.

For example, senders might be able to translate content, on-demand, into a very large set of languages and, instead of having to provide content for each language in a MIME message, they could include content for some popular languages and indicate the availability of and locations of content in other languages.

#### Example 7

This example shows a theoretical approach to include content in both English and French while providing recipients with means to obtain the content in other formats or languages.

<details>
<summary>Click here to toggle the visibility of Example 7.</summary>
<br>

```email
Mime-Version: 1.0
Message-Id: 12345678
Content-Type: multipart/alternative; boundary="boundary-example-7"

--boundary-example-7

Content-Type: text/plain
Content-Language: en

Climate change is caused by human activities. Therefore, we should reduce carbon emissions.

--boundary-example-7

Content-Type: text/plain
Content-Language: fr

Le changement climatique est causé par les activités humaines. Nous devons donc réduire les émissions de carbone.

--boundary-example-7

Content-Type: text/plain
Content-Language: other1
Content-Disposition: retrieve
Content-Alias: https://service.org/translate.php?mid=12345678&lang=other1

--boundary-example-7

Content-Type: text/plain
Content-Language: other2
Content-Disposition: retrieve
Content-Alias: https://service.org/translate.php?mid=12345678&lang=other2

--boundary-example-7--
```
</details>

### Security

[Secure Multipurpose Internet Mail Extensions (S/MIME)](https://en.wikipedia.org/wiki/S/MIME) enables security features for MIME messages including [digitally signing](https://en.wikipedia.org/wiki/Digital_signature) messages.

New MIME `Content` headers could be designed for granting permissions and authorizations to and between parts of complex MIME messages, resembling [permissions policies](https://w3c.github.io/webappsec-permissions-policy/) for `<iframe>` nested content and involving HTTP headers.

### Serialization

Traditional approaches to [serializing](https://en.wikipedia.org/wiki/Serialization) objects have tended to involve transforming object graphs into and from single formats, e.g., binary data, JSON, YAML, XML, or RDF.

Objects could, additionally, be serialized into and be deserialized from MIME messages. During serialization, algorithms could add parts to MIME messages, each part expressed using a format. During deserialization, interrelated message parts would be processed back into objects.

With support for `multipart/alternative` parts and subparts, serialization algorithms would be able to add multiple alternatives into MIME messages and deserialization algorithms would be able to contextually choose from or select from these.

## A Comparison of Message Models

### Artificial-intelligence APIs, Frameworks, and Protocols

Contemporary artificial-intelligence APIs, frameworks, and protocols include models of messages for exchange between end-users and agents. Components of message models include: message identifiers, timestamps, content parts, roles, annotations, attachments, and metadata.

Artificial-intelligence message models include: [Anthropic](https://docs.anthropic.com/en/api/messages), [Azure AI](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/responses?tabs=python-secure), [Google](https://ai.google.dev/gemini-api/docs/text-generation), [HuggingFace](https://huggingface.co/docs/text-generation-inference/main/en/messages_api), [Ollama](https://ollama.readthedocs.io/en/api/#generate-a-chat-completion), and [OpenAI](https://platform.openai.com/docs/api-reference/messages). Message models in agentic frameworks include: [AutoGen](https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/tutorial/messages.html) and [LangChain](https://python.langchain.com/api_reference/core/messages.html). Message models in multi-agent protocols include: [A2A](https://a2aproject.github.io/A2A/latest/specification/#64-message-object) and [ACP](https://agentcommunicationprotocol.dev/core-concepts/message-structure).

As one can observe, [JavaScript Object Notation (JSON)](https://en.wikipedia.org/wiki/JSON) and related [Remote Procedure Calls (JSON-RPC)](https://en.wikipedia.org/wiki/JSON-RPC) are very popular among artificial-intelligence APIs, frameworks, and protocols. JSON is also utilized by new [AIF libraries](https://github.com/arg-tech/xaif) and forthcoming standards for [representing conversation data](https://docs.vcons.org/en/current-draft).

Will artificial-intelligence APIs, frameworks, and protocols one day support the expressiveness for multipart messages having [`multipart/mixed`](https://en.wikipedia.org/wiki/MIME#mixed), [`multipart/related`](https://en.wikipedia.org/wiki/MIME#related), or [`multipart/alternative`](https://en.wikipedia.org/wiki/MIME#alternative) semantics? Will this expressiveness one day come to include that of the full hierarchical nature of MIME messages, where messages' parts can each have multiple parts?

Today, artificial-intelligence message models include support for multiple message content parts.

Today, in [Semantic Kernel](https://github.com/microsoft/semantic-kernel), messages are represented using the [`ChatMessageContent`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.semantickernel.chatmessagecontent?view=semantic-kernel-dotnet) class and derived classes. The `ChatMessageContent` class has a property, `MimeType`, for the content type of the message. The `ChatMessageContent` class also supports multiple content items using a [`ChatMessageContentItemCollection`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.semantickernel.chatcompletion.chatmessagecontentitemcollection?view=semantic-kernel-dotnet) collection.

So, it is possible.

### Activity Streams and ActivityPub

With respect to [Activity Streams](https://www.w3.org/TR/activitystreams-core/) and [ActivityPub](https://www.w3.org/TR/activitypub/), the [`Object`](https://www.w3.org/TR/activitystreams-core/#object) type supports attachments and allows a MIME content type, [`mediaType`](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-mediatype), to be specified. The default value for this `mediaType` property is `text/html` and it is presently unclear whether the `Object` type supports multipart MIME types. If not, perhaps [`Collections`](https://www.w3.org/TR/activitystreams-core/#collections) of `Objects` could be of use in these regards.

### Advantages of Multipart Messages

Advantages from supporting MIME's multipart semantics would include, but not be limited to:

1. a well-defined hierarchical structure for message parts would simplify algorithmic processing,
2. the capability to provide one or more message attachments, e.g., documents, images, audio, video, and data,
3. the capability to provide content alternatives, enabling [content negotiation](https://en.wikipedia.org/wiki/Content_negotiation), [internationalization and localization](https://en.wikipedia.org/wiki/Internationalization_and_localization),
4. interoperability with URL schemes like [RFC 2392](https://datatracker.ietf.org/doc/rfc2392/),
5. the capability to provide complex data involving multiple related parts in multiple formats,
6. useful formats for communication channels and scenarios beyond agentic chat, e.g., agentic forums,
7. the capability to provide parallel forms of content for simultaneous consumption, e.g., natural-language text and structured-knowledge argumentation, could allow for the verification and validation of content and reasoning.

## Use Cases

### Agentic Reasoning, Argument, and Debate

Artificial-intelligence agents can create, send, receive, analyze, evaluate, and respond to arguments and, in addition to participating in debates, can judge debates.

In multi-persona debate architectures, multiple agents, each configured to represent a distinct persona, engage in structured debates.

See also: [Project Debater](https://research.ibm.com/haifa/dept/vst/debater.shtml), [Argum.AI](https://argum.ai).

### Email and Mailing Lists

By making use of content-authoring software tools, end-users could create arguments comprised of interrelated natural-language and structured-knowledge parts and send these MIME messages to one another by email. Recipients could utilize software tools to analyze, verify, and validate received arguments.

When end-users replied to emails containing structured-knowledge content, content-authoring tools could provide features for their structured knowledge to reference the structured knowledge in those arguments being replied to.

Other scenarios to consider include enhancing [mailing lists](https://en.wikipedia.org/wiki/Mailing_list) with features made possible from adding structured knowledge to MIME email messages. There would be exciting possibilities with respect to new technologies for moderating discussion threads, for archiving discussion threads, for aggregating structured knowledge from discussion threads into [knowledgebases](https://en.wikipedia.org/wiki/Knowledge_base), and for enabling end-users and artificial-intelligence agents to query, poll, search, navigate, and explore mailing lists' archives and related knowledgebases.

### Internet Forums

End-users could contribute to and participate in [Internet forums](https://en.wikipedia.org/wiki/Internet_forum) for man-machine discussion and debate.

## Discussion

### Federation

For public groups, mailing-list servers, archives, and related knowledgebases could be [federated](https://en.wikipedia.org/wiki/Federation_(information_technology)), interconnected and synchronized in the sense of the [Fediverse](https://en.wikipedia.org/wiki/Fediverse). End-users would, then, be able to receive periodic [digests](https://en.wikipedia.org/wiki/Email_digest) or [interactive dashboards](https://en.wikipedia.org/wiki/Dashboard_(computing)) summarizing developments and events of interest to them from across federated public mailing lists.

Internet forums are also capable of federation. Examples of such software include [Lemmy](https://join-lemmy.org/) and [NodeBB](https://nodebb.org/).

### Publish-subscribe Pattern

The [publish-subscribe pattern](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern) is a messaging pattern in which message senders, called publishers, categorize messages into classes, or topics, and send them without needing to know which components will receive them. Examples of such protocols include [WebSub](https://en.wikipedia.org/wiki/WebSub).

Artificial-intelligence tools could categorize messages and discussion threads for purposes of routing them or digests summarizing them to interested end-users. [Embeddings](https://en.wikipedia.org/wiki/Embedding_(machine_learning)) could be of use for representing messages' and threads' classes, or topics.
