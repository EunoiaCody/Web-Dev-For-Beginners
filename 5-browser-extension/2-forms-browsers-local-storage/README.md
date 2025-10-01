# 浏览器扩展项目 第 2 部分：调用 API 与使用本地存储

## 课前测验

[Pre-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/25)

### 介绍

在本课中，你将通过提交扩展中的表单来调用一个 API，并在扩展中显示结果。此外，你还将学习如何将数据存储到浏览器的本地存储中，以便后续使用。

✅ 按照相应文件中的编号提示，将代码放到正确位置

### 在扩展中准备要操作的元素

至此，你已经为扩展构建了表单和结果区域的 HTML。从现在开始，你将主要在 `/src/index.js` 文件中逐步完善扩展。关于项目设置与构建流程，可参考[上一课](../1-about-browsers/README.md)。

在 `index.js` 中，先创建一些 `const` 变量，用于保存各字段对应的引用：

```JavaScript
// form fields
const form = document.querySelector('.form-data');
const region = document.querySelector('.region-name');
const apiKey = document.querySelector('.api-key');

// results
const errors = document.querySelector('.errors');
const loading = document.querySelector('.loading');
const results = document.querySelector('.result-container');
const usage = document.querySelector('.carbon-usage');
const fossilfuel = document.querySelector('.fossil-fuel');
const myregion = document.querySelector('.my-region');
const clearBtn = document.querySelector('.clear-btn');
```

所有这些字段都是通过它们的 CSS 类选择器引用的，正如你在上一课的 HTML 中设置的那样。

### 添加事件监听器

接着，为表单和“清除”按钮（重置表单）添加事件监听器，使得当用户提交表单或点击重置按钮时会触发逻辑；同时在文件底部调用初始化函数：

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ 注意这里是如何使用简写来监听 submit 与 click 事件的，以及事件对象是如何传给 handleSubmit 与 reset 函数的。你能用更“长”的方式写出等效代码吗？你更喜欢哪种？

### 完善 init() 与 reset() 函数

现在来编写扩展的初始化函数 `init()`：

```JavaScript
function init() {
  // if anything is in localStorage, pick it up
  const storedApiKey = localStorage.getItem('apiKey');
  const storedRegion = localStorage.getItem('regionName');

  // set icon to be generic green
  // todo

  if (storedApiKey === null || storedRegion === null) {
    // if we don't have the keys, show the form
    form.style.display = 'block';
    results.style.display = 'none';
    loading.style.display = 'none';
    clearBtn.style.display = 'none';
    errors.textContent = '';
  } else {
    // if we have saved keys/regions in localStorage, show results when they load
    displayCarbonUsage(storedApiKey, storedRegion);
    results.style.display = 'none';
    form.style.display = 'none';
    clearBtn.style.display = 'block';
  }
};

function reset(e) {
  e.preventDefault();
  // clear local storage for region only
  localStorage.removeItem('regionName');
  init();
}

```

这个函数里包含了一些有趣的逻辑。通读后你能看出它做了什么吗？

- 使用两个 `const` 检查用户是否在本地存储中保存了 APIKey 与区域代码
- 如果两者之一为 null，将表单的 display 设为 'block' 使其显示
- 隐藏结果、加载动画与清除按钮，并清空错误文本
- 如果存在密钥与区域，则启动如下流程：
  - 调用 API 获取碳强度数据
  - 隐藏结果区域
  - 隐藏表单
  - 显示重置按钮

在继续之前，了解一个浏览器中非常重要的概念会很有帮助：[LocalStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)。LocalStorage 提供了以 `key-value` 形式在浏览器中存储字符串的方式。通过 JavaScript 可以操作此类 Web 存储管理数据。LocalStorage 没有过期时间；而另一种 Web 存储 SessionStorage 会在浏览器关闭时清空。不同存储方式各有优缺点。

> 注意：你的浏览器扩展拥有独立的本地存储；主浏览器窗口是不同实例，行为也互不影响。

例如，你可以把 APIKey 设为一个字符串值；在 Edge 中通过“检查”网页（右键 -> 检查）进入 Application 面板即可查看存储内容。

![Local storage pane](images/localstorage.png)

✅ 想一想哪些情况下不应将数据存储在 LocalStorage 中。一般来说，把 API Key 放入 LocalStorage 并不是一个好主意！你能理解原因吗？在我们的案例中，因应用仅用于学习且不会发布到商店，我们暂时采用此方法。

需要注意的是，你可以通过 Web API 使用 `getItem()`、`setItem()` 或 `removeItem()` 操作 LocalStorage。这在各浏览器中都有广泛支持。

在实现 `init()` 中调用的 `displayCarbonUsage()` 之前，先编写处理初次表单提交的逻辑。

### 处理表单提交

创建一个名为 `handleSubmit` 的函数，它接收事件对象 `(e)`。阻止事件默认行为（此处我们不希望浏览器刷新），并调用 `setUpUser` 函数，传入 `apiKey.value` 与 `region.value`。这样即可使用表单中填入的两个值。

```JavaScript
function handleSubmit(e) {
  e.preventDefault();
  setUpUser(apiKey.value, region.value);
}
```

✅ 温习一下：你在上一课设置的 HTML 中有两个输入框，其 `value` 是通过文件顶部定义的 `const` 获取的，并且它们都设置了 `required`，浏览器会阻止用户提交空值。

### 设置用户信息

接下来是 `setUpUser` 函数，在这里你将设置本地存储中的 apiKey 与 regionName。添加如下函数：

```JavaScript
function setUpUser(apiKey, regionName) {
  localStorage.setItem('apiKey', apiKey);
  localStorage.setItem('regionName', regionName);
  loading.style.display = 'block';
  errors.textContent = '';
  clearBtn.style.display = 'block';
  // make initial call
  displayCarbonUsage(apiKey, regionName);
}
```

该函数在调用 API 期间会显示加载信息。到这里，我们来编写本扩展中最重要的函数！

### 显示碳强度

终于，开始请求 API！

在继续之前，先简单介绍一下 API。API（[应用程序编程接口](https://www.webopedia.com/TERM/A/API.html)）是 Web 开发者工具箱中的关键组成部分，它提供了程序间交互的标准方式。比如，当你的网站需要查询数据库时，可能会有人为你提供一个可用的 API。API 有很多类型，其中最常见的一类是 [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/)。

✅ “REST” 是 “Representational State Transfer（表述性状态转移）” 的缩写，其特点是通过不同配置的 URL 获取数据。可以花点时间研究几种常见的 API 类型，看看你更喜欢哪一种。

关于这个函数，有几点需要注意。首先，注意到这里使用了 [`async` 关键字](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function)。将函数写成异步意味着它会等待某个操作（例如数据返回）完成后再继续执行。

这里有一个关于 `async` 的短视频：

[![Async and Await for managing promises](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "Async and Await for managing promises")

> 🎥 点击上方图片观看 async/await 的讲解视频。

创建一个新函数以查询 CO2 Signal API：

```JavaScript
import axios from '../node_modules/axios';

async function displayCarbonUsage(apiKey, region) {
  try {
    await axios
      .get('https://api.co2signal.com/v1/latest', {
        params: {
          countryCode: region,
        },
        headers: {
          'auth-token': apiKey,
        },
      })
      .then((response) => {
        let CO2 = Math.floor(response.data.data.carbonIntensity);

        // calculateColor(CO2);

        loading.style.display = 'none';
        form.style.display = 'none';
        myregion.textContent = region;
        usage.textContent =
          Math.round(response.data.data.carbonIntensity) + ' grams (grams C02 emitted per kilowatt hour)';
        fossilfuel.textContent =
          response.data.data.fossilFuelPercentage.toFixed(2) +
          '% (percentage of fossil fuels used to generate electricity)';
        results.style.display = 'block';
      });
  } catch (error) {
    console.log(error);
    loading.style.display = 'none';
    results.style.display = 'none';
    errors.textContent = 'Sorry, we have no data for the region you have requested.';
  }
}
```

这是一个比较长的函数，它做了什么？

- 按最佳实践，使用 `async` 让函数以异步方式运行。函数包含 `try/catch`，因为当 API 返回数据时会涉及 Promise。由于无法控制 API 的响应速度（甚至可能不响应），因此需要通过异步方式处理这种不确定性。
- 使用 API Key 调用 co2signal API 获取你所在地区的数据。为使用该密钥，需要在请求头中进行授权设置。
- 当 API 有响应后，将响应数据的各部分赋值给你在界面中准备好的显示区域。
- 如果出现错误或没有结果，则显示错误消息。

✅ 使用异步编程模式是你的又一项重要技能。阅读[这篇文档](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function)了解可配置此类代码的多种方式。

恭喜！当你构建扩展（`npm run build`）并在扩展面板中刷新后，就会得到一个可运行的扩展！唯一尚未工作的部分是图标，我们会在下一课中修复它。

---

## 🚀 挑战

在这几节课中我们讨论了若干 API。选择一个 Web API 深入了解它提供的内容。例如，你可以看看浏览器中可用的 API，如 [HTML 拖放 API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API)。在你看来，优秀的 API 应具备什么？

## 课后测验

[Post-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/26)

## 复习与自学

本课你学习了 LocalStorage 与 API，这两者对专业的 Web 开发者都很有用。思考一下它们如何协同工作？设想你会如何设计网站来存储将被 API 使用的条目。

## 作业

[Adopt an API](assignment.md)
