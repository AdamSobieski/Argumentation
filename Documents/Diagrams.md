# Introduction

[Argument maps](https://en.wikipedia.org/wiki/Argument_map) are diagrammatic representations of the structures of one or more arguments. Argument maps are useful for representing and analyzing existing writings and for helping end-users to think through issues as parts of problem-structuring and writing processes.

# Diagram Formats

## Mermaid

[Mermaid](https://en.wikipedia.org/wiki/Mermaid_(software)) is a popular technology for generating diagrams from text descriptions. Its MIME type is `text/vnd.mermaid`.

> [!TIP]
> Here is an example Mermaid diagram.
>
> <details>
> <summary>Click here to toggle the display of this example.</summary>
> 
> ```mermaid
> graph LR
>   A[Climate change is happening] --> B[Rising global temperatures]
>   F[Human activities are the primary cause] --> A
>   G[Greenhouse gas emissions] --> F
>   H[Counter-argument: Natural cycles] --> A
> ```
> </details>

## Argdown

[Argdown](https://argdown.org/) is a markdown-inspired lightweight markup language for complex argumentation. It is intended for exchanging arguments and argument reconstructions in a universally accessible and highly human-readable way. Argdown provides tools which transform documents into argument maps.
