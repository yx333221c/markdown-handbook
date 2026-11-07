# 从 Gruber 到 CommonMark

> English: [en/from-gruber-to-commonmark.md](../en/from-gruber-to-commonmark.md)

Gruber 那份 canonical syntax description 讲清楚了写法，却没把边界写死。它是一页说明，不是无歧义的规范。子列表该缩进几个空格、块引用前要不要空行、两个同名链接定义谁优先，这些问题它没回答。GFM 规范 1.3 节后来专门列了一串。

早期实现者遇到拿不准的地方，只能去翻 `Markdown.pl` 的源码，而这份 Perl 脚本本身有 bug。于是每个解析器作者按自己的理解补空缺。十年下来分叉出几十种实现，同一篇文档贴到 GitHub wiki 和拿 Pandoc 转 docbook，结果可能不一样。

更麻烦的是，Markdown 里没有「语法错误」这回事，CommonMark 里的说法是任意字符序列都是合法文档。你写了一段自己觉得没问题的列表，渲染器照样给你一段 HTML，只是段落层级和别人那边不同。这种差异不报错，往往要等到文档挪到另一个平台、或某天 diff 里冒出一堆格式变化，才被发现。想直观对比，Babelmark 能把 20 多个实现的输出并排列出来。

2012-10-25，Jeff Atwood 发了《The Future of Markdown》，提议主流站点一起定一份正式规范和测试集。文中提到 David Greenspan 给他写的邮件，还有个工作代号 "Rockdown"。到 2014 年，John MacFarlane、David Greenspan（Meteor）、Vicent Marti（GitHub）、Neil Williams（Reddit）、Benjamin Dumke-von der Ehe（Stack Exchange）、Jeff Atwood（Discourse）等人把项目启动起来，后来叫 CommonMark。CommonMark 官网现在列的核心成员是 John MacFarlane、Martin Woodward、Jeff Atwood。

规范有版本号，比如 `0.29`，`0.30`（2021-06-19）。我不写「最新版」，因为这个编号会往前走，你读到这段时页面上的数字大概已经变了。官网列的采用者包括 Discourse、GitHub、GitLab、Reddit、Qt、Stack Overflow / Stack Exchange、Swift。

这事儿不是没有争议。有人觉得给一门以「好读」为卖点的语法配一份逐条定义的规范，方向就拧了；Gruber 那页说明和 CommonMark 的措辞也确实对不上，比如 CommonMark 明确写「任意字符序列都是合法文档」。争议的具体依据主要落在规范文本和各自的实现上，我手上没有 Gruber 对此的表态，就不替他补了。

想看规范本身怎么读，翻 [CommonMark 那篇](../../03-spec/zh/commonmark.md)；GitHub 的方言见 [GFM](../../03-spec/zh/gfm.md)。
