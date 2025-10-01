# GitHub 入门

本课介绍 GitHub 的基础知识，这是一款用于托管代码并管理变更的平台。

![Intro to GitHub](../../sketchnotes/webdev101-github.png)
> 手绘笔记作者：[Tomomi Imura](https://twitter.com/girlie_mac)

## 课前测验

[课前测验](https://ff-quizzes.netlify.app)

## 介绍

在本课中，我们将学习：

- 在本地机器上跟踪你的工作
- 与他人协作完成项目
- 如何为开源软件做贡献

### 先决条件

开始之前，先检查是否已安装 Git。在终端中输入：
`git --version`

如果未安装，请先[下载 Git](https://git-scm.com/downloads)。然后在终端中设置本地 Git 个人信息：

- `git config --global user.name "your-name"`
- `git config --global user.email "your-email"`

要检查 Git 是否已配置，可输入：
`git config --list`

你还需要一个 GitHub 账号、一个代码编辑器（例如 Visual Studio Code），并打开你的终端（或命令提示符）。

访问 [github.com](https://github.com/)，如果还没有账号就创建一个；如果已有账号，请登录并完善你的个人资料。

✅ GitHub 并不是唯一的代码托管平台；还有其他选择，但 GitHub 最为知名。

### 准备工作

你需要在本地机器（笔记本或台式机）上准备一个包含代码项目的文件夹，并在 GitHub 上准备一个公共仓库，后者将作为示例用于演示如何向他人的项目贡献代码。

---

## 代码管理

假设你在本地有一个项目文件夹，想用 Git（版本控制系统）来跟踪你的进度。有人把使用 Git 比作“写给未来自己的情书”。若干天、数周或数月后再读提交信息（commit message），你就能回忆起当时做决定的原因，或者“回滚”一次修改——前提是你写了好的“提交信息”。

### 任务：创建仓库并提交代码

> 查看视频
>
> [![Git and GitHub basics video](https://img.youtube.com/vi/9R31OUPpxU4/0.jpg)](https://www.youtube.com/watch?v=9R31OUPpxU4)

1. **在 GitHub 上创建仓库**。在 GitHub.com 的仓库标签页或右上角导航栏，找到并点击 **New**（新建仓库）。

   1. 给你的仓库（文件夹）起个名字。
   1. 点击 **Create repository**（创建仓库）。

1. **进入你的工作文件夹**。在终端中切换到你想开始跟踪的文件夹（目录）。输入：

   ```bash
   cd [name of your folder]
   ```

1. **初始化 Git 仓库**。在项目根目录输入：

   ```bash
   git init
   ```

1. **查看状态**。检查仓库状态，输入：

   ```bash
   git status
   ```

   输出可能类似如下：

   ```text
   Changes not staged for commit:
   (use "git add <file>..." to update what will be committed)
   (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   file.txt
        modified:   file2.txt
   ```

   通常，`git status` 会告诉你有哪些文件已准备好被保存到仓库，或有哪些文件存在你也许想持久化的更改。

1. **将所有文件加入跟踪**。这也被称为“暂存（stage）文件/添加到暂存区”。

   ```bash
   git add .
   ```

   这里 `git add` 加上 `.` 参数表示将所有文件及其更改加入跟踪。

1. **仅添加指定文件进行跟踪**

   ```bash
   git add [file or folder name]
   ```

   当你不想一次性提交所有文件时，只把选定文件加入暂存区会很有用。

1. **取消暂存所有文件**

   ```bash
   git reset
   ```

   该命令会一次性取消暂存所有文件。

1. **取消暂存某个特定文件**

   ```bash
   git reset [file or folder name]
   ```

   当你不想把某个文件包含进下次提交时，可用此命令仅取消该文件的暂存。

1. **持久化你的工作**。此时你已把文件添加到所谓的“暂存区”，Git 会在这里跟踪你的文件。要让更改永久保存，需要“提交（commit）”这些文件。使用 `git commit` 创建一次“提交”；一次提交代表仓库历史中的一个保存点。输入以下命令创建提交：

   ```bash
   git commit -m "first commit"
   ```

   这会提交你所有的文件，并添加消息“first commit”。之后的提交信息应尽量更具描述性，以清晰表达你做了什么样的改动。

1. **将本地 Git 仓库连接到 GitHub**。本地有个 Git 仓库当然很好，但你可能希望把文件备份到远端，并邀请他人与您协作。GitHub 是一个很好的选择。我们之前已在 GitHub 创建了仓库，接下来只需把本地仓库与 GitHub 关联起来。使用 `git remote add` 命令即可：

   > 注意：运行命令前，请先打开 GitHub 仓库页面，找到仓库的 URL。在下方命令中用你的地址替换 ```https://github.com/username/repository_name.git```。

   ```bash
   git remote add origin https://github.com/username/repository_name.git
   ```

   这会创建一个名为 "origin" 的远程连接，指向你在 GitHub 上创建的仓库。

1. **把本地文件推送到 GitHub**。现在你已在本地与 GitHub 仓库之间建立了连接。用 `git push` 将提交推送到远端：

   > 注意：你的默认分支名可能不是 ```main```。

   ```bash
   git push -u origin main
   ```

   这会把你在 "main" 分支上的提交推送到 GitHub。

1. **继续提交更多更改**。之后若要继续修改并推送到 GitHub，通常使用以下三条命令：

   ```bash
   git add .
   git commit -m "type your commit message here"
   git push
   ```

   > 小贴士：你或许还想添加一个 `.gitignore` 文件，防止不希望被跟踪的文件出现在 GitHub 上——比如你在同一文件夹里保存的个人笔记，它并不适合出现在公共仓库中。你可以在此处找到 `.gitignore` 模板：[.gitignore templates](https://github.com/github/gitignore)。

#### 提交信息（Commit messages）

一个优秀的提交标题行应能补全这句话：
“如果被合并，这次提交将会 <在此填入你的标题>”。

标题请使用祈使、现在时态：用 "change" 而不是 "changed" 或 "changes"。
正文（可选）同样建议使用祈使、现在时态。正文应包含此次变更的动机，并与先前行为进行对比。记住，你在解释的是“为什么”，而不是“如何做”。

✅ 花几分钟在 GitHub 上随便逛逛。你能找到一个特别优秀的提交信息吗？能找到一个极简的吗？在你看来，提交信息里最重要、最有用的信息是什么？

### 任务：协作

把项目放到 GitHub 上的主要原因是便于与其他开发者协作。

## 与他人一起开发项目

> 查看视频
>
> [![Git and GitHub basics video](https://img.youtube.com/vi/bFCM-PC3cu8/0.jpg)](https://www.youtube.com/watch?v=bFCM-PC3cu8)

在你的仓库中，打开 `Insights > Community`，看看你的项目与推荐的社区标准相比如何。

以下内容可以帮助改进你的 GitHub 仓库：

- **Description（描述）**。是否为你的项目添加了简要描述？
- **README**。是否编写了 README？GitHub 提供了[撰写 README 的指南](https://docs.github.com/articles/about-readmes/?WT.mc_id=academic-77807-sagibbon)。
- **Contributing guideline（贡献指南）**。项目是否提供了[贡献指南](https://docs.github.com/articles/setting-guidelines-for-repository-contributors/?WT.mc_id=academic-77807-sagibbon)？
- **Code of Conduct（行为准则）**。是否有[行为准则](https://docs.github.com/articles/adding-a-code-of-conduct-to-your-project/)？
- **License（许可证）**。也许最重要的是，是否有[开源许可证](https://docs.github.com/articles/adding-a-license-to-a-repository/)？

上述资源有助于新成员快速上手。通常，新贡献者在阅读你的代码之前会先看这些内容，以判断你的项目是否值得他们投入时间。

✅ README 虽然需要花时间准备，但常被忙碌的维护者忽视。你能找到一个特别详尽的 README 示例吗？提示：可以尝试一些[帮助创建优质 README 的工具](https://www.makeareadme.com/)。

### 任务：合并代码

贡献文档可以帮助他人为项目做出贡献。文档会说明你期望的贡献类型，以及贡献流程。贡献者通常需要完成以下步骤，才能向你的 GitHub 仓库贡献代码：

1. **Fork 仓库**。你大概率希望他人先 fork 你的项目。Fork 会在他们的 GitHub 个人空间创建你的仓库副本。
1. **Clone**。随后，将仓库克隆到本地计算机。
1. **创建分支**。要求他们为自己的工作创建一个分支（branch）。
1. **聚焦单一变更**。请贡献者一次只专注于一类变更——这样你接受并合并他们工作的概率更高。设想他们同时修了一个 bug、加了一个新功能、并更新了若干测试——如果你只想采纳其中的 1-2 项，该怎么办？

✅ 想一想在哪些场景下，“分支”对于编写和发布高质量代码尤为关键？

> 注意：以身作则，也请为你自己的工作创建分支。你进行提交时，会提交到当前“检出（checked out）”的分支。使用 `git status` 查看当前分支。

下面走一遍贡献者的工作流。假设贡献者已经 fork 并 clone 了仓库，在本地已准备好一个可用的 Git 仓库：

1. **创建分支**。使用 `git branch` 创建一个用于承载改动的分支：

   ```bash
   git branch [branch-name]
   ```

1. **切换到工作分支**。使用 `git switch` 切换到该分支并更新工作目录：

   ```bash
   git switch [branch-name]
   ```

1. **开始修改**。此时可以添加你的改动。别忘了用以下命令告诉 Git：

   ```bash
   git add .
   git commit -m "my changes"
   ```

   给提交起个好名字，这对你和你所帮助的项目维护者都很重要。

1. **与 `main` 分支合并**。当你完成工作后，希望把你的改动与 `main` 分支合并。其间 `main` 可能已有更新，因此先用以下命令获取最新变更：

   ```bash
   git switch main
   git pull
   ```

   现在要确保任何冲突（Git 无法轻易合并的情况）都发生在你的工作分支上。因此运行：

   ```bash
   git switch [branch_name]
   git merge main
   ```

   这会把 `main` 上的所有变更合入你的分支，希望一切顺利即可继续。如果不顺利，VS Code 会指示 Git “困惑”的位置，你只需在受影响的文件中选择最准确的内容。

1. **把你的工作推送到 GitHub**。推送到 GitHub 包含两步：把分支推送到你的远程仓库，然后创建一个 PR（Pull Request，拉取请求）。

   ```bash
   git push --set-upstream origin [branch-name]
   ```

   上面的命令会在你的 fork 仓库中创建该分支。

1. **创建 PR**。接下来，在 GitHub 上打开你的 fork 仓库。GitHub 会提示你是否要创建新 PR，点击后进入创建界面，你可以修改标题并补充更合适的描述。随后，原始仓库的维护者会看到这个 PR——祝你好运，他们会欣然接受并合并它。恭喜，你现在是贡献者了！

1. **清理**。成功合并 PR 后进行“清理”被视为良好实践。你需要清理本地分支和在 GitHub 上推送的远程分支。先用以下命令在本地删除：

   ```bash
   git branch -d [branch-name]
   ```

   然后到 fork 仓库的 GitHub 页面上删除刚刚推送的远程分支。

`Pull request`（拉取请求）这个术语听起来有些怪，因为你实际上是要把更改“推送”到项目中。但在合并进项目的 "main" 分支前，维护者（项目所有者）或核心团队需要先审查你的更改，因此你实际上是在请求维护者做出合并与否的决策。

PR 是用来对比分支差异并进行讨论的地方，包含评审、评论、集成测试等。一个好的 PR 与好的提交信息有相同的原则。若你的工作修复了某个问题，你可以在 PR 中引用对应的 Issue：使用 `#` 加问题编号，例如 `#97`。

🤞 祝所有检查都通过，并由项目所有者合并你的更改 🤞

将当前本地工作分支与 GitHub 上对应远程分支的所有新提交同步：

`git pull`

## 如何为开源做贡献

首先，在 GitHub 上找到你感兴趣并愿意贡献的仓库（**repo**）。你需要把它的内容复制到本地。

✅ 寻找“适合新手”的仓库，一个好办法是[搜索带有标签 'good-first-issue' 的问题](https://github.blog/2020-01-22-browse-good-first-issues-to-start-contributing-to-open-source/)。

![Copy a repo locally](images/clone_repo.png)

复制代码有多种方式。常见方式是使用 HTTPS、SSH 或 GitHub CLI（命令行工具）来“克隆（clone）”仓库内容。

打开终端，按如下方式克隆仓库：
`git clone https://github.com/ProjectURL`

切换到项目目录以便开始工作：
`cd ProjectURL`

你也可以使用 [Codespaces](https://github.com/features/codespaces)（GitHub 的云端开发环境/嵌入式编辑器）或 [GitHub Desktop](https://desktop.github.com/) 打开整个项目。

最后，你也可以下载打包（zip）的代码。

### 关于 GitHub 的更多有趣功能

你可以为任意公共仓库加星（star）、订阅（watch）以及/或者“fork”。你加星的仓库可以在右上角的下拉菜单中找到。这就像给代码加书签。

项目通常有一个问题跟踪器（issue tracker），大多数位于 GitHub 的 “Issues” 标签页（除非另有说明），用于讨论与项目相关的问题；而 “Pull Requests” 标签页用于讨论与审查正在进行的更改。

项目也可能在论坛、邮件列表或 Slack、Discord、IRC 等聊天工具中进行讨论。

✅ 逛一逛你新建的 GitHub 仓库，尝试做些事，比如修改设置、给仓库添加信息、创建一个项目（例如看板）。你能做的事情很多！

---

## 🚀 挑战

与朋友结对互相查看彼此的代码。一起创建项目、fork 代码、创建分支并合并更改。

## 课后测验

[课后测验](https://ff-quizzes.netlify.app/web/en/)

## 回顾与自学

阅读更多关于[如何为开源软件做贡献](https://opensource.guide/how-to-contribute/#how-to-submit-a-contribution)的内容。

[Git 速查表](https://training.github.com/downloads/github-git-cheat-sheet/)。

多练、多用。GitHub 在 [skills.github.com](https://skills.github.com) 上提供了很棒的学习路径：

- [First Week on GitHub](https://skills.github.com/#first-week-on-github)

你也能找到更高级的课程。

## 作业

完成课程：[First Week on GitHub](https://skills.github.com/#first-week-on-github)
