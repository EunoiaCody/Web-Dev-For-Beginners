# 浏览器扩展项目 第 1 部分：关于浏览器的一切

![Browser sketchnote](../../sketchnotes/browser.jpg)
> 由 [Wassim Chegham](https://dev.to/wassimchegham/ever-wondered-what-happens-when-you-type-in-a-url-in-an-address-bar-in-a-browser-3dob) 绘制的速记图

## 课前测验

[Pre-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/23)

### 介绍

浏览器扩展可以为浏览器添加额外功能。但在开始构建之前，你应先了解一些浏览器的工作方式。

### 关于浏览器

在这一系列课程中，你将学习如何构建一个可在 Chrome、Firefox 和 Edge 上运行的浏览器扩展。本部分将带你了解浏览器的工作原理，并搭建扩展的基础结构。

那么，浏览器究竟是什么？它是一种软件应用，允许终端用户从服务器获取内容并在网页上展示。

✅ 小知识：第一个浏览器名为“WorldWideWeb”，由蒂姆·伯纳斯-李爵士于 1990 年创建。

![early browsers](images/earlybrowsers.jpg)
> 一些早期浏览器，来源于 [Karen McGrane](https://www.slideshare.net/KMcGrane/week-4-ixd-history-personal-computing)

当用户使用 URL（统一资源定位符）地址连接到互联网时（通常通过 `http` 或 `https` 的超文本传输协议），浏览器会与 Web 服务器通信并获取网页。

随后，浏览器的渲染引擎会将其显示在用户设备上，可能是手机、台式机或笔记本电脑。

浏览器还可以缓存内容，这样就不必每次都从服务器获取。它们可以记录用户的浏览历史，存储“cookie”（包含用于记录用户活动信息的小数据片段），等等。

需要牢记的一点是：浏览器并不完全相同！每种浏览器都有其优缺点，专业的 Web 开发者需要了解如何让网页在不同浏览器中都能良好运行。这也包括适配小屏幕（如手机）以及离线用户。

有一个非常实用的网站值得在你常用的浏览器中收藏：[caniuse.com](https://www.caniuse.com)。在构建网页时，使用 caniuse 提供的技术支持情况列表会很有帮助，从而更好地支持你的用户。

✅ 如何判断你的网站用户群最常用哪些浏览器？查看你的分析数据——在 Web 开发流程中可以安装各种分析工具，它们会告诉你哪些浏览器最受用户青睐。

## 浏览器扩展

为什么要构建浏览器扩展？当你需要快速执行一些重复任务时，将它附加在浏览器上会很方便。例如，如果你经常需要检查网页上的颜色，可以安装一个取色器扩展；如果你难以记住密码，可以使用密码管理扩展。

开发浏览器扩展本身也很有趣。它们通常只处理有限的一组任务，但能做得很好。

✅ 你最喜欢的浏览器扩展有哪些？它们完成了哪些任务？

### 安装扩展

在开始构建之前，先了解一下开发与部署浏览器扩展的流程。尽管每个浏览器在具体操作上略有差异，但 Chrome 和 Firefox 与 Edge 的流程大体类似：

![screenshot of the Edge browser showing the open edge://extensions page and open settings menu](images/install-on-edge.png)

> 注意：确保开启开发者模式，并允许安装来自其他商店的扩展。

简而言之，流程如下：

- 使用 `npm run build` 构建你的扩展
- 在浏览器中，点击右上角“设置及更多”（`...` 图标）进入扩展面板
- 如果是首次安装，选择 `load unpacked`，从构建输出目录上传扩展（本项目为 `/dist`）
- 如需重载已安装的扩展，点击 `reload`

✅ 以上步骤适用于你自己构建的扩展；若要安装各浏览器扩展商店中发布的扩展，请前往相应[商店](https://microsoftedge.microsoft.com/addons/Microsoft-Edge-Extensions-Home)进行选择与安装。

### 开始上手

你将构建一个浏览器扩展，用于显示你所在地区的碳足迹，包括能源使用情况及其来源。该扩展包含一个表单，用于收集 API 密钥，以访问 CO2 Signal 的 API。

**你需要准备：**

- [一个 API 密钥](https://www.co2signal.com/)：在页面输入你的邮箱，系统会把密钥发送给你
- 与 [Electricity Map](https://www.electricitymap.org/map) 对应的[你所在地区的代码](http://api.electricitymap.org/v3/zones)（例如在波士顿，我使用 “US-NEISO”）
- [起始代码](../start)。下载 `start` 文件夹；你将在此文件夹中补全代码
- [NPM](https://www.npmjs.com) —— NPM 是一个包管理工具；在本地安装它后，即可根据 `package.json` 安装项目所需包

✅ 想了解更多包管理知识，可参阅这个[出色的 Learn 模块](https://docs.microsoft.com/learn/modules/create-nodejs-project-dependencies/?WT.mc_id=academic-77807-sagibbon)

花一点时间浏览下代码库结构：

dist
    -|manifest.json (defaults set here)
    -|index.html (front-end HTML markup here)
    -|background.js (background JS here)
    -|main.js (built JS)
src
    -|index.js (your JS code goes here)

✅ 拿到 API 密钥与区域代码后，请将它们记录在便于查找的地方以备后用。

### 为扩展构建 HTML

该扩展包含两个视图。第一个用于收集 API 密钥与区域代码：

![screenshot of the completed extension open in a browser, displaying a form with inputs for region name and API key.](images/1.png)

第二个用于展示该区域的碳使用情况：

![screenshot of the completed extension displaying values for carbon usage and fossil fuel percentage for the US-NEISO region.](images/2.png)

我们先来编写表单的 HTML，并用 CSS 进行样式美化。

在 `/dist` 文件夹中，你将创建一个表单和一个结果区域。在 `index.html` 文件中，填充如下表单区域：

```HTML
<form class="form-data" autocomplete="on">
  <div>
    <h2>New? Add your Information</h2>
  </div>
  <div>
    <label for="region">Region Name</label>
    <input type="text" id="region" required class="region-name" />
  </div>
  <div>
    <label for="api">Your API Key from tmrow</label>
    <input type="text" id="api" required class="api-key" />
  </div>
  <button class="search-btn">Submit</button>
</form>
```

该表单用于输入并保存信息到本地存储。

接着，创建结果区域；在表单结束标签之后，添加如下 div：

```HTML
<div class="result">
  <div class="loading">loading...</div>
  <div class="errors"></div>
  <div class="data"></div>
  <div class="result-container">
    <p><strong>Region: </strong><span class="my-region"></span></p>
    <p><strong>Carbon Usage: </strong><span class="carbon-usage"></span></p>
    <p><strong>Fossil Fuel Percentage: </strong><span class="fossil-fuel"></span></p>
  </div>
  <button class="clear-btn">Change region</button>
</div>
```

此时可以尝试构建。请先安装扩展所需的依赖包：

```bash
npm install
```

该命令会使用 NPM（Node 包管理器）为扩展的构建流程安装 webpack。Webpack 是一个打包工具，负责编译代码。你可以在 `/dist/main.js` 查看输出——代码会被打包在一起。

现在扩展应该可以完成构建；如果将其作为扩展部署到 Edge，你会看到一个整齐显示的表单。

恭喜你，已经迈出了构建浏览器扩展的第一步。在接下来的课程中，你将让它变得更强大、更实用。

---

## 🚀 挑战

逛逛某个浏览器扩展商店并安装一个扩展到你的浏览器。用不同方式观察其文件结构，你发现了什么？

## 课后测验

[Post-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/24)

## 复习与自学

在本课中，你了解了一些 Web 浏览器的历史；借此机会多读读其历史，看看万维网的发明者如何设想它的使用方式。以下网站可能对你有帮助：

[The History of Web Browsers](https://www.mozilla.org/firefox/browsers/browser-history/)

[History of the Web](https://webfoundation.org/about/vision/history-of-the-web/)

[An interview with Tim Berners-Lee](https://www.theguardian.com/technology/2019/mar/12/tim-berners-lee-on-30-years-of-the-web-if-we-dream-a-little-we-can-get-the-web-we-want)

## 作业

[Restyle your extension](assignment.md)
