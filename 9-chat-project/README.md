# 聊天项目

这个聊天项目展示了如何使用 GitHub Models 构建聊天助手。

完成的项目如下所示：

![聊天应用](./assets/screenshot.png)

一些背景：使用生成式 AI 构建聊天助手是开始学习 AI 的绝佳方式。在本课程中，您将学习如何将生成式 AI 集成到 Web 应用程序中，让我们开始吧。

## 连接到生成式 AI

对于后端，我们使用 GitHub Models。这是一个让您免费使用 AI 的绝佳服务。前往其游乐场并获取对应您选择的后端语言的代码。这是 [GitHub Models 游乐场](https://github.com/marketplace/models/azure-openai/gpt-4o-mini/playground) 的样子

![GitHub Models AI 游乐场](./assets/playground.png)

如前所述，选择"Code"选项卡和您选择的运行时。

![游乐场选择](./assets/playground-choice.png)

### 使用 Python

在这种情况下我们选择 Python，这意味着我们选择这个代码：

```python
"""Run this model in Python

> pip install openai
"""
import os
from openai import OpenAI

# To authenticate with the model you will need to generate a personal access token (PAT) in your GitHub settings. 
# Create your PAT token by following instructions here: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens
client = OpenAI(
    base_url="https://models.github.ai/inference",
    api_key=os.environ["GITHUB_TOKEN"],
)

response = client.chat.completions.create(
    messages=[
        {
            "role": "system",
            "content": "",
        },
        {
            "role": "user",
            "content": "What is the capital of France?",
        }
    ],
    model="openai/gpt-4o-mini",
    temperature=1,
    max_tokens=4096,
    top_p=1
)

print(response.choices[0].message.content)
```

让我们稍微清理一下这段代码，使其可重用：

```python
def call_llm(prompt: str, system_message: str):
    response = client.chat.completions.create(
        messages=[
            {
                "role": "system",
                "content": system_message,
            },
            {
                "role": "user",
                "content": prompt,
            }
        ],
        model="openai/gpt-4o-mini",
        temperature=1,
        max_tokens=4096,
        top_p=1
    )

    return response.choices[0].message.content
```

有了这个函数 `call_llm`，我们现在可以接收一个提示词和一个系统提示词，函数最终返回结果。

### 自定义 AI 助手

如果您想自定义 AI 助手，可以通过填充系统提示词来指定您希望它的行为方式，如下所示：

```python
call_llm("Tell me about you", "You're Albert Einstein, you only know of things in the time you were alive")
```

## 通过 Web API 公开

太好了，我们完成了 AI 部分，让我们看看如何将其集成到 Web API 中。对于 Web API，我们选择使用 Flask，但任何 web 框架都应该可以。让我们看看代码：

### 使用 Python

```python
# api.py
from flask import Flask, request, jsonify
from llm import call_llm
from flask_cors import CORS

app = Flask(__name__)
CORS(app)   # *   example.com

@app.route("/", methods=["GET"])
def index():
    return "Welcome to this API. Call POST /hello with 'message': 'my message' as JSON payload"


@app.route("/hello", methods=["POST"])
def hello():
    # get message from request body  { "message": "do this taks for me" }
    data = request.get_json()
    message = data.get("message", "")

    response = call_llm(message, "You are a helpful assistant.")
    return jsonify({
        "response": response
    })

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

在这里，我们创建一个 flask API 并定义一个默认路由"/"和"/chat"。后者是我们前端用来向其传递问题的。

要在此处集成 *llm.py*，我们需要执行以下操作：

- 导入 `call_llm` 函数：

   ```python
   from llm import call_llm
   from flask import Flask, request
   ```

- 从"/chat"路由调用它：

   ```python
   @app.route("/hello", methods=["POST"])
   def hello():
      # get message from request body  { "message": "do this taks for me" }
      data = request.get_json()
      message = data.get("message", "")

      response = call_llm(message, "You are a helpful assistant.")
      return jsonify({
         "response": response
      })
   ```

   在这里我们解析传入的请求以从 JSON 正文中检索 `message` 属性。然后我们使用以下调用来调用 LLM：

   ```python
   response = call_llm(message, "You are a helpful assistant")

   # return the response as JSON
   return jsonify({
      "response": response 
   })
   ```

太好了，现在我们已经完成了需要做的事情。

## 配置 CORS

我们应该指出，我们设置了类似 CORS（跨源资源共享）的东西。这意味着因为我们的后端和前端将在不同的端口上运行，我们需要允许前端调用后端。

### 使用 Python

在 *api.py* 中有一段代码设置了这个：

```python
from flask_cors import CORS

app = Flask(__name__)
CORS(app)   # *   example.com
```

现在它被设置为允许"*"（所有来源），这有点不安全，一旦投入生产，我们应该限制它。

## 运行您的项目

要运行您的项目，您需要先启动后端，然后启动前端。

### 使用 Python

好的，我们有 *llm.py* 和 *api.py*，我们如何使用后端使其工作？嗯，我们需要做两件事：

- 安装依赖项：

   ```sh
   cd backend
   python -m venv venv
   source ./venv/bin/activate

   pip install openai flask flask-cors openai
   ```

- 启动 API

   ```sh
   python api.py
   ```

   如果您在 Codespaces 中，您需要在编辑器底部转到 Ports，右键单击它并点击"Port Visibility"，然后选择"Public"。

### 开发前端

现在我们有了一个运行的 API，让我们为此创建一个前端。一个最基本的前端，我们将逐步改进。在一个 *frontend* 文件夹中，创建以下内容：

```text
backend/
frontend/
index.html
app.js
styles.css
```

让我们从 **index.html** 开始：

```html
<html>
    <head>
        <link rel="stylesheet" href="styles.css">
    </head>
    <body>
      <form>
        <textarea id="messages"></textarea>
        <input id="input" type="text" />
        <button type="submit" id="sendBtn">Send</button>  
      </form>  
      <script src="app.js" />
    </body>
</html>    
```

上面是支持聊天窗口所需的绝对最小值，因为它包含一个用于渲染消息的 textarea、一个用于输入消息的 input 和一个用于将消息发送到后端的按钮。让我们接下来看看 *app.js* 中的 JavaScript

**app.js**

```js
// app.js

(function(){
  // 1. set up elements  
  const messages = document.getElementById("messages");
  const form = document.getElementById("form");
  const input = document.getElementById("input");

  const BASE_URL = "change this";
  const API_ENDPOINT = `${BASE_URL}/hello`;

  // 2. create a function that talks to our backend
  async function callApi(text) {
    const response = await fetch(API_ENDPOINT, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ message: text })
    });
    let json = await response.json();
    return json.response;
  }

  // 3. add response to our textarea
  function appendMessage(text, role) {
    const el = document.createElement("div");
    el.className = `message ${role}`;
    el.innerHTML = text;
    messages.appendChild(el);
  }

  // 4. listen to submit events
  form.addEventListener("submit", async(e) => {
    e.preventDefault();
   // someone clicked the button in the form
   
   // get input
   const text = input.value.trim();

   appendMessage(text, "user")

   // reset it
   input.value = '';

   const reply = await callApi(text);

   // add to messages
   appendMessage(reply, "assistant");

  })
})();
```

让我们按部分查看代码：

- 1) 在这里我们获取对所有元素的引用，稍后在代码中会用到
- 2) 在这个部分，我们创建一个使用内置 `fetch` 方法调用我们后端的函数
- 3) `appendMessage` 帮助添加响应以及您作为用户输入的内容。
- 4) 在这里我们监听提交事件，最终读取输入字段，将用户的消息放在文本区域中，调用 API，在文本区域中渲染该响应。

让我们接下来看看样式，这里您可以真正疯狂地让它看起来像您想要的样子，但这里有一些建议：

**styles.css**

```
.message {
    background: #222;
    box-shadow: 0 0 0 10px orange;
    padding: 10px:
    margin: 5px;
}

.message.user {
    background: blue;
}

.message.assistant {
    background: grey;
} 
```

使用这三个类，您将根据消息来自助手还是您作为用户而以不同方式设置消息样式。如果您想获得灵感，请查看 `solution/frontend/styles.css` 文件夹。

### 更改基础 URL

这里有一件我们没有设置的事情，那就是 `BASE_URL`，在您的后端启动之前这是未知的。设置它：

- 如果您在本地运行 API，它应该设置为类似 `http://localhost:5000` 的内容。
- 如果在 Codespaces 中运行，它应该看起来像"[name]app.github.dev"。

## 作业

创建您自己的 *project* 文件夹，内容如下：

```text
project/
  frontend/
    index.html
    app.js
    styles.css
  backend/
    ...
```

复制上面指导中的内容，但可以根据您的喜好自由定制

## 解决方案

[解决方案](./solution/README.md)

## 奖励

尝试更改 AI 助手的个性。

### 对于 Python

当您在 *api.py* 中调用 `call_llm` 时，您可以将第二个参数更改为您想要的内容，例如：

```python
call_llm(message, "You are Captain Picard")
```

### 前端

同样更改 CSS 和文本以适合您的喜好，所以在 *index.html* 和 *styles.css* 中做更改。

## 总结

太好了，您从头开始学会了如何使用 AI 创建个人助手。我们使用 GitHub Models、Python 后端以及 HTML、CSS 和 JavaScript 前端来完成此操作

## 使用 Codespaces 设置

- 导航到：[Web Dev For Beginners 仓库](https://github.com/microsoft/Web-Dev-For-Beginners)
- 从模板创建（确保您已登录 GitHub）在右上角：

    ![从模板创建](./assets/template.png)

- 进入您的仓库后，创建一个 Codespace：

    ![创建 codespace](./assets/codespace.png)

    这应该会启动一个您现在可以使用的环境。
