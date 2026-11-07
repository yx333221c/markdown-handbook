# GFM：GitHub 自己那套方言

> English: [en/gfm.md](../en/gfm.md)

你在仓库里贴了个 `<div class="note">` 想调一下排版，push 之后刷新页面，标签还在，`class` 没了。渲染没出错，GitHub 在后面的安全过滤里把属性清掉了。要理解这件事，得先看 GFM 是什么。

GFM（GitHub Flavored Markdown）是 GitHub 用户内容用的方言。GitHub 在 2017 年 3 月发博客《A formal spec for GitHub Flavored Markdown》公布正式规范和参考实现，从那时起全站用户内容——评论、wiki、仓库里的 `.md` 文件——都按这份规范解析。它基于 CommonMark，是 CommonMark 的严格超集：合乎 CommonMark 的文档在 GFM 里结果一样，GFM 再往上加东西。规范页面现在标着 `Version 0.29-gfm (2019-04-06)`。

## 目录里标了 extension 的五项

GFM 规范的目录里，这五节后面都跟着 `(extension)`，意思是它们超出 CommonMark 的部分。

表格：

```markdown
| 左 | 右 |
| --- | --- |
| a | b |
```

任务列表：

```markdown
- [x] 已做
- [ ] 待办
```

删除线：

```markdown
~~这句作废~~
```

扩展自动链接。CommonMark 只认 `<https://example.com>` 这种尖括号写法，GFM 里裸写的网址、甚至 `www.example.com` 和邮箱也会变成链接：

```markdown
见 https://example.com 或 www.example.com，写信到 a@b.com
```

禁止原始 HTML（disallowed raw HTML）。规范把一份很短的名单里的标签转义成字面文字，名单外的原样留下：

```markdown
<title>会被转义</title>
<div>会原样保留</div>
```

被转义的是这九个：`<title>`、`<textarea>`、`<style>`、`<xmp>`、`<iframe>`、`<noembed>`、`<noframes>`、`<script>`、`<plaintext>`。选它们是因为这些标签会改变 HTML 剩下的部分怎么被解析。`<div>` 不在名单上，它会作为 HTML 块留下来。

## 转完 HTML 还有一道

规范 1.1 节写得很直白：转成 HTML 之后，GitHub 还会做额外的后处理和安全过滤（sanitization）。开头那个 `class` 是在这一步被清掉的，标签本身还在。你贴的属性、脚本、样式，能不能留下由这一步决定。所以别把「tagfilter 没拦 `<div>`」理解成「可以用 `<div>` 调排版」。GFM 规范 2.3 节还提到 `U+0000` 会被替换成 `U+FFFD`，同一类清理。

## 实际后果

README、issue、PR 描述、wiki 都走这套渲染。你在本地用编辑器预览 md，看到的是编辑器自带解析器或你装的插件；推到 GitHub，看到的是 GFM 加后处理。两边不一样很正常，尤其是表格、任务列表和原始 HTML。发布前在目标平台预览一次，比对着本地结果猜省事。

GFM 只是 GitHub 的方言，别的站点各有自己的一套，别把它当成行业标准。分叉怎么来的、怎么写才尽量通用，见 [zh/dialects.md](dialects.md)；CommonMark 那边的规矩在 [zh/commonmark.md](commonmark.md)。
