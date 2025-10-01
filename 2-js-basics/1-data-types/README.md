# JavaScript 基础：数据类型

![JavaScript Basics - Data types](../../sketchnotes/webdev101-js-datatypes.png)
> 手绘笔记作者：[Tomomi Imura](https://twitter.com/girlie_mac)

## 课前测验

[课前测验](https://ff-quizzes.netlify.app/web/)

本课介绍 JavaScript 的基础知识，这门语言为网页带来交互能力。

> 你也可以在 [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-variables/?WT.mc_id=academic-77807-sagibbon) 上学习本课！

[![Variables](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "Variables in JavaScript")

[![Data Types in JavaScript](https://img.youtube.com/vi/AWfA95eLdq8/0.jpg)](https://youtube.com/watch?v=AWfA95eLdq8 "Data Types in JavaScript")

> 🎥 点击上方图片，观看关于变量和数据类型的视频

让我们从变量以及填充在其中的数据类型开始！

## 变量（Variables）

变量用于存储值，这些值可以在代码中被使用并修改。

创建并“声明（declare）”一个变量的语法为：**[关键字] [名称]**，由两部分组成：

- **关键字（Keyword）**：可以是 `let` 或 `var`。

  ✅ `let` 在 ES6 中引入，赋予变量所谓的“块级作用域（block scope）”。推荐使用 `let` 而不是 `var`。我们会在后续课程更深入地讲解作用域。

- **变量名**：由你自行命名。

### 练习：使用变量

1. **声明变量**。使用 `let` 关键字声明变量：

    ```javascript
    let myVariable;
    ```

   现在已使用 `let` 声明了 `myVariable`，它当前还没有值。

1. **赋值**。使用 `=` 运算符为变量存储一个值：

    ```javascript
    myVariable = 123;
    ```

   > 注：本课中 `=` 表示“赋值运算符”，用于把一个值设置给变量，它不表示数学上的相等。

   现在 `myVariable` 已被初始化为 123。

1. **重构**。将你的代码替换为下面语句：

    ```javascript
    let myVariable = 123;
    ```

    当变量在声明的同时被赋值，这称为“显式初始化（explicit initialization）”。

1. **修改变量值**。用以下方式改变变量值：

   ```javascript
   myVariable = 321;
   ```

   一旦变量被声明，你可以在代码中的任何位置使用 `=` 和新值来更新它。

   ✅ 动手试试！你可以在浏览器里直接写 JavaScript。打开浏览器开发者工具，在控制台输入 `let myVariable = 123`，回车，再输入 `myVariable`。发生了什么？这些概念会在后续课程继续展开。

## 常量（Constants）

常量的声明与初始化与变量类似，区别在于关键字使用 `const`。常量通常以全大写命名。

```javascript
const MY_VARIABLE = 123;
```

常量与变量相似，但有两点例外：

- **必须有值**：常量必须在声明时初始化，否则运行时会报错。
- **引用不可变**：一旦初始化，常量的引用不能被改变，否则运行时会报错。看两个例子：
  - **简单值**（不允许）：

      ```javascript
      const PI = 3;
      PI = 4; // 不允许
      ```

  - **对象引用受保护**（不允许）：

      ```javascript
      const obj = { a: 3 };
      obj = { b: 5 } // 不允许
      ```

  - **对象的属性值不受保护**（允许）：

      ```javascript
      const obj = { a: 3 };
      obj.a = 5;  // 允许
      ```

      上面修改的是对象内部的值，而不是它本身的引用，因此是允许的。

   > 注：`const` 表示“引用”不可被重新赋值；值本身并非不可变（immutable），尤其当它是对象等复杂结构时。

## 数据类型（Data Types）

变量可以存储很多不同类型的值，比如数字或文本。这些不同类型被称为**数据类型**。数据类型是软件开发中的重要概念，它帮助开发者决定如何编写代码以及软件如何运行。另外，部分数据类型具有独特功能，能帮助转换或从一个值中提取额外信息。

✅ 数据类型也被称为 JavaScript 的原始类型（primitives），是语言提供的最低层数据类型。共有 7 种原始类型：string、number、bigint、boolean、undefined、null、symbol。花一分钟想象它们各自代表什么：`zebra` 是什么？`0` 呢？`true` 呢？

### 数字（Numbers）

上一节中，`myVariable` 的值是数字类型。

`let myVariable = 123;`

变量可以存储所有类型的数字，包括小数或负数。数字还可以与算术运算符一起使用，详见下一节“算术运算符（Arithmetic Operators）”。

### 算术运算符（Arithmetic Operators）

执行算术运算时可以使用若干种运算符，部分如下：

| 符号 | 描述 | 示例 |
| --- | --- | --- |
| `+` | **加法**：计算两数之和 | `1 + 2 //expected answer is 3` |
| `-` | **减法**：计算两数之差 | `1 - 2 //expected answer is -1` |
| `*` | **乘法**：计算两数之积 | `1 * 2 //expected answer is 2` |
| `/` | **除法**：计算两数之商 | `1 / 2 //expected answer is 0.5` |
| `%` | **取余**：计算两数相除的余数 | `1 % 2 //expected answer is 1` |

✅ 试一试！在浏览器控制台里做一次算术运算。结果是否出乎意料？

### 字符串（Strings）

字符串是一组位于单引号或双引号之间的字符。

- `'This is a string'`
- `"This is also a string"`
- `let myString = 'This is a string value stored in a variable';`

写字符串时请加引号，否则 JavaScript 会把它当作变量名。

### 格式化字符串（Formatting Strings）

字符串是文本，有时需要进行格式化。

要**连接（concatenate）**两个或多个字符串（将它们拼接），使用 `+` 运算符：

```javascript
let myString1 = "Hello";
let myString2 = "World";

myString1 + myString2 + "!"; //HelloWorld!
myString1 + " " + myString2 + "!"; //Hello World!
myString1 + ", " + myString2 + "!"; //Hello, World!

```

✅ 为什么在 JavaScript 中 `1 + 1 = 2`，但 `'1' + '1' = 11`？想一想。那 `'1' + 1` 又如何？

**模板字面量（Template literals）** 是另一种格式化字符串的方法，它使用反引号（`）而不是引号。任何非常规文本都需要放在占位符`${}` 中，包括那些可能是字符串的变量：

```javascript
let myString1 = "Hello";
let myString2 = "World";

`${myString1} ${myString2}!` //Hello World!
`${myString1}, ${myString2}!` //Hello, World!
```

两种方法都能实现格式化目的，但模板字面量会更“忠实”地保留空格与换行。

✅ 何时使用模板字面量，何时用普通字符串？

### 布尔（Booleans）

布尔值只有两种：`true` 或 `false`。布尔值常用于在满足某些条件时决定执行哪些代码行。很多时候，会借助运算符来设置布尔值；你也常常会看到用运算符来初始化变量或更新其值。

- `let myTrueBool = true`
- `let myFalseBool = false`

✅ 如果一个变量在布尔上下文中被计算为 `true`，我们称之为 “truthy”。有趣的是，在 JavaScript 中[除非被定义为 falsy，否则一切皆 truthy](https://developer.mozilla.org/docs/Glossary/Truthy)。

---

## 🚀 挑战

JavaScript 偶尔会以“出人意料”的方式处理数据类型。查一查这些“坑”。例如：大小写敏感可能会咬你一口！在控制台试试：`let age = 1; let Age = 2; age == Age`（结果是 `false` —— 为什么？）。你还能找到哪些坑？

## 课后测验

[课后测验](https://ff-quizzes.netlify.app)

## 回顾与自学

看看这份[JavaScript 练习列表](https://css-tricks.com/snippets/javascript/)，试着完成一个。你学到了什么？

## 作业

[数据类型练习](assignment.md)
