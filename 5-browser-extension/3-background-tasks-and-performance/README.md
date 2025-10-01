# 浏览器扩展项目 第 3 部分：了解后台任务与性能

## 课前测验

[Pre-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/27)

### 介绍

在本模块前两课中，你学习了如何构建一个表单与用于展示从 API 获取数据的显示区域。这是一种非常标准的 Web 构建方式。你还学习了如何以异步方式获取数据。你的浏览器扩展已经接近完成。

接下来需要处理一些后台任务，包括刷新扩展图标的颜色。现在正是讨论浏览器如何管理此类任务的好时机。让我们在构建 Web 资源时，从性能的角度思考这些浏览器任务。

## Web 性能基础

> “网站性能归结于两点：页面加载有多快，页面上的代码运行有多快。”—— [Zack Grossbart](https://www.smashingmagazine.com/2012/06/javascript-profiling-chrome-developer-tools/)

如何让你的网站在各种设备、各种用户、各种情境下都飞快，这个话题非常庞大。无论是标准 Web 项目还是浏览器扩展，构建时请记住以下要点。

要确保网站高效运行，首先要做的是收集其性能数据。最佳起点就是浏览器的开发者工具。在 Edge 中，你可以点击“设置及更多”（右上角三点图标），前往“更多工具 > 开发人员工具”，然后打开 Performance 面板。也可以使用快捷键：Windows 上 `Ctrl` + `Shift` + `I`，Mac 上 `Option` + `Command` + `I`。

Performance 面板包含性能剖析工具。打开一个网站（例如：[https://www.microsoft.com](https://www.microsoft.com/?WT.mc_id=academic-77807-sagibbon)），点击“Record”开始录制，然后刷新站点。随时停止录制，即可查看用于“脚本、渲染、绘制”网站的各类例程：

![Edge profiler](./images/profiler.png)

✅ 参阅 Edge 中 Performance 面板的[微软文档](https://docs.microsoft.com/microsoft-edge/devtools-guide/performance/?WT.mc_id=academic-77807-sagibbon)

> 提示：若想更准确地读取网站启动时间，请清理浏览器缓存

在时间轴中选择片段，可放大查看页面加载期间发生的事件。

选择时间轴的一段区域并查看摘要窗格，可获得页面性能的快照：

![Edge profiler snapshot](./images/snapshot.png)

查看 Event Log 面板，核查是否存在耗时超过 15 ms 的事件：

![Edge event log](./images/log.png)

✅ 熟悉你的性能剖析器！在本网站打开开发者工具，看看是否存在瓶颈。加载最慢的资源是什么？最快的又是什么？

## 剖析检查清单

一般而言，在构建网站时有一些常见“问题区域”需要留心，避免在上线时踩坑。

**资源体积**：近年来 Web 越来越“臃肿”，加载也更慢，部分原因是图片体积与使用不当。

✅ 参考 [Internet Archive](https://httparchive.org/reports/page-weight) 了解页面体积等历史趋势。

良好实践是确保图片经过优化，并按合适的尺寸与分辨率交付给用户。

**DOM 遍历**：浏览器需要基于你的代码构建 DOM。为性能考虑，应尽量保持标签精简，只使用并样式化页面真正需要的元素。同理，多余的 CSS 可做优化；仅在某一页使用的样式不必放入全局样式表。

**JavaScript**：每位 JS 开发者都应注意“阻塞渲染”的脚本，它们会阻止 DOM 的继续遍历与绘制。可考虑为内联脚本加上 `defer`（如在 Terrarium 模块所示）。

✅ 在 [Site Speed Test](https://www.webpagetest.org/) 等网站上测试站点，了解衡量站点性能的常见检查项。

既然你已经了解了浏览器如何渲染资源，下面完成扩展的最后几步：

### 创建用于计算颜色的函数

在 `/src/index.js` 中，在一系列用于访问 DOM 的 `const` 变量之后，新增 `calculateColor()` 函数：

```JavaScript
function calculateColor(value) {
  let co2Scale = [0, 150, 600, 750, 800];
  let colors = ['#2AA364', '#F5EB4D', '#9E4229', '#381D02', '#381D02'];

  let closestNum = co2Scale.sort((a, b) => {
    return Math.abs(a - value) - Math.abs(b - value);
  })[0];
  console.log(value + ' is closest to ' + closestNum);
  let num = (element) => element > closestNum;
  let scaleIndex = co2Scale.findIndex(num);

  let closestColor = colors[scaleIndex];
  console.log(scaleIndex, closestColor);

  chrome.runtime.sendMessage({ action: 'updateIcon', value: { color: closestColor } });
}
```

这段代码做了什么？你会将上一课中 API 返回的“碳强度”作为参数传入，然后计算该值与颜色数组中各阈值的接近程度，最终得到对应的颜色，并把该颜色发送给 chrome runtime。

chrome.runtime 提供了用于处理各类后台任务的 [API](https://developer.chrome.com/extensions/runtime)，你的扩展正是借助它来实现：

> “使用 chrome.runtime API 可以获取后台页、返回清单详情，并在应用或扩展的生命周期中监听与响应事件。你还可以用它将相对 URL 转为绝对 URL。”

✅ 如果你在为 Edge 开发扩展，可能会惊讶为何使用 chrome 的 API。新版 Edge 基于 Chromium 引擎构建，因此也能使用这些工具。

> 注意：若要为浏览器扩展做性能剖析，应在扩展自身中打开开发者工具，因为它是独立的浏览器实例。

### 设置默认图标颜色

现在，在 `init()` 函数中，调用 chrome 的 `updateIcon` 操作，将图标默认设置为绿色：

```JavaScript
chrome.runtime.sendMessage({
  action: 'updateIcon',
    value: {
      color: 'green',
    },
});
```

### 调用函数并执行

接着，将刚创建的函数添加到 CO2 Signal API 返回的 promise 链中进行调用：

```JavaScript
//let CO2...
calculateColor(CO2);
```

最后，在 `/dist/background.js` 中添加监听器，以处理这些后台动作：

```JavaScript
chrome.runtime.onMessage.addListener(function (msg, sender, sendResponse) {
  if (msg.action === 'updateIcon') {
    chrome.browserAction.setIcon({ imageData: drawIcon(msg.value) });
  }
});
//borrowed from energy lollipop extension, nice feature!
function drawIcon(value) {
  let canvas = document.createElement('canvas');
  let context = canvas.getContext('2d');

  context.beginPath();
  context.fillStyle = value.color;
  context.arc(100, 100, 50, 0, 2 * Math.PI);
  context.fill();

  return context.getImageData(50, 50, 100, 100);
}
```

以上代码为后台任务管理器添加了一个消息监听器。当收到名为 `updateIcon` 的消息时，将使用 Canvas API 绘制相应颜色的图标。

✅ 你将在[太空游戏课程](../../6-space-game/2-drawing-to-canvas/README.md)中进一步学习 Canvas API。

现在，重新构建扩展（`npm run build`），刷新并启动扩展，观察图标颜色的变化。是不是该去跑腿或洗碗了？现在你知道了！

恭喜你，已构建出一个实用的浏览器扩展，并进一步了解了浏览器的工作方式与性能剖析方法。

---

## 🚀 挑战

找几个历史悠久的开源网站，根据它们的 GitHub 历史分析其在这些年里如何做性能优化（如果有的话）。最常见的痛点是什么？

## 课后测验

[Post-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/28)

## 复习与自学

考虑订阅一份[性能相关的 Newsletter](https://perf.email/)

在各浏览器的开发者工具中查看 Performance 面板，了解它们评估 Web 性能的方式。你发现了哪些主要差异？

## 作业

[分析某网站的性能](assignment.md)
