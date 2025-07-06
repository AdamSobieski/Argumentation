## Text

There are a number of text templating systems, e.g., [Handlebars](https://handlebarsjs.com/), [Liquid](https://liquidjs.com/), and [Jinja](https://jinja.palletsprojects.com/en/stable/). For including these templates in multipart MIME messages, Handlebars templates have a content type of `text/x-handlebars-template`, Liquid templates `application/liquid`, and Jinja templates `text/jinja`.

## Markup

Markup-based template technologies include [Extensible Stylesheet Language Transformations (XSLT)](https://en.wikipedia.org/wiki/XSLT). For including these templates in multipart MIME messages, XSLT has a content type of `application/xslt+xml`.

## Knowledge Graphs

With respect to knowledge-graph templates, there exists [Reasonable Ontology Templates (OTTR)](https://www.ottr.xyz/).

## Diagrams
> [!NOTE]
> Main Document: [Diagrams](Diagrams.md)

Templates could be of use for producing diagrams, visual representations of arguments.

Text, markup, and knowledge graphs can all be transformed into argument diagrams. Templates for text, markup, and knowledge graphs, then, could be of use for producing content which can be transformed into argument diagrams.

## Multipart MIME

Templates could be created with which to produce multipart MIME messages from data sources. Useful features would include being able to dynamically create and ammend content into new parts of multipart messages while being able to refer to these ammended parts using the `cid:` URL scheme.

Perhaps multipart MIME messages and their parts could be represented using knowledge graphs. These knowledge graphs would be capable of being transformed into multipart MIME messages. OTTR would be useful in these approaches.

## Discussion

Advanced argument templating topics include _interactive argument templates_ and _agentic argument templates_. Interactive argument templates are templates with accompanying input forms or questionnaires which end-users or agents would complete to produce arguments. Agentic argument templates are templates which utilize [prompts](https://en.wikipedia.org/wiki/Prompt_engineering) for artificial-intelligence systems to produce arguments.

Blending these ideas together, end-users could search for, receive recommendations regarding, select from, and utilize interactive argument templates, [boilerplate](https://en.wikipedia.org/wiki/Boilerplate_text) documents, to, via [document assembly](https://en.wikipedia.org/wiki/Document_automation) techniques, create and edit arguments.

As envisioned, the interactive documents displayed to end-users would change — their text contents would update — as end-users filled-in any blank spaces in them. End-users would also be able to make use of settings panels or context menus to configure and describe their overall arguments, their sections, paragraphs, and so forth.

Some blank spaces in these interactive boilerplate documents could be automatically filled-in, contextually, based on the contents of those arguments being responded to.

Brainstorming, assuming that one could (e.g., using large language models) generate natural-language arguments from argument diagrams and argument diagrams from natural-language arguments, end-users would also be able to use content-authoring tools to view both of these representations simultaneously and to modify either to observe artificial-intelligence systems modifying and updating the other accordingly.
