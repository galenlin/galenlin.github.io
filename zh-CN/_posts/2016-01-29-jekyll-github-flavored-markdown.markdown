---
layout: post
title:  "Jekyll仿Github风格"
date:   2016-01-29 15:36:03
categories: web
tags: [jekyll, github, markdown]
---

## 配置

在`_config.xml`中使用`redcarpet`作为markdown解析器。

```ruby
markdown: redcarpet
highlighter: pygments
redcarpet:
  extensions: ["no_intra_emphasis", "tables", "autolink", "strikethrough", "fenced_code_blocks", "with_toc_data"]
```

对`posts`博客内容所包含的标签加上`markdown-body` id 与 class。

```html
<article id="markdown-body" class="post-content markdown-body">
  {\{ content \}}
</article>
```

在html的header里加入[github-markdown.css][gfm-css]，或者如本网站使用[_github-markdown.scss][gfm-scss]并在`main.css`中导入。

```css
@import
        "base",
        "layout",
        "github-markdown",
        "syntax-highlighting"
;
```

修改[_syntax-highlighting.sass][gfm-hl]来仿照github上的代码着色。

### 段落锚点链接与任务列表

在网页的`<head>`标签中加入[gfm-hack.js][gfm-hack]，使`<h2>`到`<h6>`之间的标签支持鼠标悬停时显示锚点链接，以及支持通过`- [ ]`或`- [x]`来显示任务列表。

```html
<head>
...
<script type="text/javascript" src="/js/gfm-hack.js"/>
</head>
```

### Emoji表情

在`Gemfile`中增加安装脚本。（如果没有这个文件在根目录创建一个）

```ruby
gem 'jemojy'
```

在`_config.yml`中添加依赖。

```ruby
gems: [jemoji]
```

> 本地调试时，需要先安装：sudo gem install jemojy

## 测试

### 表格

```
| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |
```

| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |

### 任务列表

```
- [ ] a task list item
- [ ] list syntax required
- [ ] normal **formatting**, @mentions, #1234 refs
- [ ] incomplete
- [x] completed
```

- [ ] a task list item
- [ ] list syntax required
- [ ] normal **formatting**, @mentions, #1234 refs
- [ ] incomplete
- [x] completed

### 代码高亮

<pre>
```java
/**
 * Greet jekyll for the github flavored markdown
 */
class GreetGFM {
    private static final String GREET = "Hello Jekyll! Hello Github Flavored Markdown!";
    public static void main(String[] args) {
        System.out.println(GREET);
    }
}
```
</pre>

```java
/**
 * Greet jekyll for the github flavored markdown
 */
class GreetGFM {
    private static final String GREET = "Hello Jekyll! Hello Github Flavored Markdown!";
    public static void main(String[] args) {
        System.out.println(GREET);
    }
}
```

### Emoji

```
这篇文章我给32个:+1:!
```

这篇文章我给32个:+1:!

## 参考文章

* [Redcarpet extensions](https://george-hawkins.github.io/basic-gfm-jekyll/redcarpet-extensions.html)
* [Github flavored emoji](https://github.com/jekyll/jemoji)
* [Emoji cheat sheet](http://www.emoji-cheat-sheet.com)

## 源代码

所有的代码都可以在[这里](https://github.com/galenlin/galenlin.github.io)找到。

[gfm-css]: https://github.com/sindresorhus/github-markdown-css
[gfm-scss]: https://github.com/galenlin/galenlin.github.io/blob/master/_sass/_github-markdown.scss
[gfm-hl]: https://github.com/galenlin/galenlin.github.io/blob/master/_sass/_syntax-highlighting.scss
[gfm-hack]: https://github.com/galenlin/galenlin.github.io/blob/master/js/gfm-hack.js
