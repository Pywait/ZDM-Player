# Git 常用命令速查手册


## 📐 核心概念：Git 的三个“仓库”

在使用命令之前，先理解Git的三个核心区域，这能帮你理解每条命令在操作什么：

| 区域 | 含义 | 对应命令 |
| :--- | :--- | :--- |
| **工作区 (Working Directory)** | 你电脑上能直接看到的文件夹，你在这里修改文件 | `git status` 查看状态 |
| **暂存区 (Staging Area)** | 一个临时存放区，你决定哪些修改要纳入下一次提交 | `git add` 把修改放入暂存区 |
| **本地仓库 (Local Repository)** | 存放所有提交历史的数据库，在你的 `.git` 文件夹里 | `git commit` 把暂存区内容永久保存 |

简单的工作流就是：**在工作区修改 → `git add` 到暂存区 → `git commit` 提交到本地仓库 → `git push` 推送到远程仓库。**


## 一、配置相关

| 操作 | 命令 |
| :--- | :--- |
| 设置全局用户名 | `git config --global user.name "你的用户名"` |
| 设置全局邮箱 | `git config --global user.email "你的邮箱"` |
| 查看所有配置 | `git config --list` |
| 查看全局配置 | `git config --global --list` |
| 查看当前仓库配置 | `git config --local --list` |
| 查看某一项配置 | `git config xx` |


## 二、新建与克隆

| 操作 | 命令 |
| :--- | :--- |
| 在当前文件夹初始化一个新仓库 | `git init` |
| 从远程仓库克隆项目到本地 | `git clone <远程仓库地址>` |
| 克隆到指定文件夹 | `git clone <远程地址> <文件夹名>` |

> **注意**：`git clone` 自带初始化功能，不需要先执行 `git init`。


## 三、日常操作（核心循环）

| 操作 | 命令 | 说明 |
| :--- | :--- | :--- |
| 查看当前状态 | `git status` | 查看哪些文件被修改、哪些待提交 |
| 添加单个文件到暂存区 | `git add <文件名>` | |
| 添加所有改动到暂存区 | `git add .` | 包括新增文件 |
| 添加所有已追踪文件的改动 | `git add -u` | 不包括新增文件 |
| 提交暂存区内容到本地仓库 | `git commit -m "提交信息"` | |
| 提交所有已追踪的改动（跳过 add） | `git commit -a -m "提交信息"` | 只对已追踪文件生效 |
| 拉取远程更新并合并 | `git pull origin main` | |
| 推送到远程仓库 | `git push origin main` | |
| 第一次推送并建立关联 | `git push -u origin main` | 之后可直接用 `git push` |

> **标准工作流**：`git status` → `git add .` → `git commit -m "xxx"` → `git pull` → `git push`


## 四、分支操作

| 操作 | 命令 |
| :--- | :--- |
| 查看所有本地分支 | `git branch` |
| 查看所有远程分支 | `git branch -r` |
| 查看所有分支（含远程） | `git branch -a` |
| 创建新分支 | `git branch <分支名>` |
| 切换到指定分支 | `git checkout <分支名>` 或 `git switch <分支名>` |
| 创建并切换到新分支 | `git checkout -b <分支名>` 或 `git switch -c <分支名>` |
| 重命名当前分支 | `git branch -m <新分支名>` |
| 删除本地分支 | `git branch -d <分支名>` |
| 强制删除本地分支（未合并时） | `git branch -D <分支名>` |
| 合并指定分支到当前分支 | `git merge <分支名>` |


## 五、查看历史与对比

| 操作 | 命令 |
| :--- | :--- |
| 查看提交历史 | `git log` |
| 查看简洁版历史（一行一条） | `git log --oneline` |
| 查看图形化分支历史 | `git log --graph` |
| 查看工作区与暂存区的差异 | `git diff` |
| 查看暂存区与本地仓库的差异 | `git diff --staged` |
| 查看两个提交之间的差异 | `git diff <commit1> <commit2>` |


## 六、撤销与回退

| 操作 | 命令 | 说明 |
| :--- | :--- | :--- |
| 放弃工作区的修改（未 add） | `git checkout -- <文件名>` | 恢复到上一次提交的状态 |
| 把文件从暂存区移回工作区 | `git reset HEAD <文件名>` | 改动保留 |
| 撤销最近一次提交，改动保留在暂存区 | `git reset --soft HEAD~1` | |
| 撤销最近一次提交，改动保留在工作区 | `git reset --mixed HEAD~1` | 默认行为 |
| 撤销最近一次提交，丢弃所有改动 | `git reset --hard HEAD~1` | ⚠️ 危险操作，不可恢复 |
| 查看所有历史操作记录 | `git reflog` | 可用于找回丢失的提交 |


## 七、远程仓库管理

| 操作 | 命令 |
| :--- | :--- |
| 查看关联的远程仓库 | `git remote -v` |
| 添加远程仓库关联 | `git remote add origin <远程地址>` |
| 修改远程仓库地址 | `git remote set-url origin <新地址>` |
| 删除远程仓库关联 | `git remote remove origin` |


## 八、常见报错与解决方案

| 报错信息 | 原因 | 解决方案 |
| :--- | :--- | :--- |
| `fatal: not a git repository` | 当前文件夹不是 Git 仓库 | 检查是否在正确的目录，或执行 `git init` |
| `error: failed to push` | 远程有新提交，本地没有 | 先 `git pull` 再 `git push` |
| `CONFLICT (content)` | 同一文件双方都改了 | 手动编辑冲突文件，然后 `git add` + `git commit` |
| `rejected: non-fast-forward` | 本地分支落后于远程 | `git pull --rebase` 再 `git push` |
| `Untracked files` | 新增文件未加入版本管理 | `git add <文件名>` |
| `fatal: destination path already exists` | clone 目标文件夹已存在 | 删除该文件夹，或 clone 到其他位置 |
| `fatal: refusing to merge unrelated histories` | 两个仓库没有共同的提交历史 | `git pull origin main --allow-unrelated-histories` |


## 九、一句话速记

> **配置一次 → clone 下来 → status 看状态 → add 加改动 → commit 拍快照 → pull 同步远程 → push 推上去**

核心命令只有五个：`status`、`add`、`commit`、`pull`、`push`，覆盖 90% 的日常操作。