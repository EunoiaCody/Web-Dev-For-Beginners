# 编程语言与开发工具简介

本课程涵盖了编程语言的基础知识。这里涵盖的主题适用于当今大多数现代编程语言。在“开发工具”部分，你将了解到作为一名开发者会用到的实用软件。

![编程简介](../../sketchnotes/webdev101-programming.png)
> 手绘笔记作者 [Tomomi Imura](https://twitter.com/girlie_mac)

## 课前测验

[课前测验](https://forms.office.com/r/dru4TE0U9n?origin=lprLink)

## 简介

在本课程中，我们将涵盖：

- 什么是编程？
- 编程语言的类型
- 程序的基本元素
- 专业开发人员的实用软件和工具

> 你可以在 [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101/introduction-programming/?WT.mc_id=academic-77807-sagibbon) 上学习本课程！

## 什么是编程？

编程（也称为编码）是为计算机或移动设备等设备编写指令的过程。我们使用编程语言编写这些指令，然后由设备解释。这些指令集可能有不同的名称，但*程序*、*计算机程序*、*应用程序 (app)* 和 *可执行文件* 是一些流行的名称。

*程序*可以是任何用代码编写的东西；网站、游戏和手机应用都是程序。虽然不写代码也可以创建程序，但其底层逻辑是由设备解释的，而该逻辑很可能是用代码编写的。一个正在*运行*或*执行*代码的程序，就是在执行指令。你正在阅读本课程的设备，就在运行一个程序，将内容打印到你的屏幕上。

✅ 做一点研究：谁被认为是世界上第一位计算机程序员？

## 编程语言

编程语言使开发人员能够为设备编写指令。设备只能理解二进制（1 和 0），而对于*大多数*开发人员来说，这不是一种非常有效的沟通方式。编程语言是人类与计算机之间沟通的工具。

编程语言有不同的格式，可能用于不同的目的。例如，JavaScript 主要用于 Web 应用程序，而 Bash 主要用于操作系统。

*低级语言*通常比*高级语言*需要更少的步骤来让设备解释指令。然而，高级语言之所以流行，是因为它们的可读性和支持性。JavaScript 被认为是一种高级语言。

下面的代码展示了使用 JavaScript 的高级语言和使用 ARM 汇编代码的低级语言之间的区别。

```javascript
let number = 10
let n1 = 0, n2 = 1, nextTerm;

for (let i = 1; i <= number; i++) {
    console.log(n1);
    nextTerm = n1 + n2;
    n1 = n2;
    n2 = nextTerm;
}
```

```c
 area ascen,code,readonly
 entry
 code32
 adr r0,thumb+1
 bx r0
 code16
thumb
 mov r0,#00
 sub r0,r0,#01
 mov r1,#01
 mov r4,#10
 ldr r2,=0x40000000
back add r0,r1
 str r0,[r2]
 add r2,#04
 mov r3,r0
 mov r0,r1
 mov r1,r3
 sub r4,#01
 cmp r4,#00
 bne back
 end
```

相信与否，*它们都在做同样的事情*：打印一个最多为 10 的斐波那契数列。

✅ 斐波那契数列被[定义](https://en.wikipedia.org/wiki/Fibonacci_number)为一组数字，其中每个数字都是前两个数字之和，从 0 和 1 开始。斐波那契数列的前 10 个数字是 0、1、1、2、3、5、8、13、21 和 34。

## 程序的基本元素

程序中的单个指令称为*语句*，通常会有一个字符或行分隔来标记指令结束或*终止*的位置。程序如何终止因语言而异。

程序中的语句可能依赖于用户或其他地方提供的数据来执行指令。数据可以改变程序的行为，因此编程语言提供了一种临时存储数据以便以后使用的方法。这些被称为*变量*。变量是指示设备在其内存中保存数据的语句。程序中的变量类似于代数中的变量，它们有唯一的名称，其值可能随时间变化。

有些语句可能不会被设备执行。这通常是开发人员在编写时有意为之，或者是在发生意外错误时偶然发生的。这种对应用程序的控制使其更加健壮和可维护。通常，这些控制上的变化发生在满足某些条件时。现代编程中用于控制程序运行方式的常用语句是 `if..else` 语句。

✅ 你将在后续课程中学习更多关于此类语句的知识。

## 开发工具

[![开发工具](https://img.youtube.com/vi/69WJeXGBdxg/0.jpg)](https://youtube.com/watch?v=69WJeXGBdxg "Tools of the Trade")

> 🎥 点击上方图片观看关于工具的视频

在本节中，你将了解一些在你开始专业开发之旅时可能会发现非常有用的软件。

**开发环境**是开发人员在编写软件时经常使用的一套独特的工具和功能。其中一些工具已根据开发人员的特定需求进行了定制，并且如果开发人员在工作、个人项目或使用不同编程语言时改变了优先级，这些工具也可能会随时间而改变。开发环境与使用它们的开发人员一样独一无二。

### 编辑器

软件开发中最关键的工具之一是编辑器。编辑器是你编写代码的地方，有时也是你运行代码的地方。

开发人员依赖编辑器还有其他一些原因：

- *调试* 通过逐行执行代码来帮助发现错误和 bug。一些编辑器具有调试功能；它们可以为特定的编程语言进行定制和添加。
- *语法高亮* 为代码添加颜色和文本格式，使其更易于阅读。大多数编辑器允许自定义语法高亮。
- *扩展和集成* 是由开发人员为开发人员提供的专业工具。这些工具并未内置于基础编辑器中。例如，许多开发人员会为他们的代码编写文档以解释其工作原理。他们可能会安装拼写检查扩展来帮助在文档中查找拼写错误。大多数扩展都旨在在特定编辑器中使用，并且大多数编辑器都提供了搜索可用扩展的方法。
- *定制* 使开发人员能够创建适合其需求的独特开发环境。大多数编辑器都具有极高的可定制性，并且还可能允许开发人员创建自定义扩展。

#### 流行的编辑器和 Web 开发扩展

- [Visual Studio Code](https://code.visualstudio.com/?WT.mc_id=academic-77807-sagibbon)
  - [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)（代码拼写检查器）
  - [Live Share](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare)（实时共享）
  - [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)（代码格式化）
- [Atom](https://atom.io/)
  - [spell-check](https://atom.io/packages/spell-check)（拼写检查）
  - [teletype](https://atom.io/packages/teletype)
  - [atom-beautify](https://atom.io/packages/atom-beautify)
  
- [Sublimetext](https://www.sublimetext.com/)
  - [emmet](https://emmet.io/)
  - [SublimeLinter](http://www.sublimelinter.com/en/stable/)

### 浏览器

另一个关键工具是浏览器。Web 开发人员依靠浏览器来查看他们的代码在 Web 上的运行情况。它还用于显示在编辑器中编写的网页的可视元素，如 HTML。

许多浏览器都带有*开发者工具*（DevTools），其中包含一组有用的功能和信息，可帮助开发人员收集和捕获有关其应用程序的重要信息。例如：如果网页出现错误，了解它们发生的时间有时会很有帮助。浏览器中的 DevTools 可以配置为捕获此信息。

#### 流行的浏览器和开发者工具

- [Edge](https://docs.microsoft.com/microsoft-edge/devtools-guide-chromium/?WT.mc_id=academic-77807-sagibbon)
- [Chrome](https://developers.google.com/web/tools/chrome-devtools/)
- [Firefox](https://developer.mozilla.org/docs/Tools)

### 命令行工具

一些开发人员更喜欢使用非图形化界面来完成日常任务，并依赖命令行来实现这一点。编写代码需要大量的输入，一些开发人员不希望打断他们在键盘上的流畅操作。他们会使用键盘快捷键在桌面窗口之间切换、处理不同的文件和使用工具。大多数任务都可以用鼠标完成，但使用命令行的一个好处是，可以使用命令行工具完成很多事情，而无需在鼠标和键盘之间切换。命令行的另一个好处是它们是可配置的，你可以保存自定义配置，稍后进行更改，并将其导入到其他开发机器中。由于开发环境对每个开发人员来说都是如此独特，有些人会避免使用命令行，有些人会完全依赖它，还有一些人则喜欢两者结合。

### 流行的命令行选项

命令行的选项会因你使用的操作系统而异。

*💻 = 操作系统预装。*

#### Windows

- [Powershell](https://docs.microsoft.com/powershell/scripting/overview?view=powershell-7/?WT.mc_id=academic-77807-sagibbon) 💻
- [命令行](https://docs.microsoft.com/windows-server/administration/windows-commands/windows-commands/?WT.mc_id=academic-77807-sagibbon)（也称为 CMD）💻
- [Windows Terminal](https://docs.microsoft.com/windows/terminal/?WT.mc_id=academic-77807-sagibbon)
- [mintty](https://mintty.github.io/)
  
#### MacOS

- [终端 (Terminal)](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac) 💻
- [iTerm](https://iterm2.com/)
- [Powershell](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-7/?WT.mc_id=academic-77807-sagibbon)

#### Linux

- [Bash](https://www.gnu.org/software/bash/manual/html_node/index.html) 💻
- [KDE Konsole](https://docs.kde.org/trunk5/en/konsole/konsole/index.html)
- [Powershell](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-7/?WT.mc_id=academic-77807-sagibbon)

#### 流行的命令行工具

- [Git](https://git-scm.com/)（💻 在大多数操作系统上预装）
- [NPM](https://www.npmjs.com/)
- [Yarn](https://classic.yarnpkg.com/en/docs/cli/)

### 文档

当开发人员想要学习新东西时，他们很可能会求助于文档来学习如何使用它。开发人员经常依靠文档来指导他们如何正确使用工具和语言，并更深入地了解其工作原理。

#### 流行的 Web 开发文档

- [Mozilla 开发者网络 (MDN)](https://developer.mozilla.org/docs/Web)，由 [Firefox](https://www.mozilla.org/firefox/) 浏览器发行商 Mozilla 提供
- [Frontend Masters](https://frontendmasters.com/learn/)
- [Web.dev](https://web.dev)，由 [Chrome](https://www.google.com/chrome/) 浏览器发行商 Google 提供
- [微软自己的开发者文档](https://docs.microsoft.com/microsoft-edge/#microsoft-edge-for-developers)，用于 [Microsoft Edge](https://www.microsoft.com/edge)
- [W3 Schools](https://www.w3schools.com/where_to_start.asp)

✅ 做一些研究：既然你已经了解了 Web 开发人员环境的基础知识，请比较并对比它与 Web 设计师的环境。

---

## 🚀 挑战

比较一些编程语言。JavaScript 与 Java 有哪些独特的特点？COBOL 与 Go 呢？

## 课后测验

[课后测验](https://ff-quizzes.netlify.app/web/)

## 复习与自学

研究一下可供程序员使用的不同语言。尝试用一种语言写一行代码，然后用另外两种语言重写它。你学到了什么？

## 作业

[阅读文档](assignment.md)
