# 第1章：创建你的第一个本地仓库

## 打开终端

在 Windows 上，我们会在 Git Bash 这个工具里运行 Git 命令。

1. 在桌面上新建一个文件夹，命名为 `my-first-repo`
2. 右键点击这个文件夹
3. 选择 **"Git Bash Here"**

你会看到一个黑色窗口弹出来。这就是你的终端，接下来所有命令都在这里输入。

如果你没看到 "Git Bash Here"，说明你可能还没安装 Git。请先下载并安装 [Git for Windows](https://git-scm.com/download/win)，安装完成后重新尝试。

## 把文件夹变成仓库

在弹出的窗口中，输入以下命令：

```bash
git init
```

> **小贴士：** 输入命令时如果不确定怎么拼，可以按 **Tab** 键，终端会自动补全。比如输入 `git i` 然后按 Tab，会自动补全成 `git init`。如果按了 Tab 没反应，说明你打错了，回去检查一下。如果有多个相同开头的候选项（比如 `git push` 和 `git pull` 都以 `git pu` 开头），按一次 Tab 不会有任何反应——这时连按两次 Tab，终端会把所有候选项列出来让你选。

你会看到类似这样的输出：

```
Initialized empty Git repository in C:/Users/你的用户名/Desktop/my-first-repo/.git/
```

现在，这个普通的文件夹变成了一个 Git 仓库。

### .git 文件夹是什么？

打开 `my-first-repo` 文件夹，你会看到一个 `.git` 文件夹。

这是 Git 的"心脏"——这个项目的提交历史、分支信息等数据都存储在这里。注意，你用 `git config --global` 设置的用户名和邮箱并不在这里，而是存在你电脑的全局配置文件中。

如果删掉 `.git` 文件夹，这个项目的版本控制就不存在了，但你的文件都还在。所以不用紧张，Git 不会"控制"你的文件，它只是在旁边默默地记录。

## 告诉 Git 你是谁

Git 需要知道每次提交是谁做的。运行这两条命令：

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

这里的邮箱不需要是真实的，随便填一个就行。本地操作，没人会看到。

## 看看现在什么状态

运行这个命令：

```bash
git status
```

你会看到：

```
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

意思是：仓库是空的，还没有提交过任何内容。

现在在 `my-first-repo` 文件夹里创建一个文件 `README.md`，随便写点什么，然后再次运行：

```bash
git status
```

这次你会看到 `README.md` 出现在 "Untracked files"（未跟踪的文件）列表中。

Git 的意思是："我看到了这个新文件，但我还没开始追踪它。"

下一章，你会学习如何把文件交给 Git 保管。
