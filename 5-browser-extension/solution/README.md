# 碳触发浏览器扩展：完整代码

使用 tmrow 的 C02 Signal API 跟踪电力使用情况，构建一个浏览器扩展，这样您就可以直接在浏览器中得到关于您所在地区的电力使用强度的提醒。使用这个扩展将帮助您根据这些信息对您的活动做出判断。

![扩展截图](../extension-screenshot.png)

## 开始使用

您需要安装 [npm](https://npmjs.com)。将此代码的副本下载到您计算机上的一个文件夹中。

安装所有必需的包：

```
npm install
```

从 webpack 构建扩展

```
npm run build
```

To install on Edge, use the 'three dot' menu on the top right corner of the browser to find the Extensions panel. From there, select 'Load Unpacked' to load a new extension. Open the 'dist' folder at the prompt and the extension will load. To use it, you will need an API key for CO2 Signal's API ([get one here via email](https://www.co2signal.com/) - enter your email in the box on this page) and the [code for your region](http://api.electricitymap.org/v3/zones) corresponding to the [Electricity Map](https://www.electricitymap.org/map) (in Boston, for example, I use 'US-NEISO').

![installing](../install-on-edge.png)

Once the API key and region is input into the extension interface, the colored dot in the browser extension bar should change to reflect your region's energy usage and give you a pointer on what energy-heavy activities would be appropriate for you to perform. The concept behind this 'dot' system was given to me by the [Energy Lollipop extension](https://energylollipop.com/) for California emissions.

