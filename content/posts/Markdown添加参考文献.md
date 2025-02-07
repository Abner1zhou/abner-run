+++
title = 'Markdown添加参考文献'
date = 2025-02-07T17:07:39+08:00
categories = ["工具教材"]
tags = ["Markdown"]
author=  "Abner Zhou"
draft = false
+++

在Markdown中编写文章，难免需要引入外部文献、网页。以下就是我收集的几种引用方式。

## 引用式链接[^2]

众所周知，[Markdown 中的链接](https://sspai.com/link?target=https%3A%2F%2Fdaringfireball.net%2Fprojects%2Fmarkdown%2Fsyntax%23link) 是这样写的：

```markdown
This is [an example](http://example.com/ "Title") inline link.

[This link](http://example.net/) has no title attribute.
```

这种广泛使用的链接写作方式被称为行内链接（inline link）。实际上，Markdown 中的链接还有另一种不太常用的写法，即引用式链接（reference-style link），它的形式如下：

```markdown
This is [an example] [id] reference-style link.

[id]: http://example.com/  "Optional Title Here"
```

可以发现，引用式链接在正文中使用了两个方括号，第一个方括号包裹超链接的文本部分，也就是这里的 `[an example]`，紧接着其后的是一个可有可无的空格，接下来使用第二个方括号包裹该链接的标识符，这里用 `[id]` 表示。

## 引用式脚注

我比较喜欢的一种方式，本文的引用方式也是用的这种方式。但是它依赖于Markdown的扩展语法，取决于Markdown编辑器是否支持。

```Markdown
Here is a footnote reference,[^1] and another.[^longnote] [^1]: Here is the footnote. [^longnote]: Here's one with multiple blocks.
```

## HTML方式脚注

需要在引用链接前增加锚点[^1] [^3]

```markdown
## 参考

<div id="refer-anchor-1"></div>
- [1] [百度学术](http://xueshu.baidu.com/)
<div id="refer-anchor-2"></div>
- [2] [Wikipedia](https://en.wikipedia.org/wiki/Main_Page)
```

**脚注添加方式**：

```markdown
## Markdown 增加文献引用  
  
这边文章是介绍如何在 Markdown 中增加文献引用。[<sup>1</sup>](#refer-anchor-1)
```

我测试过程中发现，在Obsidian中不支持，会把`- [1]`解析为todo `- [ ]`

## 引用

[^1]: [Markdown添加参考文献 | Markdown添加引用_markdown引用-CSDN博客](https://blog.csdn.net/qq_36667170/article/details/121656279)

[^2]: [在 Markdown 中使用引用式链接和脚注 - 少数派](https://sspai.com/post/77513)

[^3]: [Markdown 添加文献引用_markdown参考文献-CSDN博客](https://blog.csdn.net/u012349679/article/details/103815049)
