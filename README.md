## Introduction

### Abstract Templates

This argumentation framework utilizes abstract templates. In abstract templating, a `TemplateGenerator` provides a sequence of `Parameters`, each of which can be bound to a value, these altogether utilized when producing a `TemplateGenerated`.

```python
TPARAMETER = TypeVar("TPARAMETER", bound=Parameter, default=Parameter)
class Binding(Generic[TPARAMETER]):
    parameter: TPARAMETER
    value: Any

TGENERATED = TypeVar("TGENERATED", bound='TemplateGenerated', default='TemplateGenerated')
TPARAMETER = TypeVar("TPARAMETER", bound=Parameter, default=Parameter)
TBINDING = TypeVar("TBINDING", bound=Binding, default=Binding)
class TemplateGenerator(Generic[TGENERATED, TPARAMETER, TBINDING], ABC):
    @property
    @abstractmethod
    def parameters(self) -> Sequence[TPARAMETER]:
        pass

    @abstractmethod
    def createBinding(self, parameter: TPARAMETER, value: Any, **kwargs: Any) -> TBINDING:
        pass

    @abstractmethod
    def apply(self, bindings: Iterable[TBINDING]) -> TGENERATED:
        pass

    @abstractmethod
    def substitute(self, mapping: Mapping[TPARAMETER, TPARAMETER]) -> Self:
        pass

TGENERATOR = TypeVar("TGENERATOR", bound=TemplateGenerator, default=TemplateGenerator)
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
A `KernelBasedObject` receives a [Semantic Kernel](https://github.com/microsoft/semantic-kernel) `Kernel` in its `__init__()` function with which to access and utilize a number of artificial-intelligence services, e.g., chat-completion services.

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
class TextContent(KernelBasedObject, TemplateGenerator['TextContent', Parameter, Binding], TemplateGenerated['TextContent', Binding]):
    pass
```

### Arguments
`Argument` is a base class for a number of other argumentation-related classes in this framework. It is closed under its abstract templating operation and presents a `TextContent` claim (where `TextContent` is similarly closed under its abstract templating operation).
```python
class Argument(TemplateGenerator['Argument', Parameter, Binding], TemplateGenerated['Argument', Binding], Categorized['Argument'], ABC):
    def __init__(self, claim: TextContent, template: 'Argument' = None, bindings: Sequence[Binding] = None, categories: Iterable['Category'['Argument']] = None):
        TemplateGenerator['Argument', Parameter, Binding].__init__(self)
        TemplateGenerated['Argument', Binding].__init__(self, template, bindings)
        Categorized['Argument'].__init__(self, categories)
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
    def __init__(self, claim: TextContent, template: Argument = None, bindings: Sequence[Binding] = None, categories: Iterable['Category'[Argument]] = None):
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
