# 第6章：谁提交的？——身份验证实验

上一章，你理解了仓库之间如何传递代码。现在，让我们思考一个基本问题：**Git 怎么知道一次提交是谁做的？**

## 提交者身份是什么

回到你的 `my-first-repo` 仓库，运行：

```bash
git log
```

终端会进入浏览模式。用 **↑↓** 键滚动查看，按 **q** 退出。

你会看到每个提交都包含：

```
commit 1a2b3c4d5e6f...
Author: 你的名字 <你的邮箱>
Date:   Mon Jan 15 10:30:00 2024 +0800

    添加 README 文件
```

**提交者身份就是你在第1章用 `git config` 设置的用户名和邮箱。** Git 每次提交时，会把这两个信息写入提交记录中。

## 试试看：换个身份提交

Git 的配置可以覆盖。在本地仓库中，你可以为当前项目设置不同的身份：

```bash
git config user.name "另一个人"
git config user.email "another@example.com"
```

注意这里没有 `--global`——这只会影响当前仓库，不会改变你的全局配置。

确认一下设置是否生效：

```bash
git config user.name
git config user.email
```

现在修改 `notes.txt`，添加一行内容，然后提交：

```bash
git add notes.txt
git commit -m "用另一个身份提交"
```

运行 `git log` 看看：

```
commit 9f8e7d6c5b4a...
Author: 另一个人 <another@example.com>
Date:   Mon Jan 15 11:00:00 2024 +0800

    用另一个身份提交

commit 1a2b3c4d5e6f...
Author: 你的名字 <你的邮箱>
Date:   Mon Jan 15 10:30:00 2024 +0800

    添加 README 文件
```

**同一个仓库中，不同的提交可以有不同的作者身份。** Git 只是相信你提供的信息，它不会验证这个邮箱是不是真的是你的。

## 这意味着什么

这引出一个问题：**任何人都可以冒充别人的身份提交代码。**

举个例子：你用 GitHub 账号 `user123` 登录并推送代码，但你的提交记录里写的是 `Linus Torvalds <torvalds@linux.com>`。GitHub 会接受这次推送吗？**会。** 因为 GitHub 只关心你有没有推送权限，不关心提交记录里的作者是谁。

这就像寄快递——快递公司只确认你付了运费（登录验证），但不会查你写的寄件人名字是不是真的。

所以问题就来了：**GitHub 上那些提交的作者，你凭什么相信？**

## Git 如何防止冒名

Git 提供了一个解决方案：**GPG 签名**。

GPG（GNU Privacy Guard）是一种加密技术，基于**公钥和私钥**这一对密钥工作：

- **私钥**：只有你自己持有，绝对不能泄露
- **公钥**：可以公开给任何人

它们的关系是：**公钥加密的内容，只有私钥能解密；反过来，私钥加密的内容，也只有公钥能解密。**

在 GPG 签名中，你用私钥对提交签名，别人用你的公钥验证——验证通过就证明提交确实是你做的。配置过程相对复杂，知道它的存在就够了。

## GitHub 的"Verified"标签

在 GitHub 上看到过提交旁边的绿色"Verified"标签吗？这就是 GPG 签名的效果。

前面说过，GitHub 只保证提交是通过某个账号推送的，不验证提交记录里的作者是谁。但**Verified 标签**意味着更进一步——GitHub 用 GPG 验证了提交者的身份，确认这个提交确实是提交记录里的那个人做的。

**但记住：没有 Verified 标签不代表提交是假的。** 大多数开发者没有配置 GPG 签名，GitHub 仍然能保证这些提交是通过合法的 GitHub 账号推送的，只是没有额外验证提交者的本地身份而已。

## 你刚刚理解了什么

- Git 的提交者身份来自 `git config` 设置的用户名和邮箱
- 本地可以随意切换身份，Git 不会验证
- GPG 签名是防止冒名的技术方案
- GitHub 的"Verified"标签表示提交经过了 GPG 验证

实验完后，如果想恢复全局配置的身份：

```bash
git config --unset user.name
git config --unset user.email
```

`--unset` 会删掉当前仓库的本地配置，Git 自动回退到使用 `--global` 设置的全局用户名和邮箱。

下一章，你会把本地仓库连接到 GitHub，迈出从本地到云端的第一步。