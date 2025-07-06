## Text

There are a number of text templating systems, e.g., [Handlebars](https://handlebarsjs.com/), [Liquid](https://liquidjs.com/), and [Jinja](https://jinja.palletsprojects.com/en/stable/). For including these templates in multipart MIME messages, Handlebars templates have a content type of `text/x-handlebars-template`, Liquid templates `application/liquid`, and Jinja templates `text/jinja`.

## Markup

Markup-based template technologies include [Extensible Stylesheet Language Transformations (XSLT)](https://en.wikipedia.org/wiki/XSLT). For including these templates in multipart MIME messages, XSLT has a content type of `application/xslt+xml`.

## Knowledge Graphs

With respect to knowledge-graph templates, there exists [Reasonable Ontology Templates (OTTR)](https://www.ottr.xyz/).

## Multipart MIME Messages

Templates could be created with which to produce multipart MIME messages from data sources. Useful features would include being able to dynamically create and ammend content into new parts of multipart messages while being able to refer to these ammended parts using the `cid:` URL scheme.

Perhaps multipart MIME messages and their parts could be represented using knowledge graphs. In such approaches, OTTR could be useful for producing multipart MIME messages from templates and input data.

## Discussion

Advanced argument templating topics include _interactive argument templates_ and _agentic argument templates_. Interactive argument templates are templates with accompanying input forms or questionnaires which end-users or agents would complete to produce arguments. Agentic argument templates are templates which utilize [prompts](https://en.wikipedia.org/wiki/Prompt_engineering) for artificial-intelligence systems to produce arguments.

Blending these ideas together, one user-experience concept involves end-users being able to choose when to make use of one of many special interactive [boilerplate documents](https://en.wikipedia.org/wiki/Boilerplate_text) to create and edit arguments.

As envisioned, the interactive boilerplate documents displayed to end-users would change — their text contents would update — as end-users filled-in blank spaces in them while making use of settings panels or context menus to configure and describe the arguments, their sections, paragraphs, and so forth. Some blank spaces in these special interactive boilerplate documents could be auto-completed, filled-in contextually, based on the contents of those arguments being responded to.
