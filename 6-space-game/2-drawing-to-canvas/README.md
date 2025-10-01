# 构建太空游戏 第 2 部分：将英雄和怪物绘制到画布

## 课前测验

[课前测验](https://ff-quizzes.netlify.app/web/quiz/31)

## Canvas

Canvas 是一个 HTML 元素，默认情况下没有内容；它是一个空白画布。您需要通过在其上绘制来添加内容。

✅ 在 MDN 上阅读[更多关于 Canvas API 的信息](https://developer.mozilla.org/docs/Web/API/Canvas_API)。

通常它被声明为页面主体的一部分，如下所示：

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

在上面我们设置了 `id`、`width` 和 `height`。

- `id`：设置这个以便在需要与其交互时可以获得引用。
- `width`：这是元素的宽度。
- `height`：这是元素的高度。

## 绘制简单几何图形

Canvas 使用笛卡尔坐标系统来绘制事物。因此它使用 x 轴和 y 轴来表达某物的位置。位置 `0,0` 是左上角位置，右下角是您设置的 Canvas 的 WIDTH 和 HEIGHT。

![Canvas 的网格](canvas_grid.png)
> 图片来自 [MDN](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes)

To draw on the canvas element you will need to go through the following steps:

1. **Get a reference** to the Canvas element.
1. **Get a reference** on the Context element that sits on the canvas element.
1. **Perform a drawing operation** using the context element.

Code for the above steps usually looks like so:

```javascript
// draws a red rectangle
//1. get the canvas reference
canvas = document.getElementById("myCanvas");

//2. set the context to 2D to draw basic shapes
ctx = canvas.getContext("2d");

//3. fill it with the color red
ctx.fillStyle = 'red';

//4. and draw a rectangle with these parameters, setting location and size
ctx.fillRect(0,0, 200, 200) // x,y,width, height
```

✅ The Canvas API mostly focuses on 2D shapes, but you can also draw 3D elements to a web site; for this, you might use the [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API).

You can draw all sorts of things with the Canvas API like:

- **Geometrical shapes**, we've already showed how to draw a rectangle, but there is much more you can draw.
- **Text**, you can draw a text with any font and color you wish.
- **Images**, you can draw an image based off of an image asset like a .jpg or .png for example.

✅ Try it! You know how to draw a rectangle, can you draw a circle to a page? Take a look at some interesting Canvas drawings on CodePen. Here's a [particularly impressive example](https://codepen.io/dissimulate/pen/KrAwx).

## Load and draw an image asset

You load an image asset by creating an `Image` object and set its `src` property. Then you listen to the `load` event to know when it's ready to be used. The code looks like this:

### Load asset

```javascript
const img = new Image();
img.src = 'path/to/my/image.png';
img.onload = () => {
  // image loaded and ready to be used
}
```

### Load asset pattern

It's recommended to wrap the above in a construct like so, so it's easier to use and you only try to manipulate it when it's fully loaded:

```javascript
function loadAsset(path) {
  return new Promise((resolve) => {
    const img = new Image();
    img.src = path;
    img.onload = () => {
      // image loaded and ready to be used
      resolve(img);
    }
  })
}

// use like so

async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')
}

```

To draw game assets to a screen, your code would look like this:

```javascript
async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')

  canvas = document.getElementById("myCanvas");
  ctx = canvas.getContext("2d");
  ctx.drawImage(heroImg, canvas.width/2,canvas.height/2);
  ctx.drawImage(monsterImg, 0,0);
}
```

## Now it's time to start building your game

### What to build

You will build a web page with a Canvas element. It should render a black screen `1024*768`. We've provided you with two images:

- Hero ship

   ![Hero ship](solution/assets/player.png)

- 5*5 monster

   ![Monster ship](solution/assets/enemyShip.png)

### Recommended steps to start development

Locate the files that have been created for you in the `your-work` sub folder. It should contain the following:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

Open the copy of this folder in Visual Studio Code. You need to have a local development environment setup, preferably with Visual Studio Code with NPM and Node installed. If you don't have `npm` set up on your computer, [here's how to do that](https://www.npmjs.com/get-npm).

Start your project by navigating to the `your_work` folder:

```bash
cd your-work
npm start
```

The above will start a HTTP Server on address `http://localhost:5000`. Open up a browser and input that address. It's a blank page right now, but that will change

> Note: to see changes on your screen, refresh your browser.

### Add code

Add the needed code to `your-work/app.js` to solve the below

1. **Draw** a canvas with black background
   > tip: add two lines under the appropriate TODO in `/app.js`, setting the `ctx` element to be black and the top/left coordinates to be at 0,0 and the height and width to equal that of the canvas.
2. **Load** textures
   > tip: add the player and enemy images using `await loadTexture` and passing in the image path. You won't see them on the screen yet!
3. **Draw** hero in the center of the screen in the bottom half
   > tip: use the `drawImage` API to draw heroImg to the screen, setting  `canvas.width / 2 - 45` and `canvas.height - canvas.height / 4)`;
4. **Draw** 5*5 monsters
   > tip: Now you can uncomment the code to draw enemies on the screen. Next, go to the `createEnemies` function and build it out.

   First, set up some constants:

    ```javascript
    const MONSTER_TOTAL = 5;
    const MONSTER_WIDTH = MONSTER_TOTAL * 98;
    const START_X = (canvas.width - MONSTER_WIDTH) / 2;
    const STOP_X = START_X + MONSTER_WIDTH;
    ```

    then, create a loop to draw the array of monsters onto the screen:

    ```javascript
    for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          ctx.drawImage(enemyImg, x, y);
        }
      }
    ```

## Result

The finished result should look like so:

![Black screen with a hero and 5*5 monsters](partI-solution.png)

## Solution

Please try solving it yourself first but if you get stuck, have a look at a [solution](solution/app.js)

---

## 🚀 Challenge

You've learned about drawing with the 2D-focused Canvas API; take a look at the [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API), and try to draw a 3D object.

## Post-Lecture Quiz

[Post-lecture quiz](https://ff-quizzes.netlify.app/web/quiz/32)

## Review & Self Study

Learn more about the Canvas API by [reading about it](https://developer.mozilla.org/docs/Web/API/Canvas_API).

## Assignment

[Play with the Canvas API](assignment.md)