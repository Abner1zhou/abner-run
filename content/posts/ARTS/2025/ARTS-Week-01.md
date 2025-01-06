+++
title = 'ARTS Week 01, 2025'
date = 2025-01-01T09:12:28+08:00
categories = ['ARTS']
tags = ["Linux", "Hugo"]
author=  "Abner Zhou"
draft = false
+++
## 1.Algorithm

---

## 2.Review

[openSUSE Aeon - Desktop Linux finally done right?](https://youtu.be/1K_kGbmlewo?si=PjPZroZ4flPoNN-x)

![openSUSE Aeon](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2025/01/72bdf7d1c7fedbd5e0032eafd67f08b1-202501060916898.png)

openSUSE Aeon是衍生于openSUSE tumbleweed的桌面发行版. 最大的特点是不可变，对系统核心文件进行了只读保护。详细信息可以看[ARTS-Week-52#2.Review]({{< relref "/posts/ARTS/2024/ARTS-Week-52.md" >}})


---

## 3.Tip

### 使用Hugo的短代码

Hugo提供了两种短代码来生成链接：ref和relref。

- ref短代码：用于生成绝对路径链接，适用于任何页面。
- relref短代码：用于生成相对路径链接，仅适用于同一语言的页面。

**示例**

假设你想链接到位于/content/posts/know/blog-tips.md的文章，可以在Markdown文件中这样写：

![Hugo链接](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2025/01/ccd91a04260e4b4b56760c2ba5cee4f5-202501060925314.png)

**注意事项**

使用短代码时，路径应从content目录开始，并包括文件扩展名.md。

如果目标链接不存在，Hugo在构建时会报错，这有助于发现并修正死链126。

---

## 4.Share
