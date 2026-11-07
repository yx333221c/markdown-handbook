# Links and Images

> 中文: [zh/links-and-images.md](../zh/links-and-images.md)

For one URL in the middle of a sentence, use an inline link. Square brackets hold the text you want shown, parentheses hold the URL, and a title in double quotes can ride along after the URL:

```markdown
[the CommonMark site](https://commonmark.org "CommonMark")
```

```html
<p><a href="https://commonmark.org" title="CommonMark">the CommonMark site</a></p>
```

The quotes only delimit the title. They don't show up in the link text, and you see the title on hover. If a title needs a literal double quote, write `\"` — backslash escapes work on ASCII punctuation, the same rule that turns `\*` into a literal asterisk.

Parentheses in a URL will bite you on some renderers. With `https://example.com/a_(b)`, a parser that stops at the first `)` leaves the rest of the characters outside the link; another renderer may handle it fine. Dialects disagree here, so don't gamble. Two forms are safe: wrap the URL in angle brackets, or escape the parentheses.

```markdown
[A disambiguation page](<https://example.com/a_(b)>) and [another](https://example.com/a_\(b\))
```

```html
<p><a href="https://example.com/a_(b)">A disambiguation page</a> and <a href="https://example.com/a_(b)">another</a></p>
```

## Reference links

When the same URL shows up three or four times in a paragraph, inline links make the source painful to read. Switch to references: write `[text][id]` in the body and a definition line `[id]: url` somewhere else. When the label matches the visible text, you can drop the second pair of brackets entirely and write `[text][]`.

```markdown
Read [the full spec][cm] first, then the [CommonMark][] home page.

[cm]: https://spec.commonmark.org "CommonMark Spec"
[CommonMark]: https://commonmark.org
```

```html
<p>Read <a href="https://spec.commonmark.org" title="CommonMark Spec">the full spec</a> first, then the <a href="https://commonmark.org">CommonMark</a> home page.</p>
```

Definition lines never render as paragraphs. The renderer collects them from the whole document before it fills in the links, so you can put them at the top, at the bottom, or between two paragraphs. I keep mine at the bottom; changing a URL then means one edit, not a hunt through the prose.

One question this page won't settle: if you write two definitions with the same id, `[cm]: url1` and `[cm]: url2`, which one wins? It's one of the questions Gruber's documentation left open and the later specs pinned down, and [gfm.md](../../03-spec/en/gfm.md) has the details. For now, just don't reuse an id in the same file.

## Autolinks

Put a URL straight inside angle brackets and the URL itself becomes the link text, with no second pair of brackets to type:

```markdown
<https://example.com>
```

```html
<p><a href="https://example.com">https://example.com</a></p>
```

GFM adds one extension (marked `(extension)` in the spec's table of contents): bare `https://example.com` or `www.example.com` also turns into a link, no brackets needed. Plain CommonMark doesn't do this, so don't rely on it if the same file gets rendered in more than one place.

```markdown
https://example.com and www.example.com
```

```html
<p><a href="https://example.com">https://example.com</a> and <a href="http://www.example.com">www.example.com</a></p>
```

## Images

An image is a link with a `!` in front: `![alt](url)`. The text in the square brackets isn't a caption. It's what stands in for the image when the file fails to load, or what a screen reader says out loud.

```markdown
![A pine tree bent under snow](pine.png "Winter")
```

```html
<p><img src="pine.png" alt="A pine tree bent under snow" title="Winter" /></p>
```

Here's a blunt way to write alt text: cover the image and say in one sentence what you'd want a reader to know. Put that sentence in the brackets. `![Pine tree]` beats `![Picture]`, and `![IMG_2043.png]` is about as useful as nothing. For a purely decorative image leave it empty, `![]()`, so screen readers don't have to read out a filename.

## Where to go next

For how links interact with emphasis and inline code, see [inline.md](inline.md). The rules for opening and closing fenced code blocks are in [code.md](code.md). If something rendered wrong, [gotchas.md](gotchas.md) collects the failures. Spec-level detail lives in [commonmark.md](../../03-spec/en/commonmark.md) and [gfm.md](../../03-spec/en/gfm.md).
