## Text

There are a number of text templating systems, e.g., [Handlebars](https://handlebarsjs.com/), [Liquid](https://liquidjs.com/), and [Jinja](https://jinja.palletsprojects.com/en/stable/). Handlebars templates have a content type of `text/x-handlebars-template`, Liquid templates `application/liquid`, and Jinja templates `text/jinja`.

## Markup

> [!TIP]
> In this example, one can observe one approach to implementing markup-based templates.
> 
> <details>
> <summary>Click here to toggle the display of this example.</summary>
> <br>
>
> ```xml
> <argument>
>   <conclusion><parameter bind="object" /> is a British citizen.</conclusion>
>   <premises>
>     <argument>
>       <conclusion><parameter bind="object" /> was born in Bermuda.</conclusion>
>       <parameter bind="evidence" />
>     </argument>
>     <argument>
>       <conclusion><cite href="cid:item3">People born in Bermuda are British citizens.</cite></conclusion>
>     </argument>
>   </premises>
> </argument>
> ```
> ```xml
> <argument template="cid:item1">
>   <conclusion><object>Bob Smith</object> is a British citizen.</conclusion>
>   <premises>
>     <argument>
>       <conclusion><object>Bob Smith</object> was born in Bermuda.</conclusion>
>       <evidence href="cid:item2">Attached is a copy of the birth certificate.</evidence>
>     </argument>
>     <argument>
>       <conclusion><cite href="cid:item3">People born in Bermuda are British citizens.</cite></conclusion>
>     </argument>
>   </premises>
> </argument>
> ```

## Knowledge Graphs

With respect to knowledge-graph templates, there exists [Reasonable Ontology Templates (OTTR)](https://www.ottr.xyz/).

## Advanced

Advanced topics in templating include interactive templates and agentic templates. Interactive templates are templates with accompanying forms or questionnaires which end-users or agents could complete to produce outputs, e.g., computational representations of arguments. Agentic templates resemble scripts, including [prompts](https://en.wikipedia.org/wiki/Prompt_engineering), for artificial-intelligence systems to contextually produce natural-language arguments with accompanying structured knowledge.
