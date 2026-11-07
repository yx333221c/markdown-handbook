# A few habits I've settled on

> 中文: [zh/writing-habits.md](../zh/writing-habits.md)

These are the choices I've made for my own files, not rules anyone handed down. Each one has a reason attached. You can disagree and keep writing your way — at least you'll know what I'm trying to avoid.

## Blank lines and headings

I leave a blank line on both sides of block-level things: headings, lists, quotes, fenced code. Skip the blank line after a heading and some parsers pull the following text into the heading's context; GFM spec section 1.3 lists "must a blank line come before a block quote or heading" as one of the questions Gruber's docs never answered, so the split is real. I don't skip heading levels, and I use `#` exactly once, as the document title. I've seen openings like this:

```markdown
# Deploy notes
### 3.1 Configuration
First line of the body
```

This reads as a connected outline to a TOC and to a screen reader:

```markdown
# Deploy notes

## Configuration

First line of the body.
```

## How to wrap prose

Two ways both work. One sentence per line keeps a `git diff` change down to that one sentence; wrapping at 80 columns means no horizontal scroll in a narrow window. Each has a cost: the first gives you very long lines, the second makes a one-word edit ripple across several lines. Either way, remember soft breaks. Write this:

```markdown
This line stops halfway
and the next one finishes the sentence
```

and you get this — one space between them, not a break:

```text
This line stops halfway and the next one finishes the sentence
```

For a real break you need two trailing spaces or a trailing backslash, and linters love to strip trailing spaces as dirt. Pick one style and don't mix them.

## Lists, images, links

I nest lists with a fixed two spaces, never a tab. "How many spaces to indent a sublist" is another open question from GFM 1.3, and mixing the two is the fastest route to a list that shifts level in one renderer but not another. For images, the `alt` text should say what's in the frame: `![image](./assets/login-error.png)` might as well be empty, since a screen reader just says "image". `![Red error message below the login form](./assets/login-error.png)` tells you why the screenshot is here. Inside a repo I use relative links only — `[spec notes](../../03-spec/en/commonmark.md)` still works on another machine or in a fresh clone, while `[spec notes](/Users/me/markdown-handbook/docs/03-spec/en/commonmark.md)` only works on mine.

## Code, `HTML`, tables

Every fenced block gets a language, even if it's just `text`. Highlighting is the small part; a label tells Pandoc and docs sites what to do with the content. I've also replaced every four-space indented code block with a fence: the indented form has nowhere to put a language, and "must a blank line come before an indented code block" is yet another GFM 1.3 question. I wrap a fence inside `~~~markdown` when the fence itself is the example:

~~~markdown
```bash
pandoc input.md -o output.html
```
~~~

I stay away from raw `HTML` unless the target platform insists — GFM explicitly has `disallowed raw HTML`, so what you write may just get filtered out. And I split a table once it grows too many columns; nobody scrolls sideways to the fourth column on a phone.

## Before I commit

I look at the rendered result in the target renderer before committing, even if that's only the Preview tab above the edit box on github.com. Source that reads cleanly doesn't always lay out cleanly.

Further reading: [gotchas.md](../../02-syntax/en/gotchas.md) collects the traps, [blocks.md](../../02-syntax/en/blocks.md) covers where block elements begin and end, and [gfm.md](../../03-spec/en/gfm.md) is where those section 1.3 questions come from.
