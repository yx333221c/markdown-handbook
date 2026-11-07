# Dialects: the same md, a different page

> 中文: [zh/dialects.md](../zh/dialects.md)

Convert a piece of Markdown to docbook with Pandoc, render it in a GitHub wiki, post it on Discourse, and you may get three different results. Nobody got it wrong. Three things people treated as "the standard" never lined up in the first place.

What Gruber published on Daring Fireball is a one-page syntax description. It explains the design goal and leaves a lot unsaid. `Markdown.pl` was the first implementation, written in Perl, and its behavior drifted from that page, bugs included; Gruber stopped updating it after 2004-12-17. CommonMark and GFM came later as formal specs that pin down every edge case, but by then each site had been running its own reading for years. So you're juggling at least three references: the page, what the script actually did, and the later specs. They disagree, and none of them can be rolled back.

## With no syntax errors, the gaps stay hidden

CommonMark says any sequence of characters is a valid document. A parser that hits an ambiguous bit won't flag it; it picks one reading and quietly emits HTML. So two spaces versus three after `- a`, how far emphasis runs when you forget to close `*`, which of two `[x]: url` definitions wins: none of that surfaces while you write. You publish somewhere else, your reader sees a different page, and you hear about it only when someone asks why a heading vanished. That's why CommonMark pairs hundreds of edge cases with expected HTML, covered in [en/commonmark.md](commonmark.md).

Pandoc, Reddit, Stack Overflow, and Discourse each make their own trade-offs. A tool built for academic publishing piles on citations, tables, and multi-format export. A forum cares more about sanitizing user content and making pasted code readable. Which exact syntax rule differs, you'll have to test with real input; writing that list from memory is how errors get in.

Use Babelmark for that. It feeds one snippet to 20-plus implementations and shows their HTML side by side. If you suspect a construct will render oddly on your target, paste it in and look. Faster than reading four docs.

## Writing for portability

Rules you can follow today:

- Stick to core syntax. Build on paragraphs, headings, lists, emphasis, links, and code, the constructs every parser agrees on. Don't lean on one site's private markers.
- Tables, task list items, strikethrough, and extended autolinks are GFM additions. Say "requires GFM" where you use them, and don't assume the other side has them. See [en/gfm.md](gfm.md).
- Skip raw HTML. GitHub's post-processing filters a set of tags, other platforms apply different rules, and pasting a tag hands your layout to chance.
- Preview on the target platform before publishing. A README on GitHub and a forum post each get their own final render. Your editor's preview speaks only for itself.

Syntax traps: [en/gotchas.md](../../02-syntax/en/gotchas.md). Links and images: [en/links-and-images.md](../../02-syntax/en/links-and-images.md).

## Standardization didn't end the dialects, and it doesn't need to

CommonMark has been out for over a decade and GFM has a formal spec, yet Pandoc, Reddit, and Discourse still run their own. The reason is mundane: these sites solve different problems. A forum has to block scripts and stray tags that users paste in. A publishing tool has to turn one manuscript into docbook, LaTeX, and EPUB. GitHub has to render READMEs and issues safely in one pipeline. Forcing all of that into a single spec means making one set of needs bend to another, and buys little. If your document has to travel, the four rules above will keep the differences small enough.
