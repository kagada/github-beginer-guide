# 8. 连接到 GitHub

上一章，你理解了 Git 如何处理提交者身份，以及"Verified"标签背后的原理。现在，让我们迈出关键一步：**把你的本地仓库连接到 GitHub**。

## 注册 GitHub 账号

如果你还没有 GitHub 账号，前往 [github.com](https://github.com) 注册一个。注册过程很简单，按提示完成即可。

## 在 GitHub 上创建空仓库

点击右上角的 **+** 按钮，选择 **New repository**。

填写以下信息：
- **Repository name**：输入 `my-first-repo`（和本地仓库同名，方便理解）
- **Description**（可选）：写点描述，比如"我的第一个 GitHub 仓库"
- **Public/Private**：选择 Public（公开），这样任何人都能看到

**不要勾选** "Add a README file"、"Add .gitignore"、"Choose a license"——我们要从零开始连接已有的本地仓库。

点击 **Create repository**。你会看到一个空仓库的页面，GitHub 会给出一些命令行提示。

## 连接本地仓库到 GitHub

回到你的本地 `my-first-repo` 仓库。打开 Git Bash，先查看当前的远程配置：

```bash
git remote -v
```

如果之前没有配置过远程仓库，这条命令不会有任何输出。现在我们要把 GitHub 仓库添加为远程。

```bash
git remote add origin https://github.com/你的用户名/my-first-repo.git
```

把 `你的用户名` 替换成你实际的 GitHub 用户名。确认一下：

```bash
git remote -v
```

现在会显示：

```
origin  https://github.com/你的用户名/my-first-repo.git (fetch)
origin  https://github.com/你的用户名/my-first-repo.git (push)
```

**`origin` 只是一个别名。** 你可以叫它任何名字，但 `origin` 是约定俗成的叫法。

## 推送代码到 GitHub

现在把你的本地提交推送到 GitHub：

```bash
git push -u origin main
```

第一次推送时，Git 会弹出浏览器窗口让你登录 GitHub 并授权。这是正常的——Git 需要知道你是仓库的所有者，才有权限推送。

授权完成后，终端会显示推送进度，最终提示成功。

**`-u` 的作用**：设置上游追踪关系。之后你只需要输入 `git push`，不用再写 `origin main`。

## 验证推送结果

打开浏览器，进入你的 GitHub 仓库页面。

刷新一下——你本地的那些提交、文件（`notes.txt`、`README.md`），现在都出现在 GitHub 上了。点击 **Commits** 链接，可以看到完整的提交历史。

**你的代码已经从本地电脑上传到了云端。**

## 认证配置说明

第一次推送后，Git 会在你的系统中存储凭证。这样你后续的 `push` 和 `pull` 不用再反复登录。

Windows 上，凭证存储在 **凭据管理器** 中（搜索"Windows 凭据"即可看到）。如果将来需要切换账号或遇到认证问题，可以到这里删除或修改 GitHub 相关的凭据。

## 拉取远程更改

现在试试反向操作——从 GitHub 拉取更改。

在 GitHub 仓库页面上，点击 **Add file** → **Create new file**，创建一个名为 `hello.md` 的文件，随便写点内容，然后提交。

回到本地 Git Bash，运行：

```bash
git pull
```

终端会下载新的提交并合并。运行 `ls` 看看——`hello.md` 已经出现在本地了。

**`git pull` 获取远程最新的提交，并自动合并到当前分支。** 它相当于先 `git fetch`（下载）再 `git merge`（合并）。

## 你刚刚理解了什么

- GitHub 账号是你的云端身份
- 在 GitHub 上创建空仓库后，用 `git remote add` 连接本地
- `git push -u origin main` 第一次推送并设置上游追踪
- `git pull` 从远程获取最新更改
- 认证凭证由系统安全存储，不用每次输入
- 命令和本地裸仓库操作完全一致，只是地址换成了 URL

下一章：[9. 在 GitHub 上协作](./9-在%20GitHub%20上协作.md)
