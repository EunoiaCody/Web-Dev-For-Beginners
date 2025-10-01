# 生态瓶项目 第 3 部分：DOM 操作与闭包

![DOM and a closure](../../sketchnotes/webdev101-js.png)
> 速记图作者：[Tomomi Imura](https://twitter.com/girlie_mac)

## 课前测验

[课前测验](https://ff-quizzes.netlify.app/web/quiz/19)

### 简介

操作 DOM（文档对象模型）是 Web 开发的关键环节。根据 [MDN](https://developer.mozilla.org/docs/Web/API/Document_Object_Model/Introduction) 的定义：“文档对象模型（DOM）是对构成 Web 文档结构与内容的对象的 数据表示。” 由于在 Web 上操作 DOM 颇具挑战，人们常用 JavaScript 框架来替代原生 JS 进行 DOM 管理；不过这次我们将用原生方式自己搞定！
在此基础上，本课还会介绍 [JavaScript 闭包](https://developer.mozilla.org/docs/Web/JavaScript/Closures)：你可以把它理解为一个函数被另一个函数“包裹”，因此内部函数可以访问外部函数的作用域。

> 闭包是一个庞大而复杂的主题。本课仅涉及最基础的概念：在本项目代码中，你会看到一个闭包——通过构造外部函数与内部函数的方式，让内部函数能够访问外部函数的作用域。更多内容请阅读 MDN 的[详细文档](https://developer.mozilla.org/docs/Web/JavaScript/Closures)。
我们将用一个闭包来操作 DOM。

可以把 DOM 想象成一棵“树”，表示网页文档可以被操作的各种方式。为此，已经有多种 API（应用程序接口）可供开发者用所选编程语言来访问 DOM，以编辑、修改、重排与管理它。
![DOM tree representation](./images/dom-tree.png)

> 这是 DOM 的一种表示以及引用它的 HTML 标记。图源：[Olfa Nasraoui](https://www.researchgate.net/publication/221417012_Profile-Based_Focused_Crawler_for_Social_Media-Sharing_Websites)

在本课中，我们将为互动生态瓶项目编写 JavaScript，使用户可以在页面上拖动植物。

### 前置要求

你应当已经完成生态瓶的 HTML 与 CSS。本课结束时，你将能够通过拖拽将植物移入或移出生态瓶。

### 任务 1

在项目文件夹中新建 `script.js`，并在 `<head>` 中引入：

```html
  <script src="./script.js" defer></script>
```

> 注意：将外部脚本以 `defer` 引入，让 JavaScript 在 HTML 完全加载后再执行。你也可以使用 `async`，它会在 HTML 解析时并行执行脚本，但在我们的场景中，更重要的是在拖拽脚本执行前，所有需要拖拽的 HTML 元素已可用。

---

## DOM 元素

首先，需要在 DOM 中创建对将被操作元素的引用。我们的例子里，它们是两侧栏中等待的 14 株植物。

### 任务 2

```html
dragElement(document.getElementById('plant1'));
dragElement(document.getElementById('plant2'));
dragElement(document.getElementById('plant3'));
dragElement(document.getElementById('plant4'));
dragElement(document.getElementById('plant5'));
dragElement(document.getElementById('plant6'));
dragElement(document.getElementById('plant7'));
dragElement(document.getElementById('plant8'));
dragElement(document.getElementById('plant9'));
dragElement(document.getElementById('plant10'));
dragElement(document.getElementById('plant11'));
dragElement(document.getElementById('plant12'));
dragElement(document.getElementById('plant13'));
dragElement(document.getElementById('plant14'));
```

这段代码做了什么？你在 document 的 DOM 中查找指定 Id 的元素。还记得第一课里我们为每张植物图片都加了唯一的 Id（如 `id="plant1"`）吗？现在就要用到它们。找到元素后，把它传给稍后会实现的 `dragElement` 函数，于是这个 HTML 元素就具备了可拖拽能力（很快就会）。

✅ 为什么按 Id 引用元素？为什么不按 CSS 类？可以回顾上一课的 CSS 内容来思考。

---

## 闭包（Closure）

现在可以创建 `dragElement` 闭包了：外部函数包裹内部函数（此处我们会有三个内部函数）。
当一个或多个函数需要访问外部函数的作用域时，闭包非常有用。示例：

```javascript
function displayCandy(){
  let candy = ['jellybeans'];
  function addCandy(candyType) {
    candy.push(candyType)
  }
  addCandy('gumdrops');
}
displayCandy();
console.log(candy)
```

在这个例子中，displayCandy 函数包含了一个用于向数组添加新糖果类型的内部函数；该数组已经在外部函数中存在。如果运行这段代码，`candy` 数组会是 undefined，因为它是一个局部变量（局部于闭包）。

✅ 如何让 `candy` 数组可被访问？试着把它移动到闭包外部，这样它会成为全局变量，而不是只存在于闭包的本地作用域中。

### 任务 3

在 `script.js` 中的元素声明下方，创建一个函数：

```javascript
function dragElement(terrariumElement) {
  // 在屏幕上设置 4 个用于定位的位置值
  let pos1 = 0,
      pos2 = 0,
      pos3 = 0,
✅ The [event handler `onclick`](https://developer.mozilla.org/docs/Web/API/GlobalEventHandlers/onclick) has much more support cross-browser; why wouldn't you use it here? Think about the exact type of screen interaction you're trying to create here.

---

## The Pointerdrag function

The `terrariumElement` is ready to be dragged around; when the `onpointerdown` event is fired, the function `pointerDrag` is invoked. Add that function right under this line: `terrariumElement.onpointerdown = pointerDrag;`:

### 任务 4

```javascript
function pointerDrag(e) {
  e.preventDefault();
  console.log(e);
  pos3 = e.clientX;
  pos4 = e.clientY;
}
```

Several things happen. First, you prevent the default events that normally happen on pointerdown from occurring by using `e.preventDefault();`. This way you have more control over the interface's behavior.

> Come back to this line when you've built the script file completely and try it without `e.preventDefault()` - what happens?

Second, open `index.html` in a browser window, and inspect the interface. When you click a plant, you can see how the 'e' event is captured. Dig into the event to see how much information is gathered by one pointer down event!  

Next, note how the local variables `pos3` and `pos4` are set to e.clientX. You can find the `e` values in the inspection pane. These values capture the x and y coordinates of the plant at the moment you click on it or touch it. You will need fine-grained control over the behavior of the plants as you click and drag them, so you keep track of their coordinates.

✅ Is it becoming more clear why this entire app is built with one big closure? If it wasn't, how would you maintain scope for each of the 14 draggable plants?

Complete the initial function by adding two more pointer event manipulations under `pos4 = e.clientY`:

```html
document.onpointermove = elementDrag;
document.onpointerup = stopElementDrag;
```

Now you are indicating that you want the plant to be dragged along with the pointer as you move it, and for the dragging gesture to stop when you deselect the plant. `onpointermove` and `onpointerup` are all parts of the same API as `onpointerdown`. The interface will throw errors now as you have not yet defined the `elementDrag` and the `stopElementDrag` functions, so build those out next.

## The elementDrag and stopElementDrag functions

You will complete your closure by adding two more internal functions that will handle what happens when you drag a plant and stop dragging it. The behavior you want is that you can drag any plant at any time and place it anywhere on the screen. This interface is quite un-opinionated (there is no drop zone for example) to allow you to design your terrarium exactly as you like it by adding, removing, and repositioning plants.

### 任务 5

Add the `elementDrag` function right after the closing curly bracket of `pointerDrag`:

```javascript
function elementDrag(e) {
  pos1 = pos3 - e.clientX;
  pos2 = pos4 - e.clientY;
  pos3 = e.clientX;
  pos4 = e.clientY;
  console.log(pos1, pos2, pos3, pos4);
  terrariumElement.style.top = terrariumElement.offsetTop - pos2 + 'px';
  terrariumElement.style.left = terrariumElement.offsetLeft - pos1 + 'px';
}
```

In this function, you do a lot of editing of the initial positions 1-4 that you set as local variables in the outer function. What's going on here?

As you drag, you reassign `pos1` by making it equal to `pos3` (which you set earlier as `e.clientX`)  minus the current `e.clientX` value. You do a similar operation to `pos2`. Then, you reset `pos3` and `pos4` to the new X and Y coordinates of the element. You can watch these changes in the console as you drag. Then, you manipulate the plant's css style to set its new position based on the new positions of `pos1` and `pos2`, calculating the plant's top and left X and Y coordinates based on comparing its offset with these new positions.

> `offsetTop` and `offsetLeft` are CSS properties that set an element's position based on that of its parent; its parent can be any element that is not positioned as `static`.

All this recalculation of positioning allows you to fine-tune the behavior of the terrarium and its plants.

### 任务 6

The final task to complete the interface is to add the `stopElementDrag` function after the closing curly bracket of `elementDrag`:

```javascript
function stopElementDrag() {
  document.onpointerup = null;
  document.onpointermove = null;
}
```

This small function resets the `onpointerup` and `onpointermove` events so that you can either restart your plant's progress by starting to drag it again, or start dragging a new plant.

✅ What happens if you don't set these events to null?

Now you have completed your project!

🥇Congratulations! You have finished your beautiful terrarium. ![finished terrarium](./images/terrarium-final.png)

---

## 🚀Challenge

Add new event handler to your closure to do something more to the plants; for example, double-click a plant to bring it to the front. Get creative!

## Post-Lecture Quiz

[Post-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/20)

## Review & Self Study

While dragging elements around the screen seems trivial, there are many ways to do this and many pitfalls, depending on the effect you seek. In fact, there is an entire [drag and drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API) that you can try. We didn't use it in this module because the effect we wanted was somewhat different, but try this API on your own project and see what you can achieve.

Find more information on pointer events on the [W3C docs](https://www.w3.org/TR/pointerevents1/) and on [MDN web docs](https://developer.mozilla.org/docs/Web/API/Pointer_events).

Always check browser capabilities using [CanIUse.com](https://caniuse.com/).

## 作业

[再和 DOM 多打几次交道](assignment.md)

## Assignment

[Work a bit more with the DOM](assignment.md)
