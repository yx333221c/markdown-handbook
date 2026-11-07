# Markdown Handbook

A repository that explains Markdown: where it came from, how the syntax parses, what CommonMark and GFM actually say, and which mistakes show up in a real repo.

> 中文 / Chinese: [README.zh.md](README.zh.md)

## What's in here

Six folders, one per kind of question. Each folder has `zh/` and `en/` with identical filenames, so switching language does not change your place in the book.

| Folder | Covers |
| --- | --- |
| [`00-orientation`](docs/00-orientation/en/what-is-markdown.md) | What Markdown is, and what it is good for |
| [`01-history`](docs/01-history/en/how-it-started.md) | 2004, `Markdown.pl`, and how one syntax page turned into competing specs |
| [`02-syntax`](docs/02-syntax/en/blocks.md) | Blocks, inline markup, links, images, code fences, edge cases |
| [`03-spec`](docs/03-spec/en/commonmark.md) | CommonMark, GFM, and why dialects disagree |
| [`04-practice`](docs/04-practice/en/toolchain.md) | Editors, linters, previews, publishing |
| [`05-reference`](docs/05-reference/en/cheatsheet.md) | Cheat sheet, glossary, further reading |

Every article has a language switch at the top and links to related chapters at the bottom.

## Start here

New to Markdown: read [what-is-markdown.md](docs/00-orientation/en/what-is-markdown.md), then [blocks.md](docs/02-syntax/en/blocks.md) and [inline.md](docs/02-syntax/en/inline.md).

You already write it daily and want to know why the same file renders differently on GitHub and in Pandoc: go to [commonmark.md](docs/03-spec/en/commonmark.md) and [gfm.md](docs/03-spec/en/gfm.md).

You are staring at a document that came out wrong: [gotchas.md](docs/02-syntax/en/gotchas.md) collects the failures people actually hit.

## Why every example is inside a code block

GitHub renders `.md` files as you read them. A `#` typed as plain text becomes a heading, `*` becomes emphasis, and the syntax you meant to show disappears. So every snippet in this repo sits inside a fenced code block, and single symbols are wrapped in inline code. Showing a fenced block inside a fenced block takes an outer fence of four backticks:

````markdown
```markdown
## A short note

`README.md` lives in the repo root. Use **bold** sparingly.
```
````

Rendered, that is a level-two heading, one paragraph, and two inline code spans. The four-backtick rule comes from the spec, and [code.md](docs/02-syntax/en/code.md) explains it.

## Two languages

`README.md` is the English entry point, `README.zh.md` the Chinese one. The two versions cover the same chapters and use the same examples, but each was written on its own rather than translated line by line.

## License

MIT, see [LICENSE](LICENSE). That covers this handbook. John Gruber distributes Markdown itself under a BSD-style license, which is a separate matter.
