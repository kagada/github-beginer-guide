# 第2章：日常操作：保存和查看

上一章，你创建了一个仓库，告诉 Git 你是谁，还创建了第一个文件。现在，让我们学习如何把文件交给 Git 保管。

## 暂存区：Git 的"购物车"

在 Git 的世界里，保存修改分两步：先把要保存的文件放进"购物车"，然后结账。

这个购物车叫做**暂存区**。为什么要多这一步？因为一次提交可能只包含一部分修改。你可以选择哪些文件放入暂存区，哪些暂时不动。

## 把文件放入暂存区

确保 `my-first-repo` 文件夹里有一个 `README.md` 文件（如果没有，现在就创建一个）。

运行：

```bash
git status
```

你会看到 `README.md` 出现在 "Untracked files" 列表中。现在，把它交给 Git：

```bash
git add README.md
```

再次运行 `git status`：

```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md
```

注意 "Changes to be committed"——Git 告诉你：这个文件已经放入暂存区，准备好被提交了。

### 一次性全部加入

如果有很多文件，不需要逐个添加。用这个命令把当前目录下所有未跟踪的文件一起加入暂存区：

```bash
git add .
```

这里的 `.` 代表"当前目录下的所有内容"。

## 创建你的第一个提交

现在，把暂存区里的内容保存为一个提交：

```bash
git commit -m "添加 README 文件"
```

你会看到类似这样的输出：

```
[main (root-commit) 1a2b3c4] 添加 README 文件
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

**一次提交产生一份快照**——Git 拍下了暂存区里所有文件在这一刻的状态，永久保存下来。

提交信息（`-m` 后面的内容）应该简短清楚地描述这次改了什么。写给自己和别人看，别敷衍。

## 继续修改，继续提交

在 `README.md` 里加一行内容，然后运行：

```bash
git status
```

这次你会看到 `README.md` 出现在 "Changes not staged for commit" 列表中。Git 的意思是："这个文件我有记录，但你的修改还没放进暂存区。"

把它加入暂存区并提交：

```bash
git add README.md
git commit -m "更新 README 内容"
```

再创建一个新文件 `notes.txt`，写点东西，然后运行：

```bash
git add notes.txt
git commit -m "添加学习笔记"
```

现在你已经有三个提交了。

## 查看提交历史

运行这个命令：

```bash
git log
```

你会看到完整的提交列表，按时间倒序排列，包含提交哈希、作者、日期和提交信息。

信息太多？试试精简版：

**注意：是 `--oneline`（一行），不是 `--online`（在线）。看清楚了再敲。**

```bash
git log --oneline
```

你会看到类似这样的输出：

```
9f8e7d6 添加学习笔记
a1b2c3d 更新 README 内容
1a2b3c4 添加 README 文件
```

简洁明了——短哈希 + 提交信息。

## 你刚刚学会了什么

- `git add <file>` — 把单个文件放入暂存区
- `git add .` — 把所有修改放入暂存区
- `git commit -m "消息"` — 创建提交，保存快照
- `git log` — 查看详细历史
- `git log --oneline` — 查看精简历史

现在你已经掌握了 Git 的核心循环：修改 → 暂存 → 提交 → 查看历史。

下一章，你会学习如何撤销和修正——因为犯错是正常的，Git 随时准备帮你挽回。
