## The Computational Representation of Arguments

### Multipurpose Internet Mail Extensions

[Multipurpose Internet Mail Extensions (MIME)](https://en.wikipedia.org/wiki/MIME) can be utilized as a format to serialize arguments to, to deserialize arguments from, to store arguments in filesystems, and to transmit arguments between end-users and agents.

Using the `cid:` URL scheme from [RFC 2392](https://datatracker.ietf.org/doc/rfc2392/), contents within parts of multipart MIME messages can, wherever a URL can be used, refer to other parts in multipart MIME messages.

See also: [MHTML](https://en.wikipedia.org/wiki/MHTML), [MAFF](https://en.wikipedia.org/wiki/Mozilla_Archive_Format), [Web Archive](https://en.wikipedia.org/wiki/Web_Archive_(file_format)), [WARC](https://en.wikipedia.org/wiki/WARC_(file_format)), [HAR](https://en.wikipedia.org/wiki/HAR_(file_format)), [EPUB](https://en.wikipedia.org/wiki/EPUB).

> [!TIP]
> Models of argument such as the [Argument Interchange Format (AIF)](https://en.wikipedia.org/wiki/Argument_Interchange_Format) can be used in MIME messages.
> 
> <details>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
> 
> ```email
> Mime-Version: 1.0
> Content-Type: multipart/related; boundary="boundary-example"
> 
> --boundary-example
> 
> Content-Type: text/plain
> Content-Language: en
> 
> Climate change is caused by human activities. Therefore, we should reduce carbon emissions.
> 
> --boundary-example
> 
> Content-Type: text/turtle
> Content-Language: en
> 
> @prefix aif: <http://www.arg.dundee.ac.uk/aif#> .
> @prefix ex: <http://example.org/> .
> 
> ex:Node1 a aif:I-node ;
>     aif:claimText "Climate change is caused by human activities." .
> 
> ex:Node2 a aif:RA-node ;
>     aif:hasPremise ex:Node1 ;
>     aif:hasConclusion ex:Node3 .
> 
> ex:Node3 a aif:I-node ;
>     aif:claimText "We should reduce carbon emissions." .
> 
> --boundary-example--
> ```
> </details>

> [!TIP]
> This example shows one approach to extending or building upon the AIF model to support attaching evidence and citing scholarly and scientific publications.
> 
> <details>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
> 
> ```email
> Mime-Version: 1.0
> Content-Type: multipart/related; boundary="boundary-example"
> 
> --boundary-example
> 
> Content-Type: text/plain
> Content-Language: en
> 
> Climate change is caused by human activities. Therefore, we should reduce carbon emissions.
> 
> --boundary-example
> 
> Content-Type: text/turtle
> Content-Language: en
> 
> @prefix aif: <http://www.arg.dundee.ac.uk/aif#> .
> @prefix ex: <http://example.org/> .
> @prefix ext: <http://extension.org/> .
> 
> ex:Node1 a aif:I-node ;
>     aif:claimText "Climate change is caused by human activities." .
> 
> ex:Node2 a aif:RA-node ;
>     aif:hasPremise ex:Node1 ;
>     aif:hasConclusion ex:Node3 .
> 
> ex:Node3 a aif:I-node ;
>     aif:claimText "We should reduce carbon emissions." .
> 
> ex:Node4 a ext:E-node ;
>     ext:hasEvidence <cid:item1> .
> 
> ex:Node5 a ext:ES-node ;
>     ext:supported ex:Node1 ;
>     ext:supportedBy ex:Node4 .
> 
> ex:Node6 a ext:C-node ;
>     ext:cites <cid:item2> .
> 
> ex:Node7 a ext:CS-node ;
>     ext:supported ex:Node1 ;
>     ext:supportedBy ex:Node6 .
> 
> --boundary-example
> 
> Content-ID: <item1>
> Content-Type: application/pdf
> Content-Language: en
> Content-Disposition: attachment; filename="evidence.pdf"
> Content-Transfer-Encoding: base64
> 
> TG9yZW0gaXBzdW0gZG9sb3Igc2l0IGFtZXQsIGNvbnNlY3RldHVyIGFkaXBpc2NpbmcgZWxpdC4g
> U2VkIGRvIGVpdXNtb2QgdGVtcG9yIGluY2lkaWR1bnQgdXQgbGFib3JlIGV0IGRvbG9yZSBtYWdu
> YSBhbGlxdWEuIFV0IGVuaW0gYWQgbWluaW0gdmVuaWFtLCBxdWlzIG5vc3RydWQgZXhlcmNpdGF0
> aW9uIHVsbGFtY28gbGFib3JpcyBuaXNpIHV0IGFsaXF1aXAgZXggZWEgY29tbW9kbyBjb25zZXF1
> YXQuCg==
> 
> --boundary-example
> 
> Content-ID: <item2>
> Content-Type: text/x-bibtex
> 
> @article{Brown2023,
>   author = {Charles Brown},
>   title = {An Interesting Article},
>   journal = {Journal of Interesting Articles},
>   year = {2023}
> }
> 
> --boundary-example--
> ```
> </details>

### Hypertext Markup Language

While it may suffice to include text and argument-related data together in MIME messages for artificial-intelligence agents, human end-users might tend to prefer the addition of [hypertext](https://en.wikipedia.org/wiki/HTML5).

This format could provide end-users with enhanced presentational, interactional, and navigational features. This format could provide end-users with other features from accessing argument-related data available elsewhere in MIME messages.

Static hypertext could be automatically generated from argument-related data. Dynamic hypertext could use scripting logic to vary, at runtime, based upon loaded argument-related data.

How would embedded HTML content in MIME messages access argument-related data from other parts of MIME messages? Perhaps HTML parts could use the `cid:` scheme in [data blocks](https://html.spec.whatwg.org/multipage/scripting.html#data-block) to refer to and load content from other message parts.

### Components
> [!NOTE]
> Main Document: [Components](Documents/Components.md)

Markup languages for representing argument could be designed to be extensible with respect to defining and reusing components. Such components could be defined, not in terms of their presentation and interaction, but in terms of their semantics. One could define reusable elements in terms of mappings and transformations between them and knowledge graphs (see also: [R2RML](https://www.w3.org/TR/r2rml/) and [RML](https://kg-construct.github.io/rml-resources/portal/)).

### JavaScript Object Notation and Linked Data

[JSON](https://en.wikipedia.org/wiki/JSON) and [JSON-LD](https://en.wikipedia.org/wiki/JSON-LD) data can be included in MIME messages.

> [!TIP]
> This example shows that arguments could be represented using the AIF model expressed using JSON in a MIME message.
> 
> <details>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
> 
> ```email
> Mime-Version: 1.0
> Content-Type: multipart/related; boundary="boundary-example"
> 
> --boundary-example
> 
> Content-Type: text/plain
> Content-Language: en
> 
> Speaker 1: Disagreements between party members are entirely to be expected.
> Speaker 2: The SNP has disagreements.
> Speaker 1: It's not uncommon for there to be disagreements between party members.
> 
> --boundary-example
> 
> Content-Type: application/json
> Content-Language: en
> 
> {
>   "AIF": {
>     "descriptorfulfillments": null,
>     "edges": [
>       {
>         "edgeID": 0,
>         "fromID": 0,
>         "toID": 4
>       },
>       {
>         "edgeID": 1,
>         "fromID": 4,
>         "toID": 3
>       },
>       {
>         "edgeID": 2,
>         "fromID": 1,
>         "toID": 6
>       },
>       {
>         "edgeID": 3,
>         "fromID": 6,
>         "toID": 5
>       },
>       {
>         "edgeID": 4,
>         "fromID": 2,
>         "toID": 8
>       },
>       {
>         "edgeID": 5,
>         "fromID": 8,
>         "toID": 7
>       },
>       {
>         "edgeID": 6,
>         "fromID": 3,
>         "toID": 9
>       },
>       {
>         "edgeID": 7,
>         "fromID": 9,
>         "toID": 7
>       }
>     ],
>     "locutions": [
>       {
>         "nodeID": 0,
>         "personID": 0
>       },
>       {
>         "nodeID": 1,
>         "personID": 1
>       },
>       {
>         "nodeID": 2,
>         "personID": 2
>       }
>     ],
>     "nodes": [
>       {
>         "nodeID": 0,
>         "text": "disagreements between party members are entirely to be expected.",
>         "type": "L"
>       },
>       {
>         "nodeID": 1,
>         "text": "the SNP has disagreements.",
>         "type": "L"
>       },
>       {
>         "nodeID": 2,
>         "text": "it's not uncommon for there to be disagreements between party members.",
>         "type": "L"
>       },
>       {
>         "nodeID": 3,
>         "text": "disagreements between party members are entirely to be expected.",
>         "type": "I"
>       },
>       {
>         "nodeID": 4,
>         "text": "Default Illocuting",
>         "type": "YA"
>       },
>       {
>         "nodeID": 5,
>         "text": "the SNP has disagreements.",
>         "type": "I"
>       },
>       {
>         "nodeID": 6,
>         "text": "Default Illocuting",
>         "type": "YA"
>       },
>       {
>         "nodeID": 7,
>         "text": "it's not uncommon for there to be disagreements between party members.",
>         "type": "I"
>       },
>       {
>         "nodeID": 8,
>         "text": "Default Illocuting",
>         "type": "YA"
>       },
>       {
>         "nodeID": 9,
>         "text": "Default Inference",
>         "type": "RA"
>       }
>     ],
>     "participants": [
>       {
>         "firstname": "Speaker",
>         "participantID": 0,
>         "surname": "1"
>       },
>       {
>         "firstname": "Speaker",
>         "participantID": 1,
>         "surname": "2"
>       }
>     ],
>     "schemefulfillments": null
>   },
>   "dialog": true,
>   "ova": [],
>   "text": {
>     "txt": " Speaker 1 <span class=\"highlighted\" id=\"0\">disagreements between party members are entirely to be expected.</span>.<br><br> Speaker 2 <span class=\"highlighted\" id=\"1\">the SNP has disagreements.</span>.<br><br> Speaker 1 <span class=\"highlighted\" id=\"2\">it's not uncommon for there to be disagreements between party members.</span>.<br><br>"
>   }
> }
> 
> --boundary-example--
> ```
> </details>

### Metadata

In addition to their uses for representing arguments, argument templates, and networks of interrelated arguments, [knowledge graphs](https://en.wikipedia.org/wiki/Knowledge_graph) could be used in MIME messages to provide [metadata](https://en.wikipedia.org/wiki/Metadata) about other parts in multipart messages.

There exists a `Content-Description` header for providing text descriptions of parts. There could, in particular for content of type `multipart/related`, be a new MIME header, perhaps named `Content-Metadata`, to refer to other parts which serve as metadata for them. Additionally or instead, those parts providing metadata could use a new header, perhaps named `Content-About`, to refer to those parts which they describe.

> [!TIP]
> This example shows how one could include metadata in one MIME message part to describe content in another part.
> 
> <details>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
> 
> ```email
> Mime-Version: 1.0
> Content-Type: multipart/related; boundary="boundary-example"
> 
> --boundary-example
> 
> Content-Type: text/turtle
> Content-About: <part1>
> 
> @prefix dc: <http://purl.org/dc/terms/> .
> @prefix foaf: <http://xmlns.com/foaf/0.1/> .
> 
> <cid:part1> dc:created "2025-06-29 20:00:00.000" ;
>     dc:creator [ a foaf:Person ;
>             foaf:name "Bob Smith" ] .
> 
> --boundary-example
> 
> Content-ID: <part1>
> Content-Type: text/plain
> Content-Language: en
> 
> Climate change is caused by human activities. Therefore, we should reduce carbon emissions.
> 
> --boundary-example--
> ```
> </details>

### Content Negotiation

Agent-driven or reactive [content negotiation](https://en.wikipedia.org/wiki/Content_negotiation) is performed by algorithms in user-agents which choose among the possible variant representations. This is commonly performed using a server-provided list of representations and metadata about them.

One could provide these functionalities using MIME messages. Senders could indicate the availability of content in various formats and languages and online locations without having to include the content in MIME messages.

For example, senders might be able to translate content, on-demand, into a very large set of languages and, instead of having to provide content for each language in a MIME message, they could include content for some popular languages and indicate the availability of and locations of content in other languages.

> [!TIP]
> This example shows a theoretical approach to include content in both English and French while providing recipients with means to obtain remote content in other formats or languages.
> 
> <details>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
> 
> ```email
> Mime-Version: 1.0
> Message-Id: 12345678
> Content-Type: multipart/alternative; boundary="boundary-example"
> 
> --boundary-example
> 
> Content-Type: text/plain
> Content-Language: en
> 
> Climate change is caused by human activities. Therefore, we should reduce carbon emissions.
> 
> --boundary-example
> 
> Content-Type: text/plain
> Content-Language: fr
> 
> Le changement climatique est causé par les activités humaines. Nous devons donc réduire les émissions de carbone.
> 
> --boundary-example
> 
> Content-Type: text/plain
> Content-Language: other1
> Content-Disposition: remote
> Content-Alias: https://service.org/translate.php?mid=12345678&lang=other1
> 
> --boundary-example
> 
> Content-Type: text/plain
> Content-Language: other2
> Content-Disposition: remote
> Content-Alias: https://service.org/translate.php?mid=12345678&lang=other2
> 
> --boundary-example--
> ```
> </details>

### Serialization

Traditional approaches to [serializing](https://en.wikipedia.org/wiki/Serialization) objects have tended to involve transforming object graphs into and from single formats, e.g., binary data, JSON, YAML, XML, or RDF.

Objects could, additionally, be serialized into and be deserialized from MIME messages. During serialization, algorithms could add parts to MIME messages, each part expressed using a format. During deserialization, interrelated message parts would be processed back into objects.

With support for `multipart/alternative` parts and subparts, serialization algorithms would be able to add multiple alternatives into MIME messages and deserialization algorithms would be able to contextually choose from or select from these.

### Security

[Secure Multipurpose Internet Mail Extensions (S/MIME)](https://en.wikipedia.org/wiki/S/MIME) enables security features for MIME messages including [digitally signing](https://en.wikipedia.org/wiki/Digital_signature) messages.

New MIME `Content` headers could be designed for granting permissions and authorizations to and between parts of complex MIME messages, resembling [permissions policies](https://w3c.github.io/webappsec-permissions-policy/) for `<iframe>` nested content and involving HTTP headers.

## Argument Diagrams
> [!NOTE]
> Main Document: [Diagrams](Documents/Diagrams.md)

Argument diagrams are visual representations of one or more arguments.

## Argument Templates
> [!NOTE]
> Main Document: [Templates](Documents/Templates.md)

Argument templates are used to produce arguments.

## A Comparison of Message Models

### Artificial-intelligence APIs, Frameworks, and Protocols

Contemporary artificial-intelligence APIs, frameworks, and protocols include models of messages for exchange between end-users and agents. Components of message models include: message identifiers, timestamps, content parts, roles, annotations, attachments, and metadata.

Artificial-intelligence message models include: [Anthropic](https://docs.anthropic.com/en/api/messages), [Azure AI](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/responses?tabs=python-secure), [Google](https://ai.google.dev/gemini-api/docs/text-generation), [HuggingFace](https://huggingface.co/docs/text-generation-inference/main/en/messages_api), [Ollama](https://ollama.readthedocs.io/en/api/#generate-a-chat-completion), and [OpenAI](https://platform.openai.com/docs/api-reference/messages). Message models in agentic frameworks include: [AutoGen](https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/tutorial/messages.html) and [LangChain](https://python.langchain.com/api_reference/core/messages.html). Message models in multi-agent protocols include: [A2A](https://a2aproject.github.io/A2A/latest/specification/#64-message-object) and [ACP](https://agentcommunicationprotocol.dev/core-concepts/message-structure).

As one can observe, [JavaScript Object Notation (JSON)](https://en.wikipedia.org/wiki/JSON) and related [Remote Procedure Calls (JSON-RPC)](https://en.wikipedia.org/wiki/JSON-RPC) are very popular among artificial-intelligence APIs, frameworks, and protocols. JSON is also utilized by new [AIF libraries](https://github.com/arg-tech/xaif) and forthcoming standards for [representing conversation data](https://docs.vcons.org/en/current-draft).

Will artificial-intelligence APIs, frameworks, and protocols one day support the expressiveness for multipart messages having [`multipart/mixed`](https://en.wikipedia.org/wiki/MIME#mixed), [`multipart/related`](https://en.wikipedia.org/wiki/MIME#related), or [`multipart/alternative`](https://en.wikipedia.org/wiki/MIME#alternative) semantics? Will this expressiveness one day come to include that of the full hierarchical nature of MIME messages, where messages' parts could each be comprised of multiple parts?

Today, artificial-intelligence message models include support for multiple message content parts.

Today, in [Semantic Kernel](https://github.com/microsoft/semantic-kernel), messages are represented using the [`ChatMessageContent`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.semantickernel.chatmessagecontent?view=semantic-kernel-dotnet) class and derived classes. The `ChatMessageContent` class has a property, `MimeType`, for the content type of the message. The `ChatMessageContent` class also supports multiple content items using a [`ChatMessageContentItemCollection`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.semantickernel.chatcompletion.chatmessagecontentitemcollection?view=semantic-kernel-dotnet) collection.

So, it is possible.

### Activity Streams and ActivityPub

With respect to [Activity Streams](https://www.w3.org/TR/activitystreams-core/) and [ActivityPub](https://www.w3.org/TR/activitypub/), the [`Object`](https://www.w3.org/TR/activitystreams-core/#object) type supports attachments and allows a MIME content type, [`mediaType`](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-mediatype), to be specified. The default value for this `mediaType` property is `text/html` and it is presently unclear whether the `Object` type supports multipart MIME types. If not, perhaps [`Collections`](https://www.w3.org/TR/activitystreams-core/#collections) of `Objects` could be of use in these regards.

### Advantages of Multipart Messages

Advantages from supporting MIME's multipart semantics would include, but not be limited to:

1. a well-defined hierarchical structure for message parts to simplify processing,
2. the capability to provide one or more message attachments, e.g., documents, images, audio, video, and data,
3. the capability to provide content alternatives, enabling [content negotiation](https://en.wikipedia.org/wiki/Content_negotiation), [internationalization and localization](https://en.wikipedia.org/wiki/Internationalization_and_localization),
4. interoperability with [RFC 2392](https://datatracker.ietf.org/doc/rfc2392/) URL schemes,
5. the capability to express and include complex data involving multiple interrelated parts in multiple formats,
6. enabling scenarios beyond agentic instant-messaging and chat, e.g., agentic Internet forums,
7. the capability to provide parallel forms of content for simultaneous consumption, e.g., natural-language text and structured-knowledge argumentation.

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
