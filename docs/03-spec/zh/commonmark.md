# CommonMark：给一份没有语法错误的语法定规矩

> English: [en/commonmark.md](../en/commonmark.md)

这段源码你先看一遍：

```markdown
- a
  - b
```

再缩进一格，或者把 `  - b` 改成 `   - b`，有的解析器把 `- b` 当成 `a` 的子列表，有的把它当成同一行的延续，还有的当成一段缩进代码。几种输出都算「合法」。Gruber 在 Daring Fireball 上写的 canonical syntax description 是一页说明，配着 `Markdown.pl` 这个 Perl 脚本，里头没有逐条可判定的规则。脚本自己有 bug，而且 2004 年 12 月 17 日发完 `Markdown 1.0.1` 之后就再没动过。各实现的作者只能自己补规则，GitHub wiki、Pandoc、各种编辑器因此互相对不上。

更要命的是 Markdown 里没有「语法错误」这回事。任意字符序列都是合法文档，解析器不会报错，只会安静地给你一个 HTML。同一段文字在两个平台渲染得不一样，往往要等你把文档发出去、别人截图问你「怎么少了标题」，才发现。

## 那十四个没人回答的问题

GFM 规范 1.3 节把 Gruber 没写清的地方列了一串，十四个。挑几个真会绊到人的：

子列表到底缩进几个空格。上面那个例子里，两空格和三空格在一些实现里结果不同，CommonMark 按内容和列表标记的对齐来定，不再靠猜。

```markdown
- parent
  - two spaces
- parent
   - three spaces
```

块引用和标题前面要不要空行。下面两段，一个贴着段落，一个隔了空行，旧解析器对「块能不能直接打断段落」的处理不统一：

```markdown
Some text
> a quote

Some text

# a heading
```

缩进代码块前面要不要空行。四个空格的行若紧跟在段落后面，有的实现当代码块，有的当段落的软换行延续：

```markdown
A paragraph
    indented line
```

还有行内标记的优先级和同名链接定义的取舍。`*a **b** c*` 里谁先闭合、`[x]` 对应两个 `[x]: url` 时用哪一个，这些都得一条条写死。CommonMark 把每个边界情况配上一个输入和一段期望 HTML，攒成几百个例子。

## 解析分两步

CommonMark 要求解析器先扫块结构，再处理行内。先把文档切成段落、标题、列表、引用、代码块，再在每一行内部解析强调、链接、代码。块级优先于行内，所以 `# a *b*` 里的 `*` 不会反过来改变标题的边界。

块又分两类。container block 能装别的东西，比如列表项、块引用、列表本身；leaf block 只装自己的文本，比如段落、标题、缩进代码块、围栏代码块、主题分隔线。要判断一段源码属于哪一层，靠的就是这个区分。

## 版本、测试、谁在做

规范自带例子，每个例子都是一段 Markdown 加一段期望 HTML，可以直接当一致性测试跑。仓库里的 `spec_tests.py` 读 `spec.txt`，把每个例子喂给实现，比对输出。你要写解析器，或者只想确认某个工具到底听不听话，跑它就够了。

版本有 `0.29`、`0.30`（2021-06-19）。写稿时别断言哪个是最新，去官网看当前标注。

CommonMark 官网现在列的核心成员是 John MacFarlane、Martin Woodward、Jeff Atwood。采用者名单里有 Discourse、GitHub、GitLab、Reddit、Qt、Stack Overflow / Stack Exchange、Swift。

想接着看语法细节，去 [zh/blocks.md](../../02-syntax/zh/blocks.md) 和 [zh/inline.md](../../02-syntax/zh/inline.md)；踩坑清单在 [zh/gotchas.md](../../02-syntax/zh/gotchas.md)。GitHub 在自己的方言里又加了几条，见 [zh/gfm.md](gfm.md)。
