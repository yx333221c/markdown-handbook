# Markdown 是什么

> English: [en/what-is-markdown.md](../en/what-is-markdown.md)

Markdown 有两个意思，容易混：一套用纯文本写排版的语法，以及 2004 年 John Gruber 写来把这类文本转成 HTML 的 Perl 脚本 `Markdown.pl`。Aaron Swartz 跟他一起做的。脚本默认吐 XHTML，加 `--html4tags` 才换成 HTML 风格。现在你多半只碰到前者，当年这名字却是连着脚本一起叫的。

Gruber 在 Daring Fireball 的 Markdown 主页上把目标写成一句话：

> "The overriding design goal for Markdown's formatting syntax is to make it as readable as possible."

同一页他还说，语法最大的灵感来自纯文本邮件的写法。想想你写邮件时的习惯：用 `>` 引上一段、用 `*` 标重点、空一行分段、拿 `-` 起一串清单。这些不用教，读起来也不挡眼。Markdown 把这些习惯收成了规则，源文件本身就能给人看。

你在 README、issue、wiki、还有静态站点生成器产出的页面里会一遍遍撞见它。写的人存的是 `.md` 纯文本，读的人看到标题、列表和链接。仓库里那份 `README.md`，在 GitHub 上打开带格式，下载下来用记事本照样能改。

管不了的也清楚：复杂排版、要把东西钉在页面某个位置的精确布局、表格里合并单元格，纯文本语法都给不出稳妥写法。往里塞原始 HTML 是个常见办法，但 GitHub 转完 HTML 还会再做一轮安全过滤（sanitization），留下什么由平台说了算。这类需求交给排版工具。

一小段入门。源码：

```markdown
# 周六的发布清单

先写上 **版本号**，再列要改的东西：

- 更新 `README.md`
- 关掉 #42 那个 issue

> 别在周五下午发版。
```

转出来的 HTML：

```html
<h1>周六的发布清单</h1>
<p>先写上 <strong>版本号</strong>，再列要改的东西：</p>
<ul>
<li>更新 <code>README.md</code></li>
<li>关掉 #42 那个 issue</li>
</ul>
<blockquote>
<p>别在周五下午发版。</p>
</blockquote>
```

`#` 后面得跟空格才是标题，`#42` 只是普通文字。块级元素怎么断行、怎么嵌套，接着读 [blocks.md](../../02-syntax/zh/blocks.md)。
