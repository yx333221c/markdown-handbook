# 链接与图片

> English: [en/links-and-images.md](../en/links-and-images.md)

一句话里插个网址，最省事的是行内链接。方括号写显示文字，圆括号写 URL，URL 后面还能用双引号补一个 title：

```markdown
[CommonMark 官网](https://commonmark.org "CommonMark")
```

```html
<p><a href="https://commonmark.org" title="CommonMark">CommonMark 官网</a></p>
```

双引号只负责把 title 圈住，不会出现在链接文字里，鼠标悬上去才看得到。title 自己要带一个双引号，就写成 `\"`——反斜杠转义对 ASCII 标点有效，`\*` 显示成字面星号也是同一条规则。

URL 里带括号，有些渲染器会坏。像 `https://example.com/a_(b)` 这种地址，碰到在第一个 `)` 就收工的解析器，后面的字符全掉在链接外面；换个渲染器又可能没事。各方言对括号的处理不一致，别赌，两种写法都稳：URL 包进尖括号，或者把括号转义。

```markdown
[消歧义页](<https://example.com/a_(b)>) 和 [另一页](https://example.com/a_\(b\))
```

```html
<p><a href="https://example.com/a_(b)">消歧义页</a> 和 <a href="https://example.com/a_(b)">另一页</a></p>
```

## 引用式链接

同一个网址在一段里出现三四次，行内写法会把正文撑得没法读。换成引用式：正文写 `[text][id]`，另起一行写定义 `[id]: url`。标签和显示文字一样时，第二个方括号可以整套省掉，变成 `[text][]`。

```markdown
先看 [规范全文][cm]，再翻 [CommonMark][]。

[cm]: https://spec.commonmark.org "CommonMark Spec"
[CommonMark]: https://commonmark.org
```

```html
<p>先看 <a href="https://spec.commonmark.org" title="CommonMark Spec">规范全文</a>，再翻 <a href="https://commonmark.org">CommonMark</a>。</p>
```

定义行不会渲染成段落。渲染器先把整篇的定义读进去，再回头填链接，所以它们放在开头、结尾、两段中间都行。我习惯堆在文末，改 URL 时不用在正文里翻。

还有个问题这页不答：同一个 id 写两条定义，`[cm]: url1` 和 `[cm]: url2`，哪条生效？这是 Gruber 文档没回答、后来由规范定死的问题之一，细节留给 [gfm.md](../../03-spec/zh/gfm.md)。眼下只提醒一句，别在同一篇里复用 id。

## 自动链接

网址直接塞进尖括号，显示文字就是网址本身，不用再写一遍方括号：

```markdown
<https://example.com>
```

```html
<p><a href="https://example.com">https://example.com</a></p>
```

GFM 多了一条扩展（规范目录里标了 `(extension)`）：不加尖括号，光写 `https://example.com` 或 `www.example.com` 也会变成链接。CommonMark 原本不认这个，文件要在多个地方渲染时别依赖它。

```markdown
https://example.com 和 www.example.com
```

```html
<p><a href="https://example.com">https://example.com</a> 和 <a href="http://www.example.com">www.example.com</a></p>
```

## 图片

图片就是链接前面加个 `!`：`![alt](url)`。方括号里的 alt 文本不是图片说明，是图片没加载出来、或者被屏幕阅读器念出来时顶替图片的那句话。

```markdown
![被雪压弯的一棵松树](pine.png "冬日")
```

```html
<p><img src="pine.png" alt="被雪压弯的一棵松树" title="冬日" /></p>
```

写 alt 有个笨办法：把图片捂住，用一句话说清你希望读者知道什么，把这句填进去。`![松树]` 比 `![图片]` 有用，`![IMG_2043.png]` 基本等于没写。纯装饰的图片就留空 `![]()`，别让阅读器念一串文件名。

## 下一步

链接跟强调、行内代码怎么套在一起，看 [inline.md](inline.md)；围栏代码块的开闭规则在 [code.md](code.md)；渲染出来不对劲，翻 [gotchas.md](gotchas.md)。规范层面的细节在 [commonmark.md](../../03-spec/zh/commonmark.md) 和 [gfm.md](../../03-spec/zh/gfm.md)。
