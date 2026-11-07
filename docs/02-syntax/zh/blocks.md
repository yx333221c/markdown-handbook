# 块级语法

> English: [en/blocks.md](../en/blocks.md)

空行在 Markdown 里是语法的一部分。两段文字连着写、中间不留空行，解析器把它们并成一段；留一个空行，才是两段。标题、列表、代码块都要靠它切分。

```markdown
first line
second line

new paragraph
```

空行把上面劈成两段，输出也就跟着分成两个 `<p>`：

```html
<p>first line
second line</p>
<p>new paragraph</p>
```

## ATX 标题

行首写 1 到 6 个 `#`，后面跟一个空格或者干脆到行尾，就是标题。这个写法沿自 Aaron Swartz 2002 年的 `atx`，所以规范里叫 ATX 标题。开头 `#` 后面不空一格的话，`#hashtag` 和 `#5 bolt` 都只是普通文字。行尾还能补一串 `#` 当闭合，几个都行，解析器会把它去掉。

```markdown
### Title ###

#hashtag
#5 bolt
####### seven

    # indented
```

第一行是标题，`#hashtag` 那几行是段落，七个 `#` 也超了上限，最后那行缩进四个空格，掉进代码块：

```html
<h3>Title</h3>
<p>#hashtag
#5 bolt
####### seven</p>
<pre><code># indented
</code></pre>
```

开头 `#` 的个数直接定级别，一张小表就够：

| 开头 `#` 个数 | 输出 | 写法 |
| --- | --- | --- |
| 1 到 6 | `<h1>` 到 `<h6>` | `# Title` 到 `###### Title` |
| 超过 6 | 普通段落 | `####### Title` |

我觉得闭合 `#` 该少用，它和正文里的井号容易看混，读起来还多一串符号。

## Setext 标题

Setext 是另一种标题写法，靠文字下面的 `=` 或 `-` 定级：`=` 出 `<h1>`，`-` 出 `<h2>`。

```markdown
Title
=====

Foo
---
bar
```

`Title` 变一级标题，`Foo` 后面那行 `---` 被当成二级标题的下划线，`bar` 才是段落：

```html
<h1>Title</h1>
<h2>Foo</h2>
<p>bar</p>
```

坑就在这儿：`Foo` 后面跟 `---`，你本意可能是画条分隔线，结果拿到一个 `<h2>`。想要分隔线就换成 `***`，或者前后补空行。这个撞车我不喜欢，所以平时只用 ATX。

## 主题分隔线

单独一行写三个及以上 `-`、`*`、`_`，中间允许夹空格，就是一条 `<hr />`。少于三个不算，混着用不同符号也不算。

```markdown
---
***
___
- - -

    ---
```

前四行都是分隔线，最后一行因为缩进了四个空格，进了代码块：

```html
<hr />
<hr />
<hr />
<hr />
<pre><code>---
</code></pre>
```

四个空格这条线得记牢：标题和分隔线碰到它都会变成代码块。

## 块引用与惰性续行

`>` 开头是块引用，连着写两个 `>` 就是嵌套。惰性续行（lazy continuation）有点怪：一行没写 `>` 也可能被算进引用里，只要它接得上前面的段落。

```markdown
> first
continued lazily
>
> > nested
```

`continued lazily` 没有 `>`，照样并进第一段；空行之后 `> >` 开了一层嵌套：

```html
<blockquote>
<p>first
continued lazily</p>
<blockquote>
<p>nested</p>
</blockquote>
</blockquote>
```

想让引用干净收尾，补一个空行最省事。

## 列表：标记、嵌套、松散与紧凑

无序用 `-`、`*`、`+`，有序用数字加 `.`。子列表要对齐父项文字的起点：`- one` 里 `-` 加空格占两格，下一层的 `-` 就缩进两格。Gruber 的原始说明没回答子列表到底缩进几个空格、列表项什么时候该包 `<p>`，GFM 规范 1.3 节把这类悬案列了一串，CommonMark 后来把它们写成了明确规则。

```markdown
- one
  - nested

1. first
2. second
```

两格缩进造出子列表，空行把无序和有序分成两个列表：

```html
<ul>
<li>one
<ul>
<li>nested</li>
</ul>
</li>
</ul>
<ol>
<li>first</li>
<li>second</li>
</ol>
```

紧凑列表（tight）的项里没有 `<p>`，松散列表（loose）有。决定权又在空行：项与项之间一留空行，整张列表就松散了。

```markdown
- one
- two
```

贴着写的两项，输出里光秃秃的：

```html
<ul>
<li>one</li>
<li>two</li>
</ul>
```

```markdown
- one

- two
```

中间加一个空行，每项都被 `<p>` 包起来：

```html
<ul>
<li>
<p>one</p>
</li>
<li>
<p>two</p>
</li>
</ul>
```

同一张列表里只要有一项松散，整张都按松散处理。你改 CSS 时觉得行距变大，多半是源码里多敲了一个回车。

## 块级优先于行内

解析器先定块的结构，再回头处理行内标记，块级标记的优先级（precedence）更高。CommonMark 规范 3.1 节拿这个例子说明：

```markdown
- `one
- two`
```

两个反引号看着像能凑成一对行间代码，但列表先被切开了，反引号只好当字面字符留在各自项里：

```html
<ul>
<li>`one</li>
<li>two`</li>
</ul>
```

## 延伸阅读

- [行内语法](inline.md)
- [链接与图片](links-and-images.md)
- [CommonMark 规范](../../03-spec/zh/commonmark.md)
