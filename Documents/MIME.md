## Metadata

There exists a `Content-Description` header for providing text descriptions of parts. There could be created a new MIME header, perhaps named `Content-Metadata`, to refer to those parts which serve as metadata for a message or message part.

### Message Parts

[Knowledge graphs](https://en.wikipedia.org/wiki/Knowledge_graph) could be of use in multipart MIME messages for providing [metadata](https://en.wikipedia.org/wiki/Metadata) about other parts in multipart messages.

> [!TIP]
> One could include metadata in one MIME message part to describe another message part.
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
> Content-Type: text/turtle
> 
> @prefix dc: <http://purl.org/dc/terms/> .
> @prefix foaf: <http://xmlns.com/foaf/0.1/> .
> 
> <cid:part2> dc:created "2025-06-29 20:00:00.000" ;
>     dc:creator [ a foaf:Person ;
>             foaf:name "Bob Smith" ] .
> 
> --boundary-example
> 
> Content-ID: <part2>
> Content-Type: text/plain
> Content-Language: en
> Content-Metadata: <part1>
> 
> Climate change is caused by human activities. Therefore, we should reduce carbon emissions.
> 
> --boundary-example--
> ```
> </details>

### Whole Messages

[Knowledge graphs](https://en.wikipedia.org/wiki/Knowledge_graph) could be of use in multipart MIME messages to describe them, their parts, and any relationships between their parts.

> [!TIP]
> One could include metadata in a MIME message part to describe the containing message using the `mid:` URL scheme and its message parts using the `cid:` URL scheme.
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
> @prefix ex: <http://www.example.org#> .
> @prefix foaf: <http://xmlns.com/foaf/0.1/> .
> 
> <mid:12345678> dc:created "2025-06-29 20:00:00.000" ;
>     dc:creator [ a foaf:Person ;
>             foaf:name "Bob Smith" ] ;
>     dc:hasPart <cid:part1>,
>         <cid:part2>,
>         <cid:part3> .
> 
> <cid:part2> ex:hasDiagram <cid:part3> .
> 
> --boundary-example
> 
> Content-ID: <part2>
> Content-Type: text/plain
> Content-Language: en
> 
> Climate change is happening and causing rising global temperatures.
> Climate change is primarily caused by human activities or is a result of natural cycles.
> Greenhouse gas emissions contribute to anthropogenic factors causing climate change.
> 
> --boundary-example
> 
> Content-ID: <part3>
> Content-Type: text/vnd.mermaid
> Content-Language: en
> 
> graph LR
>  A[Climate change is happening] --> B[Rising global temperatures]
>  F[Human activities are the primary cause] --> A
>  G[Greenhouse gas emissions] --> F
>  H[Counter-argument: Natural cycles] --> A
> 
> --boundary-example--
> ```
> </details>

## Content Negotiation

Agent-driven or reactive [content negotiation](https://en.wikipedia.org/wiki/Content_negotiation) is performed by algorithms in user-agents which choose among the possible variant representations. This is commonly performed using a server-provided list of representations and metadata about them.

One could provide these functionalities using MIME messages. Senders could indicate the availability of content in various formats and languages and online locations without having to include the content in MIME messages.

> [!TIP]
> One could include content in some formats and languages while providing recipients with means to obtain remote content in other formats or languages.
> 
> <details open>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
> 
> ```email
> Mime-Version: 1.0
> Message-Id: <12345678>
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
> Content-Language: de
> Content-Disposition: remote
> Content-Alias: https://service.org/translate.php?mid=12345678&lang=de
> 
> --boundary-example
> 
> Content-Type: text/plain
> Content-Language: es
> Content-Disposition: remote
> Content-Alias: https://service.org/translate.php?mid=12345678&lang=es
> 
> --boundary-example--
> ```
> </details>

## Diffs and Patches
> [!NOTE]
> More: [Patches.md](Patches.md)

Using multipart MIME, changes to text-based files, e.g., diffs, and to knowledge graphs could be accompanied by annotations, comments, justifications, and/or provenance data, and could be subsequently discussed, argued, and debated.

## Serialization and Deserialization

Traditional approaches to [serialization](https://en.wikipedia.org/wiki/Serialization) have tended to involve transforming object graphs into single formats, e.g., binary data, JSON, YAML, XML, or RDF.

Object graphs could, additionally, be serialized into and deserialized from MIME messages. During serialization, algorithms could add message parts to MIME messages. During deserialization, interrelated message parts, these parts perhaps utilizing multiple formats, would be processed back into object graphs.

## Security

[Secure Multipurpose Internet Mail Extensions (S/MIME)](https://en.wikipedia.org/wiki/S/MIME) enables security features for MIME messages such as [digitally signing](https://en.wikipedia.org/wiki/Digital_signature) messages.

## See Also

* [MHTML](https://en.wikipedia.org/wiki/MHTML)
* [MAFF](https://en.wikipedia.org/wiki/Mozilla_Archive_Format)
* [Web Archive](https://en.wikipedia.org/wiki/Web_Archive_(file_format))
* [WARC](https://en.wikipedia.org/wiki/WARC_(file_format))
* [HAR](https://en.wikipedia.org/wiki/HAR_(file_format))
* [EPUB](https://en.wikipedia.org/wiki/EPUB)
