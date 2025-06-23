## Introduction

This project is an argumentation framework designed for interoperability with a large number of artificial-intelligence models and services. This project will explore agentic approaches to creating, analyzing, validating, and evaluating argumentation and debate.

This project utilizes [Semantic Kernel](https://github.com/microsoft/semantic-kernel) to enable developers to more readily explore argumentation-related scenarios using their choice of models and services, e.g.: [OpenAI](https://platform.openai.com/docs/introduction), [Azure OpenAI](https://azure.microsoft.com/en-us/products/ai-services/openai-service), [HuggingFace](https://huggingface.co/), [NVidia](https://www.nvidia.com/en-us/ai-data-science/products/nim-microservices/), or [Ollama](https://ollama.com/).

## Models and Data Structures

### Abstract Templates

This framework makes use of abstract templates. In abstract templating, a `Template` provides a sequence of parameters, each of which can be bound to a value, and these bound parameters altogether can be utilized to produce a `TemplateGenerated`.

```python
TPARAMETER = TypeVar("TPARAMETER", bound=Parameter, default=Parameter)
class Binding(Generic[TPARAMETER], ABC):
    @property
    @abstractmethod
    def parameter(self) -> TPARAMETER:
        pass

    @property
    @abstractmethod
    def value(self) -> Any:
        pass

TGENERATE = TypeVar("TGENERATE", bound='TemplateGenerated', default='TemplateGenerated')
TPARAMETER = TypeVar("TPARAMETER", bound=Parameter, default=Parameter)
TBINDING = TypeVar("TBINDING", bound=Binding, default=Binding)
class Template(Generic[TGENERATE, TPARAMETER, TBINDING], ABC):
    @property
    @abstractmethod
    def parameters(self) -> Sequence[TPARAMETER]:
        pass

    @abstractmethod
    def createBinding(self, parameter: TPARAMETER, value: Any, **kwargs: Any) -> TBINDING:
        pass

    @abstractmethod
    def apply(self, bindings: Iterable[TBINDING]) -> TGENERATE:
        pass

    @abstractmethod
    def substitute(self, mapping: Mapping[TPARAMETER, TPARAMETER]) -> Self:
        pass

TGENERATOR = TypeVar("TGENERATOR", bound=Template, default=Template)
TBINDING = TypeVar("TBINDING", bound=Binding, default=Binding)
class TemplateGenerated(Generic[TGENERATOR, TBINDING], ABC):
    def __init__(self, template: TGENERATOR, bindings: Sequence[TBINDING]):
        self._template = template
        self._bindings = bindings or []

    _template: (TGENERATOR | None)
    _bindings: Sequence[TBINDING]

    @property
    def template(self) -> (TGENERATOR | None):
        return self._template

    @property
    def bindings(self) -> Sequence[TBINDING]:
        return self._bindings
```

### Kernel-based Objects
A `KernelBasedObject` receives a Semantic Kernel `Kernel` in its constructor method with which to access and utilize a number of artificial-intelligence services, e.g., chat-completion services.

```python
class KernelBasedObject:
    def __init__(self, kernel: Kernel):
        self._kernel = kernel

    _kernel: Kernel

    @property
    def kernel(self) -> Kernel:
        return self._kernel
```

### Text Content
`TextContent`, sketched below, is inspired by [clipboarding](https://www.w3.org/TR/clipboard-apis/) and [data-transfer](https://html.spec.whatwg.org/multipage/dnd.html#the-datatransfer-interface) concepts to allow text content to be made available in multiple formats, e.g., `text/plain`, in multiple languages, e.g., `en`, and in multiple styles, e.g., `MLA`.

```python
class TextContent(KernelBasedObject, Template['TextContent', Parameter, Binding], TemplateGenerated['TextContent', Binding]):
    pass
```

### Arguments
`Argument` is a base class for a number of other argumentation-related classes in this framework. This type is closed under its abstract templating operation and presents a `TextContent` claim (where the `TextContent` type similarly closed under its abstract templating operation).

```python
class Argument(Template['Argument', Parameter, Binding], TemplateGenerated['Argument', Binding], Categorized, ABC):
    def __init__(self, claim: TextContent, template: 'Argument' = None, bindings: Sequence[Binding] = None, categories: Iterable[Category] = None):
        Template['Argument', Parameter, Binding].__init__(self)
        TemplateGenerated['Argument', Binding].__init__(self, template, bindings)
        Categorized.__init__(self, categories)
        self._claim = claim

    _claim: TextContent

    @property
    def claim(self) -> TextContent:
        return self._claim
```

A `BridgingArgument` is a type of argument which represents and argues a relationship between a number of premises and a conclusion. This abstract base class starts to resemble some [philosophical definitions of arguments](https://plato.stanford.edu/entries/argument/): "a complex symbolic structure where some parts, known as the premises, offer support to another part, the conclusion."

```python
TARGUMENT = TypeVar("TARGUMENT", bound=Argument, default=Argument)
class BridgingArgument(Generic[TARGUMENT], Argument, ABC):
    def __init__(self, claim: TextContent, template: Argument = None, bindings: Sequence[Binding] = None, categories: Iterable[Category] = None):
        Argument.__init__(self, claim, template, bindings, categories)

    @property
    @abstractmethod
    def premises(self) -> Sequence[TARGUMENT]:
        pass

    @property
    @abstractmethod
    def conclusion(self) -> TARGUMENT:
        pass
```

## Multipurpose Internet Mail Extensions (MIME)

[Multipurpose Internet Mail Extensions (MIME)](https://en.wikipedia.org/wiki/MIME) could be used as a format to serialize arguments to, to deserialize arguments from, to store arguments in filesystems, and to transmit arguments between machines or between artificial-intelligence agents. In Python, working with MIME messages can be done using the [`Message`](https://docs.python.org/3/library/email.compat32-message.html#email.message.Message) class from the `email.message` namespace.

In addition to the [Argument Interchange Format (AIF)](https://en.wikipedia.org/wiki/Argument_Interchange_Format), a new markup language could be of use for expressing and representing both arguments and argument templates.

In the sketch below, one can observe that argument representation formats can use the Content-ID (`cid:`) URL scheme [[RFC 2392](https://datatracker.ietf.org/doc/rfc2392/)] to refer to other serialized objects (e.g., text, JSON, markup, or binary) elsewhere in the multipart data.

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
      <conclusion><cite href="cid:item6">People born in Bermuda are British citizens.</cite></conclusion>
    </argument>
  </premises>
</argument>

--boundary-example-1

Content-ID: <item1>
Content-Type: application/argument+xml
Content-Language: en

<argument>
  <conclusion><parameter href="cid:item4">The person</parameter> is a British citizen.</conclusion>
  <premises>
    <argument>
      <conclusion><parameter href="cid:item4">The person</parameter> was born in Bermuda.</conclusion>
      <evidence-parameter href="cid:item5">Attached is a copy of the birth certificate.</evidence-parameter>
    </argument>
    <argument>
      <conclusion><cite href="cid:item6">People born in Bermuda are British citizens.</cite></conclusion>
    </argument>
  </premises>
</argument>

--boundary-example-1

Content-ID: <item2>
Content-Type: application/octet-stream
Content-Transfer-Encoding: base64

R0lGODlhGAGgAPEAAP/////ZRaCgoAAAACH+PUNvcHlyaWdodCAoQykgMTk5NSBJRVRGLiBVbmF1dGhvcml6ZWQgZHVwbGljYXRpb24gcHJvaGliaXRlZC4A...

--boundary-example-1

Content-ID: <item3>
Content-Type: application/pdf
Content-Language: en
Content-Disposition: attachment; filename="birth_certificate.pdf"
Content-Transfer-Encoding: base64

R0lGODlhGAGgAPEAAP/////ZRaCgoAAAACH+PUNvcHlyaWdodCAoQykgMTk5NSBJRVRGLiBVbmF1dGhvcml6ZWQgZHVwbGljYXRpb24gcHJvaGliaXRlZC4A...

--boundary-example-1

Content-ID: <item4>
Content-Type: application/octet-stream
Content-Transfer-Encoding: base64

R0lGODlhGAGgAPEAAP/////ZRaCgoAAAACH+PUNvcHlyaWdodCAoQykgMTk5NSBJRVRGLiBVbmF1dGhvcml6ZWQgZHVwbGljYXRpb24gcHJvaGliaXRlZC4A...

--boundary-example-1

Content-ID: <item5>
Content-Type: application/octet-stream
Content-Transfer-Encoding: base64

R0lGODlhGAGgAPEAAP/////ZRaCgoAAAACH+PUNvcHlyaWdodCAoQykgMTk5NSBJRVRGLiBVbmF1dGhvcml6ZWQgZHVwbGljYXRpb24gcHJvaGliaXRlZC4A...

--boundary-example-1

Content-ID: <item6>
Content-Type: text/x-bibtex

@article{Brown2023,
author = {John Brown},
title = {An Interesting Article},
journal = {Journal of Interesting Articles},
year = {2023},
}

--boundary-example-1--
```

## Other Templating Systems

[Semantic Kernel](https://github.com/microsoft/semantic-kernel) is interoperable with a number of templating systems and interesting possiblities include exploring these, e.g., [Handlebars](https://handlebarsjs.com/) or [Jinja2](https://jinja.palletsprojects.com/en/stable/), instead of, in addition to, or in combination with the above templating approaches. Such templates could also be referenced by URL in, stored in, and transmitted in MIME messages.

Handlebars templates have a content type of `text/x-handlebars-template` and Jinja templates `text/jinja`.
