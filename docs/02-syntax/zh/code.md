# 代码块

> English: [en/code.md](../en/code.md)

写代码块有两条路：每行缩进四个空格，或者用围栏围起来。两条路都能到，规则差得远。

## 缩进代码块

每行前面敲四个空格，就是缩进代码块。两个前提：前面得空一行，而且它不能从一段正文中间直接接上——紧跟段落的缩进行会被当成这段的延续。

```markdown
A blank line first.

    def hello():
        print("hi")
```

```html
<p>A blank line first.</p>
<pre><code>def hello():
    print("hi")
</code></pre>
```

把空行删掉，那行缩进行就只是上一句的续行：

```markdown
This is a paragraph.
    print("hi")
```

```html
<p>This is a paragraph.
print("hi")</p>
```

## 围栏代码块

开头至少三个反引号或波浪号，结尾再来一段收住。下面这个源码块外层用 `~~~markdown`，没用三反引号：例子里本身有三反引号，三反引号当外层会被内层提前闭合，整篇渲染就塌了。

~~~markdown
```js
console.log("hi");
```
~~~

```html
<pre><code class="language-js">console.log("hi");
</code></pre>
```

开头围栏后面跟的那串叫 info string，第一个词通常当语言名。渲染器给它加 `language-` 前缀做成 class，上面就成了 `class="language-js"`，预览和高亮工具靠这个认语言。用反引号开的围栏，info string 里不能再出现反引号。

开闭有几条硬规则，踩了不报错，只会安静地渲染错：

- 开闭必须同一种字符。三反引号开头、三波浪号收尾，不算闭合。
- 闭合那段不能比开头短。四个反引号开头，三个收不住，那一行只是代码内容。
- 闭合那一行后面只能跟空格。多写一个词，围栏继续往下吃后面的内容。
- 围栏最多缩进三个空格。四个空格一起，整段改按缩进代码块处理。

把围栏整体缩进四个空格试试，它就不再是围栏了：

```markdown
A blank line first.

    ```js
    console.log("hi");
    ```
```

~~~html
<p>A blank line first.</p>
<pre><code>```js
console.log("hi");
```
</code></pre>
~~~

上面这个结果块里带三反引号，外层同样用波浪号收。忘了写闭合围栏也不算语法错误：CommonMark 里任意字符序列都是合法文档，解析器会一直吃到文件结尾，或者吃到所在的列表项、引用块结束，把剩下的全收进代码块。

## 围栏里再放围栏

写教程要展示一段带围栏的代码，外层就不能再是三个反引号。把外层加长到四个，内层的三反引号就只是普通文本：

````markdown
# Demo

Wrap the code in a fence and tag the language:

```python
print("hi")
```
````

```html
<h1>Demo</h1>
<p>Wrap the code in a fence and tag the language:</p>
<pre><code class="language-python">print("hi")
</code></pre>
```

外层四个开、四个闭，内层三开三闭，谁也不碰谁，这段可以直接贴进文件渲染。换 `~~~markdown` 开、`~~~` 收也一样：波浪号和反引号互不认，内层怎么折腾都碰不到外层。我更常用波浪号，省得数反引号。

## 什么时候用哪种

写教程我基本只用围栏式。理由很实在：能标语言。开头跟个 `python`，输出里就带上 `class="language-python"` 这样的 class，预览、高亮、读源码的人都认得出是什么；缩进式交出去是一坨没有标记的等宽文本，什么信息都不带。围栏式还照收空行和以 `#` 开头的行，缩进式遇到这些得处处小心。

缩进式我只留两处。目标环境认不认围栏没把握时，四个空格更保险，它不依赖解析器实现了哪一版语法；在列表或引用里随手补两行，敲四个空格比开一对围栏少几下，我也懒得讲究。新写的东西，围栏式，标上语言。

## 下一步

行内代码和反引号怎么配对，看 [inline.md](inline.md)；链接里的尖括号和括号转义在 [links-and-images.md](links-and-images.md)；渲染出来不对劲，翻 [gotchas.md](gotchas.md)。规范版本和 GFM 的扩展在 [commonmark.md](../../03-spec/zh/commonmark.md)、[gfm.md](../../03-spec/zh/gfm.md)。
