# Inline syntax

> 中文: [zh/inline.md](../zh/inline.md)

The parser cuts the document into blocks first, then works through the markers inside each line. Emphasis, code, links, and line breaks all live at this level. Watch the symbols: a lone asterisk opens emphasis, and you need an escape or a code span to keep it literal.

## Emphasis

`*x*` and `_x_` give you `<em>`. `**x**` and `__x__` give you `<strong>`.

```markdown
*em* and _em_
**strong** and __strong__
```

The two lines form one paragraph, and all four forms take effect:

```html
<p><em>em</em> and <em>em</em>
<strong>strong</strong> and <strong>strong</strong></p>
```

## Which side a delimiter sits on

CommonMark sorts a delimiter run like `*` into left-flanking and right-flanking by checking the characters on either side. Whitespace, punctuation, or letters decide whether the run can open, close, or do both. Intraword underscores don't create emphasis, so `foo_bar_baz` stays as you typed it. With `*foo *bar* baz*`, the inner pair wins first and the outer pair wraps the whole phrase. The algorithm gets fiddly, and I'll leave it there.

```markdown
foo_bar_baz stays plain

*foo *bar* baz*
```

The underscore line stays plain; the asterisk line becomes two nested `<em>` elements:

```html
<p>foo_bar_baz stays plain</p>
<p><em>foo <em>bar</em> baz</em></p>
```

## Strikethrough

You write `~~x~~` for strikethrough. It's a GFM extension, and plain CommonMark doesn't recognize it.

```markdown
~~gone~~
```

CommonMark prints it literally; on GitHub you get `<del>gone</del>`:

```html
<p>~~gone~~</p>
```

## Code spans and backticks

A single backtick wraps a code span. When the content carries a backtick of its own, use two backticks on the outside and you can keep a literal one inside.

```markdown
use `code` here

`` a ` backtick inside ``
```

The second line uses double backticks, and the output keeps the inner backtick:

```html
<p>use <code>code</code> here</p>
<p><code>a ` backtick inside</code></p>
```

## Backslash escapes

Backslash escapes work on ASCII punctuation only. `\*` gives you a literal asterisk; in `\A` the backslash prints too, because `A` isn't punctuation.

```markdown
\* works \A stays \q stays
```

Only the first asterisk escapes; the other two keep their backslashes:

```html
<p>* works \A stays \q stays</p>
```

### One wrong turn

You paste `/tmp/*important*/notes.txt` into an issue, and the two asterisks turn into emphasis delimiters, so the directory name goes italic.

```markdown
the file is /tmp/*important*/notes.txt
```

You get `important` wrapped in `<em>`:

```html
<p>the file is /tmp/<em>important</em>/notes.txt</p>
```

Escape each asterisk instead:

```markdown
the file is /tmp/\*important\*/notes.txt
```

Back to literal asterisks:

```html
<p>the file is /tmp/*important*/notes.txt</p>
```

## Soft and hard line breaks

Press Enter at the end of a line and you get a soft break, which the browser usually folds into one space. For a hard break, add two trailing spaces or a trailing backslash; the output gets a `<br />`.

```markdown
soft
break

hard  
stop

back\
slash
```

The first paragraph keeps a soft break; the other two each get a `<br />`:

```html
<p>soft
break</p>
<p>hard<br />
stop</p>
<p>back<br />
slash</p>
```

## Autolinks, entities, character references

Angle brackets around a URL make an autolink: `<https://example.com>`. You can also write entities and numeric character references directly: `&copy;` gives you `©`, `&#35;` gives you `#`, and `&#x41;` gives you `A`.

```markdown
<https://example.com>
```

The URL inside the angle brackets turns into a clickable link by itself:

```html
<p><a href="https://example.com">https://example.com</a></p>
```

Now the character references:

```markdown
&copy; &#35; &#x41;
```

All three turn back into characters:

```html
<p>© # A</p>
```

One catch: `&#42;` can't stand in for `*` as an emphasis delimiter. Character references only show up as text; they don't take part in structure.

## Inline HTML

CommonMark lets you write inline HTML straight into the text, and `<em>html</em>` passes through as-is.

```markdown
inline <em>html</em> here
```

The tags survive into the output:

```html
<p>inline <em>html</em> here</p>
```

GitHub also runs a sanitization pass over raw HTML in user content. Which tags it escapes and which attributes it strips is covered in [the GFM chapter](../../03-spec/en/gfm.md).

## Further reading

- [Block syntax](blocks.md)
- [Links and images](links-and-images.md)
- [Code blocks](code.md)
- [The CommonMark spec](../../03-spec/en/commonmark.md)
