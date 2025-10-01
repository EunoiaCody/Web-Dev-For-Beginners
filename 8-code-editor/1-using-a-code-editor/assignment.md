# 使用 vscode.dev 创建简历网站

_如果招聘人员向你索要简历，而你发给他们一个 URL，那该有多酷啊？_ 😎

<!----
TODO: add an optional image
![使用代码编辑器](../../sketchnotes/webdev101-vscode-dev.png)
> 手绘笔记作者 [Author name](https://example.com)
---->

<!---
## 课前测验
[课前测验](https://ff-quizzes.netlify.app/web/quiz/3)
---->

## 目标

完成这个作业后，你将学会如何：

- 创建一个网站来展示你的简历

### 先决条件

1. 一个 GitHub 账户。导航到 [GitHub](https://github.com/) 并创建账户（如果你还没有的话）。

## 步骤

**步骤 1：** 创建一个新的 GitHub 仓库并给它命名为 `my-resume`

**步骤 2** 在你的仓库中创建一个 `index.html` 文件。我们将在 github.com 上至少添加一个文件，因为你无法在 vscode.dev 上打开空仓库

点击 `creating a new file` 链接，输入名称 `index.html` 并选择 `Commit new file` 按钮

![在 github.com 上创建新文件](../images/new-file-github.com.png)

**步骤 3：** 打开 [VSCode.dev](https://vscode.dev) 并选择 `Open Remote Repository` 按钮

复制你刚为简历网站创建的仓库的 URL 并粘贴到输入框中：

_将 `your-username` 替换为你的 github 用户名_

```
https://github.com/your-username/my-resume
```

✅ 如果成功，你将看到你的项目和 index.html 文件在浏览器的文本编辑器中打开。

![创建新文件](../images/project-on-vscode.dev.png)

**步骤 4：** 打开 `index.html` 文件，将下面的代码粘贴到你的代码区域并保存

<details>
    <summary><b>负责简历网站内容的 HTML 代码。</b></summary>
    
        <html>

            <head>
                <link href="style.css" rel="stylesheet">
                <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
                <title>你的名字写在这里！</title>
            </head>
            <body>
                <header id="header">
                    <!-- 带有你的姓名和职位的简历标题 -->
                    <h1>你的名字写在这里！</h1>
                    <hr>
                    你的职位！
                    <hr>
                </header>
                <main>
                    <article id="mainLeft">
                        <section>
                            <h2>联系方式</h2>
                            <!-- 包括社交媒体的联系信息 -->
                            <p>
                                <i class="fa fa-envelope" aria-hidden="true"></i>
                                <a href="mailto:username@domain.top-level domain">在这里写你的邮箱</a>
                            </p>
                            <p>
                                <i class="fab fa-github" aria-hidden="true"></i>
                                <a href="github.com/yourGitHubUsername">在这里写你的用户名！</a>
                            </p>
                            <p>
                                <i class="fab fa-linkedin" aria-hidden="true"></i>
                                <a href="linkedin.com/yourLinkedInUsername">在这里写你的用户名！</a>
                            </p>
                        </section>
                        <section>
                            <h2>技能</h2>
                            <!-- 你的技能 -->
                            <ul>
                                <li>技能 1！</li>
                                <li>技能 2！</li>
                                <li>技能 3！</li>
                                <li>技能 4！</li>
                            </ul>
                        </section>
                        <section>
                            <h2>教育背景</h2>
                            <!-- 你的教育经历 -->
                            <h3>在这里写你的课程！</h3>
                            <p>
                                在这里写你的学校！
                            </p>
                            <p>
                                开始 - 结束日期
                            </p>
                        </section>            
                    </article>
                    <article id="mainRight">
                        <section>
                            <h2>关于</h2>
                            <!-- 关于你 -->
                            <p>写一段关于自己的简介！</p>
                        </section>
                        <section>
                            <h2>工作经验</h2>
                            <!-- 你的工作经验 -->
                            <h3>职位名称</h3>
                            <p>
                                组织名称 | 开始月份 – 结束月份
                            </p>
                            <ul>
                                    <li>任务 1 - 写你做了什么！</li>
                                    <li>任务 2 - 写你做了什么！</li>
                                    <li>写你贡献的结果/影响</li>
                                    
                            </ul>
                            <h3>职位名称 2</h3>
                            <p>
                                组织名称 | 开始月份 – 结束月份
                            </p>
                            <ul>
                                    <li>任务 1 - 写你做了什么！</li>
                                    <li>任务 2 - 写你做了什么！</li>
                                    <li>写你贡献的结果/影响</li>
                                    
                            </ul>
                        </section>
                    </article>
                </main>
            </body>
        </html>
</details>

添加你的简历详情来替换 HTML 代码中的_占位符文本_

**步骤 5：** 将鼠标悬停在 My-Resume 文件夹上，点击 `New File ...` 图标并在你的项目中创建 2 个新文件：`style.css` 和 `codeswing.json` 文件

**步骤 6：** 打开 `style.css` 文件，粘贴下面的代码并保存

 <details>
        <summary><b>用于格式化网站布局的 CSS 代码。</b></summary>
            
            body {
                font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
                font-size: 16px;
                max-width: 960px;
                margin: auto;
            }
            h1 {
                font-size: 3em;
                letter-spacing: .6em;
                padding-top: 1em;
                padding-bottom: 1em;
            }

            h2 {
                font-size: 1.5em;
                padding-bottom: 1em;
            }

            h3 {
                font-size: 1em;
                padding-bottom: 1em;
            }
            main { 
                display: grid;
                grid-template-columns: 40% 60%;
                margin-top: 3em;
            }
            header {
                text-align: center;
                margin: auto 2em;
            }

            section {
                margin: auto 1em 4em 2em;
            }

            i {
                margin-right: .5em;
            }

            p {
                margin: .2em auto
            }

            hr {
                border: none;
                background-color: lightgray;
                height: 1px;
            }

            h1, h2, h3 {
                font-weight: 100;
                margin-bottom: 0;
            }
            #mainLeft {
                border-right: 1px solid lightgray;
            }
            
</details>

**步骤 6：** 打开 `codeswing.json` 文件，粘贴下面的代码并保存

    {
    "scripts": [],
    "styles": []
    }

**步骤 7：** 安装 `Codeswing extension` 来在代码区域可视化简历网站。

点击活动栏上的_`扩展`_图标并输入 Codeswing。要么点击扩展活动栏上的_蓝色安装按钮_来安装，要么使用在你选择扩展以加载其他信息时代码区域出现的安装按钮。安装扩展后立即观察你的代码区域，看看对项目的更改 😃

![安装扩展](../images/install-extension.gif)

安装扩展后你的屏幕上将看到这个。

![Codeswing 扩展的实际效果](../images/after-codeswing-extension-pb.png)

如果你对所做的更改满意，将鼠标悬停在 `Changes` 文件夹上并点击 `+` 按钮来暂存更改。

输入一个提交消息（_对你对项目所做更改的描述_）并通过点击 `检查` 来提交你的更改。完成项目工作后，选择左上角的汉堡菜单图标返回 GitHub 上的仓库。

恭喜 🎉 你刚刚使用 vscode.dev 通过几个步骤创建了你的简历网站。

## 🚀 挑战

打开一个你有权限进行更改的远程仓库并更新一些文件。接下来，尝试使用你的更改创建一个新分支并进行 Pull Request。

<!----
## 课后测验
[课后测验](https://ff-quizzes.netlify.app/web/quiz/4)
---->

## 复习与自学

阅读更多关于 [VSCode.dev](https://code.visualstudio.com/docs/editor/vscode-web?WT.mc_id=academic-0000-alfredodeza) 及其其他功能的信息。
