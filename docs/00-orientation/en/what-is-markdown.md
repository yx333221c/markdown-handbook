# What Markdown Is

> 中文: [zh/what-is-markdown.md](../zh/what-is-markdown.md)

The word has two meanings and people mix them up. Markdown is a syntax for writing formatted text as plain text. It is also `Markdown.pl`, the Perl script John Gruber wrote in 2004 to turn that text into HTML, with Aaron Swartz working alongside him. The script emits XHTML by default and switches to HTML-style tags with `--html4tags`. You will mostly deal with the syntax these days, but the name once covered both.

On the Markdown page at Daring Fireball, Gruber put the goal in one line:

> "The overriding design goal for Markdown's formatting syntax is to make it as readable as possible."

The same page says the biggest source of inspiration was plain-text email. Think about how you already write a message: `>` to quote someone, `*` to mark a word, a blank line to start a new paragraph, `-` to open a list. None of that needs teaching, and it does not get in the way while you read. Markdown turned those habits into rules, so the source file stays readable on its own.

You meet it in READMEs, issues, wikis, and pages built by static site generators. The author saves a `.md` file; the reader sees headings, lists, and links. A `README.md` in a repo renders with formatting on GitHub, and you can still open the downloaded copy in Notepad and edit it.

The limits are just as clear. Fancy typesetting, precise layout that pins a block to a spot on the page, and merged cells in a table have no reliable spelling in this syntax. People sometimes drop raw HTML in to get around that, but GitHub runs a sanitization pass after converting to HTML, so the platform decides what survives. Hand those jobs to a layout tool.

A short starter. The source:

```markdown
# Saturday release checklist

Write the **version number** first, then list what changes:

- Update `README.md`
- Close issue #42

> Don't ship on a Friday afternoon.
```

The HTML it turns into:

```html
<h1>Saturday release checklist</h1>
<p>Write the <strong>version number</strong> first, then list what changes:</p>
<ul>
<li>Update <code>README.md</code></li>
<li>Close issue #42</li>
</ul>
<blockquote>
<p>Don't ship on a Friday afternoon.</p>
</blockquote>
```

`#` needs a space after it to become a heading, so `#42` stays plain text. For how block elements break and nest, go to [blocks.md](../../02-syntax/en/blocks.md).
