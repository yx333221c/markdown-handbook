# Cheat Sheet

> 中文: [zh/cheatsheet.md](../zh/cheatsheet.md)

Keep this page open when you cannot remember how a symbol is spelled. Every example below sits in a fenced block, because that block is the source you came to see; single symbols in the prose get inline code. For why a rule ended up the way it did, read [commonmark.md](../../03-spec/en/commonmark.md) and [gfm.md](../../03-spec/en/gfm.md).

## Headings

`#` at the start, followed by a space. One to six of them give you `<h1>` through `<h6>`. Close with another run of `#` on the same line and the parser drops it. `#hashtag` stays plain text.

```markdown
# One
### Three
## Two ##
#hashtag
```

Setext is the other spelling: underline the text with `=` or `-`.

```markdown
Big title
=========

Small title
-----------
```

`=` gives `<h1>`, `-` gives `<h2>`. It collides with the thematic break, so whether `---` is an underline or a rule depends on the blank line above it. I stick to `#`.

## Paragraphs and line breaks

A blank line starts a new paragraph. A single newline usually folds into a space; that is a soft break. For a hard break, leave two trailing spaces or end the line with `\`:

```markdown
First line  
Second line

First line\
Second line
```

Both produce a `<br>`. Editors strip trailing spaces when you paste, so the `\` form is less fragile.

## Emphasis

`*x*` or `_x_` becomes `<em>`; `**x**` or `__x__` becomes `<strong>`.

```markdown
*italic*  _also italic_
**bold**  __also bold__
```

`snake_case_name` stays literal, since CommonMark does not make emphasis from underscores inside a word. Forget to close a `*` and the rest of the paragraph turns italic. For a literal asterisk write `\*`; backslash escapes only work on ASCII punctuation.

## Lists

`-`, `*`, or `+` open a bullet list. A number and a dot open an ordered one. Indent to nest, and leave a blank line before the sub-list:

```markdown
- Apple
- Pear
  - Bartlett
- Banana

1. First
2. Second
```

Mixing `-` and `*` in one file works but gets hard to scan, so I use `-` everywhere. Gruber's page never settled how many spaces a sub-list needs, or when a list item should wrap in `<p>`. The GFM spec lists those open questions in section 1.3.

## Block quotes

`>` opens a quote. Put `>` on consecutive lines to keep one paragraph; `>>` nests another quote:

```markdown
> Quoted line,
> continued here.
>
> > One level deeper.
```

In GFM, `> ` followed by `- [ ]` gives you a task list item, covered below.

## Code

Wrap short spans in backticks, like `README.md`. For a block you have two options. A fenced block uses at least three backticks or tildes; the closing fence must use the same character and be at least as long as the opening one:

````markdown
```python
print("hi")
```
````

That snippet needs an outer fence of four backticks to hold it. The first word of the info string usually names the language, and the HTML gets a `language-` prefixed class such as `language-python`. An indented code block instead puts four spaces at the front of every line, needs a blank line before it, and cannot interrupt a paragraph:

```markdown
    four spaces in
    still code
```

## Links, images, autolinks

Three ways to write a link. Add `!` at the front for an image:

```markdown
[text](https://example.com "title")
[text][id]
<https://example.com>
![alt text](pic.png)

[id]: https://example.com
```

The `[id]: url` line is a link reference definition. Put it anywhere; it renders nothing visible. Gruber never said which of two same-named definitions wins. The square brackets on an image hold the `alt` text, so do not leave them empty.

## Thematic breaks

Three or more `-`, `*`, or `_` on their own line make a thematic break, with spaces allowed between them:

```markdown
---
***
- - -
```

Four spaces of indent turn the same line into an indented code block instead. Watch the blank line above, since that is what separates a break from a Setext `-` underline.

## GFM extensions

These are not in Gruber's original syntax. GitHub added them, and the GFM spec marks each with `(extension)` in its table of contents. A plain CommonMark parser ignores them.

```markdown
| Column A | Column B |
| --- | --- |
| one | two |

- [x] done
- [ ] todo

~~strike this~~

www.example.com
```

Inside a table, `|` is structural. Write `\|` when you need a literal pipe in a cell. GFM also runs sanitization after the HTML conversion and disallows certain raw HTML. Tables, task lists, strikethrough, extended autolinks, and disallowed raw HTML: those five are the full set of GFM extensions over CommonMark. To check whether a site supports them, feed the same source into Babelmark and compare.

## One source-to-HTML pair

Heading, emphasis, and a link together:

```markdown
## Release notes

Read **CHANGELOG**, then the [spec](https://spec.commonmark.org/).
```

The HTML:

```html
<h2>Release notes</h2>
<p>Read <strong>CHANGELOG</strong>, then the <a href="https://spec.commonmark.org/">spec</a>.</p>
```

`##` becomes `<h2>`, and with no blank line the two lines stay one paragraph. Blocks live in [blocks.md](../../02-syntax/en/blocks.md), inline markup in [inline.md](../../02-syntax/en/inline.md), and the fence rules in [code.md](../../02-syntax/en/code.md).
