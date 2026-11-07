# 把文件放到别人看得见的地方

> English: [en/publishing.md](../en/publishing.md)

写完的 `.md` 总得有个落处，而落处决定它长什么样。

仓库根的 `README.md` 是 GitHub 自动渲染的：打开仓库主页，文件列表下面那段就是它，不用点、不用配。中文版我放 `README.zh.md`，GitHub 不会替你把它顶上去，读者得自己点进那个文件才看得到，所以 `README.md` 里留一条链接过去比什么都实在。issue、PR 描述、wiki 的输入框走的也是 GFM，表格、任务列表、删除线这些扩展语法在那几处都能用；你在 PR 里贴的 `- [x]` 会真的渲染成勾掉的方框，不是因为 Markdown 本来如此，是因为 GitHub 用的是 GFM。

出了仓库页就别想当然。GitHub Pages 配 Jekyll，或者换个静态站点生成器，它们对 Markdown 的处理不一定等于 GitHub 仓库页：可能换了解析器，可能先抽掉 front matter，可能按自己的规则重写链接。同一份文件在 Pages 上少了任务列表的方框，多半是这个原因，不是你写错了。Pandoc 转 `docx` / `pdf` / `html` 也同理——表格、任务列表这类扩展语法可能丢，也可能变个样子，所以先转一份看看结果再批量处理，比事后逐页修省事。

最容易断的是相对链接和图片。假设仓库里是这样：

```text
docs/
  guide.md
  assets/
    login-error.png
```

`guide.md` 里写 `![报错提示](./assets/login-error.png)` 没事。等把 `guide.md` 单独搬到站点根目录下、或者 `assets/` 没跟着一起拷，路径就指不到东西了；有些人图省事写死 `https://github.com/me/repo/blob/main/...`，换 fork 又失效。这种断链在源码里看不出来，只有打开目标页面才现形，所以发布前在目标平台预览一次，这套流程值得走一遍。

顺带一句：开源仓库里最该先写的两个文件是 `LICENSE` 和 `README.md`。没有许可，别人连能不能用都不敢判断；`README.md` 又是主页默认显示的那份。

想弄清 GitHub 这套多出来的语法，看 [gfm.md](../../03-spec/zh/gfm.md)；想核对某个渲染差异到底归谁，[dialects.md](../../03-spec/zh/dialects.md) 和 [commonmark.md](../../03-spec/zh/commonmark.md) 分别在讲方言分叉和规范本身。
