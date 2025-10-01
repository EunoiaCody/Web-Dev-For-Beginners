# JavaScript 基础：数组与循环（Arrays and Loops）

![JavaScript Basics - Arrays](../../sketchnotes/webdev101-js-arrays.png)
> 手绘笔记作者：[Tomomi Imura](https://twitter.com/girlie_mac)

## 课前测验

[课前测验](https://ff-quizzes.netlify.app/web/quiz/13)

本课继续介绍 JavaScript 的基础。你将学习用于处理数据的“数组（arrays）”与“循环（loops）”。

[![Arrays](https://img.youtube.com/vi/1U4qTyq02Xw/0.jpg)](https://youtube.com/watch?v=1U4qTyq02Xw "Arrays")

[![Loops](https://img.youtube.com/vi/Eeh7pxtTZ3k/0.jpg)](https://www.youtube.com/watch?v=Eeh7pxtTZ3k "Loops")

> 🎥 点击上方图片，观看关于数组与循环的视频。

> 你也可以在 [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-arrays/?WT.mc_id=academic-77807-sagibbon) 上学习本课！

## 数组（Arrays）

在任何语言里，处理数据都是常见任务；当数据以结构化形式组织（例如数组）时，处理起来就容易得多。数组以类似“列表”的结构存储数据。数组的一个巨大优势是：它可以在同一个数组中存储不同类型的数据。

✅ 数组无处不在！想想生活中的“数组”例子，比如“太阳能电池板阵列（array）”。

数组的语法是方括号：

```javascript
let myArray = [];
```

这是一个空数组。当然，也可以在声明时就填充数据。数组内多个值之间用逗号分隔：

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
```

数组中的每个值都有一个唯一的编号，称为“索引（index）”，它按距离数组起始处的距离，从 0 开始计数。上例中，字符串 "Chocolate" 的索引是 0，而 "Rocky Road" 的索引是 4。使用方括号加索引来读取、修改或插入数组值。

✅ 数组从 0 开始计数这点是否让你惊讶？在一些语言中，索引从 1 开始。背后有一段历史，可以[在维基百科上阅读](https://en.wikipedia.org/wiki/Zero-based_numbering)。

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors[2]; //"Vanilla"
```

你可以利用索引修改一个值：

```javascript
iceCreamFlavors[4] = "Butter Pecan"; //Changed "Rocky Road" to "Butter Pecan"
```

也可以在给定索引处插入一个新值：

```javascript
iceCreamFlavors[5] = "Cookie Dough"; //Added "Cookie Dough"
```

✅ 更常见的向数组添加值的方式是使用数组方法，如 `array.push()`。

要知道数组里有多少项，使用 `length` 属性：

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors.length; //5
```

✅ 现在就试试！在浏览器控制台里创建并操作一个你自己的数组。

## 循环（Loops）

循环允许我们执行重复或“迭代（iterative）”的任务，能节省大量时间与代码。每次迭代都可以有不同的变量、数值和条件。JavaScript 中有多种循环，它们略有差异，但本质上都是“遍历数据”。

### for 循环（For Loop）

`for` 循环需要 3 个部分：

- `counter` 计数器变量，通常初始化为一个数字，用于统计迭代次数
- `condition` 条件表达式，使用比较运算符，在其为 `false` 时停止循环
- `iteration-expression` 每次迭代结束时运行，通常用于改变计数器的值

```javascript
// Counting up to 10
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

✅ 在浏览器控制台运行这段代码。稍微改变计数器、条件或迭代表达式，会发生什么？你能让它“倒着数”，做一个倒计时吗？

### while 循环（While loop）

与 `for` 的语法不同，`while` 只需要一个条件；当条件变为 `false` 时停止循环。循环中的条件通常依赖其它值，比如计数器，因此必须在循环期间进行管理。计数器的初始值需要在循环外创建，满足条件所需的表达式（包括更新计数器）需要在循环内维护。

```javascript
//Counting up to 10
let i = 0;
while (i < 10) {
 console.log(i);
 i++;
}
```

✅ 何时选 for，何时用 while？这个问题在 StackOverflow 上也有很多讨论，[也许对你有启发](https://stackoverflow.com/questions/39969145/while-loops-vs-for-loops-in-javascript)。

## 循环与数组（Loops and Arrays）

数组常与循环一起使用，因为大多数终止条件都需要用到数组的 `length`，而索引也常作为计数器的值。

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];

for (let i = 0; i < iceCreamFlavors.length; i++) {
  console.log(iceCreamFlavors[i]);
} //Ends when all flavors are printed
```

✅ 在浏览器控制台里试着遍历你自己的数组。

---

## 🚀 挑战

除了 for 与 while，还有其他遍历数组的方式：如 [forEach](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)、[for-of](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/for...of) 与 [map](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/map)。用其中一种改写你的数组遍历代码。

## 课后测验

[课后测验](https://ff-quizzes.netlify.app/web/quiz/14)

## 回顾与自学

JavaScript 的数组拥有许多方法，对数据处理非常有用。[阅读这些方法](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)，并在你创建的数组上尝试（例如 push、pop、slice、splice）。

## 作业

[Loop an Array](assignment.md)
