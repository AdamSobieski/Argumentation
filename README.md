## Introduction

### Abstract Templating

This argumentation framework utilizes abstract templating, detailed below.

A `TemplateGenerator` provides a set of `Parameters` which can be bound to values to produce a `TemplateGenerated`.

Below, both `TextContent` and `Argument` are closed under this operation. They are each both `TemplateGenerators` and `TemplateGenerated`.

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
class TemplateGenerated(Generic[TGENERATOR, TBINDING]):
    def __init__(self, template: TGENERATOR, bindings: Sequence[TBINDING]):
        self._template = template
        self._bindings = bindings

    _template: (TGENERATOR | None)
    _bindings: Sequence[TBINDING]

    @property
    def template(self) -> (TGENERATOR | None):
        return self._template

    @property
    def bindings(self) -> Sequence[TBINDING]:
        return self._bindings
```

### Text Content
`TextContent`, sketched below, harnesses new XML-based approaches to deliver abstract-templating and other features for natural-language text strings.

This data structure is based on [clipboarding](https://www.w3.org/TR/clipboard-apis/) and [data transfer](https://html.spec.whatwg.org/multipage/dnd.html#the-datatransfer-interface) concepts to allow text content to be made available in multiple formats, e.g., `text/plain`, multiple languages, e.g., `en`, and multiple styles, e.g., `MLA`.

This data structure is a `KernelBasedObject`, meaning it receives a [Semantic Kernel](https://github.com/microsoft/semantic-kernel) `Kernel` in its `__init__()` function with which to access a number of artificial-intelligence services, e.g., a chat completion service.

```python
class TextContent(KernelBasedObject, TemplateGenerator['TextContent', Parameter, Binding], TemplateGenerated['TextContent', Binding]):
    pass
```

### Argument
Starting simply, `Argument` is a base class for a number of other argumentation-related classes in this framework. It is closed under its abtract templating operation and presents a `TextContent` claim, where `TextContent` is similarly closed under its abstract templating operation.
```python
class Argument(TemplateGenerator['Argument', Parameter, Binding], TemplateGenerated['Argument', Binding], Categorized['Argument']):
    def __init__(self, claim: TextContent = None, template: 'Argument' = None, bindings: Sequence[Binding] = None, categories: Iterable['Category'['Argument']] = None):
        TemplateGenerator['Argument', Parameter, Binding].__init__(self)
        TemplateGenerated['Argument', Binding].__init__(self, template, bindings)
        Categorized['Argument'].__init__(self, categories)
        self.claim = claim

    claim: TextContent
```
