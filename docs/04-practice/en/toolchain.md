# The tools around a Markdown file

> 中文: [zh/toolchain.md](../zh/toolchain.md)

You usually have more than one renderer open on the same file, and they don't agree.

A file that looks fine in VS Code and fine on the GitHub repo page can come out different once you run it through Pandoc to `docbook`. The CommonMark motivation list names exactly this split: the same document can render differently in a GitHub wiki and in Pandoc's docbook output, and since Markdown has no such thing as a syntax error, you often don't notice for a long time. Before you edit, work out which renderer you're looking at — the preview pane, the repo page, or a file that came out of a command.

## Previews in the editor

On the editor side, VS Code ships a Markdown preview that puts source and result side by side and never touches your file. Obsidian and Typora go the other way: you type into the rendered page and characters like `#` and `*` stay hidden most of the time. That's the whole difference — one keeps the source in front of you, the other doesn't. Don't bother memorising version numbers; install one and open it.

## Converting on the command line

Pandoc is the command-line workhorse. The basic conversion is one line:

```bash
pandoc input.md -o output.html
```

That answers "I have `input.md` and I want an `output.html` I can open in a browser". To pick a different target you use `-t`, but I'm not going to recite what goes after it. Run this instead:

```bash
pandoc --help
```

Read the format list yourself; it's safer than a list that may already be out of date.

## Reference implementations and checkers

When you can't tell how a bit of syntax should render, check it against the CommonMark reference implementations. `cmark` (C) and `commonmark.js` (JavaScript) both follow the spec text closely; `cmark` just prints `HTML` to the terminal:

```bash
cmark input.md
```

`commonmark.js` fits better inside Node or a browser — it parses the document into an AST first, then renders. Either one is a better yardstick than some editor's preview.

Blank lines, heading jumps and trailing spaces are the job of linters like `markdownlint`. `npx markdownlint-cli2 "**/*.md"` sweeps a whole tree; check `npx markdownlint-cli2 --help` for the exact flags. One snag: trailing spaces are exactly what a hard line break needs — two spaces at the end of a line, or a trailing backslash, produce a hard break, while a soft break usually collapses into a single space when rendered — and lint rules tend to flag trailing spaces as dirt. The two tools fight over this. Read the config before you decide which one wins.

Formatters such as Prettier go further and reflow prose line breaks:

```bash
npx prettier --check "docs/**/*.md"
```

`--check` reports without writing. Run `--write` and those two carefully spaced lines can get folded into one, the trailing spaces gone with them. If you want hard breaks to survive, keep the formatter off Markdown's line wrapping.

## Two comparisons that need no install

Two more ways to compare, neither of which needs installing. Babelmark feeds the same snippet to more than 20 implementations and lines up the `HTML` each one produces — handy when you're staring at "why does this look different everywhere". And when you edit a `.md` file on github.com, the Preview tab above the edit box shows you the result before you commit; it runs GitHub's own GFM, which is the same thing your readers get after you push.

Further reading: [gfm.md](../../03-spec/en/gfm.md) covers what GFM adds to CommonMark, [code.md](../../02-syntax/en/code.md) goes into fenced and inline code, and [cheatsheet.md](../../05-reference/en/cheatsheet.md) works as a quick reference.
