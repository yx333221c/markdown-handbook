# GFM: GitHub's own dialect

> 中文: [zh/gfm.md](../zh/gfm.md)

You drop a `<div class="note">` into a repo file to nudge the layout, push, refresh, and the tag is still there while the `class` is gone. Rendering worked fine; GitHub's sanitization step stripped the attribute. To see why, start with what GFM actually is.

GFM (GitHub Flavored Markdown) is the dialect GitHub uses for user content. In March 2017 GitHub published a blog post, "A formal spec for GitHub Flavored Markdown," with the spec and a reference implementation; from then on all user content across the site (comments, wikis, `.md` files in repos) parsed against it. It builds on CommonMark and is a strict superset: a CommonMark document renders the same under GFM, then GFM adds more. The spec page currently reads `Version 0.29-gfm (2019-04-06)`.

## The five entries marked extension

In the GFM spec's table of contents, these five sections carry `(extension)`, meaning they go beyond CommonMark.

Tables:

```markdown
| left | right |
| --- | --- |
| a | b |
```

Task list items:

```markdown
- [x] done
- [ ] todo
```

Strikethrough:

```markdown
~~scratch this~~
```

Extended autolinks. CommonMark only links `<https://example.com>` inside angle brackets. GFM also turns a bare URL, `www.example.com`, or an email address into a link:

```markdown
See https://example.com or www.example.com, or mail a@b.com
```

Disallowed raw HTML. The spec escapes a short list of tags into literal text and leaves everything else alone:

```markdown
<title>gets escaped</title>
<div>stays as an HTML block</div>
```

The nine escaped tags are `<title>`, `<textarea>`, `<style>`, `<xmp>`, `<iframe>`, `<noembed>`, `<noframes>`, `<script>`, and `<plaintext>`. They're on the list because each changes how the rest of the HTML gets parsed. `<div>` is not one of them, so it survives as an HTML block.

## There's a step after the HTML

Section 1.1 says it plainly: once the Markdown is HTML, GitHub runs extra post-processing and sanitization. That's what stripped the `class` at the start; the tag itself stayed. A later stage decides whether your attributes, scripts, or styles survive. So "tagfilter doesn't block `<div>`" does not mean "you can style a README with `<div>`". Section 2.3 covers the same kind of cleanup, replacing `U+0000` with `U+FFFD`.

## What this means day to day

READMEs, issues, PR descriptions, and wikis all go through this pipeline. Preview an md file locally and you're seeing your editor's parser or a plugin you installed. Push to GitHub and you're seeing GFM plus post-processing. The two disagree, most often on tables, task lists, and raw HTML. Preview once on the target platform before you publish; it beats guessing from a local result.

GFM is GitHub's dialect. Other sites run their own, so don't call it an industry standard. Where the split came from and how to stay portable: [en/dialects.md](dialects.md). The CommonMark rules underneath: [en/commonmark.md](commonmark.md).
