---
title: "hugo 的安装与使用"
keywords: ['stridedot', 'StrideDot', 'hugo install']
description: "如何安装hugo，以及如何使用hugo"
author: "StrideDot"
slug: install-hugo
date: '2022-11-09'
lastmod: '2022-11-09'
draft: false
math: false
comments: true
image: ""
resources:
- name: ""
  src: ""

tags: ["hugo"]
categories: ["hugo"]
---


Hugo 是个用于构建静态网站的快速、现代且灵活的开源静态站点生成器。
它使用 Go 语言编写，以极快的速度生成静态网页，支持简单易懂的文件结构、主题和模板。
Hugo 注重性能，使得用户能够在几秒内生成整个网站，它会将你使用 markdown 编写的内容转换成 HTML 文件。
适用于用于个人博客和企业网站。

---

# Step 1: Fork hugo

进入 [hugo](https://github.com/gohugoio/hugo) 页面，点击 `fork`，`hugo` 项目将同步到自己的 github 账户中。   

---

# Step 2: Git Clone

执行 `git clone` 命令

```shell
$ git clone https://gitclone.com/github.com/stridedot/hugo.git --depth=1
```

如果 clone 比较慢，可以在修改

`https://github.com/stridedot/hugo.git --depth=1`

为

`https://gitclone.com/github.com/stridedot/hugo.git --depth=1`

来加快下载速度

---

# Step 3: 安装依赖

进入 hugo 文件并 install

```shell
$ cd hugo
$ go install
```

---

# Step 4: 编译

```shell
$ go build -o D:/software/Hugo/bin/hugo.exe main.go
```

---

# Step 5: 加入环境变量

点击**开始**菜单，搜索“环境变量”即可看到

我们的 `hugo` 可执行文件是 `D:/software/Hugo/bin/hugo.exe` 。

---

# Step 6: 测试 hugo

```shell
$ hugo version
hugo v0.121.0-DEV windows/amd64 BuildDate=unknown
```



