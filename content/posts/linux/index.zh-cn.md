---
weight: 4
title: "Ubuntu"
date: 2022-02-25T21:57:40+08:00
lastmod: 2022-02-25T16:45:40+08:00
draft: false
author: "Qitas"
authorLink: "https://www.qitas.cn"
description: "这篇文章总结了基本的Linux使用."
resources:
- name: "featured-image"
  src: "featured-image.png"

tags: ["Markdown", "HTML"]
categories: ["Markdown"]

lightgallery: true
---


事实上编写 Web内容很麻烦. [WYSIWYG]^(所见即所得) 编辑器帮助减轻了这一任务. 但通常会导致代码太糟, 或更糟糕的是, 网页也会很丑.

没有通常伴随的所有复杂和丑陋的问题, **Markdown** 是一种更好的生成 **HTML** 内容的方式.

一些主要好处是:

1. Markdown 简单易学, 几乎没有多余的字符, 因此编写内容也更快.
2. 用 Markdown 书写时出错的机会更少.
3. 可以产生有效的 XHTML 输出.
4. 将内容和视觉显示保持分开, 这样就不会打乱网站的外观.
5. 可以在你喜欢的任何文本编辑器或 Markdown 应用程序中编写内容.
6. Markdown 使用起来很有趣!


```markdown
### 一个很棒的标题 {#custom-id}
```

输出的 HTML 看起来像这样:

```html
<h3 id="custom-id">一个很棒的标题</h3>
```
{{< /admonition >}}

## 2 注释

注释是和 HTML 兼容的：

```html
<!--
这是一段注释
-->
```

**不能**看到以下的注释:

<!--
这是一段注释
-->

## 3 水平线

HTML 中的 `<hr>` 标签是用来在段落元素之间创建一个 "专题间隔" 的.
使用 Markdown, 你可以用以下方式创建一个 `<hr>` 标签:

* `___`: 三个连续的下划线
* `---`: 三个连续的破折号
* `***`: 三个连续的星号

呈现的输出效果如下:

___
---
***

## 4 段落

按照纯文本的方式书写段落, 纯文本在呈现的 HTML 中将用 `<p>`/`</p>` 标签包裹.

如下段落:

```markdown
Lorem ipsum dolor sit amet, graecis denique ei vel, at duo primis mandamus. Et legere ocurreret pri,
animal tacimates complectitur ad cum. Cu eum inermis inimicus efficiendi. Labore officiis his ex,
soluta officiis concludaturque ei qui, vide sensibus vim ad.
```

输出的 HTML 看起来像这样:

```html
<p>Lorem ipsum dolor sit amet, graecis denique ei vel, at duo primis mandamus. Et legere ocurreret pri, animal tacimates complectitur ad cum. Cu eum inermis inimicus efficiendi. Labore officiis his ex, soluta officiis concludaturque ei qui, vide sensibus vim ad.</p>
```

可以使用一个空白行进行**换行**.

## 5 内联

如果你需要某个 HTML 标签 (带有一个类), 则可以简单地像这样使用:

```html
Markdown 格式的段落.

<div class="class">
    这是 <b>HTML</b>
</div>

Markdown 格式的段落.
```

## 6 强调

### 加粗

用于强调带有较粗字体的文本片段.

以下文本片段会被 **渲染为粗体**.

```markdown
**渲染为粗体**
__渲染为粗体__
```

输出的 HTML 看起来像这样:

```html
<strong>渲染为粗体</strong>
```

### 斜体

用于强调带有斜体的文本片段.

以下文本片段被 _渲染为斜体_.

```markdown
*渲染为斜体*
_渲染为斜体_
```

输出的 HTML 看起来像这样:

```html
<em>渲染为斜体</em>
```

### 删除线

按照 [[GFM]^(GitHub flavored Markdown)](https://github.github.com/gfm/) 你可以使用删除线.

```markdown
~~这段文本带有删除线.~~
```

呈现的输出效果如下:

~~这段文本带有删除线.~~

输出的 HTML 看起来像这样:

```html
<del>这段文本带有删除线.</del>
```

