---
title: pixiJs 
date: 2025-03-02
author: "pzc"
cover: /assets/images/jpg/150.jpg
categories: [javaScript]
tags: [webgl,canvas]
---
## 来源

笔记来源：

[《从Canvas到PixiJs》专栏简介🔥🔥面对网页性能要求越来越高的今天，项目性能优化已经成了项目开发中必不可少的 - 掘金 (juejin.cn)](https://juejin.cn/post/7161696291469131806)

[欢迎 | PixiJS 中文网 (nodejs.cn)](https://pixi.nodejs.cn/8.x/guides)

## 介绍

PixiJS 是一个用于创建2D图形和互动内容的开源HTML5 JavaScript库。它专注于提供高性能的渲染引擎，使得开发者能够构建出流畅的动画和复杂的视觉效果，非常适合开发游戏、演示和其他需要丰富图形界面的应用程序。

### 主要特点：
- **跨平台兼容性**：PixiJS 能在多种平台上运行，包括桌面浏览器、移动设备等。
- **高性能渲染**：通过WebGL进行硬件加速渲染，同时在不支持WebGL的环境中回退使用Canvas 2D API，确保了良好的性能和广泛的兼容性。
- **易于使用的API**：PixiJS 提供了一套直观且易于学习的API，简化了2D图形编程的复杂度。
- **丰富的功能集**：包括精灵(Sprite)、文本渲染、滤镜效果、纹理管理和动画等功能，满足各种2D图形需求。
- **插件系统**：支持扩展，允许开发者添加自定义功能或集成第三方插件来增强PixiJS的功能。

PixiJS 广泛应用于网页游戏、广告、教育软件以及任何需要高质量2D图形表现的领域。无论是新手还是有经验的开发者，都可以利用PixiJS的强大功能来实现创意想法。如果你对开始使用PixiJS感兴趣，可以访问其官方网站获取更多资源和文档支持。

## 资料

要获取PixiJS的官方资料，你可以直接访问PixiJS的官方网站。官方网站是学习和使用PixiJS的最佳资源来源，提供了包括文档、教程、示例以及API参考在内的丰富内容。

这里是如何开始的几个步骤：

1. **访问官方网站**：前往 [PixiJS官网](https://pixijs.com/) 可以找到最新的信息和资源。
2. **阅读文档**：在官网上，你可以找到详细的[文档](https://pixijs.download/dev/docs/index.html)，这些文档涵盖了从入门到高级的各种主题。
3. **查看示例**：网站上还提供了一系列的[示例](https://pixijs.com/examples)代码，可以帮助你快速理解如何使用不同的功能。
4. **加入社区**：遇到问题或想要分享你的项目时，可以考虑加入[PixiJS的官方论坛](https://github.com/pixijs/pixijs/discussions)或者其[Discord频道](https://discord.gg/pixijs)，与其他开发者交流心得。

## 将文本添加到舞台--Hello PixiJs

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <script src="https://pixijs.download/release/pixi.js"></script>
    <title>PixiJs</title>
  </head>
  <body>
    <!-- <h1> Hello PixiJS</h1> -->
    <script>
      // 创建一个新的 PIXI.Application 实例
      let app = new PIXI.Application({ width: 640, height: 360, backgroundColor: 0x1099bb });
      // 将实例添加到 DOM 中
      document.body.appendChild(app.view);
      // 创建一个文本样式
      const skewStyle = new PIXI.TextStyle({
        fontFamily: 'Arial',
        dropShadow: true,
        dropShadowAlpha: 0.8,
        dropShadowAngle: 2.1,
        dropShadowBlur: 4,
        dropShadowColor: '0x111111',
        dropShadowDistance: 10,
        fill: ['#ffffff'],
        stroke: '#004620',
        fontSize: 60,
        fontWeight: 'lighter',
        lineJoin: 'round',
        strokeThickness: 12,
      });
      // 创建一个文本类型
      const skewText = new PIXI.Text('Hello PixiJS', skewStyle);
      // 将文本倾斜
      skewText.skew.set(0.1, -0.1);
      // 定义文本在舞台（app）中的位置
      skewText.x = 10;
      skewText.y = 100;
      // 将文本添加到舞台（app）中
      app.stage.addChild(skewText);
    </script>
  </body>
</html>
```

## 将图片添加到舞台

```js
      // 创建一个图像精灵
      const luFei = PIXI.Sprite.from('https://img1.baidu.com/it/u=2082729884,1583333066&fm=253&fmt=auto&app=138&f=JPEG?w=400&h=711');
      // 把精灵的原点设置为图片的中心点
      luFei.anchor.set(0.5);
      // 把精灵缩小0.5倍
      luFei.scale.set(0.5);
      // 把精灵定位在画布的中心
      luFei.x = app.screen.width / 2;
      luFei.y = app.screen.height / 2;
      // 把图像精灵添加到舞台（app）上
      app.stage.addChild(luFei);
      // 为舞台添加一个更新循环的方法
      app.ticker.add(() => {
          // 让图像精灵每次更新旋转0.01度
          luFei.rotation += 0.01;
      });
```

## 加载资源到舞台

```js
import { Application, Assets, Sprite } from 'pixi.js';

// Create a new application
const app = new Application();

// Initialize the application
await app.init({ background: '#1099bb', resizeTo: window });

// Append the application canvas to the document body
document.body.appendChild(app.canvas);

// Start loading right away and create a promise
const texturePromise = Assets.load('https://pixi.nodejs.cn/assets/bunny.png');

// When the promise resolves, we have the texture!
texturePromise.then((resolvedTexture) =>
{
    // create a new Sprite from the resolved loaded Texture
    const bunny = Sprite.from(resolvedTexture);

    // center the sprite's anchor point
    bunny.anchor.set(0.5);

    // move the sprite to the center of the screen
    bunny.x = app.screen.width / 2;
    bunny.y = app.screen.height / 2;

    app.stage.addChild(bunny);
});
```

### **Assets**a开箱即用，可以加载以下资源类型，无需外部插件：

- 纹理（`avif`、`webp`、`png`、`jpg`、`gif`）
- 精灵表 (`json`)
- 位图字体（`xml`、`fnt`、`txt`）
- 网页字体（`ttf`、`woff`、`woff2`）
- Web fonts (`ttf`, `woff`, `woff2`)
- Json 文件 (`json`)
- 文本文件 (`txt`)

### **可取别名，多资源读取**

```js
Assets.add({ alias: 'flowerTop', src: 'https://pixi.nodejs.cn/assets/flowerTop.png' });
Assets.add({ alias: 'eggHead', src: 'https://pixi.nodejs.cn/assets/eggHead.png' });
const texturesPromise = Assets.load(['flowerTop', 'eggHead']); // => Promise<{flowerTop: Texture, eggHead: Texture}>

```

## 容器

[容器](https://pixijs.download/release/docs/scene.Container.html) 类提供了一个简单的显示对象，其功能正如其名称所暗示的那样 - 将一组子对象收集在一起。

### 常用属性

| 属性           | 描述                                                         |
| -------------- | ------------------------------------------------------------ |
| **position**   | X 和 Y 位置以像素为单位给出，并更改对象相对于其父对象的位置，也可以直接用作 `object.x` / `object.y` |
| **rotation**   | 旋转以弧度指定，并顺时针旋转对象 (0.0 - 2 * Math.PI)         |
| **angle**      | 角度是旋转的别名，以度而不是弧度指定 (0.0 - 360.0)           |
| **pivot**      | 对象旋转的点（以像素为单位） - 还设置子对象的原点            |
| **alpha**      | 不透明度从 0.0（完全透明）到 1.0（完全不透明），由子级继承   |
| **scale**      | 比例指定为百分比，1.0 为 100% 或实际大小，并且可以为 x 和 y 轴独立设置 |
| **skew**       | Skew 与 CSS skew() 函数类似，在 x 和 y 方向上变换对象，并以弧度指定 |
| **visible**    | 对象是否可见，作为布尔值 - 防止更新和渲染对象和子对象        |
| **renderable** | 是否应该渲染对象 - 当 `false` 时，对象仍然会更新，但不会渲染，不影响子对象 |

#### position （位置）

```js
 // 创建一个新的 PIXI.Application 实例
      let app = new PIXI.Application({ width: 640, height: 360, backgroundColor: 0x1099bb });
      // 将实例添加到 DOM 中
      document.body.appendChild(app.view);
      // 创建一个图像精灵
      const luFei = PIXI.Sprite.from('https://img1.baidu.com/it/u=2082729884,1583333066&fm=253&fmt=auto&app=138&f=JPEG?w=400&h=711');
      // 通过 position 设置精灵在画布中的位置
      // luFei.position.x = app.screen.width/2
      // luFei.position.y = app.screen.height/2
      // 上面注释的是分别设置 也可以统一设置
      luFei.position.set(app.screen.width/2, app.screen.height/2); 
      // 把图像精灵添加到舞台（app）上
      app.stage.addChild(luFei);
```

#### pivot （枢轴、中心点）

把枢轴设置在精灵X和Y分别在100的位置      

luFei.pivot.set(100, 100);

####  anchor （描点）

 anchor可以移动精灵图的纹理原点，通过设置0-1的值。pivot通过设置像素值来改变精灵的x和y的原点值。

```js
luFei.anchor.set(X, Y); // 默认（0, 0）
      // 通过 anchor 设置精灵的右上角为图片精灵的原点
      luFei.anchor.set(1, 0);
```

anchor 和 pivot很相似，都可以设置精灵的焦点。但他们也是有区别的

pivot 是基于 anchor 来设置的，当 anchor 为默认值（0, 0）的时候，pivot 设置多少就是多少，但当 anchor 设置以后，pivot的值就要基于anchor后的焦点来设置。

#### scale （缩放）

设置的时候值为0-1，1即为100%（实际大小）

```js
// 分别设置
luFei.scale.x = 0.5; // x坐标缩小一半
luFei.scale.y = 1; // y坐标保持实际大小
// 统一设置
luFei.scale.set(0.5， 1);
// 若X和Y的值相同,比如都为0.5
luFei.position.set(0.5);
```

#### rotation （旋转）

```js
      // 通过 rotation 设置精灵的旋转角度
      luFei.rotation = 0.5 * Math.PI //90度
```

#### angle （角度）

angle 和 rotation 具有相同的效果。不同点是 rotation 以弧度为单位，angle 以度为单位。

```js
      // 通过 angle 设置精灵的角度
      luFei.angle = 45
```

#### skew （偏斜）

```js
 // 通过 skew 设置精灵的偏斜
 luFei.skew.set(0.5, 0) // x轴倾斜0.5
```

#### alpha （透明度）

```js
      // 通过 alpha 设置精灵的透明度 0-1(透明到不透明）
      luFei.alpha = 0.5
```

#### visible (可见否）

```js
	  // 通过 visible 设置精灵的可见度
      luFei.visible = false
```

#### renderable （渲染）

renderable 和 visible 显示的效果一样，但不一样的是，visible 会渲染到画布，renderable 不会渲染到画布上。

```js
      // 通过 renderable 设置精灵是否可被渲染
      luFei.renderable = false
```

#### mask（掩模）

掩模是一个物体，能将精灵的可见性限制于掩模的形状。 举个例子看一下就懂了，首先咱们再添加一个圆（图形精灵）到画布上。

```js
// 创建一个新的 PIXI.Application 实例
      let app = new PIXI.Application({ width: 640, height: 360, backgroundColor: 0x1099bb });
      // 将实例添加到 DOM 中
      document.body.appendChild(app.view);
      // 创建一个图像精灵
      const luFei = PIXI.Sprite.from('https://img1.baidu.com/it/u=2082729884,1583333066&fm=253&fmt=auto&app=138&f=JPEG?w=400&h=711');
      // 上面注释的是分别设置 也可以统一设置
      luFei.position.set(app.screen.width/2, app.screen.height/2); 
      // 设置图片精灵的中心点为原点
      luFei.anchor.set(0.5);
      // 通过 scale 设置精灵的缩放比例
      luFei.scale.set(0.5);
      // 把图像精灵添加到舞台（app）上
      app.stage.addChild(luFei);
      // 创建一个图形类
      const graphics = new PIXI.Graphics();
      // 指定一个简单的单色填充
      graphics.beginFill(0xFF0000);
      // 通过图形类画一个圆
      graphics.drawCircle(app.screen.width/2, app.screen.height/2, 100);
      // 填充上一次设置的 beginFill()
      graphics.endFill();

      // 把圆添加到舞台（app）上
      // app.stage.addChild(graphics);

      // 把圆形精灵以掩模的形式添加在图片精灵上
      luFei.mask = graphics
```

#### zIndex (图层层级)

和 CSS 里的 z-index 一样，zIndex 的值越大，层级就越高。
父精灵设置了sortableChildren为true, 子精灵才能按照zIndex的value值进行层级的排序。

```js
// 创建一个新的 PIXI.Application 实例
      let app = new PIXI.Application({ 
        width: 640, 
        height: 360, 
        backgroundColor: 0x1099bb
      });
      // 只有父精灵设置了sortableChildren为true, 子精灵才能按照zIndex的value值进行层级的排序
      app.stage.sortableChildren = true
      // 将实例添加到 DOM 中
      document.body.appendChild(app.view);

      // 创建一个图像精灵
      const luFei = PIXI.Sprite.from('https://img1.baidu.com/it/u=2082729884,1583333066&fm=253&fmt=auto&app=138&f=JPEG?w=400&h=711');
      // 上面注释的是分别设置 也可以统一设置
      luFei.position.set(app.screen.width/2 - 150, app.screen.height/2 - 100); 
      // 设置图片精灵的中心点为原点
      luFei.anchor.set(0.5);
      // 通过 scale 设置精灵的缩放比例
      luFei.scale.set(0.5);
      luFei.zIndex = 1

      // 创建一个图像精灵
      const luFei1 = PIXI.Sprite.from('https://img1.baidu.com/it/u=2082729884,1583333066&fm=253&fmt=auto&app=138&f=JPEG?w=400&h=711');
      // 上面注释的是分别设置 也可以统一设置
      luFei1.position.set(app.screen.width/2, app.screen.height/2); 
      // 设置图片精灵的中心点为原点
      luFei1.anchor.set(0.5);
      // 通过 scale 设置精灵的缩放比例
      luFei1.scale.set(0.5);
      luFei1.zIndex = 2

      // 创建一个图像精灵
      const luFei2 = PIXI.Sprite.from('https://img1.baidu.com/it/u=2082729884,1583333066&fm=253&fmt=auto&app=138&f=JPEG?w=400&h=711');
      // 上面注释的是分别设置 也可以统一设置
      luFei2.position.set(app.screen.width/2 + 150, app.screen.height/2 + 100); 
      // 设置图片精灵的中心点为原点
      luFei2.anchor.set(0.5);
      // 通过 scale 设置精灵的缩放比例
      luFei2.scale.set(0.5);
      luFei2.zIndex = 1

      // 把图像精灵添加到舞台（app）上
      app.stage.addChild(luFei);
      app.stage.addChild(luFei1);
      app.stage.addChild(luFei2);
```



#### 过滤器

容器对象的另一个常见用途是作为过滤内容的宿主。

| AlphaFilter        | 与设置 `alpha` 属性类似，但展平 Container 而不是单独应用于子项。 |
| ------------------ | ------------------------------------------------------------ |
| BlurFilter         | 应用模糊效果                                                 |
| ColorMatrixFilter  | 颜色矩阵是应用更复杂的色调或颜色变换（例如棕褐色调）的灵活方法。 |
| DisplacementFilter | 置换贴图创建视觉偏移像素，例如创建波浪水效果。               |
| NoiseFilter        | 创建随机噪声（例如颗粒效果）。                               |

底层原理glsl和wgsl

## interactive（事件交互）

启用 DisplayObject 的事件交互。默认触摸（Touch）、指针（pointer）和鼠标（mouse）事件将不会被触发，除非交互式设置为true。

```js
      // 开启事件交互
      luFei.interactive = true;

      // 给图像精灵添加点击事件，
      luFei.addListener('click', () => {
        console.log('luFei click') 
      })
```

## hitArea (命中区域）

当我们给一个添加了事件交互的精灵再添加一个命中区域时，那么精灵的事件交互就只是在命中区域内起作用。

```js
      // 开启事件交互
      luFei.interactive = true;
      // 开启按钮模式
      luFei.buttonMode = true;
      // 定义一个矩形对象
      let rec = new PIXI.Rectangle(0, 0, 100, 100);
      // 在图像精灵上添加矩形的命中区域
      luFei.hitArea = rec

      // 给图像精灵添加点击事件，
      luFei.addListener('click', () => {
        console.log('luFei click') 
      })
```

## pixelLine

`pixelLine` 属性是 PixiJS 图形 API 的一个巧妙功能，允许你创建保持 1 像素粗细的线条，无论缩放或缩放级别如何。作为图形 API 的一部分，它为开发者提供了 PixiJS 为构建和描边形状提供的所有功能。

// Create a Graphics object and draw a pixel-perfect line
let graphics = new Graphics()
  .moveTo(0, 0)
  .lineTo(100, 100)
  .stroke({ color: 0xff0000, pixelLine: true });

// Add it to the stage
app.stage.addChild(graphics);

// Even if we scale the Graphics object, the line remains 1 pixel wide
graphics.scale.set(2);
