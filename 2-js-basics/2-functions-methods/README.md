# JavaScript 基础：方法与函数

![JavaScript Basics - Functions](../../sketchnotes/webdev101-js-functions.png)
> 手绘笔记作者：[Tomomi Imura](https://twitter.com/girlie_mac)

## 课前测验

[课前测验](https://ff-quizzes.netlify.app)

编写代码时，我们总希望代码易读。听起来有点反直觉，但代码“被读”的次数远多于“被写”。为了让代码易维护，开发者工具箱里的一件核心工具就是“函数（function）”。

[![Methods and Functions](https://img.youtube.com/vi/XgKsD6Zwvlc/0.jpg)](https://youtube.com/watch?v=XgKsD6Zwvlc "Methods and Functions")

> 🎥 点击上方图片，观看关于方法与函数的视频。

> 你也可以在 [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-functions/?WT.mc_id=academic-77807-sagibbon) 上学习本课！

## 函数（Functions）

从本质上说，函数是一段可以按需执行的代码块。它非常适合需要多次执行相同任务的场景：与其在多处复制粘贴同一逻辑（将来要改还不容易），不如把它集中到一个地方，需要时就调用——甚至可以在函数中调用其他函数！

给函数命名同样重要。名字看似微不足道，但它为一段代码提供了快捷的“文档”。把它想象成按钮上的标签：如果按钮写着“Cancel timer”，我就知道它会停止计时。

## 创建并调用函数

函数的语法如下：

```javascript
function nameOfFunction() { // function definition
  // function definition/body
}
```

若要创建一个显示问候语的函数，可以这样写：

```javascript
function displayGreeting() {
  console.log('Hello, world!');
}
```

当我们需要调用（invoke）函数时，使用函数名后跟 `()`。值得注意的是，函数可以在调用之前或之后定义；JavaScript 编译器会帮你找到它。

```javascript
// 调用函数
displayGreeting();
```

> 注意：有一种特殊的函数叫做“方法（method）”，你其实已经用过了！上面的示例中我们使用的 `console.log` 就是方法。方法与函数的不同在于，方法是附着在某个对象上的（本例中是 `console`），而普通函数是“自由”的。很多开发者会交替使用这两个术语。

### 函数的最佳实践

创建函数时可以记住如下实践：

- 一如既往，使用有描述性的名字，便于知道函数的用途
- 使用驼峰命名（camelCasing）来组合多个单词
- 让函数聚焦于一个具体任务

## 向函数传递信息

为了让函数更可复用，通常会向它传入信息。以上面的 `displayGreeting` 为例，它只能显示 “Hello, world!”——并不是很有用。如果我们想更灵活些，比如允许调用者指定要问候的名字，可以添加一个“参数（parameter）”。参数（有时也称“实参 argument”）是传入函数的附加信息。

参数在函数定义的圆括号中按逗号分隔列出：

```javascript
function name(param, param2, param3) {

}
```

我们可以更新 `displayGreeting` 来接受一个名字并显示出来：

```javascript
function displayGreeting(name) {
  const message = `Hello, ${name}!`;
  console.log(message);
}
```

当调用函数并传入参数时，把参数写在圆括号内：

```javascript
displayGreeting('Christopher');
// 运行后显示 "Hello, Christopher!"
```

## 默认值（Default values）

我们可以通过添加更多参数来让函数更灵活。但如果并不想强制所有值都必须提供呢？仍以问候为例，我们可以把 name 设为必需（需要知道问候谁），而让问候词本身可选。如果没有自定义，就提供一个默认值。给参数提供默认值的方式与给变量赋值类似：`parameterName = 'defaultValue'`。完整示例如下：

```javascript
function displayGreeting(name, salutation='Hello') {
  console.log(`${salutation}, ${name}`);
}
```

调用时，我们可以选择是否为 `salutation` 传值：

```javascript
displayGreeting('Christopher');
// 显示 "Hello, Christopher"

displayGreeting('Christopher', 'Hi');
// 显示 "Hi, Christopher"
```

## 返回值（Return values）

到目前为止，我们构建的函数都会把内容输出到[控制台](https://developer.mozilla.org/docs/Web/API/console)。有时这正合所需，尤其当函数会调用其他服务时。但如果我想写个帮助函数来计算一个值，并把它返回供其他地方使用呢？

可以通过“返回值（return value）”实现。返回值由函数返回，和字符串或数字等字面量一样可以被存入变量。

当函数要返回内容时，使用关键字 `return`。`return` 期望一个返回的值或引用，例如：

```javascript
return myVariable;
```

我们可以写一个函数来构建问候消息并把值返回给调用者：

```javascript
function createGreetingMessage(name) {
  const message = `Hello, ${name}`;
  return message;
}
```

调用该函数时，我们会把返回值存入变量，这与给变量设置静态值（如 `const name = 'Christopher'`）非常相似：

```javascript
const greetingMessage = createGreetingMessage('Christopher');
```

## 把函数作为函数的参数

随着编程经验的增长，你会遇到把“函数作为参数”传给另一个函数的情况。当我们不知道某件事何时发生或完成，但知道完成后要做某事时，这个技巧非常常用。

例如，[setTimeout](https://developer.mozilla.org/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout) 会启动一个定时器，并在到时执行代码。我们需要告诉它要执行的代码——这正是函数大显身手的时候！

运行下面的代码，3 秒后你会看到 “3 seconds has elapsed” 的消息：

```javascript
function displayDone() {
  console.log('3 seconds has elapsed');
}
// 定时器的单位是毫秒
setTimeout(displayDone, 3000);
```

### 匿名函数（Anonymous functions）

再看看我们写的东西：我们为了只用一次而创建了一个有名字的函数。随着应用变复杂，可能会写出一堆只被调用一次的函数，这并不理想。好在并非总要给函数取名！

当把函数作为参数传递时，可以不事先创建函数，而是在参数位置直接写。语法仍然使用 `function` 关键字，只是把它放在参数里。

把上面的代码改写为匿名函数：

```javascript
setTimeout(function() {
  console.log('3 seconds has elapsed');
}, 3000);
```

运行新代码你会发现结果一样：我们创建了一个函数，但没有给它名字！

### 箭头函数（Fat arrow functions）

很多编程语言（包括 JavaScript）都有一种简写叫“箭头函数”或“胖箭头函数”。它使用 `=>` 这个看起来像箭头的符号，因此得名。使用 `=>` 可以省略 `function` 关键字。

再把代码改写为箭头函数：

```javascript
setTimeout(() => {
  console.log('3 seconds has elapsed');
}, 3000);
```

### 何时使用哪种方式

我们已经看到三种把函数作为参数传递的方式，何时使用哪一种？如果你知道函数会被多处复用，就按常规方式单独创建；如果只在一个地方用，一般匿名函数更合适。至于使用箭头函数还是传统的 `function` 语法，取决于你的喜好，但你会注意到大多数现代开发者更偏爱 `=>`。

---

## 🚀 挑战

你能用“一句话”说明函数与方法的区别吗？试试看！

## 课后测验

[课后测验](https://ff-quizzes.netlify.app)

## 回顾与自学

值得[多了解一下箭头函数](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Functions/Arrow_functions)，它们在代码中越来越常见。练习先写一个普通函数，再用这种语法改写它。

## 作业

[Fun with Functions](assignment.md)
