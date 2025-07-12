## The Computational Representation of Arguments

### Multipurpose Internet Mail Extensions
> [!NOTE]
> More: [Documents/MIME.md](Documents/MIME.md)

[Multipurpose Internet Mail Extensions (MIME)](https://en.wikipedia.org/wiki/MIME) can be utilized as a format to serialize arguments to, to deserialize arguments from, to store arguments as files, and to transmit arguments between end-users and agents.

> [!TIP]
> The [Argument Interchange Format (AIF)](https://en.wikipedia.org/wiki/Argument_Interchange_Format) can be used in MIME messages.
> 
> <details open>
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
> @prefix ex: <http://example.org/#> .
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

Wherever a URL can be used, contents within parts of multipart MIME messages can use the `cid:` URL scheme from [RFC 2392](https://datatracker.ietf.org/doc/rfc2392/) to refer to other parts of multipart MIME messages.

> [!TIP]
> One could reference a picture or image in a multimodal argument.
> 
> <details open>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
> 
> ```email
> Mime-Version: 1.0
> Message-ID: <12345678>
> Content-Type: multipart/related; boundary="boundary-example"
> 
> --boundary-example
> 
> Content-ID: <part1>
> Content-Type: text/turtle
> Content-Language: en
> 
> @prefix aif: <http://www.arg.dundee.ac.uk/aif#> .
> @prefix ex: <http://example.org/#> .
> @prefix ext: <http://extension.org/#> .  
> 
> ex:Node1 a ext:E-node ;
>     ext:hasEvidence <cid:part2> .
> 
> ex:Node2 a ext:ES-node ;
>     ext:supported ex:Node3 ;
>     ext:supportedBy ex:Node1 .
> 
> ex:Node3 a aif:I-node ;
>     aif:claimText "We should reduce carbon emissions." .
> 
> --boundary-example
> 
> Content-ID: <part2>
> Content-Type: image/png
> Content-Transfer-Encoding: base64
> 
> TG9yZW0gaXBzdW0gZG9sb3Igc2l0IGFtZXQsIGNvbnNlY3RldHVyIGFkaXBpc2NpbmcgZWxpdC4g
> U2VkIGRvIGVpdXNtb2QgdGVtcG9yIGluY2lkaWR1bnQgdXQgbGFib3JlIGV0IGRvbG9yZSBtYWdu
> YSBhbGlxdWEuIFV0IGVuaW0gYWQgbWluaW0gdmVuaWFtLCBxdWlzIG5vc3RydWQgZXhlcmNpdGF0
> aW9uIHVsbGFtY28gbGFib3JpcyBuaXNpIHV0IGFsaXF1aXAgZXggZWEgY29tbW9kbyBjb25zZXF1
> YXQuCg==
> 
> --boundary-example--
> ```
> </details>

> [!TIP]
> One could attach other resources as evidence and otherwise cite scholarly and scientific publications.
> 
> <details open>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
> 
> ```email
> Mime-Version: 1.0
> Content-Type: multipart/related; boundary="boundary-example"
> 
> --boundary-example
> 
> Content-ID: <part1>
> Content-Type: text/plain
> Content-Language: en
> 
> Climate change is caused by human activities. Therefore, we should reduce carbon emissions.
> 
> --boundary-example
> 
> Content-ID: <part2>
> Content-Type: text/turtle
> Content-Language: en
> 
> @prefix aif: <http://www.arg.dundee.ac.uk/aif#> .
> @prefix ex: <http://example.org/#> .
> @prefix ext: <http://extension.org/#> .
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
>     ext:hasEvidence <cid:part3> .
> 
> ex:Node5 a ext:ES-node ;
>     ext:supported ex:Node1 ;
>     ext:supportedBy ex:Node4 .
> 
> ex:Node6 a ext:C-node ;
>     ext:cites <cid:part4> .
> 
> ex:Node7 a ext:CS-node ;
>     ext:supported ex:Node1 ;
>     ext:supportedBy ex:Node6 .
> 
> --boundary-example
> 
> Content-ID: <part3>
> Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet
> Content-Language: en
> Content-Disposition: attachment; filename="evidence.xslx"
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
> Content-ID: <part4>
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

Using a potential `Content-Metadata` header, one could include, as a message part, metadata describing a multipart message and its parts.

> [!TIP]
> One could argue about proposed revisions to text-based resources (e.g., a source-code file), knowledge-graph resources (e.g., a knowledgebase), and diagrammatic resources (e.g., a concept map).
> 
> <details open>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
>
> ```email
> Mime-Version: 1.0
> Message-ID: <12345678>
> Content-Type: multipart/related; boundary="boundary-example"
> Content-Metadata: <part1>
> 
> --boundary-example
> 
> Content-ID: <part1>
> Content-Type: text/turtle
> 
> @prefix dc: <http://purl.org/dc/terms/> .
> @prefix ex: <http://example.org/#> .
> @prefix foaf: <http://xmlns.com/foaf/0.1/> .
> 
> <mid:12345678> dc:created "2025-06-29 20:00:00.000" ;
>     dc:creator [ a foaf:Person ;
>             foaf:name "Bob Smith" ] ;
>     dc:hasPart <cid:part1>,
>         <cid:part2>,
>         <cid:part3> .
> 
> <cid:part2> ex:arguesForPerforming <cid:part3> .
> 
> <cid:part3> ex:patches <https://www.storage.org/kb-endpoint#>
>
> --boundary-example
>
> Content-ID: <part2>
> Content-Type: text/turtle
> Content-Language: en
> 
> @prefix aif: <http://www.arg.dundee.ac.uk/aif#> .
> @prefix ex: <http://example.org/#> .
> 
> ex:Node1 a aif:I-node ;
>     aif:claimText "This triple was missing from the knowledgebase." .
> 
> ex:Node2 a aif:RA-node ;
>     aif:hasPremise ex:Node1 ;
>     aif:hasConclusion ex:Node3 .
> 
> ex:Node3 a aif:I-node ;
>     aif:claimText "This triple should be added to the knowledgebase." .
> 
> --boundary-example
> 
> Content-ID: <part3>
> Content-Type: text/ldpatch
> 
> Add { <http://example.org/#s1> <http://example.org/#p1> <http://example.org/#o1> } .
> 
> --boundary-example--
> ```
> </details>

### Extensible Markup Language Literals

The AIF's `claimText` property could be provided with, beyond simple text-string literals, XML content.

> [!TIP]
> XML can enable referring to multimedia resources, evidence, cited resources, and other content &ndash; other parts of a multipart MIME message &ndash; in an inline manner within literals.
> <details open>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
>   
> ```turtle
> ex:Node1
> aif:claimText
> "As one can see in <picture src='cid:part2'>this picture</picture>..."^^rdf:XMLLiteral .
> ```
> ```turtle
> ex:Node1
> aif:claimText
> "<evidence href='cid:part3'>This data</evidence> indicates..."^^rdf:XMLLiteral .
> ```
> ```turtle
> ex:Node1
> aif:claimText
> "<cite href='cid:part4'>This paper</cite> suggests..."^^rdf:XMLLiteral .
> ```
> ```turtle
> ex:Node1
> aif:claimText
> "<ref href='cid:part5#triple'>This triple</ref> should be added..."^^rdf:XMLLiteral .
> ```
> </details>

### Argument Diagrams
> [!NOTE]
> More: [Documents/Diagrams.md](Documents/Diagrams.md)

[Argument diagrams](https://en.wikipedia.org/wiki/Argument_map) are visual representations of one or more arguments. These diagrams are useful for representing and analyzing existing argumentative writings and for helping end-users to think through issues during problem-structuring and argumentative writing processes.

> [!TIP]
> Argument diagrams could accompany other formats of arguments in MIME messages.
> 
> <details open>
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
> Climate change is happening and causing rising global temperatures.
> Climate change is primarily caused by human activities or is a result of natural cycles.
> Greenhouse gas emissions contribute to anthropogenic factors causing climate change.
>
> --boundary-example
>
> Content-Type: text/vnd.mermaid
> Content-Language: en
>
> graph LR
>  A[Climate change is happening] --> B[Rising global temperatures]
>  F[Human activities are the primary cause] --> A
>  G[Greenhouse gas emissions] --> F
>  H[Counter-argument: Natural cycles] --> A
>
> --boundary-example---
> ```

## A Comparison of Message Models

### Artificial-intelligence APIs, Frameworks, and Protocols

Contemporary artificial-intelligence APIs, frameworks, and protocols include models of messages for exchange between end-users and agents. Components of message models include: message identifiers, timestamps, content parts, roles, annotations, attachments, and metadata.

Artificial-intelligence message models include: [Anthropic](https://docs.anthropic.com/en/api/messages), [Azure AI](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/responses?tabs=python-secure), [Google](https://ai.google.dev/gemini-api/docs/text-generation), [HuggingFace](https://huggingface.co/docs/text-generation-inference/main/en/messages_api), [Ollama](https://ollama.readthedocs.io/en/api/#generate-a-chat-completion), and [OpenAI](https://platform.openai.com/docs/api-reference/messages). Message models in agentic frameworks include: [AutoGen](https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/tutorial/messages.html) and [LangChain](https://python.langchain.com/api_reference/core/messages.html). Message models in multi-agent protocols include: [A2A](https://a2aproject.github.io/A2A/latest/specification/#64-message-object) and [ACP](https://agentcommunicationprotocol.dev/core-concepts/message-structure).

As one can observe, [JavaScript Object Notation (JSON)](https://en.wikipedia.org/wiki/JSON) and related [Remote Procedure Calls (JSON-RPC)](https://en.wikipedia.org/wiki/JSON-RPC) are very popular among artificial-intelligence APIs, frameworks, and protocols. JSON is also utilized by new [AIF libraries](https://github.com/arg-tech/xaif) and emerging standards for [conversation transcripts](https://datatracker.ietf.org/group/vcon/about/).

Will artificial-intelligence APIs, frameworks, and protocols one day support the expressiveness for multipart messages having [`multipart/mixed`](https://en.wikipedia.org/wiki/MIME#mixed), [`multipart/related`](https://en.wikipedia.org/wiki/MIME#related), or [`multipart/alternative`](https://en.wikipedia.org/wiki/MIME#alternative) semantics? Will this expressiveness one day come to include that of the full hierarchical and recursive nature of MIME messages, where messages' parts can each be comprised of multiple parts?

Today, artificial-intelligence message models include support for multiple message content parts.

Today, in [Semantic Kernel](https://github.com/microsoft/semantic-kernel), messages are represented using the [`ChatMessageContent`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.semantickernel.chatmessagecontent?view=semantic-kernel-dotnet) class and derived classes. The `ChatMessageContent` class has a property, `MimeType`, for the content type of the message. The `ChatMessageContent` class also supports multiple content items using a [`ChatMessageContentItemCollection`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.semantickernel.chatcompletion.chatmessagecontentitemcollection?view=semantic-kernel-dotnet) collection.

So, it is possible.

### Activity Streams and ActivityPub

With respect to [Activity Streams](https://www.w3.org/TR/activitystreams-core/) and [ActivityPub](https://www.w3.org/TR/activitypub/), the [`Object`](https://www.w3.org/TR/activitystreams-core/#object) type supports attachments and allows a MIME content type, [`mediaType`](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-mediatype), to be specified. The default value for this `mediaType` property is `text/html` and it is presently unclear whether the `Object` type supports multipart MIME types. If not, perhaps [`Collections`](https://www.w3.org/TR/activitystreams-core/#collections) of `Objects` could be of use in these regards.

### Advantages of Multipart Messages

Benefits and advantages from supporting MIME's multipart semantics include:

1. a well-defined hierarchical and recursive structure for messages' parts to simplify processing,
2. the capability to provide one or more message attachments, e.g., documents, images, audio, video, and data,
3. the capability to provide content alternatives, enabling [content negotiation](https://en.wikipedia.org/wiki/Content_negotiation), [internationalization and localization](https://en.wikipedia.org/wiki/Internationalization_and_localization),
4. interoperability with [RFC 2392](https://datatracker.ietf.org/doc/rfc2392/) URL schemes (`cid:` and `mid:`),
5. the capability to express and include complex data involving multiple interrelated parts in multiple formats,
6. the capability to provide parallel forms of content for simultaneous consumption, e.g., text, hypertext, and structured-knowledge argumentation.
7. enabling scenarios beyond agentic instant-messaging and chat, e.g., agentic Internet forums,

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

End-users could contribute to and participate in [Internet forums](https://en.wikipedia.org/wiki/Internet_forum) for (man-machine) discussion and debate.

## Discussion

### Federation

For public groups, mailing-list servers, archives, and related knowledgebases could be [federated](https://en.wikipedia.org/wiki/Federation_(information_technology)), interconnected and synchronized in the sense of the [Fediverse](https://en.wikipedia.org/wiki/Fediverse). End-users would, then, be able to receive periodic [digests](https://en.wikipedia.org/wiki/Email_digest) or [interactive dashboards](https://en.wikipedia.org/wiki/Dashboard_(computing)) summarizing developments and events of interest to them from across federated public mailing lists.

Internet forums are also capable of federation. Examples of such software include [Lemmy](https://join-lemmy.org/) and [NodeBB](https://nodebb.org/).

### Publish-subscribe Pattern

The [publish-subscribe pattern](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern) is a messaging pattern in which message senders, called publishers, categorize messages into classes, or topics, and send them without needing to know which components will receive them. Examples of such protocols include [WebSub](https://en.wikipedia.org/wiki/WebSub).

Artificial-intelligence tools could categorize messages and discussion threads for purposes of routing them or digests summarizing them to interested end-users. [Embeddings](https://en.wikipedia.org/wiki/Embedding_(machine_learning)) could be of use for representing messages' and threads' classes, or topics.

## Related Work

* [IETF Structured Email Working Group](https://datatracker.ietf.org/group/sml/about/)
