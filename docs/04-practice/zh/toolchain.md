# 你手边的工具

> English: [en/toolchain.md](../en/toolchain.md)

写 Markdown 的人手里往往同时有几个渲染器，它们对同一份文件的看法并不一致。

你在 VS Code 里看着正常，推到 GitHub 仓库页也正常，再用 Pandoc 转 `docbook` 可能就变了样子。CommonMark 的动机清单里就有这种分叉：同一篇文档在 GitHub wiki 和 Pandoc 转 `docbook` 时可能不一样，而 Markdown 里没有「语法错误」这回事，差异常常很久才被发现。改文件之前，先弄清你盯着的是预览栏、仓库页，还是命令行转出来的那份。

## 编辑器里的预览

编辑器这一层，VS Code 自带 Markdown 预览，源码和结果并排，不改写文件；Obsidian、Typora 这类所见即所得编辑器反过来，你直接在排好版的样子上打字，`#`、`*` 平时藏起来。分界就在这儿：一个让你一直看见源码，一个让你大部分时间看不见。版本号别去记，装上打开试一下就清楚。

## 命令行转换

命令行最常用的是 Pandoc，最基础的转换一行就够：

```bash
pandoc input.md -o output.html
```

解决的是「有份 `input.md`，想要一份浏览器能打开的 `output.html`」。换目标格式用 `-t`，但后面能接什么我不替你背，先跑：

```bash
pandoc --help
```

翻到格式那段自己看，比记一份可能已经变了的清单稳妥。

## 拿参考实现和检查工具当尺子

拿不准某段语法该怎么渲染，就看 CommonMark 的参考实现。C 写的 `cmark`、JavaScript 写的 `commonmark.js` 都贴着规范文本实现，`cmark` 在终端直接吐 `HTML`：

```bash
cmark input.md
```

`commonmark.js` 更适合 Node 或浏览器，先把文档解析成语法树（AST）再渲染。拿它们当尺子，比拿某个编辑器的预览当尺子靠谱。

空行、标题跳级、行尾空格这类毛病交给 `markdownlint` 一类工具，`npx markdownlint-cli2 "**/*.md"` 能扫整个目录，具体 flag 先看 `npx markdownlint-cli2 --help`。有处要留意：行尾空格恰恰是硬换行靠的东西（行尾两个空格或行尾一个反斜杠才硬换行，软换行渲染时通常合成一个空格），lint 规则却常把行尾空格当脏东西报。两个工具在这件事上打架，先看配置再决定听谁的。

Prettier 这类格式化器会重排散文的换行：

```bash
npx prettier --check "docs/**/*.md"
```

`--check` 只看不改。真跑了 `--write`，按硬换行排好的两行可能被捋成一行，行尾那两个空格也没了。想留硬换行，就别让格式化器动 Markdown 的换行。

## 不用装东西的两种对照

还有两个不用装东西的对照办法。Babelmark 把同一段源码丢给 20 多个实现，并排列出 `HTML` 输出，遇到「怎么每个地方都不一样」时最省事。在 github.com 上编辑 `.md` 文件，编辑框上方的预览（Preview）标签能先看结果再提交，它走的正是 GitHub 自己那套 GFM，也就是推上去之后读者看到的那套。

延伸阅读：[gfm.md](../../03-spec/zh/gfm.md) 讲 GFM 比 CommonMark 多出来的东西，[code.md](../../02-syntax/zh/code.md) 里围栏和行间代码写得更细，[cheatsheet.md](../../05-reference/zh/cheatsheet.md) 当速查表用。
