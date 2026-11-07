# Code Blocks

> 中文: [zh/code.md](../zh/code.md)

There are two ways to write a code block: indent every line by four spaces, or wrap it in a fence. Both work, and the rules behind them have almost nothing in common.

## Indented code blocks

Four spaces in front of every line makes an indented code block. Two conditions: a blank line before it, and it can't pick up in the middle of a paragraph, because an indented line that follows prose directly is just a continuation of that paragraph.

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

Delete the blank line and the indented line becomes part of the sentence above:

```markdown
This is a paragraph.
    print("hi")
```

```html
<p>This is a paragraph.
print("hi")</p>
```

## Fenced code blocks

Open with at least three backticks or tildes, close with another run. The source block below uses `~~~markdown` for its outer fence rather than three backticks: the example itself contains a three-backtick line, which would close a three-backtick outer fence early and wreck the rest of the page.

~~~markdown
```js
console.log("hi");
```
~~~

```html
<pre><code class="language-js">console.log("hi");
</code></pre>
```

The text after the opening fence is the info string. Its first word is normally taken as the language name, and the renderer adds a `language-` prefix to make a class, so you get `class="language-js"` above. Previews and highlighters use that to pick a language. A fence opened with backticks can't contain a backtick in its info string.

A few hard rules about opening and closing. Break one and nothing complains; the block just quietly renders wrong:

- Open and close with the same character. Three backticks followed by three tildes is not a closing fence.
- The closing run can't be shorter than the opening one. Open with four backticks and a line of three is only code content.
- A closing fence line can be followed by spaces and nothing else. Add a word and the fence keeps eating everything below it.
- A fence can be indented by up to three spaces. Indent it four and the whole thing is treated as an indented code block instead.

Indent a fence by four spaces and it stops being a fence:

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

That result block carries three-backtick lines, so its outer fence is tildes again. Forgetting the closing fence isn't a syntax error either: in CommonMark any sequence of characters is a valid document, and the parser keeps reading until the file ends, or until the list item or block quote that contains the fence ends, pulling everything in between into the code block.

## A fence inside a fence

When a tutorial needs to show a snippet that already has a fence, the outer fence can't be three backticks. Lengthen it to four and the inner three-backtick lines become plain text:

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

Four backticks open and four close, with three opening and three closing inside; neither fence touches the other, and you can paste this straight into a file. Opening with `~~~markdown` and closing with `~~~` works just as well: tildes and backticks don't recognise each other, so the inner fence can't end the outer one. I reach for tildes more often, because there are fewer backticks to count.

## Which one to use

In tutorials I use fenced blocks almost exclusively, for a plain reason: they carry a language tag. Put `python` after the opening fence and the output gets a class like `class="language-python"` that previews and highlighters recognise. An indented block hands over an unmarked slab of monospace text. Fenced blocks also swallow blank lines and lines starting with `#` without fuss, where indented blocks make you watch every line.

I keep indented blocks for two cases. When I'm not sure the target handles fences, four spaces are safer, since they don't depend on which version of the syntax the parser implemented. And for two quick lines inside a list or a quote, four spaces are fewer keystrokes than a pair of fences, and I don't bother being fussy. For anything new: fenced, with a language tag.

## Where to go next

For inline code and how backticks pair up, see [inline.md](inline.md). Angle brackets and escaped parentheses in links are in [links-and-images.md](links-and-images.md). When the output looks wrong, [gotchas.md](gotchas.md) collects the failures. Spec versions and GFM's extensions live in [commonmark.md](../../03-spec/en/commonmark.md) and [gfm.md](../../03-spec/en/gfm.md).
