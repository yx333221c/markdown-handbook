# Markdown 手册

一份讲 Markdown 的仓库：从 2004 年的来历，到语法怎么解析、规范怎么定，再到实际写稿时真会踩的坑。

> English: [README.md](README.md)

## 这里有什么

按问题类型分成六个文件夹。每个文件夹里 `zh/` 和 `en/` 用同样的文件名，换语言不用重新找位置。

| 文件夹 | 讲什么 |
| --- | --- |
| [`00-orientation`](docs/00-orientation/zh/what-is-markdown.md) | Markdown 是什么，适合拿来干什么 |
| [`01-history`](docs/01-history/zh/how-it-started.md) | 2004 年、`Markdown.pl`，以及一页语法说明怎么变成几份互相打架的规范 |
| [`02-syntax`](docs/02-syntax/zh/blocks.md) | 块级元素、行内标记、链接图片、代码块，还有那些边界情况 |
| [`03-spec`](docs/03-spec/zh/commonmark.md) | CommonMark、GFM，以及各方言为什么对不上 |
| [`04-practice`](docs/04-practice/zh/toolchain.md) | 编辑器、校验工具、预览和发布 |
| [`05-reference`](docs/05-reference/zh/cheatsheet.md) | 速查表、术语表、延伸阅读 |

每篇开头有语言切换，结尾有指向相关章节的链接。

## 从哪开始

没写过 Markdown：先看 [what-is-markdown.md](docs/00-orientation/zh/what-is-markdown.md)，再看 [blocks.md](docs/02-syntax/zh/blocks.md) 和 [inline.md](docs/02-syntax/zh/inline.md)。

天天在写，只想弄明白同一份文件为什么在 GitHub 和 Pandoc 里渲染不一样：[commonmark.md](docs/03-spec/zh/commonmark.md) 和 [gfm.md](docs/03-spec/zh/gfm.md)。

眼前这份文档已经渲染错了：[gotchas.md](docs/02-syntax/zh/gotchas.md) 收的都是真会碰上的故障。

## 例子为什么都包在代码块里

GitHub 会把 `.md` 渲染成排版。正文里光写个 `#` 就变成标题，`*` 变成强调，想展示的符号反而没了。所以这个仓库里每段示例都放在围栏代码块里，单个符号用行间代码包住。要在代码块里再展示一个代码块，外层得用四个反引号：

````markdown
```markdown
## 一小段说明

`README.md` 放在仓库根目录，**加粗**少用一点。
```
````

渲染出来是一个二级标题、一段正文、两处行间代码。四个反引号的规则来自规范，[code.md](docs/02-syntax/zh/code.md) 讲了来龙去脉。

## 两版语言

`README.md` 是英文入口，`README.zh.md` 是中文入口。两版章节和例子对得上，但各自写，不是逐句对译。

## 许可

本手册用 MIT，见 [LICENSE](LICENSE)。这只管这份手册。Markdown 本身是 John Gruber 以 BSD 风格许可发布的，是另一回事。
