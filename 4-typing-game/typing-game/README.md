# 使用事件创建一个游戏

## 课前测验

[Pre-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/21)

## 事件驱动编程

在创建基于浏览器的应用时，我们会提供图形用户界面（GUI），以便用户与我们构建的功能交互。与浏览器交互最常见的方式是点击和在各类元素中输入。作为开发者的挑战在于：我们并不知道用户何时会执行这些操作！

[事件驱动编程](https://en.wikipedia.org/wiki/Event-driven_programming) 是我们用来构建 GUI 的编程方式。拆开这个短语，核心词是 **event（事件）**。[Event](https://www.merriam-webster.com/dictionary/event)（韦氏词典）的定义是“发生的事情”。这正好描述了我们的处境：我们知道会发生某些事情，需要在发生时执行相应代码，但我们不知道它具体何时发生。

我们通过创建函数来标记希望执行的那段代码。在[过程式编程](https://en.wikipedia.org/wiki/Procedural_programming)中，函数会按特定顺序被调用。在事件驱动编程中也是如此，不同之处在于函数将“如何”被调用。

为处理事件（按钮点击、输入等），我们会注册**事件监听器**。事件监听器是一个函数，用于监听事件发生并作出响应。它可以更新 UI、调用服务器，或执行任何需要对用户操作作出回应的逻辑。我们可以使用 [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) 并提供要执行的函数来添加事件监听器。

> 注意：创建事件监听器有很多方式。你可以使用匿名函数，也可以创建具名函数。你可以使用各种捷径，例如设置 `click` 属性，或使用 `addEventListener`。在本练习中，我们将聚焦于 `addEventListener` 与匿名函数——这是 Web 开发者最常用的技巧之一；同时它也最灵活，`addEventListener` 适用于所有事件，事件名可以作为参数传入。

### 常见事件

在创建应用时，你可以监听[数十种事件](https://developer.mozilla.org/docs/Web/Events)。基本上，用户在页面上的任何操作都会触发事件，这让你可以更好地掌控体验。幸运的是，通常只需少量常见事件即可。以下是几个常见事件（包含我们在游戏中会用到的两种）：

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event)：用户点击了某个元素（通常是按钮或超链接）
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event)：用户点击了鼠标右键
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event)：用户选中了一些文本
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event)：用户输入了文本

## 创建游戏

我们将通过创建一个游戏来探索 JavaScript 中事件的工作方式。游戏用于测试玩家的打字能力——这是所有开发者都应具备却常被低估的技能。大家都应该多练打字！游戏的大致流程如下：

- 玩家点击开始按钮，出现需要输入的一句名言
- 玩家在文本框中尽快输入这句名言
  - 每完成一个单词，下一个单词会被高亮
  - 如果玩家打错字，文本框会变红
  - 当玩家完成整句输入，会显示成功提示与用时

让我们开始构建游戏，一边学习事件！

### 文件结构

我们需要 3 个文件：**index.html**、**script.js** 和 **style.css**。先把它们准备好，后续会更顺手。

- 打开控制台或终端，新建工作文件夹并进入：

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- 打开 Visual Studio Code

```bash
code .
```

- 在 VS Code 中创建下列三个文件：
  - index.html
  - script.js
  - style.css

## 创建用户界面

根据需求，我们的 HTML 页面需要一些元素。就像一份菜谱，我们需要准备这些“食材”：

- 用于显示要输入的名言的区域
- 用于显示消息（例如成功提示）的区域
- 用于输入的文本框
- 开始按钮

这些元素都需要设置 ID，以便在 JavaScript 中获取与控制。我们还将引入稍后创建的 CSS 与 JavaScript 文件。

创建 **index.html** 文件，添加如下 HTML：

```html
<!-- inside index.html -->
<html>
<head>
  <title>Typing game</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Typing game!</h1>
  <p>Practice your typing skills with a quote from Sherlock Holmes. Click **start** to begin!</p>
  <p id="quote"></p> <!-- This will display our quote -->
  <p id="message"></p> <!-- This will display any status messages -->
  <div>
    <input type="text" aria-label="current word" id="typed-value" /> <!-- The textbox for typing -->
    <button type="button" id="start">Start</button> <!-- To start the game -->
  </div>
  <script src="script.js"></script>
</body>
</html>
```

### 启动应用

迭代式开发有助于随时观察效果。启动我们的应用吧。VS Code 有个很好用的扩展 [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon)，它可以在本地托管应用，并在你每次保存时自动刷新浏览器。

- 打开上面的链接安装 [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon)，点击 **Install**
  - 浏览器会提示打开 VS Code，随后 VS Code 会提示执行安装
  - 如被提示，请重启 VS Code
- 安装完成后，在 VS Code 中按 Ctrl-Shift-P（或 Cmd-Shift-P）打开命令面板
- 输入 **Live Server: Open with Live Server**
  - Live Server 将开始托管你的应用
- 打开浏览器访问 <https://localhost:5500>
- 现在你应该能看到刚刚创建的页面！

接下来添加一些功能。

## 添加 CSS

完成 HTML 后，添加基础样式。我们需要高亮玩家当前应输入的单词，并在输入错误时让文本框显得不同（着色）。我们将用两个类来实现。

创建 **style.css** 文件，添加如下样式：

```css
/* inside style.css */
.highlight {
  background-color: yellow;
}

.error {
  background-color: lightcoral;
  border: red;
}
```

✅ 在 CSS 层面，你可以随意美化页面。花点时间让页面更好看：

- 选择更合适的字体
- 给标题上色
- 调整元素尺寸

## JavaScript

界面已经准备好，下面专注于提供逻辑的 JavaScript。我们将拆成几个步骤：

- [创建常量](#添加常量)
- [添加开始事件监听](#添加开始逻辑)
- [添加输入事件监听](#添加输入逻辑)

首先，创建 **script.js** 文件。

### 添加常量

为了让编程更顺手，我们需要准备一些东西，像做菜一样列个清单：

- 所有名言的数组
- 存放当前名言所有单词的数组（初始为空）
- 记录玩家正在输入的单词索引
- 玩家点击开始时的时间

同时，我们需要一些 UI 元素的引用：

- 文本框（**typed-value**）
- 名言显示区域（**quote**）
- 消息显示区域（**message**）

```javascript
// inside script.js
// all of our quotes
const quotes = [
    'When you have eliminated the impossible, whatever remains, however improbable, must be the truth.',
    'There is nothing more deceptive than an obvious fact.',
    'I ought to know by this time that when a fact appears to be opposed to a long train of deductions it invariably proves to be capable of bearing some other interpretation.',
    'I never make exceptions. An exception disproves the rule.',
    'What one man can invent another can discover.',
    'Nothing clears up a case so much as stating it to another person.',
    'Education never ends, Watson. It is a series of lessons, with the greatest for the last.',
];
// store the list of words and the index of the word the player is currently typing
let words = [];
let wordIndex = 0;
// the starting time
let startTime = Date.now();
// page elements
const quoteElement = document.getElementById('quote');
const messageElement = document.getElementById('message');
const typedValueElement = document.getElementById('typed-value');
```

✅ 试着给游戏再添加几句名言吧

> 注意：我们可以通过 `document.getElementById` 在代码中随时获取元素。由于会频繁引用这些元素，使用常量可以避免字符串拼写错误。像 [Vue.js](https://vuejs.org/) 或 [React](https://reactjs.org/) 这样的框架，也能帮助你更好地集中管理代码。

花一分钟看看关于 `const`、`let` 和 `var` 的视频：

[![Types of variables](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "Types of variables")

> 🎥 点击上方图片观看变量类型相关视频。

### 添加开始逻辑

开始游戏时，玩家会点击“开始”。当然，我们不知道他们何时点击，这正是[事件监听器](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener)发挥作用的地方。事件监听器允许我们监听事件发生并执行相应代码。在这里，我们要在用户点击开始时运行代码。

当用户点击 **Start** 时，我们需要：选择一条名言、设置界面、并初始化当前单词与计时的状态。下面是需要添加的 JavaScript，后文会逐步解释：

```javascript
// at the end of script.js
document.getElementById('start').addEventListener('click', () => {
  // get a quote
  const quoteIndex = Math.floor(Math.random() * quotes.length);
  const quote = quotes[quoteIndex];
  // Put the quote into an array of words
  words = quote.split(' ');
  // reset the word index for tracking
  wordIndex = 0;

  // UI updates
  // Create an array of span elements so we can set a class
  const spanWords = words.map(function(word) { return `<span>${word} </span>`});
  // Convert into string and set as innerHTML on quote display
  quoteElement.innerHTML = spanWords.join('');
  // Highlight the first word
  quoteElement.childNodes[0].className = 'highlight';
  // Clear any prior messages
  messageElement.innerText = '';

  // Setup the textbox
  // Clear the textbox
  typedValueElement.value = '';
  // set focus
  typedValueElement.focus();
  // set the event handler

  // Start the timer
  startTime = new Date().getTime();
});
```

来分解一下这段代码：

- 设置单词追踪
  - 使用 [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) 与 [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) 随机从 `quotes` 数组中选择一条名言
  - 将 `quote` 拆分为 `words` 数组，以便追踪玩家当前输入到哪个单词
  - 将 `wordIndex` 设为 0，表示从第一个单词开始
- 设置界面
  - 创建 `spanWords` 数组，把每个单词包在 `span` 元素中
    - 这样可以在界面上高亮当前单词
  - 使用 `join` 拼成字符串，设置到 `quoteElement.innerHTML`
    - 将名言显示给玩家
  - 将第一个 `span` 的 `className` 设为 `highlight`，使其高亮
  - 通过将 `messageElement.innerText` 设为空字符串来清空消息
- 设置文本框
  - 清空 `typedValueElement.value`
  - 调用 `typedValueElement.focus()` 获取焦点
- 调用 `getTime` 开始计时

### 添加输入逻辑

当玩家输入时，会触发 `input` 事件。该监听器会检查玩家是否输入正确，并处理游戏当前状态。回到 **script.js**，在末尾添加下面的代码，随后我们再做解释：

```javascript
// at the end of script.js
typedValueElement.addEventListener('input', () => {
  // Get the current word
  const currentWord = words[wordIndex];
  // get the current value
  const typedValue = typedValueElement.value;

  if (typedValue === currentWord && wordIndex === words.length - 1) {
    // end of sentence
    // Display success
    const elapsedTime = new Date().getTime() - startTime;
    const message = `CONGRATULATIONS! You finished in ${elapsedTime / 1000} seconds.`;
    messageElement.innerText = message;
  } else if (typedValue.endsWith(' ') && typedValue.trim() === currentWord) {
    // end of word
    // clear the typedValueElement for the new word
    typedValueElement.value = '';
    // move to the next word
    wordIndex++;
    // reset the class name for all elements in quote
    for (const wordElement of quoteElement.childNodes) {
      wordElement.className = '';
    }
    // highlight the new word
    quoteElement.childNodes[wordIndex].className = 'highlight';
  } else if (currentWord.startsWith(typedValue)) {
    // currently correct
    // highlight the next word
    typedValueElement.className = '';
  } else {
    // error state
    typedValueElement.className = 'error';
  }
});
```

来分解一下这段代码！我们首先获取当前单词与玩家已输入的内容。接着用层叠式判断：先判断是否整句完成、是否一个单词完成、是否当前仍然正确、最后才是错误状态。

- 整句完成：当 `typedValue` 等于 `currentWord` 且 `wordIndex` 等于 `words.length - 1`
  - 用当前时间减去 `startTime` 得到 `elapsedTime`
  - 除以 1000 将毫秒转为秒
  - 显示成功消息
- 单词完成：当 `typedValue` 以空格结尾（表示一个单词的结束）且 `typedValue.trim()` 等于 `currentWord`
  - 将 `typedValueElement.value` 置空，为下一个单词做准备
  - `wordIndex++` 进入下一个单词
  - 遍历 `quoteElement.childNodes`，将其 `className` 清空
  - 将当前单词的 `className` 设为 `highlight` 以高亮
- 单词仍然正确（但未完成）：`currentWord` 以 `typedValue` 开头
  - 清空 `typedValueElement.className` 保持默认
- 否则即为错误
  - 将 `typedValueElement.className` 设为 `error`

## 测试你的应用

恭喜来到最后一步！现在验证应用是否正常工作。试一试吧！即便出现错误也不必担心，**所有开发者**都会遇到错误。观察提示信息并按需调试即可。

点击 **Start**，开始输入！它应该看起来类似之前看到的动画效果。

![Animation of the game in action](../images/demo.gif)

---

## 🚀 挑战

尝试添加更多功能：

- 在完成后禁用 `input` 事件监听，并在点击按钮时重新启用
- 当玩家完成整句输入后禁用文本框
- 使用模态对话框显示成功消息
- 使用 [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage) 存储最高分

## 课后测验

[Post-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/22)

## 复习与自学

阅读浏览器提供给开发者的[所有可用事件](https://developer.mozilla.org/docs/Web/Events)，并思考你会在什么场景使用它们。

## 作业

[Create a new keyboard game](assignment.md)
