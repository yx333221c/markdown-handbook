# Where Markdown Came From

> 中文: [zh/how-it-started.md](../zh/how-it-started.md)

In 2004 John Gruber and Aaron Swartz built Markdown. Gruber wrote the converter, a Perl script called `Markdown.pl`, and you handed it a plain text file to get HTML back.

Gruber wrote down where the syntax came from on the Markdown page at Daring Fireball. Plain text email was the biggest source, along with the habits people had picked up on Usenet: `*` for emphasis, `>` for quoted lines, a blank line between paragraphs. Those marks had been in email for years, and readers already knew them. He put the design goal in one sentence:

> "The overriding design goal for Markdown's formatting syntax is to make it as readable as possible."

He wanted the file you'd actually email to someone to double as the source a parser reads. Markdown goes out under a BSD-style license on Gruber's own licensing page. This repo uses MIT, which is a different thing.

`Markdown 1.0.1` came out on 2004-12-17. `Markdown.pl` was last updated the same day, and Gruber never touched it again (the CommonMark site records this). The Perl source you can read today stops in 2004.

There are two ways to write a heading. Aaron Swartz's `atx` from 2002 marked headings with a leading `#`; those are atx-style headings now. Setext is the other: you underline the text with `=` for a first-level heading or `-` for a second-level one. `Markdown.pl` accepts both. Atx counts levels with the number of `#` characters, while setext's two underlines only give you two; CommonMark and GFM fix atx at one to six `#` and require a space (or end of line) after the opening one, so `#hashtag` isn't a heading:

```markdown
# A first-level heading
## A second-level heading
### A third-level heading

A first-level heading
=====================

A second-level heading
----------------------
```

I reach for atx more often, because setext's `-` underline collides with the `---` thematic break and gets hard to read in a long file. `Markdown.pl` outputs XHTML by default, so you get `<br />`; add `--html4tags` and you get HTML-style `<br>` instead.

Next, [why that one page wasn't enough](from-gruber-to-commonmark.md), or the [timeline](timeline.md) if you want the dates in one place.
