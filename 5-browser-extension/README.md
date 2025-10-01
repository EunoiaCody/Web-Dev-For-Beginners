# 构建浏览器扩展

在构建另一类 Web 资源的同时，开发浏览器扩展也是审视应用性能的一种有趣方式。本模块包含以下课程：浏览器的工作原理与扩展的部署、如何构建表单、调用 API 并使用本地存储，以及如何评估并提升你的网站性能。

你将构建一个可在 Edge、Chrome 和 Firefox 上运行的浏览器扩展。这个扩展类似一个为特定任务定制的迷你网站：它会通过 [C02 Signal API](https://www.co2signal.com) 查询指定地区的用电情况与碳强度，并返回该地区的碳足迹读数。

当用户在表单中输入 API 密钥与区域代码后，便可随时调用该扩展以查询当地用电情况，从而为用户的用电决策提供参考。例如，在你所在地区用电高峰期（高碳强度时段），最好延后使用烘干机等高碳排活动。

## 主题

1. [关于浏览器](1-about-browsers/README.md)
2. [表单与本地存储](2-forms-browsers-local-storage/README.md)
3. [后台任务与性能](3-background-tasks-and-performance/README.md)

### 图片说明

![a green browser extension](extension-screenshot.png)

## 致谢

这个“网页碳触发器”的想法来自 Asim Hussain，他是微软 Green Cloud Advocacy 团队的负责人，也是 [Green Principles](https://principles.green/) 的作者。它最初是一个[网站项目](https://github.com/jlooper/green)。

该浏览器扩展的结构受到 [Adebola Adeniran 的 COVID 扩展](https://github.com/onedebos/covtension) 的启发。

“圆点”图标系统的灵感来自加州排放浏览器扩展 [Energy Lollipop](https://energylollipop.com/) 的图标结构。

这些课程由 [Jen Looper](https://www.twitter.com/jenlooper) 倾心撰写 ♥️
