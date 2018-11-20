---
layout: post
title:  "Jekyll Github Flavored Markdown"
date:   2016-01-29 15:36:03
categories: web
tags: [jekyll, github, markdown]
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

Add [gfm-hack.js][gfm-hack] to html `<head>` to enable `<h2>` ~ `<h6>` hover anchor and `- [ ]` or `- [x]` task list in github.

```html
<head>
...
<script type="text/javascript" src="/js/gfm-hack.js"></script>
</head>
```

### Emoji

Add the install script in `Gemfile`, if not exists the file then create one.

```ruby
gem 'jemoji'
```

Add the dependency in `_config.yml`.

```ruby
gems: [jemoji]
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

### Emoji

```
I give this ariticle 32 ：+1：! (the colon here should be half-width)
```

I give this ariticle 32 :+1:!

## Reference

* [Redcarpet extensions](https://george-hawkins.github.io/basic-gfm-jekyll/redcarpet-extensions.html)
* [Github flavored emoji](https://github.com/jekyll/jemoji)
* [Emoji cheat sheet](http://www.emoji-cheat-sheet.com)

## Source

All the sources are on [here](https://github.com/galenlin/galenlin.github.io).

[gfm-css]: https://github.com/sindresorhus/github-markdown-css
[gfm-scss]: https://github.com/galenlin/galenlin.github.io/blob/master/_sass/_github-markdown.scss
[gfm-hl]: https://github.com/galenlin/galenlin.github.io/blob/master/_sass/_syntax-highlighting.scss
[gfm-hack]: https://github.com/galenlin/galenlin.github.io/blob/master/js/gfm-hack.js
