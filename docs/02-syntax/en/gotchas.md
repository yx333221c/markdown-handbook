# When the Output Looks Wrong

> 中文: [zh/gotchas.md](../zh/gotchas.md)

## A whole paragraph turned italic

```markdown
Name the file *report at the start, not report* at the end.
```

```html
<p>Name the file <em>report at the start, not report</em> at the end.</p>
```

You wanted two literal asterisks, or you started italicising "report" and never closed it. The renderer only reads pairs: it finds the second `*` and drops everything between into `<em>`. For literal asterisks write `\*`, or wrap them in inline code. For emphasis, add the closing `*`.

## No heading, because there's no space after `#`

```markdown
#deploy checklist
Read the doc first.
```

```html
<p>#deploy checklist
Read the doc first.</p>
```

No space after `#` means plain text, with the next line folded in by a soft break. CommonMark and GFM define an ATX heading as 1–6 `#` characters followed by a space (or the end of the line). Some older implementations don't require the space, so the same file can become a heading somewhere else. Add the space:

```markdown
# Deploy checklist
Read the doc first.
```

```html
<h1>Deploy checklist</h1>
<p>Read the doc first.</p>
```

## A four-space indented line inside prose became code

```markdown
This paragraph explains the install steps.

    Indenting this by four spaces turned it into code.
```

```html
<p>This paragraph explains the install steps.</p>
<pre><code>Indenting this by four spaces turned it into code.
</code></pre>
```

A line starting with four spaces, with a blank line before it, is an indented code block. Markdown has no syntax for visually indenting prose. Without the blank line, CommonMark reads it as a continuation of the paragraph and still eats the four spaces. Want code? Use a fence and tag the language, as [code.md](code.md) explains. Want a quote? Use `>`. Want structure? Use a list.

## `---` turned the line above into a level-two heading

```markdown
Pre-release check
---
```

```html
<h2>Pre-release check</h2>
```

A `---` directly under a line of text makes that line a setext heading: `-` underlines give `<h2>`, `=` gives `<h1>`. It's a heading underline, not a horizontal rule. Put a blank line between the text and the `---` if you wanted a rule. I avoid setext headings, for exactly this collision.

```markdown
Pre-release check

---
```

```html
<p>Pre-release check</p>
<hr />
```

The same trap catches `* * *`. Three or more `-`, `*` or `_` on a line by themselves, spaces allowed between them, form a thematic break: type it as decoration inside a list item, or on its own line, and you get a rule.

```markdown
First paragraph done.

* * *

Second paragraph.
```

```html
<p>First paragraph done.</p>
<hr />
<p>Second paragraph.</p>
```

For three literal asterisks write `\* \* \*`, or wrap them in inline code: `* * *`. Indenting the line by four spaces won't help; that lands you back in a code block.

## The table didn't render because there were no blank lines around it

```markdown
Read this table first:
| Column | Value |
| --- | --- |
| a | 1 |
Then change the config.
```

```html
<p>Read this table first:
| Column | Value |
| --- | --- |
| a | 1 |
Then change the config.</p>
```

Tables are a GFM block-level extension, marked `(extension)` in the spec. Butt one up against a paragraph and follow it with another sentence, and plenty of renderers won't recognise it; the lines fold into a paragraph with the pipes printed literally. Dialects disagree on whether a table can interrupt a paragraph, so put a blank line on each side:

```markdown
Read this table first:

| Column | Value |
| --- | --- |
| a | 1 |

Then change the config.
```

```html
<p>Read this table first:</p>
<table>
<thead><tr><th>Column</th><th>Value</th></tr></thead>
<tbody><tr><td>a</td><td>1</td></tr></tbody>
</table>
<p>Then change the config.</p>
```

## A `|` inside a cell split the columns wrong

```markdown
| Command | Meaning |
| --- | --- |
| a | b | escape the pipe |
```

```html
<table>
<thead><tr><th>Command</th><th>Meaning</th></tr></thead>
<tbody><tr><td>a</td><td>b</td></tr></tbody>
</table>
```

The header declares two columns, but the `|` cuts this row into three cells. GFM keeps as many cells as the header has and silently drops the rest, so the missing words vanish without a warning. To put a pipe inside a cell, escape it as `\|` — GFM requires the escape even inside inline code:

```markdown
| Command | Meaning |
| --- | --- |
| `a\|b` | escape the pipe |
```

```html
<table>
<thead><tr><th>Command</th><th>Meaning</th></tr></thead>
<tbody><tr><td><code>a|b</code></td><td>escape the pipe</td></tr></tbody>
</table>
```

## You wrote `<div class="note">` and the styling didn't take

```markdown
<div class="note">
This text is wrapped in a div.
</div>
```

```html
<div>
This text is wrapped in a div.
</div>
```

"Disallowed raw HTML" is one of GFM's `(extension)` entries, but its tagfilter escapes only nine tags: `<title>`, `<textarea>`, `<style>`, `<xmp>`, `<iframe>`, `<noembed>`, `<noframes>`, `<script>`, `<plaintext>`. The spec says all other HTML tags are left untouched, and `<div>` isn't on the list, so the tag survives. What disappears is the `class`: GitHub runs a sanitization pass after generating the HTML, and that's where attributes get stripped. For a callout use a block quote `>`, or just write a normal paragraph. Don't lean on a `div` for layout.

```markdown
> This text sits inside a block quote.
```

```html
<blockquote>
<p>This text sits inside a block quote.</p>
</blockquote>
```

## Two trailing spaces for a hard break disappeared after formatting

```markdown
First line  
Second line
```

```html
<p>First line<br />
Second line</p>
```

A hard line break comes from two spaces at the end of a line, or a trailing `\`. You can't see the two spaces in an editor, and formatters strip them; the next line then joins the first as one paragraph, because soft breaks collapse to a single space. A trailing `\` is easier to spot, or split into two paragraphs with a blank line.

```markdown
First line\
Second line
```

```html
<p>First line<br />
Second line</p>
```

## Parentheses in a URL cut the link short

```markdown
See [the API docs](https://example.com/docs/v2_(beta)).
```

```html
<p>See <a href="https://example.com/docs/v2_(beta">the API docs</a>).</p>
```

The href lost its tail and a stray `)` showed up after the link. Some parsers treat the first `)` in a URL as the end of the link, and dialects disagree, so don't gamble. Wrap the URL in angle brackets, or escape the parentheses as `\(` and `\)`. More forms in [links-and-images.md](links-and-images.md).

```markdown
See [the API docs](<https://example.com/docs/v2_(beta)>).
```

```html
<p>See <a href="https://example.com/docs/v2_(beta)">the API docs</a>.</p>
```

## CRLF on Windows doesn't match elsewhere

```markdown
# Release notes

Every change goes in this file.
```

```text
Saved as CRLF: line one\r\nline two\r\n
Saved as LF:   line one\nline two\n
```

Save the same file twice and the bytes at the end of each line differ. The extra `\r` occasionally throws off hard breaks and code-block boundaries when a team edits one repo on different systems. I won't claim here which tool does what: save your file in both formats in your own editor, render each, and you'll see the difference. Picking one line ending for the repo beats debugging it later.

## Where to go next

Inline marker pairing is in [inline.md](inline.md), block elements in [blocks.md](blocks.md), and fence rules in [code.md](code.md). For the specs see [commonmark.md](../../03-spec/en/commonmark.md) and [gfm.md](../../03-spec/en/gfm.md). The [cheatsheet.md](../../05-reference/en/cheatsheet.md) is a quick reference.
