## Introduction

Using multipart MIME, changes to text-based files, e.g., [diffs](https://en.wikipedia.org/wiki/Diff), or to knowledge graphs could be accompanied by justifications, comments, annotations, and/or provenance data, and could be subsequently discussed, argued for, or argued against.

## Text Patching

A MIME type for text-based differences is `text/x-diff`.

> [!TIP]
> Here is an example of a text-based difference.
> ```diff
> - foo(buf, size);
> + foo(obj->buf, obj->size);
> ```

## Knowledge Graph Patching

The MIME type for [linked-data patches](https://www.w3.org/TR/ldpatch/) is `text/ldpatch`.

> [!TIP]
> Here is an example initial knowledge graph, a linked-data patch, and a resultant knowledge graph.
>
> <details open>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
> 
> ```turtle
> @prefix schema: <http://schema.org/> .
> @prefix profile: <http://ogp.me/ns/profile#> .
> @prefix ex: <http://example.org/vocab#> .
> @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
> 
> <#> a schema:Person ;
>   schema:alternateName "TimBL" ;
>   profile:first_name "Tim" ;
>   profile:last_name "Berners-Lee" ;
>   schema:workLocation [ schema:name "W3C/MIT" ] ;
>   schema:performerIn _:b1, _:b2 ;
>   ex:preferredLanguages ( "en" "fr" ).
> 
> _:b1 schema:name "F2F5 - Linked Data Platform" ;
>   schema:url <https://www.w3.org/2012/ldp/wiki/F2F5> .
> 
> _:b2 a schema:Event ;
>   schema:name "TED 2009" ;
>   schema:startDate "2009-02-04" ;
>   schema:url <http://conferences.ted.com/TED2009/> .
> ```
> ```turtle
> @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
> @prefix schema: <http://schema.org/> .
> @prefix profile: <http://ogp.me/ns/profile#> .
> @prefix ex: <http://example.org/vocab#> .
> 
> Delete { <#> profile:first_name "Tim" } .
> Add {
>   <#> profile:first_name "Timothy" ;
>     profile:image <https://example.org/timbl.jpg> .
> } .
> 
> Bind ?workLocation <#> / schema:workLocation .
> Cut ?workLocation .
> 
> UpdateList <#> ex:preferredLanguages 1..2 ( "fr-CH" ) .
> 
> Bind ?event <#> / schema:performerIn [ / schema:url = <https://www.w3.org/2012/ldp/wiki/F2F5> ]  .
> Add { ?event rdf:type schema:Event } .
> 
> Bind ?ted <http://conferences.ted.com/TED2009/> / ^schema:url ! .
> Delete { ?ted schema:startDate "2009-02-04" } .
> Add {
>   ?ted schema:location [
>     schema:name "Long Beach, California" ;
>     schema:geo [
>       schema:latitude "33.7817" ;
>       schema:longitude "-118.2054"
>     ]
>   ]
> } .
> ```
> ```turtle
> @prefix schema: <http://schema.org/> .
> @prefix profile: <http://ogp.me/ns/profile#> .
> @prefix ex: <http://example.org/vocab#> .
> @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
> 
> <#> a schema:Person ;
>   schema:alternateName "TimBL" ;
>   profile:first_name "Timothy" ;
>   profile:last_name "Berners-Lee" ;
>   profile:image <https://example.org/timbl.jpg> ;
>   schema:performerIn _:b1, _:b2 ;
>   ex:preferredLanguages ( "en" "fr-CH" ) .
> 
> _:b1 a schema:Event ;
>   schema:name "F2F5 - Linked Data Platform" ;
>   schema:url <https://www.w3.org/2012/ldp/wiki/F2F5> .
> 
> _:b2 a schema:Event ;
>   schema:name "TED 2009" ;
>   schema:url <http://conferences.ted.com/TED2009/> ;
>   schema:location [
>     schema:name "Long Beach, California";
>     schema:geo [ schema:latitude "33.7817" ; schema:longitude "-118.2054" ]
>   ] .
> ```

## Multipart MIME
> [!NOTE]
> More: [MIME.md](MIME.md)

> [!TIP]
> One could comment on a text-based difference using multipart MIME.
> 
> <details open>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
> 
> ```email
> Mime-Version: 1.0
> Message-ID: 12345678
> Content-Type: multipart/related; boundary="boundary-example"
> 
> --boundary-example
> 
> Content-Type: text/turtle
> Content-About: mid:12345678
> 
> @prefix dc: <http://purl.org/dc/terms/> .
> @prefix ex: <http://www.example.org#> .
> @prefix foaf: <http://xmlns.com/foaf/0.1/> .
> 
> <mid:12345678> dc:created "2025-06-29 20:00:00.000" ;
>     dc:creator [ a foaf:Person ;
>             foaf:name "Bob Smith" ] ;
>     dc:hasPart <cid:part1>,
>         <cid:part2> .
> 
> <cid:part1> ex:commentsOn <cid:part2> .
>
> <cid:part2> ex:patches <https://www.storage.org/file123.cpp>
> 
> --boundary-example
> 
> Content-ID: <part1>
> Content-Type: text/plain
> Content-Language: en
> 
> I think that this is a good idea.
> 
> --boundary-example
> 
> Content-ID: <part2>
> Content-Type: text/x-diff
> 
> - foo(buf, size);
> + foo(obj->buf, obj->size);
> 
> --boundary-example---
> ```
> </details>

More examples coming soon.

## See Also

* [Patch](https://en.wikipedia.org/wiki/Patch_(computing))
