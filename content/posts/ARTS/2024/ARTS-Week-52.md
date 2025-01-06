+++
title = 'ARTS Week 52, 2024'
date = 2024-12-30T09:41:55+08:00
categories = ['ARTS']
tags = ["Linux"]
author=  "Abner Zhou"
draft = false
+++
## 1.Algorithm

---

## 2.Review

[Immutable Linux Distros: Are They Right for You? Take the Test.](https://linuxblog.io/immutable-linux-distros-are-they-right-for-you-take-the-test/)

不可改变的 Linux 发行版

这一段写的就是我的经历，我刚开始使用Linux的时候，就是喜欢折腾，喜欢了解Linux的细节，喜欢配置每一个小细节。随着年龄增长、经验的增加，慢慢的开始追求稳定，开始追求“just works”。

>When I started using Linux many years ago, it was all about the challenge of making Arch Linux work and learning how Linux works. I loved tweaking and configuring every little detail.
>A few years later, I switched to Debian SID and would configure it to create a fairly stable system. But it was also a great learning opportunity. Things would break, but I enjoyed the challenge and countless hours of troubleshooting that came with running bleeding-edge software.
>As life changed, I found myself wanting to spend time elsewhere. I switched to Linux Mint and later Ubuntu and enjoyed the “just works” nature of those distros.

对于系统的更新，要综合考虑稳定性、安全性、灵活性。`Immutable Linux`设计思路在于对核心系统进行了只读保护，在使用的过程中保证不受更改，防止易操作、未授权的变更。

同时也提到了一个原子更新的概念，即在更新系统的时候，重启系统，保证所有更新生效，如果更新失败，那么系统会回滚到之前的版本，这样可以保证系统的稳定性。

### 那么快照和Btrfs是否能够实现这个功能？就不用替换操作系统那么麻烦了

作者认为快照是防止系统更新挂了以后很好的一种备份措施，但`Immutable Linux`从源头上解决了这个问题，直接防止问题出现。因为快照也会带来一些问题，比如快照失效，漏打快照，存储占用过高等。

而Btrfs的运维成本非常高，需要运维人员对这个文件系统有丰富的经验才行。直接选择`Immutable Linux`，比如`OpenSUSE`，`Fedora`直接集成了Btrfs，可以拿来即用。

---

## 3.Tip

### 在VS Code中设置环境变量

在运行Python的，通过环境变量的方式来获取密钥，为了方便测试，我就想在`.env`文件中设置环境变量，在我测试Python代码的时候能够自动读取环境变量。省的我每次都在terminal中设置环境变量。

文件结构如下

```tree
├─ .vscode/
│  ├─ launch.json
├─ .env
├─ testenv.py
```

`launch.json`里面的内容

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Current File",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "justMyCode": true,
            "envFile": "${workspaceFolder}/.env"
        }
    ]
}
```

`.env`设置环境变量

```
test_environment_variable=64
```

---

## 4.Share
