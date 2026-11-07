# Block syntax

> 中文: [zh/blocks.md](../zh/blocks.md)

Blank lines are part of the syntax in Markdown. Write two lines with no gap and you get one paragraph; leave an empty line and you get two. Headings, lists, and code blocks all depend on that gap.

```markdown
first line
second line

new paragraph
```

That empty line splits the text, and the output follows with two paragraphs:

```html
<p>first line
second line</p>
<p>new paragraph</p>
```

## ATX headings

One to six `#` marks at the start of a line, followed by a space or the end of the line, make a heading. Aaron Swartz's `atx` from 2002 gave the style its name. Skip the space and you get plain text: `#hashtag` and `#5 bolt` stay put. You may close the line with more `#` marks, and the parser drops them.

```markdown
### Title ###

#hashtag
#5 bolt
####### seven

    # indented
```

The first line becomes a heading, the hashtag lines stay a paragraph, seven `#` marks overshoot the limit, and the last line, indented four spaces, becomes a code block:

```html
<h3>Title</h3>
<p>#hashtag
#5 bolt
####### seven</p>
<pre><code># indented
</code></pre>
```

Count the opening `#` marks and you know the level:

| Opening `#` marks | Output | Spelling |
| --- | --- | --- |
| 1 to 6 | `<h1>` through `<h6>` | `# Title` through `###### Title` |
| more than 6 | a paragraph | `####### Title` |

I leave the closing `#` marks out. They look like stray punctuation, and the extra characters clutter the source.

## Setext headings

Setext headings work differently: you underline the text with `=` for `<h1>` or `-` for `<h2>`.

```markdown
Title
=====

Foo
---
bar
```

The `---` under `Foo` acts as a level-two underline, so you get `<h1>` for `Title`, `<h2>` for `Foo`, and a paragraph for `bar`:

```html
<h1>Title</h1>
<h2>Foo</h2>
<p>bar</p>
```

You may want a rule under `Foo`, but `---` gives you an `<h2>` instead. Use `***` or set the dashes off with blank lines. I stick to ATX because I keep hitting this collision.

## Thematic breaks

Three or more `-`, `*`, or `_` characters on their own line, with spaces allowed between them, give you an `<hr />`. Two characters do nothing, and mixing symbols does nothing either.

```markdown
---
***
___
- - -

    ---
```

You get four rules; the last line, indented four spaces, turns into a code block:

```html
<hr />
<hr />
<hr />
<hr />
<pre><code>---
</code></pre>
```

Keep the four-space rule in mind. Headings and rules both turn into code blocks once you cross it.

## Block quotes and lazy continuation

You open a block quote with `>` and nest one with two `>` marks. Lazy continuation is the odd part: a line without `>` can still join the quote when it continues the paragraph above.

```markdown
> first
continued lazily
>
> > nested
```

You left `>` off `continued lazily`, and the line joins the first paragraph; after the blank line you open a nested quote with `> >`:

```html
<blockquote>
<p>first
continued lazily</p>
<blockquote>
<p>nested</p>
</blockquote>
</blockquote>
```

Add a blank line when you want the quote to end cleanly.

## Lists: markers, nesting, loose and tight

Unordered lists take `-`, `*`, or `+`. Ordered lists take a number and `.`. A sublist lines up with the parent item's text: in `- one`, the `-` plus its space take two columns, so you indent the inner `-` by two spaces. Gruber's syntax page never said how far to indent a sublist, or when a list item should carry a `<p>`. Section 1.3 of the GFM spec lists those open questions; CommonMark later pinned the rules down.

```markdown
- one
  - nested

1. first
2. second
```

Two spaces give you the sublist; the blank line splits the unordered list from the ordered one:

```html
<ul>
<li>one
<ul>
<li>nested</li>
</ul>
</li>
</ul>
<ol>
<li>first</li>
<li>second</li>
</ol>
```

In a tight list the items carry no `<p>`. In a loose one they do. You decide which one you get with a blank line between items.

```markdown
- one
- two
```

Written back to back, the items stay bare:

```html
<ul>
<li>one</li>
<li>two</li>
</ul>
```

```markdown
- one

- two
```

Add one blank line and you get a `<p>` around each item:

```html
<ul>
<li>
<p>one</p>
</li>
<li>
<p>two</p>
</li>
</ul>
```

One loose item makes the whole list loose. If your CSS shows bigger gaps than you expect, look for an extra Enter in the source.

## Blocks win over inlines

The parser fixes the block structure first and handles inline markers afterwards, so block markers take precedence. Section 3.1 of the CommonMark spec uses this example:

```markdown
- `one
- two`
```

The two backticks look like they could open and close a code span, but the list splits first, leaving each backtick as literal text in its own item:

```html
<ul>
<li>`one</li>
<li>two`</li>
</ul>
```

## Further reading

- [Inline syntax](inline.md)
- [Links and images](links-and-images.md)
- [The CommonMark spec](../../03-spec/en/commonmark.md)
