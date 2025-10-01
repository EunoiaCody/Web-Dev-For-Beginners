# 构建太空游戏 第 1 部分：介绍

![视频](../images/pewpew.gif)

## 课前测验

[课前测验](https://ff-quizzes.netlify.app/web/quiz/29)

### 游戏开发中的继承和组合

在之前的课程中，您构建的应用程序范围很小，因此不需要太担心设计架构。但是，当您的应用程序在规模和范围上增长时，架构决策就成为一个更大的关注点。在 JavaScript 中创建大型应用程序有两种主要方法：*组合*或*继承*。两者都有优缺点，但让我们从游戏的上下文中解释它们。

✅ 有史以来最著名的编程书籍之一与[设计模式](https://en.wikipedia.org/wiki/Design_Patterns)有关。

在游戏中，您有 `游戏对象`，它们是存在于屏幕上的对象。这意味着它们在笛卡尔坐标系中有一个位置，特征是有 `x` 和 `y` 坐标。当您开发游戏时，您会注意到所有游戏对象都有一个标准属性，这对您创建的每个游戏都很常见，即元素：

- **基于位置** 大多数（如果不是全部）游戏元素都基于位置。这意味着它们有一个位置，一个 `x` 和 `y`。
- **可移动** 这些是可以移动到新位置的对象。这通常是英雄、怪物或 NPC（非玩家角色），但不是例如树这样的静态对象。
- **自我毁灭** 这些对象只存在一段设定的时间，然后它们会将自己设置为删除。通常这由一个 `dead` 或 `destroyed` 布尔值表示，向游戏引擎发出信号，表明此对象不应再被渲染。
- **冷却** '冷却'是短期对象中的典型属性。典型的例子是一段文本或图形效果，如爆炸，应该只能看到几毫秒。

✅ Think about a game like Pac-Man. Can you identify the four object types listed above in this game?

### Expressing behavior

All we described above are behavior that game objects can have. So how do we encode those? We can express this behavior as methods associated to either classes or objects.

**Classes**

The idea is to use `classes` in conjunction with `inheritance` to accomplish adding a certain behavior to a class.

✅ Inheritance is an important concept to understand. Learn more on [MDN's article about inheritance](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain).

Expressed via code, a game object can typically look like this:

```javascript

//set up the class GameObject
class GameObject {
  constructor(x, y, type) {
    this.x = x;
    this.y = y;
    this.type = type;
  }
}

//this class will extend the GameObject's inherent class properties
class Movable extends GameObject {
  constructor(x,y, type) {
    super(x,y, type)
  }

//this movable object can be moved on the screen
  moveTo(x, y) {
    this.x = x;
    this.y = y;
  }
}

//this is a specific class that extends the Movable class, so it can take advantage of all the properties that it inherits
class Hero extends Movable {
  constructor(x,y) {
    super(x,y, 'Hero')
  }
}

//this class, on the other hand, only inherits the GameObject properties
class Tree extends GameObject {
  constructor(x,y) {
    super(x,y, 'Tree')
  }
}

//a hero can move...
const hero = new Hero();
hero.moveTo(5,5);

//but a tree cannot
const tree = new Tree();
```

✅ Take a few minutes to re-envision a Pac-Man hero (Inky, Pinky or Blinky, for example) and how it would be written in JavaScript. 

**Composition**

A different way of handling object inheritance is by using *Composition*. Then, objects express their behavior like this:

```javascript
//create a constant gameObject
const gameObject = {
  x: 0,
  y: 0,
  type: ''
};

//...and a constant movable
const movable = {
  moveTo(x, y) {
    this.x = x;
    this.y = y;
  }
}
//then the constant movableObject is composed of the gameObject and movable constants
const movableObject = {...gameObject, ...movable};

//then create a function to create a new Hero who inherits the movableObject properties
function createHero(x, y) {
  return {
    ...movableObject,
    x,
    y,
    type: 'Hero'
  }
}
//...and a static object that inherits only the gameObject properties
function createStatic(x, y, type) {
  return {
    ...gameObject
    x,
    y,
    type
  }
}
//create the hero and move it
const hero = createHero(10,10);
hero.moveTo(5,5);
//and create a static tree which only stands around
const tree = createStatic(0,0, 'Tree'); 
```

**Which pattern should I use?**

It's up to you which pattern you choose. JavaScript supports both these paradigms.

--

Another pattern common in game development addresses the problem of handling the game's user experience and performance.

## Pub/sub pattern

✅ Pub/Sub stands for 'publish-subscribe'

This pattern addresses the idea that the disparate parts of your application shouldn't know about one another. Why is that? It makes it a lot easier to see what's going on in general if various parts are separated. It also makes it easier to suddenly change behavior if you need to. How do we accomplish this? We do this by establishing some concepts:

- **message**: A message is usually a text string accompanied by an optional payload (a piece of data that clarifies what the message is about). A typical message in a game can be `KEY_PRESSED_ENTER`.
- **publisher**: This element *publishes* a message and sends it out to all subscribers.
- **subscriber**: This element *listens* to specific messages and carries out some task as the result of receiving this message, such as firing a laser.

The implementation is quite small in size but it's a very powerful pattern. Here's how it can be implemented:

```javascript
//set up an EventEmitter class that contains listeners
class EventEmitter {
  constructor() {
    this.listeners = {};
  }
//when a message is received, let the listener to handle its payload
  on(message, listener) {
    if (!this.listeners[message]) {
      this.listeners[message] = [];
    }
    this.listeners[message].push(listener);
  }
//when a message is sent, send it to a listener with some payload
  emit(message, payload = null) {
    if (this.listeners[message]) {
      this.listeners[message].forEach(l => l(message, payload))
    }
  }
}

```

To use the above code we can create a very small implementation:

```javascript
//set up a message structure
const Messages = {
  HERO_MOVE_LEFT: 'HERO_MOVE_LEFT'
};
//invoke the eventEmitter you set up above
const eventEmitter = new EventEmitter();
//set up a hero
const hero = createHero(0,0);
//let the eventEmitter know to watch for messages pertaining to the hero moving left, and act on it
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});

//set up the window to listen for the keyup event, specifically if the left arrow is hit, emit a message to move the hero left
window.addEventListener('keyup', (evt) => {
  if (evt.key === 'ArrowLeft') {
    eventEmitter.emit(Messages.HERO_MOVE_LEFT)
  }
});
```

Above we connect a keyboard event, `ArrowLeft` and send the `HERO_MOVE_LEFT` message. We listen to that message and move the `hero` as a result. The strength with this pattern is that the event listener and the hero don't know about each other. You can remap the `ArrowLeft` to the `A` key. Additionally it would be possible to do something completely different on `ArrowLeft` by making a few edits to the eventEmitter's `on` function:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

As things gets more complicated when your game grows, this pattern stays the same in complexity and your code stays clean. It's really recommended to adopt this pattern.

---

## 🚀 Challenge

Think about how the pub-sub pattern can enhance a game. Which parts should emit events, and how should the game react to them? Now's your chance to get creative, thinking of a new game and how its parts might behave.

## Post-Lecture Quiz

[Post-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/30)

## Review & Self Study

Learn more about Pub/Sub by [reading about it](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon).

## Assignment

[Mock up a game](assignment.md)
