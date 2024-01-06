# md-tester

Test environment for different markdown configurations and setup.

Goal is to create an environment in which:

1. Literal Programming[^why] [^how] documents can be made,
2. Based on `python` to allow for commonality, extensibility, and a wide spread code base and knowledge,
3. In an opinionated layout and style and so allow the author to focus on the content and ensure consistent output using `pandoc`,

The opinionated part comes in the following forms:

1. Same layout of `markdown` files, handled using a [linter](#markdown-linter),
2. A [superset](#syntax) of `commonmark` similar to `rmarkdown` and `pandoc` style `markdown`,
3. Various [output methods](#outputs) using templates.

[^why]: [The Why](https://blog.esciencecenter.nl/literate-programming-in-science-1669094541a7)
[^how]: [The How](https://blog.esciencecenter.nl/literate-programming-in-science-ed94dcc8f758)

## Syntax

In addition to the github flavoured markdown (GFM), the following is expected:

- Properties using `{}`, for example allowing unnumbered or unlisted items in a table of contents,
- Named blocks such as code, text, equasions,
- Fenced code blocks that can be executed, `python` only for now (`` ``` ``),
- Inline code with single backticks (`` ` ``),
- Advanced tables,
- Smartypants,
- Super- and subscript,
- Bibliography, but also with option to include referenced files as attachments,
- Macros for, for example:
    - report specific items (signers, hold lists, revision history, etc.),
    - inclusion of standardised texts (summary blocks, etc.),
    - lists or features from other sources (itp, planning, MDR), etc.,
- Automatic `diff`-ed reports,
- Definition lists,
- Abbreviations,
- ...

Not all ideas have been fully thought out, but note that `Word` isn't easy either and people have taken time to **learn it**.

## Markdown Linter

`pymarkdownlnt` is used as a linter to check for errors on commit. Configuration is done in `pyproject.toml`, with the following notes:

- Extensions:
    - `markdown-disallow-raw-html` enabled,
    - `front-matter` enabled.
    - `markdown-task-list-items` disabled. Some specific status for tasks should be allowed such as cancelled (`-`) and in progress (`/`).
- Plugins:
    - `emphasis-style` forced to use an understore (`_`),
    - `heading-style` forced to use `atx` style only (`#`), without closing,
    - `code-block-style` disabled to allow both indented and backtick style.
    - `fenced-code-language` disabled to allow blocks without a style. This may change in the future, provided a default style could be set,
    - `line-length` disabled to allow very long lines. This has to do with some differences with how hard and soft returns are used and parsed. Would be nice if this can be set to say 80 chars.
    - `no-blanks-blockquote` disabled to allow enters in quotes.
    - `no-duplicate-header` disabled to allow headings with the same text in a single document. Might be confusing at times, but some documents include variants of the same thing. Here headers with the same text can be helpful. Just make sure its is level 2 or below.
    - `ol-prefix` disabled to allow ordered lists to start with a specific number. For example `9.`.
    - `single-h1` disabled to allow multiple level 1 headers in the same document. The `title` is the main one and should be in the `yaml` `front-matter` - there doesn't seem to be a rule for that?

> [!note]
> `pymarkdownlnt` is more commonly known as `pymarkdown`, however there is a pypi package with that name as well. Do not confuse the two.

## Outputs

To reduce control over the styling of a document and to allow authors to focus on the content.

- markdown -- for `git`, `diff`, etc.
- html -- bookdown style,
- pdf -- Tufte would be nice (side margins, etc.),

## Outstanding

- [ ] A lot.
- [ ] Check `title` in `front-matter` is a [linter rule](#markdown-linter) to meet.

### Nice to haves

In no order at all:

- [ ] DO NOT RE-INVENT THE WHEEL and `KISS`,
- [ ] Extract code or texts for future use, copy paste style.
- [ ] Post processing of lessons and final documentation,
- [ ] Checkable items, to log who, date, etc.,
- [ ] A suitable editor (`for dummies`),
    - Live and editable preview,
    - Automatic correction of numbered lists,
    - Automatic correction of references when a header or id changes,
    - Tools to allow quick generation of a basic document,
    - Clear error messages (`python>=3.11` style),
- [ ] Standardised build commands (`make`, cli/web? interface),
- [ ] Collect actions, and todos (`obsidian dataview`?),
