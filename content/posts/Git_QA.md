+++
title = 'Git 常见问题'
date = 2024-06-05
draft = true
categories = ["工具教材"]
tags = ["Git", "VCS"]

+++

## Git提交到仓库以后，如何撤销或修改

### 撤销提交

#### 1. 通过 `revert` 撤销

`git revert` 会创建一个新的提交，撤销之前的更改，而不会修改提交历史。

```bash
# 撤销最近的一个提交
git revert <commit-hash>
```

#### 2. 通过 `reset` 撤销

如果你想直接删除已经推送的提交，可以使用 `git reset`。

**但需要注意，这种方法会修改提交历史，对其他协作者可能会造成影响。**

```bash
# 回退到某个提交，保留修改
git reset --soft <commit-hash>

# 回退到某个提交，不保留修改
git reset --hard <commit-hash>

# 强制推送更改到远程仓库
git push --force

```

### 修改提交

#### 1. 修改最后一次提交

你可以使用 `--amend` 选项来修改最近一次的提交信息。

```bash
# 修改最近一次提交的提交信息
git commit --amend

# 修改后，强制推送到远程仓库
git push --force
```

#### 2. 修改特定提交

如果你需要修改历史中的某个提交，可以使用 `git rebase` 交互式模式。

```bash
# 交互式变基，进入编辑模式
git rebase -i <commit-hash>^

# 在编辑器中将目标提交的 `pick` 改为 `edit` 或 `e`

# 修改提交内容
git commit --amend

# 继续变基
git rebase --continue

# 强制推送更改到远程仓库
git push --force
```

## 不小心提交了一个无关文件怎么办？

比如不小心把密码文件、log文件、某一个大文件提交到了仓库里，如何删除？

```bash
git-filter-repo --force --invert-paths --path PATH-TO-FILE
```
