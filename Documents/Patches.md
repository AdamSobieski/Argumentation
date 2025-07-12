## Introduction

Using multipart MIME, changes to text-based files, e.g., [diffs](https://en.wikipedia.org/wiki/Diff), to knowledge graphs, and to diagrams could be accompanied by annotations, comments, justifications, and/or provenance data, and could be subsequently discussed, argued, and debated.

## Patching Text

A MIME type for text-based differences is `text/x-diff`.

> [!TIP]
> Here is an example of a text-based difference.
>
> <details open>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
>
> ```diff
> - foo(buf, size);
> + foo(obj->buf, obj->size);
> ```
> </details>

## Patching Knowledge Graphs

The MIME type for [linked-data patches](https://www.w3.org/TR/ldpatch/) is `text/ldpatch`.

> [!TIP]
> Here is an example initial knowledge graph, linked-data patch, and resultant knowledge graph.
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

## Patching Diagrams
> [!NOTE]
> More: [Diagrams.md](Diagrams.md)

Patching diagrams can be performed by patching their text-, markup-, or graph-based representations.

## Multipart MIME
> [!NOTE]
> More: [MIME.md](MIME.md)

> [!TIP]
> One could comment on text-based differences or patches.
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
> @prefix ex: <http://www.example.org/#> .
> @prefix foaf: <http://xmlns.com/foaf/0.1/> .
> 
> <mid:12345678> dc:created "2025-06-29 20:00:00.000" ;
>     dc:creator [ a foaf:Person ;
>             foaf:name "Bob Smith" ] ;
>     dc:hasPart <cid:part1>,
>         <cid:part2>,
>         <cid:part3> .
> 
> <cid:part2> ex:commentsOn <cid:part3> .
>
> <cid:part3> ex:patches <https://www.storage.org/file123.cpp>
> 
> --boundary-example
> 
> Content-ID: <part2>
> Content-Type: text/plain
> Content-Language: en
> 
> I think that this is a good idea.
> 
> --boundary-example
> 
> Content-ID: <part3>
> Content-Type: text/x-diff
> 
> - foo(buf, size);
> + foo(obj->buf, obj->size);
> 
> --boundary-example--
> ```
> </details>

> [!TIP]
> One could argue for or against a proposed revision to a knowledgebase.
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

> [!TIP]
> One could argue for or against a proposed revision to a diagram.
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
> <cid:part3> ex:patches <https://www.storage.org/mindmap.mmd>
> 
> --boundary-example
> 
> Content-ID: <part2>
> Content-Type: text/turtle
> 
> @prefix aif: <http://www.arg.dundee.ac.uk/aif#> .
> @prefix ex: <http://example.org/#> .
> 
> ex:Node1 a aif:I-node ;
>     aif:claimText "This content was missing from the diagram." .
> 
> ex:Node2 a aif:RA-node ;
>     aif:hasPremise ex:Node1 ;
>     aif:hasConclusion ex:Node3 .
> 
> ex:Node3 a aif:I-node ;
>     aif:claimText "This content should be added to the diagram." .
> 
> --boundary-example
> 
> Content-ID: <part3>
> Content-Type: text/x-diff
> 
> @@ -10,7 +10,8 @@
>          Uses
>              Creative techniques
>              Strategic planning
>              Argument mapping
> +      On revision processes
>      Tools
>        Pen and paper
>        Mermaid
> 
> --boundary-example--
> ```
> </details>

## Discussion

People and artificial-intelligence agents, during a process of deliberating about a proposed revision to a resource, can each observe, consider, and discuss: (1) the initial resource, (2) the proposed patch or revision process, (3) the proposed resource which results from the application of the proposed patch or revision process to the initial resource, and (4) any differences between the initial and resultant resources.

> [!TIP]
> This diagram shows an abstract model of the topics of discussion when deliberating making a revision to a resource.
> <details open>
> <summary>Click here to toggle the display of this diagram.</summary>
> <br>
>
> ```mermaid
> flowchart LR
>  agent1(Agent 1)
>  agent2(Agent 2)
>  before(Initial Resource)
>  revision(Proposed Patch<br/>or Revision Process)
>  after(Proposed Resource)
>  difference(Differences<br/>Between Resources)  
>  agent1 --- before
>  agent1 --- revision
>  agent1 --- after
>  agent1 --- difference  
>  before --- agent2
>  revision --- agent2
>  after --- agent2
>  difference --- agent2  
> ```
> </details>

## See Also

* [Diff](https://en.wikipedia.org/wiki/Diff)
* [Patch](https://en.wikipedia.org/wiki/Patch_(computing))
