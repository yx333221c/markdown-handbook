# Glossary

> 中文: [zh/glossary.md](../zh/glossary.md)

You will hit these words reading a spec or a forum thread. Come back here. Sorted by the English headword; both language versions use the same order. A short snippet where a snippet helps.

**ATX** names headings written with 1 to 6 `#` characters, after Aaron Swartz's `atx` project from 2002. You need a space after the `#`, so `#hashtag` stays plain text. A closing run of `#` on the same line is fine; the parser drops it.

```markdown
## Level two ##
```

**Babelmark** is an online comparison tool. Paste one piece of source and it lines up the HTML from more than twenty implementations. It does not judge which is right, it just shows you the diff.

**CommonMark** is the project John MacFarlane and others started in 2014 to write an unambiguous spec for Markdown, plus a test suite. The reason was concrete: Gruber's page left a pile of questions open, implementers had to read a buggy `Markdown.pl`, and the same document came out differently elsewhere.

**conformance test** is a set of "source in, expected HTML out" samples that checks a parser against a spec. CommonMark ships them with the spec; run them and you see where a parser drifts. The spec carries version numbers, so write "0.30 (2021)" and do not call it the latest.

**container block / leaf block** splits blocks into two kinds. A container holds other blocks, the way a quote or a list does; a leaf ends at itself, the way a heading, a thematic break, or a code block does. The parser uses the split to decide where a nesting level closes.

**dialect / flavor** describes what happens when everyone takes the same base and changes or adds a little. GFM is one; CommonMark implementations differ among themselves too. Either word works.

**fenced code block** wraps code in at least three backticks or tildes. Opening and closing fences must use the same character, and the closing one cannot be shorter. The original `Markdown.pl` had no such thing. The tildes below are the outer fence, since they have to hold a pair of backticks inside:

~~~markdown
```python
print("hi")
```
~~~

**GFM** is the dialect GitHub uses for user content. GitHub published a formal spec in 2017, built on CommonMark and a strict superset of it, marked `Version 0.29-gfm (2019-04-06)`. Tables, task lists, strikethrough, extended autolinks, and disallowed raw HTML are the whole set of its additions.

```markdown
- [x] done
- [ ] todo
```

**indented code block** is the older spelling, before fences. Put four spaces in front of every line, leave a blank line above it, and do not let it interrupt a paragraph. You cannot name the language this way; that is a fence feature.

```markdown
    four spaces in
    still code
```

**info string** is the text after the backticks on the opening fence line. Its first word usually names the language, such as `python`, and the HTML gets a `language-` prefixed class like `language-python`.

**inline / block** says where markup lives. Inline markup travels with the text in a paragraph: `*emphasis*`, links, code spans. A block takes a chunk of its own, like headings, lists, or quotes, and blocks need blank lines between them.

**soft / hard line break** is about one newline in your source. Leave it plain and the renderer usually folds it into a space; add two trailing spaces or a `\` and you get a `<br>`. Pasting tends to eat trailing spaces, so I use `\`:

```markdown
First line\
Second line
```

**link reference definition** is a standalone `[id]: url` line that stores the address for a reference link. It renders nothing visible and can go anywhere; stacking the definitions at the end of a file is a common habit. Gruber never decided which of two same-named definitions wins.

```markdown
[spec][cm]

[cm]: https://commonmark.org/
```

**Pandoc** is a document converter that reads Markdown and writes docbook, PDF, Word, and more. It brings its own dialect and extensions, so a file converted to docbook in Pandoc may not match the same file in a GitHub wiki.

**sanitization** is a cleaning pass after the HTML conversion, stripping unsafe attributes and working alongside GFM's escaped-tag list. GFM spec section 1.1 says the pass exists; section 2.3 also replaces `U+0000` with `U+FFFD`. Paste `<div class="note">` into an issue and the tag often survives while `class` disappears. That's this step.

**Setext** writes headings by underlining a line of text with `=` or `-`. `=` gives `<h1>`, `-` gives `<h2>`, and the name comes from an old tool called Setext. It collides with the `---` rule, so I rarely use it.

```markdown
Title
=======
```

**thematic break** is three or more `-`, `*`, or `_` on a line by itself, rendered as an `<hr>`. Spaces between the characters are allowed. Indent it four spaces and the parser reads it as a code block.

```markdown
- - -
```

For the symbols worked into examples, go back to [cheatsheet.md](cheatsheet.md). The spec story is in [commonmark.md](../../03-spec/en/commonmark.md), why implementations disagree in [dialects.md](../../03-spec/en/dialects.md), and the GitHub additions in [gfm.md](../../03-spec/en/gfm.md).
