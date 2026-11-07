# 行内语法

> English: [en/inline.md](../en/inline.md)

解析器先切块，再回头处理一行之内的标记。强调、代码、链接、换行都活在这一层。写的时候留意符号：一个星号是强调定界符，想让它当字面星号，得转义或者包进行间代码。

## 强调

`*x*` 和 `_x_` 出 `<em>`，`**x**` 和 `__x__` 出 `<strong>`。

```markdown
*em* and _em_
**strong** and __strong__
```

两行合成一段，四种写法各自生效：

```html
<p><em>em</em> and <em>em</em>
<strong>strong</strong> and <strong>strong</strong></p>
```

## 定界符怎么判左右

CommonMark 给 `*` 这类定界符分了左右：看它前后是空白、标点还是字母，决定这段能开、能闭，还是两边都行。词内下划线不产生强调，`foo_bar_baz` 原样留着。嵌套的 `*foo *bar* baz*` 先认里层那对，外层再包住整句；算法有点绕，这里不铺开。

```markdown
foo_bar_baz stays plain

*foo *bar* baz*
```

下划线那行没动，星号那行成了两层 `<em>`：

```html
<p>foo_bar_baz stays plain</p>
<p><em>foo <em>bar</em> baz</em></p>
```

## 删除线

删除线写 `~~x~~`，这是 GFM 扩展，CommonMark 本身不认。

```markdown
~~gone~~
```

纯 CommonMark 原样输出；在 GitHub 上你会拿到 `<del>gone</del>`：

```html
<p>~~gone~~</p>
```

## 行间代码与反引号

单个反引号包住一段行间代码。内容里自带反引号时，外层改用两个反引号，中间就能留一个字面反引号。

```markdown
use `code` here

`` a ` backtick inside ``
```

第二行用双反引号，输出里保留了中间那个反引号：

```html
<p>use <code>code</code> here</p>
<p><code>a ` backtick inside</code></p>
```

## 反斜杠转义

反斜杠转义只对 ASCII 标点有效。`\*` 显示字面星号；`\A` 里的反斜杠会跟着打印出来，因为 `A` 不是标点。

```markdown
\* works \A stays \q stays
```

只有第一个星号被转义，另外两处连反斜杠一起显示：

```html
<p>* works \A stays \q stays</p>
```

### 写错一次：渲染成什么，怎么改

你在 issue 里贴路径 `/tmp/*important*/notes.txt`，两个星号被当成强调定界符，目录名斜体了。

```markdown
the file is /tmp/*important*/notes.txt
```

结果 `important` 被 `<em>` 包住：

```html
<p>the file is /tmp/<em>important</em>/notes.txt</p>
```

把两个星号各转义一次就好：

```markdown
the file is /tmp/\*important\*/notes.txt
```

星号回到字面：

```html
<p>the file is /tmp/*important*/notes.txt</p>
```

## 软换行与硬换行

一行写到头直接回车是软换行，渲染时通常合成一个空格。想硬换行，行尾补两个空格，或者一个反斜杠，输出里就是 `<br />`。

```markdown
soft
break

hard  
stop

back\
slash
```

第一段是软换行，后两段各拿到一个 `<br />`：

```html
<p>soft
break</p>
<p>hard<br />
stop</p>
<p>back<br />
slash</p>
```

## 自动链接、实体与字符引用

尖括号包住网址就是自动链接：`<https://example.com>`。实体和数字字符引用也能直接写：`&copy;` 出 `©`，`&#35;` 出 `#`，`&#x41;` 出 `A`。

```markdown
<https://example.com>
```

尖括号里的网址自己变成可点的链接：

```html
<p><a href="https://example.com">https://example.com</a></p>
```

再看字符引用：

```markdown
&copy; &#35; &#x41;
```

三个都还原成字符：

```html
<p>© # A</p>
```

注意 `&#42;` 不能顶替 `*` 去当强调定界符；字符引用只管显示，不参与结构。

## 行内 HTML

CommonMark 允许你直接写行内 HTML，`<em>html</em>` 会原样进输出。

```markdown
inline <em>html</em> here
```

标签留在结果里：

```html
<p>inline <em>html</em> here</p>
```

GitHub 还会对用户内容里的原始 HTML 做一轮安全过滤，哪些标签被转义、哪些属性被清掉，细节留给 [GFM 那篇](../../03-spec/zh/gfm.md)。

## 延伸阅读

- [块级语法](blocks.md)
- [链接与图片](links-and-images.md)
- [代码块](code.md)
- [CommonMark 规范](../../03-spec/zh/commonmark.md)
