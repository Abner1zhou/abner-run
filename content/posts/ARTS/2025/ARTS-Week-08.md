+++
title = 'ARTS Week 08, 2025'
date = 2025-02-22T15:49:06+08:00
categories = ['ARTS']
tags = []
author=  "Abner Zhou"
draft = false
+++
## 1.Algorithm



---

## 2.Review

[Deep Dive into LLMs like ChatGPT](https://www.youtube.com/watch?v=7xTGNNLPyMI)

视频中提到一个观点，问答模型基于很多专家的标注，模型其实实在模拟专家来回答问题。大模型很难凭空创造出知识，但是能够将专家的知识复制给任何人，也就是每个人都可以拥有一个专家库。

基础模型以及涵盖了互联网上大量的信息，再经过标注者的后训练（fine-tuning）以后，就能将这些信息整理后，输出有效的答案。

---

## 3.Tip

CICD中密钥的保存，可以通过passphrase二层加密。 `.gitlab-ci.yml` 中添加如下内容：

```bash
before_script:

- mkdir -p ~/.ssh

- echo "$SSH_PRIVATE_KEY" > ~/.ssh/id_rsa

- chmod 600 ~/.ssh/id_rsa

- eval "$(ssh-agent -s)"

- echo "$SSH_PASSPHRASE" | setsid ssh-add ~/.ssh/id_rsa

- ssh-keyscan -H host_name > ~/.ssh/known_hosts
```

---

## 4.Share

[笔记的方法]({{< ref "笔记的方法" >}})