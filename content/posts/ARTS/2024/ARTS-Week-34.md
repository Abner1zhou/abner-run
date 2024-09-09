+++
title = 'ARTS Week 34'
date = 2024-08-23T09:09:52+08:00
categories = ['ARTS']
tags = ["Linux"]
author=  "Abner Zhou"
draft = false

+++
## 1.Algorithm

---

## 2.Review

### [O(zero)](https://koliber.com/articles/o-zero)

我们常会使用大O表示法来衡量一个算法的运算效率，比如O(n^2)就是运算成本较高的，O(n)相对线性一点，O(1)表示极高的效率

![O(zero) reigns supreme](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2024/08/3c68287595a86295038ddb59f0d1cf70-o-zero.webp)

但是该作者认为我们应该追求O(Zero)   O(0)。其实这不是一种代码算法，我们应该减少工作中的一些无用功，直达目的，这就是O(Zero)的中心思想。 To be a 10x engineer， 有时，决定一件事根本不需要做，比做一件无用的事效率高 100 倍。

### [Tacit Knowledge is Dangerous](https://er4hn.info/blog/2023.08.26-tacit-knowledge-dangerous/)

> [https://news.ycombinator.com/item?id=38614195](https://news.ycombinator.com/item?id=38614195)

隐形知识是危险的，隐性知识又称为"部落知识"，指的是有些知识没有文档，只掌握在团队成员的头脑里面。

如果你想掌握这些知识，只有去询问团队成员（前提是你知道这些知识由谁掌握）。

![Relative time scales for learning](https://aiit-backup.oss-cn-shanghai.aliyuncs.com/images/2024/08/0c9e4b8906c23cf10b1dc464440a6cc0-graph_relative_time.png)

隐形知识的优点是，省去了文档成本，而且询问相关成员比自己阅读文档更快，当然前提是那位成员能够快速响应。

隐形知识的缺点是，一旦团队扩大规模，它就会失败。对于掌握知识的团队成员来说，回答问题所占用的时间是一个拖累，影响了生产力，也拖慢了团队的开发速度。

另一方面，随着团队规模的扩大和知识变得更加分散，你自己阅读文档和观看视频讲座，会比向他人寻求帮助更快速和方便。

所以，团队越是大，就越要避免"隐形知识"，所有知识尽量文档化，让团队成员能够方便地查阅。

---

## 3.Tip

如何在Linux中使用tar压缩文件，通常可以使用这样的命令

```shell
tar -czvf logs_archive.tar.gz *
```

解读各字母的含义

- `-c` 表示创建一个压缩包
- `-z` 使用`gzip`算法进行压缩
- `-v` 显示压缩的具体信息、文件列表
- `-f` 指定压缩包的存放位置以及命名，通常以`.tar.gz`结尾

---

## 4.Share
