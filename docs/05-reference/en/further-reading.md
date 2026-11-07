# Further Reading

> 中文: [zh/further-reading.md](../zh/further-reading.md)

Every page below opens. They are grouped by when you would reach for them, with one line of description each. Chapters in this handbook give the context that a bare link cannot.

## Original docs

[Markdown at Daring Fireball](https://daringfireball.net/projects/markdown/) is Gruber's project home page. You will find the design-goal quote there, plus the way into the syntax page. [Markdown: Syntax](https://daringfireball.net/projects/markdown/syntax) is the original write-up, with the rules and the examples. Gruber did not write it as a spec, and that fact explains a lot of later trouble. [The Markdown license page](https://daringfireball.net/projects/markdown/license) is Gruber's own wording, BSD-style. The handbook uses MIT; those are separate matters.

If you want to check a sentence against the source, the home page and the syntax page are enough.

## Specs

[The CommonMark site](https://commonmark.org/) lists the core members and adopters and links to the spec and test suite. [The CommonMark spec](https://spec.commonmark.org/) is the spec itself, shipped with a conformance test suite. [Version 0.30](https://spec.commonmark.org/0.30/) carries a number, 2021, so point at it when you cite a particular rule. The same site also hosts a [help page](https://commonmark.org/help/), shorter than the spec and easier to scan first.

[The GFM spec](https://github.github.com/gfm/) covers GitHub's user content and is marked `Version 0.29-gfm (2019-04-06)`. Say "0.29-gfm" rather than "the latest"; that label can date.

## Discussion and background

[The Future of Markdown](https://blog.codinghorror.com/the-future-of-markdown/) is Jeff Atwood's post from October 2012, asking major sites to agree on a formal spec and a test suite. He quotes an email from David Greenspan and mentions the working name "Rockdown". [A formal spec for GitHub Markdown](https://github.blog/engineering/user-experience/a-formal-spec-for-github-markdown/) is the engineering post GitHub published with the GFM spec. [CommonMark Discuss](https://talk.commonmark.org/) is the forum, where people pick at the cases the spec leaves open.

## Tools

[Babelmark](https://babelmark.github.io/) takes one snippet and lines up the HTML from more than twenty implementations. When a file renders differently on two sites, compare it here before you start guessing. [Pandoc](https://pandoc.org/) is a document converter that reads Markdown and writes docbook, PDF, Word, and more, with a dialect and extensions of its own.

## Elsewhere in the handbook

For the symbols, [cheatsheet.md](cheatsheet.md); for the vocabulary, [glossary.md](glossary.md). The 2004 story is in [how-it-started.md](../../01-history/en/how-it-started.md), what the spec fixed in [commonmark.md](../../03-spec/en/commonmark.md), and GitHub's additions in [gfm.md](../../03-spec/en/gfm.md).
