# 生态瓶项目 第 1 课：HTML 入门

![Introduction to HTML](../../sketchnotes/webdev101-html.png)
> 手绘笔记作者：[Tomomi Imura](https://twitter.com/girlie_mac)

## 课前测验

[课前测验](https://ff-quizzes.netlify.app/web/quiz/15)

> 视频参考
>
> [![Git and GitHub basics video](https://img.youtube.com/vi/1TvxJKBzhyQ/0.jpg)](https://www.youtube.com/watch?v=1TvxJKBzhyQ)

### 介绍

HTML（HyperText Markup Language，超文本标记语言）是 Web 的“骨架”。如果说 CSS “打扮”你的 HTML，而 JavaScript 让它“活”起来，那么 HTML 就是你 Web 应用的“身体”。HTML 的语法也反映了这个理念，因为它包含 “head”、“body”、“footer”等标签。

本课将使用 HTML 搭建我们虚拟生态瓶界面的“骨架”。它将包含一个标题和三列：左右两列放可拖拽的植物，中间区域是玻璃罐状的生态瓶。完成本课后，你能看到两列中的植物，但界面看起来还有点奇怪；别担心，下一课我们会用 CSS 美化它。

### 任务 1

在你的电脑上创建名为“terrarium”的文件夹，并在其中创建 `index.html`。你可以在 VS Code 中完成：新开一个 VS Code 窗口，点击“打开文件夹”，选择新建的文件夹；在资源管理器面板点击新建文件按钮，创建 `index.html`：

![explorer in VS Code](images/vs-code-index.png)

或者：

在 git bash 中执行命令：

- `mkdir terrarium`
- `cd terrarium`
- `touch index.html`
- `code index.html` 或 `nano index.html`

> `index.html` 告诉浏览器它是文件夹的默认文件；例如 `https://anysite.com/test` 这样的 URL 背后，可能就是一个名为 `test` 的文件夹，其中包含 `index.html`。URL 中不一定会显示 `index.html`。

---

## DocType 与 html 标签

HTML 文件的第一行是 doctype。把它放在最顶部有点反直觉，但这样可以告诉老旧浏览器按当前 HTML 规范以标准模式渲染页面。

> 小贴士：在 VS Code 中把鼠标悬停在标签上，可以看到来自 MDN 的参考说明。

第二行应为 `<html>` 的开始标签，当前紧随其后的是闭合标签 `</html>`。这对标签是你界面的根元素。

### 任务 2

在 `index.html` 的顶部加入以下内容：

```HTML
<!DOCTYPE html>
<html></html>
```

✅ 通过查询字符串设置 DocType 可以触发不同模式：[怪癖模式与标准模式](https://developer.mozilla.org/docs/Web/HTML/Quirks_Mode_and_Standards_Mode)。这些模式是为非常老的浏览器（如 Netscape Navigator 4、IE5）保留的。通常坚持使用标准 doctype 即可。

---

## 文档的 head

HTML 文档的 head 区域包含网页的关键信息，即[元数据](https://developer.mozilla.org/docs/Web/HTML/Element/meta)。本例中，我们告知将要渲染该页面的 Web 服务器如下信息：

- 页面标题
- 页面元数据，包括：
  - 字符集（character set），指出页面使用的字符编码
  - 浏览器信息，包括 `x-ua-compatible`（声明支持 IE=edge）
  - 视口（viewport）加载时的行为。把初始缩放设置为 1，可以控制页面首次加载时的缩放级别。

### 任务 3

在 `<html>` 的开始与结束标签之间，加入 `head` 代码块：

```html
<head>
  <title>Welcome to my Virtual Terrarium</title>
  <meta charset="utf-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
</head>
```

✅ 如果把 viewport 设置为 `<meta name="viewport" content="width=600">` 会发生什么？了解更多[视口](https://developer.mozilla.org/docs/Web/HTML/Viewport_meta_tag)。

---

## 文档的 body

### HTML 标签

在 HTML 中，通过在 .html 文件里添加标签来创建网页元素。每个标签通常都有一对起止标签，例如 `<p>hello</p>` 表示一个段落。现在在 `<html>` 标签对内部加入一对 `<body>` 标签；此时你的标记如下：

### 任务 4

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Welcome to my Virtual Terrarium</title>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
  </head>
  <body></body>
</html>
```

现在可以开始搭建页面了。通常我们使用 `<div>` 来创建页面中的各个区域。我们将创建一系列包含图片的 `<div>`。

### 图片（Images）

有一个不需要闭合标签的 HTML 标签是 `<img>`，因为它的 `src` 属性包含了渲染该元素所需的全部信息。

在你的应用中创建 `images` 文件夹，把[源码目录](../solution/images)中的图片复制进来（有 14 张植物图片）。

### 任务 5

把这些植物图片放进 `<body></body>` 之间的两列中：

```html
<div id="page">
  <div id="left-container" class="container">
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant1" src="./images/plant1.png" />
    </div>
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant2" src="./images/plant2.png" />
    </div>
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant3" src="./images/plant3.png" />
    </div>
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant4" src="./images/plant4.png" />
    </div>
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant5" src="./images/plant5.png" />
    </div>
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant6" src="./images/plant6.png" />
    </div>
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant7" src="./images/plant7.png" />
    </div>
  </div>
  <div id="right-container" class="container">
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant8" src="./images/plant8.png" />
    </div>
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant9" src="./images/plant9.png" />
    </div>
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant10" src="./images/plant10.png" />
    </div>
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant11" src="./images/plant11.png" />
    </div>
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant12" src="./images/plant12.png" />
    </div>
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant13" src="./images/plant13.png" />
    </div>
    <div class="plant-holder">
      <img class="plant" alt="plant" id="plant14" src="./images/plant14.png" />
    </div>
  </div>
</div>
```

> 说明：Span vs Div。Div 被视为“块级”元素，Span 是“行内”元素。如果把这些 div 改成 span，会发生什么？

加上这些标记后，植物会出现在屏幕上。现在它看起来还很糙，因为还没用 CSS 美化；我们会在下一课处理。

每张图片都有 alt 文本，即使看不到或无法渲染图片也能显示。这是一个很重要的可访问性属性。之后的课程会讲更多，但现在请记住：当用户因为网络慢、src 出错或使用屏幕阅读器等原因无法查看图片时，alt 属性可以提供替代信息。

✅ 你注意到每张图片的 alt 都是一样的吗？这是好实践吗？为什么？可以怎么改进？

---

## 语义化标记（Semantic markup）

一般来说，编写 HTML 时尽量使用有意义的“语义”。这意味着你用 HTML 标签去表达它们被设计时所代表的数据或交互类型。例如，页面的主标题应使用 `<h1>`。

在 `<body>` 起始标签下方加入：

```html
<h1>My Terrarium</h1>
```

使用语义化标记（如标题用 `<h1>`、无序列表用 `<ul>`）有助于屏幕阅读器在页面中导航。通常，按钮应写成 `<button>`，列表项用 `<li>`。虽然也可以用带点击处理器的 `<span>` 伪装按钮，但若元素看起来就是按钮，辅助技术更容易定位与操作它。因此尽量使用语义化标记。

✅ 看看屏幕阅读器是如何[与网页交互](https://www.youtube.com/watch?v=OUDV1gqs9GA)的。你能理解为何“非语义化”的标记会让用户受挫吗？

## 生态瓶

界面的最后一部分是创建一段将来由 CSS 美化的标记，用来呈现生态瓶。

### 任务

在最后一个 `</div>` 标签上方加入：

```html
<div id="terrarium">
  <div class="jar-top"></div>
  <div class="jar-walls">
    <div class="jar-glossy-long"></div>
    <div class="jar-glossy-short"></div>
  </div>
  <div class="dirt"></div>
  <div class="jar-bottom"></div>
</div>
```

✅ 虽然你加入了这段标记，但屏幕上毫无变化。为什么？

---

## 🚀Challenge

HTML 里有些“上古”标签挺好玩，但你不应该在项目中使用[此类废弃标签](https://developer.mozilla.org/docs/Web/HTML/Element#Obsolete_and_deprecated_elements)。不过你能否用老旧的 `<marquee>` 让 h1 标题横向滚动？（做完记得撤销）

## 课后测验

[课后测验](https://ff-quizzes.netlify.app/web/quiz/16)

## 回顾与自学

HTML 是“久经考验”的构建体系，支撑着今天的 Web。了解一些历史：研究旧标签与新标签。你能找出哪些标签为何被弃用、哪些被加入？未来可能引入哪些标签？

在 [Microsoft Learn](https://docs.microsoft.com/learn/modules/build-simple-website/?WT.mc_id=academic-77807-sagibbon) 学更多关于为 Web 与移动设备构建站点的知识。

## 作业

[练习 HTML：制作博客样机](assignment.md)
