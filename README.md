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
`TextContent`, sketched below, makes use of markup-based techniques to deliver abstract templating and other features for natural-language text. This data structure is inspired by [clipboarding](https://www.w3.org/TR/clipboard-apis/) and [data-transfer](https://html.spec.whatwg.org/multipage/dnd.html#the-datatransfer-interface) concepts to allow text content to be made available in multiple formats, e.g., `text/plain`, in multiple languages, e.g., `en`, and in multiple styles, e.g., `MLA`.

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

## Using Multipurpose Internet Mail Extensions (MIME)

[Multipurpose Internet Mail Extensions (MIME)](https://en.wikipedia.org/wiki/MIME) could be used as a format to serialize arguments to, to deserialize arguments from, to store arguments in filesystems, and to transmit arguments between machines.

In the sketch below, one can observe that argumentation-related markup languages could use the Content-ID (`cid:`) URL scheme [[RDF 2392](https://datatracker.ietf.org/doc/rfc2392/)] to refer to other serialized objects (e.g., JSON, markup, or binary) elsewhere in the multipart data.

```
Mime-Version: 1.0
Content-Type: multipart/related; boundary="boundary-example-1"

Bob Smith is a British citizen. Bob Smith was born in Bermuda. People born in Bermuda are British citizens. Attached is a copy of the birth certificate.

--boundary-example-1--
Content-Type: text/argument+xml

<text template-href="cid:foo1">
  <sentence class="conclusion"><object href="cid:foo2">Bob Smith</object> is a British citizen.</sentence>
  <sentence class="premise"><object href="cid:foo2">Bob Smith</object> was born in Bermuda.</sentence>
  <sentence class="premise">People born in Bermuda are British citizens.</sentence>
  <sentence class="premise"><evidence href="cid:foo3">Attached is a copy of the birth certificate.<evidence></sentence>
</text>

--boundary-example-1--

Content-ID: <foo1>
Content-Type: text/argument+xml

<text>
  <sentence class="conclusion"><parameter href="cid:foo4">The seller</parameter> is a British citizen.</sentence>
  <sentence class="premise"><parameter" href="cid:foo4">The seller</parameter> was born in Bermuda.</sentence>
  <sentence class="premise">People born in Bermuda are British citizens.</sentence>
  <sentence class="premise"><evidence-parameter>Attached is a copy of the birth certificate.</evidence-parameter></sentence>
</text>

--boundary-example-1--

Content-ID: <foo2>
Content-Type: application/octet-stream
Content-Transfer-Encoding: BASE64

R0lGODlhGAGgAPEAAP/////ZRaCgoAAAACH+PUNvcHlyaWdodCAoQykgMTk5NSBJRVRGLiBVbmF1dGhvcml6ZWQgZHVwbGljYXRpb24gcHJvaGliaXRlZC4A...

--boundary-example-1--

Content-ID: <foo3>
Content-Type: application/pdf
Content-Disposition: attachment; filename="birth_certificate.pdf"
Content-Transfer-Encoding: BASE64

R0lGODlhGAGgAPEAAP/////ZRaCgoAAAACH+PUNvcHlyaWdodCAoQykgMTk5NSBJRVRGLiBVbmF1dGhvcml6ZWQgZHVwbGljYXRpb24gcHJvaGliaXRlZC4A...

--boundary-example-1--

Content-ID: <foo4>
Content-Type: application/octet-stream
Content-Transfer-Encoding: BASE64

R0lGODlhGAGgAPEAAP/////ZRaCgoAAAACH+PUNvcHlyaWdodCAoQykgMTk5NSBJRVRGLiBVbmF1dGhvcml6ZWQgZHVwbGljYXRpb24gcHJvaGliaXRlZC4A...
```
