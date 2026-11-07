# 术语表

> English: [en/glossary.md](../en/glossary.md)

读规范或论坛时撞上这些词，回来查这一页。按英文词头字母排，两版顺序一样。能配源码的就配上。

**ATX** 指 1~6 个 `#` 开头写标题的写法，名字来自 Aaron Swartz 2002 年的 `atx` 项目。`#` 后得跟空格，`#hashtag` 不算标题；行尾补一串 `#` 收尾，解析器会丢掉。

```markdown
## 二级标题 ##
```

**Babelmark** 是个在线对比工具，同一段源码丢进去，它并排摆出二十多个实现各自吐的 HTML。它不判对错，只把差异摊给你看。

**CommonMark** 是 2014 年 John MacFarlane 等人发起的项目，要给 Markdown 写一份无歧义的规范和测试集。起因很实在：Gruber 的说明留了一堆没答的问题，各实现只能去翻有 bug 的 `Markdown.pl`，同一篇文档换个地方就变样。

**conformance test** 是一组「源码 → 期望 HTML」样例，验解析器合不合规范。CommonMark 把它跟规范一起发，跑一遍就知道哪儿偏了。规范有版本号，写「0.30（2021）」即可，别断言是最新。

**container block / leaf block** 把块级元素分两类：能装别的块的是 container，比如引用、列表；装到自己就到底是 leaf，比如标题、分隔线、代码块。解析器靠它判断嵌套在哪收口。

**方言 / flavor** 指同一套底子各家改一点、加一点，长成自己的样子。GFM 算一种，CommonMark 各实现之间也对不齐。两个词基本能换着用。

**围栏代码块（fenced code block）** 用至少三个反引号或波浪号把代码围一圈，开闭得同一种字符，闭合那串不能比开头短。最早的 `Markdown.pl` 里没有它。下面外层用波浪号才装得下里面那对反引号：

~~~markdown
```python
print("hi")
```
~~~

**GFM** 是 GitHub 用户内容用的方言，2017 年发布正式规范，基于 CommonMark，是它的严格超集，规范页面标 `Version 0.29-gfm (2019-04-06)`。表格、任务列表、删除线、扩展自动链接、禁止原始 HTML，就这五项。

```markdown
- [x] 已做
- [ ] 待做
```

**缩进代码块（indented code block）** 是围栏之外的老写法，每行敲四个空格，前面空一行，也不能打断段落。想标语言名就做不到，那是围栏的活。

```markdown
    四个空格起头
    第二行照旧
```

**info string** 是开栏那行、反引号后面跟着的一串字。第一个词通常当语言名，转出的 HTML 里加 `language-` 前缀的 class，比如 `language-python`。

**行内 / 块级（inline / block）** 分的是标记待在哪儿。行内跟着段落文字走，像 `*强调*`、链接、行间代码；块级自己占一块，像标题、列表、引用，彼此要空行。

**软换行 / 硬换行（soft / hard line break）** 说的是源码敲一次回车会怎样。只敲回车多半并成一个空格；行尾补两个空格或放一个 `\` 才出 `<br>`。粘贴容易吃掉尾部空格，我更常用 `\`：

```markdown
第一行\
第二行
```

**link reference definition** 指 `[id]: url` 这种单独成行、给引用式链接存地址的定义。它不渲染成可见内容，放哪儿都行，堆在文件末尾是常见习惯。多个同名定义谁优先，Gruber 没定。

```markdown
[规范][cm]

[cm]: https://commonmark.org/
```

**Pandoc** 是个文档转换器，读进 Markdown，吐出 docbook、PDF、Word 之类。它自带方言和扩展，所以同一份文件在 Pandoc 转 docbook 时可能跟 GitHub wiki 里不一样。

**sanitization** 是转完 HTML 后再走的一轮清洗，清掉不安全的属性，也和 GFM 里那份转义名单配合。GFM 规范 1.1 节明确写了有这一步，2.3 节还规定 `U+0000` 换成 `U+FFFD`。你在 issue 里贴的 `<div class="note">` 标签往往还在、`class` 没了，就是它干的。

**Setext** 拿 `=` 或 `-` 垫在文字下一行，`=` 出 `<h1>`、`-` 出 `<h2>`，名字来自老工具 Setext。它跟 `---` 分隔线容易撞，我一般少用。

```markdown
标题
=======
```

**主题分隔线（thematic break）** 是三个及以上 `-`、`*`、`_` 单独成行，渲染成 `<hr>`，中间夹空格也认。行首缩进四个空格，解析器就当代码块处理。

```markdown
- - -
```

对着例子查符号回 [cheatsheet.md](cheatsheet.md)。规范的来历在 [commonmark.md](../../03-spec/zh/commonmark.md)，各家为什么对不上看 [dialects.md](../../03-spec/zh/dialects.md)，GitHub 的扩展看 [gfm.md](../../03-spec/zh/gfm.md)。
