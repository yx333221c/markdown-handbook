# 延伸阅读

> English: [en/further-reading.md](../en/further-reading.md)

下面这些页面都能打开，按你什么时候会用到它们分了四组。每条只说它是干什么的。手册正文里引用到的规矩，回对应章节能找到上下文。

## 原始文档

[Daring Fireball 的 Markdown 主页](https://daringfireball.net/projects/markdown/) 放着设计目标那句原话，语法说明也从这页进。[Markdown: Syntax](https://daringfireball.net/projects/markdown/syntax) 是原始语法说明，规则和例子都写在这里，Gruber 没把它写成规范。[Markdown 许可页](https://daringfireball.net/projects/markdown/license) 是 Gruber 自己写的许可，BSD 风格；本手册用 MIT，两码事。

想对着原文核一句，用主页和语法页就够，不用绕到别处。

## 规范

[CommonMark 官网](https://commonmark.org/) 列着核心成员和采用者，也是规范和测试集的入口。[CommonMark 规范](https://spec.commonmark.org/) 是规范正文，跟 conformance test 一起发。[0.30 版规范](https://spec.commonmark.org/0.30/) 带版本号，2021 年的，引用具体规则时指它比较清楚。官网还挂了一页 [help](https://commonmark.org/help/)，篇幅比规范短，先扫一遍再啃正文省点劲。

[GFM 规范](https://github.github.com/gfm/) 是 GitHub 用户内容用的那份，当前页面标着 `Version 0.29-gfm (2019-04-06)`。写「0.29-gfm」别写成「最新版」，说不准哪天就换了。

## 讨论与背景

[The Future of Markdown](https://blog.codinghorror.com/the-future-of-markdown/) 是 Jeff Atwood 2012 年 10 月发的帖子，提议主流站点一起定一份正式规范和测试集，里面提到 David Greenspan 给他的邮件和工作代号 "Rockdown"。[A formal spec for GitHub Markdown](https://github.blog/engineering/user-experience/a-formal-spec-for-github-markdown/) 是 GitHub 发布 GFM 正式规范时写的工程博客。[CommonMark Discuss](https://talk.commonmark.org/) 是讨论论坛，规范没写死的边界情况常在那儿来回掰。

## 工具

[Babelmark](https://babelmark.github.io/) 让你贴一段源码，并排看二十多个实现吐出来的 HTML。同一份文件在两个站点上不一样时，先来这里比一遍，比猜快。[Pandoc](https://pandoc.org/) 是文档转换器，读进 Markdown，吐出 docbook、PDF、Word 等格式；它自带方言和扩展。

## 手册里接着看

符号记不住翻 [cheatsheet.md](cheatsheet.md)，术语查 [glossary.md](glossary.md)。2004 年那段的来历在 [how-it-started.md](../../01-history/zh/how-it-started.md)，规范怎么收拾乱局看 [commonmark.md](../../03-spec/zh/commonmark.md)，GitHub 加了哪些东西看 [gfm.md](../../03-spec/zh/gfm.md)。
