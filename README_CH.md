# commit 信息指南

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)


这是一份理解 commit 信息的重要性以及如何写好 commit 信息的指南。


它会帮助你学习什么是 commit，为什么一个好的commit信息是重要的，以及计划（重）写一个 commit 记录的最好实践和技巧。

## 其他语言版本

- [English](README.md)
- [Português](README_pt-BR.md)
- [Deutsch](README_de-DE.md)
- [中文简体](README_CH.md)

## 什么是 commit

简单来说，commit 是写在你本地仓库里的，对于本地文件的一个 _快照_。与一些人的想法相反，[git 不仅存储着文件之间的差异，它同样存储着所有文件的所有版本](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences)。对于在一次提交中并未做任何修改的文件来说，git 只是存储了指向上一个版本相同文件的链接。

下面的图片展示了 git 如何随时间存储数据，每一个 "Version" 是一次 commit.

![](https://i.stack.imgur.com/AQ5TG.png)

## 为什么 commit 信息如此重要？

- 加快和精简代码审查
- 帮助理解文件变化
- 解释并不能只用代码解释的缘由
- 帮助未来的维护者理解为什么以及如何发生这些变化，使故障排除和调试更简单

为了更好理解上述结果，我们在下面章节使用一些良好实践和标准的描述。

## 良好实践

这里是从我个人经历，网上的文章以及其他一些指导中收集的实践。如果你有其他更好的（或者不认同的），请随时开一个 Pull Request 提供帮助。

### 使用命令式语句

```
# Good
Use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend
```

_为什么使用命令语句_

一个 commit 信息描述了所引用的改变时实际上**做的**，它的成效，而不是做过什么。

[这篇来自 Chris Beams 的好文章](https://chris.beams.io/posts/git-commit/)中提供了帮我写出更好的命令式提交信息的简单句式：

```
If applied, this commit will <commit message>
```

例如：

```
# Good
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### 第一个字母大写

```
# Good
Add `use` method to Credit model
```

```
# Bad
add `use` method to Credit model
```

第一个字母使用大写形式的原因是跟随大写字母开始一个句子的语法规则。

这个实践的使用可能因为人和人，团队以及团队，甚至语言和语言之间的差异而不同（译者：很明显中文没有大写之说），大写与否，坚持一个标准并同意使用是最重要的。

### 尝试在不用看源码的情况下传达变更做了什么


```
# Good
Add `use` method to Credit model
```

```
# Bad
Add `use` method
```

```
# Good
Increase left padding between textbox and layout frame
```

```
# Bad
Adjust css
```

这在很多场景很有用（例如，好几次 commit，多个改变和重构），可以帮助审查者理解提交者所思考的。

### 在信息主体解释“为什么”，“针对什么”，“如何”以及附加细节

```
# Good
Fix method name of InventoryBackend child classes

Classes derived from InventoryBackend were not
respecting the base class interface.

It worked because the cart was calling the backend implementation
incorrectly.
```

```
# Good
Serialize and deserialize credits to json in Cart

Convert the Credit instances to dict for two main reasons:

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
  - Dict and built-in types are pickleable by default
```

```
# Good
Add `use` method to Credit

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

提交信息的主题和正文使用空行分隔。其他的空行会被视为信息正文的一部分。

Characters like `-`, `*` and \` are elements that improve readability.
像 `-`,`*`和`\`等字符是提高可读性的元素。

### 避免使用通用信息或者没有上下文的信息

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### 限制每行字符数

标题最大50个字符，正文72个字符是[推荐的标准](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)。

### 保持语言一致性

对于项目所有者：选择一门语言并使用它写所有的commit信息。理想情况下，它应该和代码注释以及默认翻译区域（对于本地项目）等等一致。

对于贡献者来说：使用和提交历史相同的语言写下你的提交信息。

```
# Good
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# Good (Portuguese example)
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# Bad (mixes English and Portuguese)
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### 模板

这里是一个编写模板，最初出现在由 [Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) 在 [_Pro Git Book](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project)一书中编写。 

```
Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequences of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
```

## Rebase vs. Merge

This section is a **TL;DR** of Atlassian's excellent tutorial, ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).
这个部分来自 Atlassian 的优秀教程["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** Applies your branch commits, one by one, upon the base branch, generating a new tree.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**TL;DR:** Creates a new commit, called (appropriately) a _merge commit_, with the differences between the two branches.

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### Why do some people prefer to rebase over merge?

I particularly prefer to rebase over merge. The reasons include:

* It generates a "clean" history, without unnecessary merge commits
* _What you see is what you get_, i.e., in a code review all changes come from a specific and entitled commit, avoiding changes hidden in merge commits
* More merges are resolved by the committer, and every merge change is in a commit with a proper message
    * It's unusual to dig in and review merge commits, so avoiding them ensures all changes have a commit where they belong

### When to squash

"Squashing" is the process of taking a series of commits and condensing them into a single commit.

It's useful in several situations, e.g.:

- Reducing commits with little or no context (typo corrections, formatting, forgotten stuff)
- Joining separate changes that make more sense when applied together
- Rewriting _work in progress_ commits

### When to avoid rebase or squash?

Avoid rebase and squash in public commits or in shared branches where multiple people work on.
Rebase and squash rewrite history and overwrite existing commits, doing it on commits that are on shared branches (i.e., commits pushed to a remote repository or that comes from others branches) can cause confusion and people may lose their changes (both locally and remotely) because of divergent trees and conflicts.

## Useful git commands

### rebase -i

Use it to squash commits, edit messages, rewrite/delete/reorder commits, etc.

```
pick 002a7cc Improve description and update document title
pick 897f66d Add contributing section
pick e9549cf Add a section of Available languages
pick ec003aa Add "What is a commit" section"
pick bbe5361 Add source referencing as a point of help wanted
pick b71115e Add a section explaining the importance of commit messages
pick 669bf2b Add "Good practices" section
pick d8340d7 Add capitalization of first letter practice
pick 925f42b Add a practice to encourage good descriptions
pick be05171 Add a section showing good uses of message body
pick d115bb8 Add generic messages and column limit sections
pick 1693840 Add a section about language consistency
pick 80c5f47 Add commit message template
pick 8827962 Fix triple "m" typo
pick 9b81c72 Add "Rebase vs Merge" section

# Rebase 9e6dc75..9b81c72 onto 9e6dc75 (15 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into the previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

#### fixup

Use it to clean up commits easily and without needing a more complex rebase.
[This article](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html) has very good examples of how and when to do it.

### cherry-pick

It is very useful to apply that commit you made on the wrong branch, without the need to code it again.

Example:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

Let's say we have the following diff:

```diff
diff --git a/README.md b/README.md
index 7b45277..6b1993c 100644
--- a/README.md
+++ b/README.md
@@ -186,10 +186,13 @@ bebebe Corrige nome de método na classe InventoryBackend
 ``
 # Bad (mixes English and Portuguese)
 ababab Usa o InventoryBackendPool para recuperar o backend de estoque
-efefef Add `use` method to Credit model
 cdcdcd Agora vai
 ``

+### Template
+
+This is a template, [written originally by Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), which appears in the [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).
+
 ## Contributing

 Any kind of help would be appreciated. Example of topics that you can help me with:
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

We can use `git add -p` to add only the patches we want to, without the need to change the code that is already written.
It's useful to split a big change into smaller commits or to reset/checkout specific changes.

```
Stage this hunk [y,n,q,a,d,/,j,J,g,s,e,?]? s
Split into 2 hunks.
```

#### hunk 1

```diff
@@ -186,7 +186,6 @@
 ``
 # Bad (mixes English and Portuguese)
 ababab Usa o InventoryBackendPool para recuperar o backend de estoque
-efefef Add `use` method to Credit model
 cdcdcd Agora vai
 ``

Stage this hunk [y,n,q,a,d,/,j,J,g,e,?]?
```

#### hunk 2

```diff
@@ -190,6 +189,10 @@
 ``
 cdcdcd Agora vai
 ``

+### Template
+
+This is a template, [written originally by Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), which appears in the [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).
+
 ## Contributing

 Any kind of help would be appreciated. Example of topics that you can help me with:
Stage this hunk [y,n,q,a,d,/,K,j,J,g,e,?]?

```

#### hunk 3

```diff
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

## Other interesting stuff

https://whatthecommit.com/

## Like it?

[Say thanks!](https://saythanks.io/to/RomuloOliveira)

## Contributing

Any kind of help would be appreciated. Example of topics that you can help me with:

- Grammar and spelling corrections
- Translation to other languages
- Improvement of source referencing
- Incorrect or incomplete information

## Inspirations, sources and further reading

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
