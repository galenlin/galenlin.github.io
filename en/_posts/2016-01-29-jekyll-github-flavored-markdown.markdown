---
layout: post
title:  "Jekyll Github Flavored Markdown"
date:   2016-01-29 15:36:03
categories: jekyll github markdown
---

## Getting Started

Use `redcarpet` as markdown processor in `_config.xml`.

```ruby
markdown: redcarpet
highlighter: pygments
redcarpet:
  extensions: ["no_intra_emphasis", "tables", "autolink", "strikethrough", "fenced_code_blocks", "with_toc_data"]
```

Add `markdown-body` id and class for `posts` content.

```html
<article id="markdown-body" class="post-content markdown-body">
  {\{ content \}}
</article>
```

Add [github-markdown.css][gfm-css] to html header or save it as [_github-markdown.scss][gfm-scss] and import it in your `main.css`.

```css
@import
        "base",
        "layout",
        "github-markdown",
        "syntax-highlighting"
;
```

Modify the [_syntax-highlighting.sass][gfm-hl] to adjust code colors as github.

### Hover anchor and Task list

Add [gfm-hack.js][gfm-hack] to your jekyll `default.html` to enable `<h2>` ~ `<h6>` hover anchor and `- [ ]` or `- [x]` task list in github.

```html
<script type="text/javascript" src="/js/gfm-hack.js"/>
```

## Tests

### Table

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

### Task List

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

### Highlighting

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

## Reference

* https://george-hawkins.github.io/basic-gfm-jekyll/redcarpet-extensions.html

## Source

All the sources are on [here](https://github.com/galenlin/galenlin.github.io).

[gfm-css]: https://github.com/sindresorhus/github-markdown-css
[gfm-scss]: https://github.com/galenlin/galenlin.github.io/blob/master/_sass/_github-markdown.scss
[gfm-hl]: https://github.com/galenlin/galenlin.github.io/blob/master/_sass/_syntax-highlighting.scss
[gfm-hack]: https://github.com/galenlin/galenlin.github.io/blob/master/js/gfm-hack.js
