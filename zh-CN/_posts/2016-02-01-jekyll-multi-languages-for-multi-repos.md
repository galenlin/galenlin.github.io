---
layout: post
title:  "Gitcafe中文博客镜像"
date:   2016-02-01 14:03:03
categories: jekyll
---

开始准备在git上用Jekyll写博客时，有两件纠结的事情你可能会碰到：

* 放在哪，Github or Gitcafe?
  * github历史悠久，更具国际性
  * gitcafe在国内访问速度快

* 用什么语言写， English or Native?
  * 用英语，能加强练习，对学习有帮助
  * 用中文，方便国内开发者阅读，可以更好的分享与传播

那么，在github上用英文，在gitcafe上用中文，可不可以呢？

答案是肯定的。

## 目录结构

```
[yourname.github.io]
  |-- _config.yml
  |-- _config.zh-CN.yml
  |-- en
  |    |-- _posts
  |    |     +-- 2016-02-01-**.md
  |    +-- about.md
  +-- zh-CN
       |-- _posts
       |     +-- 2016-02-01-**.md
       +-- about.md
```

## 原理

使用`exclude`配置，对英文版本，排除`zh-CN`目录；对中文版本，排除`en`目录

## 配置

_config.yml

```ruby
exclude: ["zh-CN"]
```

_config.zh-CN.yml

```ruby
exclude: ["en"]
```

## 上传github

与普通无异， `git commit ...`

## 镜像gitcafe

在clone的`yourname.github.io`目录下，调用命令：

```
$ jekyll build --config _config.yml,_config.zh-CN.yml -d [你的gitcafe的clone目录]
```

> 注意--config后面逗号隔开的部分，往后的文件会覆盖与之前文件重名部分的配置，也就是exclude被重写成了["en"]。

在gitcafe目录下，调用命令：

```
$ git add .
$ git commit . -m "Regenerate from github"
```

## 待实现

- [ ] 自动化






