# Putting the file where people can see it

> 中文: [zh/publishing.md](../zh/publishing.md)

A finished `.md` file has to land somewhere, and where it lands decides how it looks.

GitHub renders the root `README.md` for you: open a repo's main page and that's the block sitting under the file list — no clicking, no setup. I put the Chinese version in `README.zh.md`, and GitHub doesn't promote it for you; readers have to open that file themselves. A link to it from `README.md` does more than any amount of hoping they'll notice. Issue bodies, PR descriptions and wiki pages also run GFM, so tables, task lists and strikethrough all work there. A `- [x]` in your PR turns into a checked box because GitHub uses GFM, not because plain Markdown does that.

Once you leave the repo page, stop assuming. GitHub Pages with Jekyll, or a different static site generator, may not handle Markdown the way the repo page does: a different parser, front matter stripped out first, links rewritten under their own rules. Task-list boxes missing from your Pages site usually come from that, not from a typo in your file. The same goes for Pandoc to `docx` / `pdf` / `html` — extension syntax like tables and task lists can disappear or come out changed. Convert one file and inspect it before you run the whole batch; it's cheaper than fixing pages one at a time afterward.

Relative links and images break most often. Say your repo looks like this:

```text
docs/
  guide.md
  assets/
    login-error.png
```

`![Error message](./assets/login-error.png)` inside `guide.md` works fine. Move `guide.md` alone to the site root, or copy it without `assets/`, and the path points at nothing. Hard-coding `https://github.com/me/repo/blob/main/...` just moves the problem — it dies on a fork. You can't see a broken link in the source; it shows up only when you open the target page. Preview on the target platform once before you publish. That step earns its keep.

One more thing: the two files worth writing first in an open-source repo are `LICENSE` and `README.md`. Without a license nobody can tell whether they're allowed to use the code, and `README.md` is what the main page shows by default.

For the syntax GitHub adds, see [gfm.md](../../03-spec/en/gfm.md). To work out who owns a rendering difference, [dialects.md](../../03-spec/en/dialects.md) covers the splits and [commonmark.md](../../03-spec/en/commonmark.md) covers the spec itself.
