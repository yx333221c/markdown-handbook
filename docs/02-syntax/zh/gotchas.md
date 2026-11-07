# 渲染出错的时候

> English: [en/gotchas.md](../en/gotchas.md)

## 一整段突然变成斜体

```markdown
文件名写 *report 开头就行，别用 report* 结尾。
```

```html
<p>文件名写 <em>report 开头就行，别用 report</em> 结尾。</p>
```

你只想打两个字面星号，或者给「report」加斜体时漏了收尾的 `*`。渲染器只认配对：找到第二个 `*`，把中间一整截塞进 `<em>`。字面星号写成 `\*` 或包进行间代码；要强调就补齐闭合的 `*`。

## `#` 后面没空格，标题没出来

```markdown
#部署清单
先把文档过一遍。
```

```html
<p>#部署清单
先把文档过一遍。</p>
```

`#` 后面没空格就只是普通正文，下一行还会被软换行并进来。CommonMark 和 GFM 规定 ATX 标题是 1–6 个 `#` 后跟空格（或到行尾）；有些老实现不要求空格，换个地方渲染可能就成了标题。补上空格：

```markdown
# 部署清单
先把文档过一遍。
```

```html
<h1>部署清单</h1>
<p>先把文档过一遍。</p>
```

## 正文里四个空格缩进的那行成了代码块

```markdown
这一段讲安装步骤。

    把四个空格当成对齐用，结果它变成了代码。
```

```html
<p>这一段讲安装步骤。</p>
<pre><code>把四个空格当成对齐用，结果它变成了代码。
</code></pre>
```

四个空格开头的行，前面隔着空行就是缩进代码块，不是「往里挪一点」。Markdown 没有给正文做视觉缩进的语法。紧跟段落没空行时，CommonMark 把它当续行，四个空格照样被吃掉。要代码用围栏并标语言，见 [code.md](code.md)；要引用写 `>`，要分层用列表。

## `---` 把上一行变成了二级标题

```markdown
发布前检查
---
```

```html
<h2>发布前检查</h2>
```

底下垫一行 `---`，上面那行就成了 setext 二级标题：`-` 下划线给 `<h2>`，`=` 给 `<h1>`。它是标题下划线，不是分隔线。想画分隔线，文字和 `---` 中间空一行。我不用 setext 标题，就因为它跟 `---` 撞车。

```markdown
发布前检查

---
```

```html
<p>发布前检查</p>
<hr />
```

同一类坑还有 `* * *`。三个及以上 `-`、`*`、`_` 单独成行、中间带空格也行，就是主题分隔线：在列表项里当装饰敲一行，结果是一条横线。

```markdown
第一段写完。

* * *

第二段。
```

```html
<p>第一段写完。</p>
<hr />
<p>第二段。</p>
```

想要三个字面星号，写成 `\* \* \*` 或包进行间代码 `* * *`。缩进四个空格也不行，那就掉回代码块了。

## 表格前后没空行，整张表没渲染

```markdown
先看这张表：
| 列 | 值 |
| --- | --- |
| a | 1 |
然后改配置。
```

```html
<p>先看这张表：
| 列 | 值 |
| --- | --- |
| a | 1 |
然后改配置。</p>
```

表格是 GFM 标了 `(extension)` 的块级结构。前面紧贴正文、后面直接接下一句时，很多渲染器不认它，这些行并进段落，管道符原样印出来。各方言对「表格能不能打断段落」处理不一致，前后各空一行最省事：

```markdown
先看这张表：

| 列 | 值 |
| --- | --- |
| a | 1 |

然后改配置。
```

```html
<p>先看这张表：</p>
<table>
<thead><tr><th>列</th><th>值</th></tr></thead>
<tbody><tr><td>a</td><td>1</td></tr></tbody>
</table>
<p>然后改配置。</p>
```

## 单元格里的 `|` 把列切错了

```markdown
| 命令 | 说明 |
| --- | --- |
| a | b | 管道符要转义 |
```

```html
<table>
<thead><tr><th>命令</th><th>说明</th></tr></thead>
<tbody><tr><td>a</td><td>b</td></tr></tbody>
</table>
```

表头两列，这行被 `|` 切成三个单元格，多出来的「管道符要转义」直接没了。GFM 按表头列数截取，多出的单元格静默丢掉，所以丢了字也没人提醒你。单元格里写管道符要用 `\|` 转义，包在行间代码里也一样：

```markdown
| 命令 | 说明 |
| --- | --- |
| `a\|b` | 管道符要转义 |
```

```html
<table>
<thead><tr><th>命令</th><th>说明</th></tr></thead>
<tbody><tr><td><code>a|b</code></td><td>管道符要转义</td></tr></tbody>
</table>
```

## 写了 `<div class="note">`，样式却没生效

```markdown
<div class="note">
这段被包在 div 里。
</div>
```

```html
<div>
这段被包在 div 里。
</div>
```

GFM 里「禁止原始 HTML」标着 `(extension)`，但它的 tagfilter 只转义九个标签：`<title>`、`<textarea>`、`<style>`、`<xmp>`、`<iframe>`、`<noembed>`、`<noframes>`、`<script>`、`<plaintext>`。规范原话是「其余 HTML 标签原样保留」，`<div>` 不在名单上，所以标签还在。真正没了的是 `class`：GitHub 转完 HTML 之后还有一轮 sanitization，属性在那儿被清掉。想做提示块用引用 `>`，或者写成普通段落，别靠 `div` 调排版。

```markdown
> 这段被包在引用里。
```

```html
<blockquote>
<p>这段被包在引用里。</p>
</blockquote>
```

## 行尾两个空格的硬换行，一格式化就没了

```markdown
第一行  
第二行
```

```html
<p>第一行<br />
第二行</p>
```

硬换行靠行尾两个空格，或者行尾一个 `\`。两个空格在编辑器里看不见，格式化工具一跑常被清掉，下一行就跟上一行并成一段——软换行渲染时通常合并成一个空格。改成行尾 `\` 更显眼，或者空一行分成两段。

```markdown
第一行\
第二行
```

```html
<p>第一行<br />
第二行</p>
```

## URL 里的括号把链接截断了

```markdown
看 [API 说明](https://example.com/docs/v2_(beta))。
```

```html
<p>看 <a href="https://example.com/docs/v2_(beta">API 说明</a>)。</p>
```

点开链接地址少了一截，末尾还多出个 `)`。有些解析器碰到 URL 里第一个 `)` 就当链接结束，各方言处理不一致，别赌。URL 包进尖括号，或把括号写成 `\(` 和 `\)`。更多写法见 [links-and-images.md](links-and-images.md)。

```markdown
看 [API 说明](<https://example.com/docs/v2_(beta)>)。
```

```html
<p>看 <a href="https://example.com/docs/v2_(beta)">API 说明</a>。</p>
```

## Windows 的 CRLF 和别的环境对不上

```markdown
# 发布记录

改动都记在这份文件里。
```

```text
CRLF 存盘：第一行\r\n第二行\r\n
LF   存盘：第一行\n第二行\n
```

同一份文件存两遍，行尾字节就不一样。多出来的 `\r` 偶尔会让硬换行、代码块边界的判断对不上，一群人用不同系统改同一个仓库时尤其容易撞见。具体哪个工具怎么处理，我不下断言：拿你的编辑器存成两种格式各渲染一遍，差异自己看得见。仓库里统一一种行尾，比事后排查省事。

## 下一步

行内标记的配对在 [inline.md](inline.md)，块级元素在 [blocks.md](blocks.md)，围栏开闭在 [code.md](code.md)。规范看 [commonmark.md](../../03-spec/zh/commonmark.md) 和 [gfm.md](../../03-spec/zh/gfm.md)；速查表 [cheatsheet.md](../../05-reference/zh/cheatsheet.md)。
