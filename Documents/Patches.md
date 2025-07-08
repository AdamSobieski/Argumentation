## Introduction

Using multipart MIME, one could implement a form of collaborative [version control](https://en.wikipedia.org/wiki/Version_control) system. Changes to text-based files or to knowledge graphs, e.g., [diffs](https://en.wikipedia.org/wiki/Diff), could be accompanied by justifications, comments, and annotations, and could be subsequently discussed, argued for, or argued against.

## Text Patching

A MIME type for text-based differences is `text/x-diff`.

> [!TIP]
> Here is an example of a text-based difference.
> ```diff
> - foo(buf, size);
> + foo(obj->buf, obj->size);
> ```

## Knowledge Graph Patching

A MIME type for [Linked Data patches](https://www.w3.org/TR/ldpatch/) is `text/ldpatch`.

> [!TIP]
> Here is an example initial knowledge graph:
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

> [!TIP]
> Here is an example linked-data patch.
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

> [!TIP]
> Here is an example resultant knowledge graph.
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

## Multipart MIME Example

Coming soon.

## See Also

* [File Comparison](https://en.wikipedia.org/wiki/File_comparison)
* [Patch](https://en.wikipedia.org/wiki/Patch_(computing))
