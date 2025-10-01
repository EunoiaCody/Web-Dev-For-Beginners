# JavaScript 基础：做出决策（Making Decisions）

![JavaScript Basics - Making decisions](../../sketchnotes/webdev101-js-decisions.png)

> 手绘笔记作者：[Tomomi Imura](https://twitter.com/girlie_mac)

## 课前测验

[课前测验](https://ff-quizzes.netlify.app/web/quiz/11)

做出决策并控制代码执行的顺序，能让你的代码更可复用、更健壮。本节介绍在 JavaScript 中控制数据流的语法，尤其是结合布尔（Boolean）类型时的重要性。

[![Making Decisions](https://img.youtube.com/vi/SxTp8j-fMMY/0.jpg)](https://youtube.com/watch?v=SxTp8j-fMMY "Making Decisions")

> 🎥 点击上方图片观看“Making Decisions”视频。

> 你也可以在 [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-if-else/?WT.mc_id=academic-77807-sagibbon) 上学习本课！

## 布尔值速览（Booleans）

布尔值只有两种：`true` 或 `false`。当满足某些条件时，布尔值帮助决定哪些代码行应该运行。

将布尔变量设为 true 或 false：

`let myTrueBool = true`
`let myFalseBool = false`

✅ 布尔（Boolean）一词来源于英国数学家、哲学家和逻辑学家 George Boole（1815–1864）。

## 比较运算符与布尔（Comparison Operators and Booleans）

用运算符做比较来评估条件，得到一个布尔值。常见运算符如下：

| 符号 | 描述 | 示例 |
| --- | --- | --- |
| `<` | **小于**：若左侧值小于右侧值，返回 `true` | `5 < 6 // true` |
| `<=` | **小于等于**：若左侧值小于或等于右侧值，返回 `true` | `5 <= 6 // true` |
| `>` | **大于**：若左侧值大于右侧值，返回 `true` | `5 > 6 // false` |
| `>=` | **大于等于**：若左侧值大于或等于右侧值，返回 `true` | `5 >= 6 // false` |
| `===` | **全等**：若左右两边值相等且类型相同，返回 `true` | `5 === 6 // false` |
| `!==` | **不全等**：与全等相反的布尔结果 | `5 !== 6 // true` |

✅ 在浏览器控制台里写几个比较表达式检验一下。有没有让你意外的结果？

## if 语句（If Statement）

如果条件为 true，if 语句会执行它的代码块：

```javascript
if (condition) {
  //Condition is true. Code in this block will run.
}
```

常用逻辑运算符来构造条件：

```javascript
let currentMoney;
let laptopPrice;

if (currentMoney >= laptopPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
}
```

## if..else 语句（If..Else Statement）

当条件为 false 时，可以使用 `else` 执行另一段代码；`else` 与 `if` 搭配使用，但它是可选的。

```javascript
let currentMoney;
let laptopPrice;

if (currentMoney >= laptopPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
} else {
  //Condition is false. Code in this block will run.
  console.log("Can't afford a new laptop, yet!");
}
```

✅ 在浏览器控制台里运行上面的代码，改改 `currentMoney` 与 `laptopPrice` 的值，观察 `console.log()` 的变化。

## switch 语句（Switch Statement）

`switch` 根据不同条件执行不同操作。使用 `switch` 选择要执行的众多代码块之一。

```javascript
switch (expression) {
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
  // code block
}
```

```javascript
// program using switch statement
let a = 2;

switch (a) {
  case 1:
    a = "one";
    break;
  case 2:
    a = "two";
    break;
  default:
    a = "not found";
    break;
}
console.log(`The value is ${a}`);
```

✅ 在浏览器控制台里运行并理解上述代码，修改变量 a 的值，观察 `console.log()` 的变化。

## 逻辑运算符与布尔（Logical Operators and Booleans）

有时做决定需要不止一次比较，可以把多个比较用逻辑运算符串联起来，得到一个布尔值。

| 符号 | 描述 | 示例 |
| --- | --- | --- |
| `&&` | **逻辑与**：比较两个布尔表达式，只有两边都为 true 才返回 true | `(5 > 6) && (5 < 6 ) //One side is false, other is true. Returns false` |
| `\|\|` | **逻辑或**：比较两个布尔表达式，任一边为 true 即返回 true | `(5 > 6) \|\| (5 < 6) //One side is false, other is true. Returns true` |
| `!` | **逻辑非**：返回布尔表达式相反的值 | `!(5 > 6) // 5 is not greater than 6, but "!" will return true` |

## 在条件里使用逻辑运算符（Conditions and Decisions with Logical Operators）

可以在 if..else 语句中使用逻辑运算符来构造条件：

```javascript
let currentMoney;
let laptopPrice;
let laptopDiscountPrice = laptopPrice - laptopPrice * 0.2; //Laptop price at 20 percent off

if (currentMoney >= laptopPrice || currentMoney >= laptopDiscountPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
} else {
  //Condition is true. Code in this block will run.
  console.log("Can't afford a new laptop, yet!");
}
```

### 取反运算符（Negation operator）

我们已经看到如何用 `if...else` 来实现条件逻辑。`if` 中的表达式都需要能求值为 true/false。使用 `!` 可以“取反”表达式：

```javascript
if (!condition) {
  // runs if condition is false
} else {
  // runs if condition is true
}
```

### 三元表达式（Ternary expressions）

表达条件逻辑不止 `if...else` 一种方式。还可以使用“三元运算符”，其语法如下：

```javascript
let variable = condition ? <return this if true> : <return this if false>
```

一个更直观的例子：

```javascript
let firstNumber = 20;
let secondNumber = 10;
let biggestNumber = firstNumber > secondNumber ? firstNumber : secondNumber;
```

✅ 花点时间多读几遍上面的代码。你理解这些运算符的工作方式了吗？

上面的意思是：

- 如果 `firstNumber` 大于 `secondNumber`
- 则把 `firstNumber` 赋给 `biggestNumber`
- 否则赋值为 `secondNumber`。

三元表达式只是下面这段代码的紧凑写法：

```javascript
let biggestNumber;
if (firstNumber > secondNumber) {
  biggestNumber = firstNumber;
} else {
  biggestNumber = secondNumber;
}
```

---

## 🚀 挑战

先用逻辑运算符写一个小程序，再把它改写成三元表达式版。你更喜欢哪种语法？

---

## 课后测验

[课后测验](https://ff-quizzes.netlify.app/web/quiz/12)

## 回顾与自学

在 [MDN](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators) 上阅读更多关于可用运算符的资料。

也可以看看 Josh Comeau 精彩的[运算符速查表](https://joshwcomeau.com/operator-lookup/)！

## 作业

[Operators](assignment.md)
