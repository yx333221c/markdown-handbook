# Markdown 是怎么来的

> English: [en/how-it-started.md](../en/how-it-started.md)

2004 年，John Gruber 和 Aaron Swartz 一起做出了 Markdown。转换器是 Gruber 用 Perl 写的，文件名 `Markdown.pl`。你喂给它一篇纯文本，它吐回一段 HTML，当时就这么用。

Gruber 在 Daring Fireball 的 Markdown 主页上写了灵感来源：最大的一份来自纯文本邮件，还有 Usenet 上人们约定俗成的写法，用 `*` 圈出强调，用 `>` 表示引文，用空行分段。这些记号在邮件里用了很多年，读者一眼就懂。设计目标他写成了这样一句话：

> "The overriding design goal for Markdown's formatting syntax is to make it as readable as possible."

翻成中文，大意是「这套语法压倒一切的目标，是让源文件本身尽量好读」，出处同上，即 Daring Fireball 的 Markdown 主页。你写的是能直接发给别人看的文字，机器解析排在第二位。

Markdown 用的是 BSD 风格许可，写在 Gruber 自己的许可页上。本仓库用 MIT，跟 Markdown 的许可不是一回事，别混。

`Markdown 1.0.1` 在 2004-12-17 发布，`Markdown.pl` 最后一次更新也是这一天，之后再没动过（CommonMark 官网如此记述）。你现在能读到的那份 Perl 源码，停在 2004 年。

标题写法有两套。Aaron Swartz 2002 年的 `atx` 用行首的 `#` 表示标题层级，今天大家管这种叫 atx 风格标题。另一套是 setext 风格，标题下面垫一行 `=` 或 `-`，`=` 给一级，`-` 给二级。`Markdown.pl` 两种都认。atx 用 `#` 的个数分层级，setext 只有两种下划线，也就只能到两级；CommonMark 和 GFM 把 atx 定成 1 到 6 个 `#`，且开头 `#` 后面要留空格或行尾，所以 `#hashtag` 不算标题：

```markdown
# 一级标题
## 二级标题
### 三级标题

一级标题
=======

二级标题
-------
```

我个人更常用 atx，因为 setext 的 `-` 下划线和 `---` 分隔线撞车，文档一长就容易看花眼。`Markdown.pl` 默认输出 XHTML，比如 `<br />`；加 `--html4tags` 就切成 HTML 风格的 `<br>`。

接下来可以看 [规范是怎么定下来的](from-gruber-to-commonmark.md)，或者翻 [时间线](timeline.md) 对一遍日期。
