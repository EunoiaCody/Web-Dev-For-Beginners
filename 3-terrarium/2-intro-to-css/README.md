# 生态瓶项目 第 2 部分：CSS 入门

![Introduction to CSS](../../sketchnotes/webdev101-css.png)
> 速记图作者：[Tomomi Imura](https://twitter.com/girlie_mac)

## 课前测验

[课前测验](https://ff-quizzes.netlify.app/web/quiz/17)

### 简介

CSS（层叠样式表）解决了 Web 开发中的一个重要问题：如何让网站“看起来更好”。给应用添加样式能提升可用性和观感；你还可以用 CSS 实现响应式网页设计（RWD），让应用在不同屏幕尺寸下都能很好地展示。CSS 不仅仅是“好看”，其规范还包含动画与变换，可为应用提供更复杂的交互。CSS 工作组维护当前的 CSS 规范进展，你可以在[W3C 网站](https://www.w3.org/Style/CSS/members)上关注他们的工作。

> 注意：CSS 和 Web 上的其他技术一样在不断演进，并非所有浏览器都支持最新规范。实现前请查阅 [CanIUse.com](https://caniuse.com) 以确认兼容性。

在本课中，我们将为线上生态瓶添加样式，并学习多个 CSS 概念：层叠、继承、选择器、定位，以及用 CSS 构建布局。过程中我们会完成生态瓶的页面布局，并用 CSS 构建出“生态瓶”本体。

### 前置要求

你应当已经完成生态瓶的 HTML，并准备好开始加样式。

> 视频参考
>
> [![Git and GitHub basics video](https://img.youtube.com/vi/6yIdOIV9p1I/0.jpg)](https://www.youtube.com/watch?v=6yIdOIV9p1I)

### 任务 1

在生态瓶项目文件夹中新建 `style.css`，并在 `<head>` 中引入：

```html
<link rel="stylesheet" href="./style.css" />
```

---

## 层叠（Cascade）

“层叠样式表”的“层叠”指的是样式会按优先级“层层传递并覆盖”。网站作者定义的样式优先于浏览器默认样式；写在标签上的内联样式优先于外部样式表中的样式。

### 任务

给 `<h1>` 标签添加内联样式 "color: red"：

```HTML
<h1 style="color: red">My Terrarium</h1>
```

然后，在 `style.css` 中添加：

```CSS
h1 {
  color: blue;
}
```

✅ 你的页面显示成哪种颜色？为什么？有没有办法覆盖样式？在什么情况下你会这么做，或不这么做？

---

## 继承（Inheritance）

样式会从祖先元素“继承”到后代元素，嵌套的子元素会继承父元素的样式。

### 任务 2

给 body 设置字体，并观察一个嵌套元素的字体：

```CSS
body {
  font-family: helvetica, arial, sans-serif;
}
```

打开浏览器开发者工具的 Elements 面板，观察 H1 的字体。正如浏览器所显示的，它从 body 继承了字体：

![inherited font](images/1.png)

✅ 你能让某个嵌套元素“继承”到不同的属性吗？

---

## CSS 选择器（Selectors）

### 标签（Tags）

此时你的 `style.css` 只给少量标签加了样式，页面看起来有点奇怪：

```CSS
body {
  font-family: helvetica, arial, sans-serif;
}

h1 {
  color: #3a241d;
  text-align: center;
}
```

按标签名写样式可以控制某些唯一元素，但你还需要控制生态瓶中很多植物的样式，这时就要充分利用选择器。

### ID（Ids）

为左右容器添加样式。由于左右容器各只有一个，它们在标记中使用 id。要为它们写样式，使用 `#`：

```CSS
#left-container {
  background-color: #eee;
  width: 15%;
  left: 0px;
  top: 0px;
  position: absolute;
  height: 100%;
  padding: 10px;
}

#right-container {
  background-color: #eee;
  width: 15%;
  right: 0px;
  top: 0px;
  position: absolute;
  height: 100%;
  padding: 10px;
}
```

这里我们把容器绝对定位到屏幕最左和最右，并用百分比设置宽度，以便在小屏上也能自适应。

✅ 这段代码重复较多，不够“DRY”（Don't Repeat Yourself）。你能找到更好的写法吗？比如结合 id 和 class？这需要你修改标记并重构 CSS：

```html
<div id="left-container" class="container"></div>
```

### 类（Classes）

上面的例子中，你为两个唯一元素添加了样式。如果希望样式应用于屏幕上的多个元素，可以使用 CSS 类。用它来布局左右容器中的植物。

注意每株植物在 HTML 标记中都同时拥有 id 和 class。id 将在后续 JavaScript 中用于操控植物位置；class 则用于为所有植物赋予统一样式。

```html
<div class="plant-holder">
  <img class="plant" alt="plant" id="plant1" src="./images/plant1.png" />
</div>
```

在 `style.css` 中加入：

```CSS
.plant-holder {
  position: relative;
  height: 13%;
  left: -10px;
}

.plant {
  position: absolute;
  max-width: 150%;
  max-height: 150%;
  z-index: 2;
}
```

这段代码中混合使用了相对定位和绝对定位（下一节会讲）。注意高度使用了百分比：

- plant-holder 的高度设置为 13%，这样每个垂直容器里都能展示所有植物，无需滚动；
- plant-holder 左移以便让植物在其容器内更居中。由于图片带有较大的透明背景，为了更好拖拽，需要向左推一点以便更好地适配屏幕；
- 植物本身设置了 150% 的最大宽度，这样浏览器缩小时它也会等比缩小。试着调整窗口大小，植物会留在各自容器中并缩放以适配；
- 使用了 z-index 来控制元素的“高度层级”，让植物显示在容器之上，像是在生态瓶里。

✅ 为什么需要同时拥有 plant-holder 和 plant 这两个选择器？

## CSS 定位（Positioning）

混合不同的定位属性（static、relative、fixed、absolute、sticky）可能有点棘手，但如果用得当，就能很好地控制页面元素。

绝对定位的元素相对于其最近的“已定位”祖先元素进行定位；若没有，则相对文档的 body 定位。

相对定位的元素会基于其初始位置，按 CSS 给定的偏移量进行调整。

在本例中，`plant-holder` 是相对定位，它位于一个绝对定位的容器之内。其结果是侧栏容器固定在左右两侧，plant-holder 嵌套其中并在侧栏内部进行位置调整，为垂直排列的植物留出空间。

> 植物 `plant` 本身也使用了绝对定位，这对后续实现拖拽是必要的（下一课会用到）。

✅ 试着切换侧栏容器与 plant-holder 的定位方式，会发生什么？

## CSS 布局（Layouts）

现在用你学到的知识，纯 CSS 构建出“生态瓶”本体！

首先，把 `.terrarium` 下的子元素用 CSS 样式化为带圆角的矩形：

```CSS
.jar-walls {
  height: 80%;
  width: 60%;
  background: #d1e1df;
  border-radius: 1rem;
  position: absolute;
  bottom: 0.5%;
  left: 20%;
  opacity: 0.5;
  z-index: 1;
}

.jar-top {
  width: 50%;
  height: 5%;
  background: #d1e1df;
  position: absolute;
  bottom: 80.5%;
  left: 25%;
  opacity: 0.7;
  z-index: 1;
}

.jar-bottom {
  width: 50%;
  height: 1%;
  background: #d1e1df;
  position: absolute;
  bottom: 0%;
  left: 25%;
  opacity: 0.7;
}

.dirt {
  width: 60%;
  height: 5%;
  background: #3a241d;
  position: absolute;
  border-radius: 0 0 1rem 1rem;
  bottom: 1%;
  left: 20%;
  opacity: 0.7;
  z-index: -1;
}
```

注意这里大量使用了百分比。缩小浏览器，你会看到玻璃瓶也随之缩放。还要留意各个元素的宽高百分比，以及元素如何绝对定位在视口底部的中间位置。

我们还使用了 `rem` 作为圆角的单位，它是相对字体大小的长度单位。可在 [CSS 规范](https://www.w3.org/TR/css-values-3/#font-relative-lengths) 中了解更多。

✅ 尝试改变瓶子与泥土的颜色和透明度。会发生什么？为什么？

---

## 🚀 挑战

给瓶子的左下区域增加“泡泡状”的高光，让它更像玻璃。你需要为 `.jar-glossy-long` 和 `.jar-glossy-short` 添加样式来表现反光。效果如下：

![finished terrarium](./images/terrarium-final.png)

若要完成课后测验，请学习这个 Learn 模块：[用 CSS 为 HTML 应用添加样式](https://docs.microsoft.com/learn/modules/build-simple-website/4-css-basics/?WT.mc_id=academic-77807-sagibbon)

## 课后测验

[课后测验](https://ff-quizzes.netlify.app/web/quiz/18)

## 复习与自学

CSS 看似简单，但要让应用在所有浏览器、所有屏幕尺寸下都表现完美并不容易。CSS Grid 与 Flexbox 是为此而生的布局工具，让工作更结构化、更可靠。试试这些小游戏来学习它们：[Flexbox Froggy](https://flexboxfroggy.com/) 与 [Grid Garden](https://codepip.com/games/grid-garden/)。

## 作业

[CSS 重构](assignment.md)
