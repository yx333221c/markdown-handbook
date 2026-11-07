# CommonMark: rules for a syntax with no syntax errors

> 中文: [zh/commonmark.md](../zh/commonmark.md)

Look at this:

```markdown
- a
  - b
```

Add one more space, or change `  - b` to `   - b`, and parsers disagree. Some treat `- b` as a sublist under `a`. Some read it as a lazy continuation of the same item. Others call it an indented code block. All three answers are legal. John Gruber's canonical syntax description on Daring Fireball is a one-page explanation shipped alongside a Perl script, `Markdown.pl`. It has no rules you can test a case against. The script had bugs, and after Gruber released `Markdown 1.0.1` on 2004-12-17 he stopped updating it. The people maintaining each implementation filled the gaps themselves, so a GitHub wiki, a Pandoc conversion, and your editor's preview stopped agreeing.

Here's the part that stings: Markdown has no syntax errors. Any sequence of characters is a valid document. A parser won't complain; it just hands you some HTML. You find out two platforms disagree when someone screenshots your published page and asks why the heading disappeared.

## Fourteen questions nobody answered

Section 1.3 of the GFM spec lists fourteen things Gruber's page left open. A few that actually trip you up:

How many spaces indent a sublist. In the example above, two spaces and three spaces give different results in older implementations. CommonMark pins this to the alignment of the content after the list marker.

```markdown
- parent
  - two spaces
- parent
   - three spaces
```

Whether a block quote or a heading needs a blank line before it. One version sits flush against a paragraph, the other has a blank line. Old parsers disagreed on whether a block can interrupt a paragraph at all.

```markdown
Some text
> a quote

Some text

# a heading
```

Whether an indented code block needs a blank line. A four-space line right after a paragraph becomes a code block in some tools and a soft-wrapped continuation in others.

```markdown
A paragraph
    indented line
```

Then there's inline precedence and duplicate link definitions. In `*a **b** c*`, which delimiter closes first? When `[x]` has two `[x]: url` definitions, which one wins? CommonMark writes each case down as one input plus one expected HTML snippet, and collected hundreds of them.

## Two parsing phases

CommonMark makes you build block structure first, then handle inline content. Cut the document into paragraphs, headings, lists, quotes, and code blocks; only then parse emphasis, links, and code spans inside those lines. Blocks win over inlines, so the `*` in `# a *b*` can't redraw the heading's boundary.

Blocks come in two kinds. A container block holds other blocks: a list item, a block quote, a list. A leaf block holds only text: a paragraph, a heading, an indented or fenced code block, a thematic break. Deciding which layer a piece of source belongs to is exactly what this split buys you.

## Versions, tests, people

The spec ships its own examples, each one a Markdown input paired with expected HTML, ready to run as conformance tests. `spec_tests.py` reads `spec.txt`, feeds every example to an implementation, and diffs the output. Writing a parser? Run it. Just want to know whether your editor follows the rules? Run it too.

Versions include `0.29` and `0.30` (2021-06-19). Don't claim either is current; check the site for whatever it marks now.

The CommonMark site currently lists John MacFarlane, Martin Woodward, and Jeff Atwood as core members. Adopters listed there: Discourse, GitHub, GitLab, Reddit, Qt, Stack Overflow / Stack Exchange, Swift.

For the syntax itself, see [en/blocks.md](../../02-syntax/en/blocks.md) and [en/inline.md](../../02-syntax/en/inline.md); the trap list is [en/gotchas.md](../../02-syntax/en/gotchas.md). GitHub layered its own extensions on top, covered in [en/gfm.md](gfm.md).
