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

## 精灵（Sprite）
在 PixiJS 中，**精灵（Sprite）** 是一个非常基础且重要的显示对象，用于展示2D图像。它是基于 `Texture` 的显示对象，能够方便地处理和展示图片、动画帧等。

### 基本概念

- **精灵（Sprite）**：可以简单理解为带有位置、旋转、缩放等属性的图像。它通常是从一个 `Texture` 创建出来的，这个 `Texture` 可以是整个图像或者是一张大图的一部分（如纹理图集中的某个子图像）。
### 创建精灵

创建一个精灵通常是通过以下步骤：

1. 加载或创建一个 `BaseTexture`。
2. 使用 `BaseTexture` 创建一个 `Texture`。
3. 使用 `Texture` 创建一个 `Sprite`。

```javascript
// 从一个图像路径加载BaseTexture，并创建Sprite
let sprite = PIXI.Sprite.from('image.png');

// 或者更详细的方式
let baseTexture = PIXI.BaseTexture.from('image.png');
let texture = new PIXI.Texture(baseTexture);
let sprite = new PIXI.Sprite(texture);
```

### 精灵的主要属性

精灵具有许多可调整的属性，使得它可以被灵活地操作：

- **position**：精灵的位置，可以通过 `x` 和 `y` 属性来设置。
- **scale**：精灵的缩放比例，使用 `scale.x` 和 `scale.y` 来调整大小。
- **rotation**：精灵的旋转角度，单位是弧度。
- **anchor**：精灵的锚点，默认位于左上角 `(0, 0)`，可以通过改变这个值来控制旋转和缩放的中心点。
- **alpha**：精灵的透明度，取值范围是 0 到 1。

### 应用场景

- **静态图像**：直接展示一张图片。
- **动画**：通过不断更换精灵的 `Texture` 来实现动画效果。
- **游戏开发**：精灵非常适合用来表示游戏中的角色、道具等元素。

通过理解和使用精灵，你可以利用 PixiJS 轻松创建出各种复杂的2D图形和互动内容。

## 图形（Graphics）

在 PixiJS 中，**Graphics** 对象是用于绘制矢量图形的强大工具。它允许开发者直接在画布上创建和修改各种形状，而无需依赖外部图像资源。以下是关于 Graphics 的详细介绍。

### 主要特性

#### 1. 矢量绘图
Graphics 对象支持绘制多种基本的矢量图形，如矩形、圆形、椭圆、线段等。通过一系列的方法调用，可以构建复杂的图形组合。

#### 2. 动态更新
由于所有内容都是程序生成的，Graphics 对象非常适合需要动态更新的场景。例如，在游戏中实时更新的生命值条、技能冷却指示器等。

#### 3. 高度可定制化
可以通过设置线条宽度、颜色、透明度以及填充色来高度定制化你的图形。

#### 4. 支持路径绘制
除了基本图形外，Graphics 还支持更高级的功能，如绘制自由曲线、贝塞尔曲线等，这为创建复杂图形提供了可能。

### 常用方法介绍

#### 创建 Graphics 对象
```javascript
let graphics = new PIXI.Graphics();
```

#### 设置线条样式
`lineStyle(lineWidth, color, alpha)`：定义线条的宽度、颜色和透明度。
- `lineWidth`: 线条宽度，默认为0（无边框）。
- `color`: 十六进制颜色值。
- `alpha`: 透明度，范围从0到1。

示例：
```javascript
graphics.lineStyle(2, 0xFF3300, 1); // 设置红色、宽度为2的线条
```

#### 开始填充
`beginFill(color, alpha)`：设置填充的颜色和透明度。
- `color`: 填充颜色，十六进制表示。
- `alpha`: 填充颜色的透明度。

示例：
```javascript
graphics.beginFill(0x66CCFF, 1); // 蓝色填充
```

#### 结束填充
`endFill()`：结束当前填充区域，开始新的绘制操作。

#### 绘制基本形状
PixiJS 提供了几种绘制基本形状的方法：

- `drawRect(x, y, width, height)`：绘制矩形。
- `drawCircle(x, y, radius)`：绘制圆形。
- `drawEllipse(x, y, width, height)`：绘制椭圆。
- `drawPolygon(points)`：绘制多边形，参数是一个点数组。

示例：
```javascript
// 绘制一个矩形
graphics.drawRect(50, 50, 100, 100);
// 绘制一个圆形
graphics.drawCircle(200, 200, 50);
```

#### 清除图形
`clear()`：清除所有绘制的内容，并重置样式设置。

#### 其他功能
- **移动坐标系**：使用 `moveTo(x, y)` 和 `lineTo(x, y)` 可以实现自定义路径的绘制。
- **贝塞尔曲线**：`bezierCurveTo(cpX, cpY, cpX2, cpY2, toX, toY)` 用于绘制平滑的曲线。

### 实际应用案例

假设我们需要在游戏界面中显示一个带有阴影效果的按钮，可以使用 Graphics 来实现这个需求。

```javascript
const app = new PIXI.Application({width: 800, height: 600});
document.body.appendChild(app.view);

let button = new PIXI.Graphics();

// 绘制阴影
button.beginFill(0x000000, 0.5);
button.drawRect(47, 47, 106, 56);
button.endFill();

// 绘制按钮主体
button.beginFill(0x66CCFF);
button.drawRect(50, 50, 100, 50);
button.endFill();

// 添加文本
let text = new PIXI.Text('Click Me', {fontSize: 24, fill: 'white'});
text.x = 60;
text.y = 65;

// 将文本添加到按钮上
button.addChild(text);

// 添加按钮到舞台
app.stage.addChild(button);
```

在这个例子中，我们首先使用半透明黑色绘制了一个稍微偏移的矩形作为阴影，然后在其上方绘制了主按钮，并添加了文本标签。

Graphics 在 PixiJS 中提供了一种强大的方式来创建和管理动态或静态的矢量图形，无论是简单的几何图形还是复杂的自定义路径，都可以轻松实现。

## 图形与精灵（Graphics and **Sprite**）

在 PixiJS 中，**Graphics** 和 **Sprite** 都是用于绘制和显示2D图形的对象，但它们的功能和使用场景有所不同。理解这两者的区别有助于选择合适的工具来实现特定的视觉效果。

### Graphics

**Graphics** 是一个非常灵活的对象，允许开发者直接在画布上绘制各种形状，如矩形、圆形、线条等，而不需要依赖外部图像资源。它非常适合用于创建动态或程序生成的图形。

#### 主要特点

- **灵活性**：可以绘制任意形状，包括路径、多边形、圆弧等。
- **实时性**：由于所有内容都是通过代码生成的，因此非常适合需要动态更新的场景。
- **无纹理依赖**：不依赖于外部图片资源，减少了对额外文件的需求。

### Sprite

**Sprite** 是基于 `Texture` 的显示对象，通常用于展示图像或动画帧。它是从现有的图像资源（如 PNG 文件）加载而来，并且可以进行缩放、旋转、平移等变换。

#### 主要特点

- **高效渲染**：由于使用预渲染的图像数据，适合用于高性能的游戏和应用中。
- **易于管理**：可以通过 `Texture` 来管理和复用图像资源，减少内存占用。
- **支持复杂内容**：可以展示复杂的图像、动画序列等。

### 区别总结

| 特性         | Graphics                             | Sprite                             |
| ------------ | ------------------------------------ | ---------------------------------- |
| **来源**     | 程序生成的形状                       | 预渲染的图像                       |
| **灵活性**   | 高，可以绘制任意形状                 | 固定，依赖于图像资源               |
| **性能**     | 相对较低，特别是在绘制大量复杂图形时 | 高效，特别适合高性能游戏和应用     |
| **适用场景** | 动态生成的图形，如图表、UI元素等     | 显示静态或动画图像，如角色、道具等 |
| **资源需求** | 不需要外部图像文件                   | 需要外部图像文件                   |

### 结论

- 如果你需要绘制动态或程序生成的图形，如 UI 元素、图表、几何形状等，**Graphics** 是更好的选择。
- 如果你需要展示高质量的图像或动画，特别是那些可以从外部资源加载的图像，那么 **Sprite** 更适合你。

根据具体的应用需求，合理选择使用 Graphics 或 Sprite 可以帮助你更高效地实现所需的视觉效果。

## 文本（Text）

在 PixiJS 中，文本渲染是通过 `Text` 类实现的。它允许开发者在应用中显示和操作文本，并提供了丰富的样式设置选项以满足不同的需求。以下是对 PixiJS 文本（`Text`）类的详细介绍。

### 创建文本

创建一个基本的文本对象非常简单，只需实例化 `PIXI.Text` 并指定文本内容和样式即可。

### 样式属性

PixiJS 的 `Text` 类提供了多种样式属性，可以用来定制文本的外观：

- **fontFamily**：字体系列，默认值为 `'Arial'`。
- **fontSize**：字体大小，单位为像素，默认值为 `20`。
- **fill**：文本颜色，可以是十六进制颜色值、CSS颜色名称或渐变对象。
- **align**：文本对齐方式，可选值有 `'left'`, `'center'`, `'right'`，默认值为 `'left'`。
- **fontWeight**：字体粗细，如 `'bold'` 或 `'normal'`。
- **wordWrap**：是否启用自动换行，默认值为 `false`。
- **wordWrapWidth**：当 `wordWrap` 启用时，指定文本的最大宽度。
- **stroke**：描边颜色，与 `fill` 类似。
- **strokeThickness**：描边厚度，默认值为 `0`（无描边）。
- **dropShadow**：是否启用阴影，默认值为 `false`。
- **dropShadowColor**：阴影颜色。
- **dropShadowBlur**：阴影模糊程度。
- **dropShadowAngle**：阴影角度，单位为弧度。
- **dropShadowDistance**：阴影偏移距离。

#### 示例：带描边和阴影的文本

```javascript
let styledText = new PIXI.Text('Styled Text', {
    fontFamily: 'Arial',
    fontSize: 48,
    fill: '#ffffff',
    stroke: '#ff3300',
    strokeThickness: 4,
    dropShadow: true,
    dropShadowColor: '#000000',
    dropShadowBlur: 4,
    dropShadowAngle: Math.PI / 6,
    dropShadowDistance: 6
});

styledText.x = app.screen.width / 2;
styledText.y = app.screen.height / 2;
styledText.anchor.set(0.5);

app.stage.addChild(styledText);
```

利用 PixiJS 的 `Text` 类创建出丰富多彩且高效的应用界面

## 纹理

在 PixiJS 中，**纹理（Texture）** 是用于渲染图像的基本单位。理解纹理的概念对于有效地使用 PixiJS 来创建高效的2D图形和动画非常重要。

### 纹理的基本概念

- **纹理（Texture）**：是一个用于显示的图像数据块，通常是从 `BaseTexture` 创建而来。它定义了图像如何被绘制到屏幕上，包括图像的尺寸、透明度等属性。
- **BaseTexture**：是对实际图像资源（如 PNG 或 JPG 文件）的一个引用。一个 `BaseTexture` 可以被多个 `Texture` 对象共享使用。

### 纹理的工作原理

1. **加载 BaseTexture**：首先需要加载或创建一个 `BaseTexture`。这通常是通过从文件系统加载一张图片来完成的。
   
   ```javascript
   let baseTexture = PIXI.BaseTexture.from('image.png');
   ```

2. **创建 Texture**：基于 `BaseTexture` 创建一个 `Texture`。这个 `Texture` 可以是整个 `BaseTexture` 或者其中的一部分（例如，从一个纹理图集中的某个子图像）。

   ```javascript
   let texture = new PIXI.Texture(baseTexture);
   // 或者直接获取整个图像作为纹理
   let texture = PIXI.Texture.from('image.png');
   ```

3. **使用 Texture**：一旦有了 `Texture`，就可以用它来创建精灵或其他显示对象，并将它们添加到舞台上进行渲染。

### 纹理的类型

PixiJS 支持多种类型的纹理，包括但不限于：

- **静态纹理**：最常用的类型，用于展示静态图像。
- **纹理图集（Texture Atlas）**：包含多个小图的大型图像，可以更高效地加载和管理多个图像资源。
  
  ```javascript
  let texture = PIXI.Texture.fromFrame('frameName'); // 假设已经加载了一个纹理图集
  ```

- **可重复纹理（Tiling Texture）**：用于平铺显示图像，适合制作背景等需要重复显示相同图案的情况。

### 纹理的管理和优化

为了提高性能和节省内存，PixiJS 提供了一些机制来管理和优化纹理：

- **缓存机制**：PixiJS 自动缓存加载的 `BaseTexture` 和 `Texture`，如果多次尝试加载相同的图像资源，PixiJS 将重用已有的 `BaseTexture`。
  
- **销毁机制**：当不再需要某个 `Texture` 或 `BaseTexture` 时，可以通过调用 `destroy()` 方法来释放相关的资源，防止内存泄漏。

  ```javascript
  texture.destroy();
  baseTexture.destroy();
  ```

- **纹理图集**：使用纹理图集不仅可以减少HTTP请求的数量，还能更好地利用内存，因为所有的小图都打包在一个大图中，减少了加载时间和内存占用。

### 示例代码

以下是一个简单的例子，展示了如何加载并使用纹理来创建一个精灵：

```javascript
// 创建PixiJS应用实例
const app = new PIXI.Application({width: 800, height: 600});
document.body.appendChild(app.view);

// 加载BaseTexture并创建Texture
let baseTexture = PIXI.BaseTexture.from('example.png');
let texture = new PIXI.Texture(baseTexture);

// 使用Texture创建一个Sprite
let sprite = new PIXI.Sprite(texture);

// 设置精灵的位置
sprite.x = app.screen.width / 2;
sprite.y = app.screen.height / 2;

// 添加精灵到舞台
app.stage.addChild(sprite);
```

理解和有效使用纹理是掌握 PixiJS 的关键之一。通过合理管理和优化纹理，你可以创建出更加流畅且高效的2D图形应用。

## 纹理的生命周期

在 PixiJS 中，纹理（Texture）的生命周期涉及从创建到销毁的过程。理解纹理的生命周期有助于更好地管理内存和资源，从而提高应用的性能和稳定性。以下是纹理生命周期的主要阶段：

### 1. 创建

**创建纹理**通常通过加载图像文件或者使用已有的 `BaseTexture` 来实现。PixiJS 提供了多种方式来创建纹理。

- **从文件加载**：这是最常见的方法，通过指定图片路径直接创建纹理。
  
  ```javascript
  let texture = PIXI.Texture.from('image.png');
  ```

- **基于 BaseTexture 创建**：首先需要有一个 `BaseTexture`，然后可以基于它创建一个或多个 `Texture` 对象。
  
  ```javascript
  let baseTexture = PIXI.BaseTexture.from('image.png');
  let texture = new PIXI.Texture(baseTexture);
  ```

### 2. 使用

一旦纹理被创建，就可以用于渲染图形对象，如精灵（Sprite）、文本（Text）等。纹理被添加到显示列表中，并参与每一帧的渲染过程。

```javascript
let sprite = new PIXI.Sprite(texture);
app.stage.addChild(sprite); // 将精灵添加到舞台上进行渲染
```

### 3. 缓存

PixiJS 自动对 `BaseTexture` 和 `Texture` 进行缓存。这意味着如果多次尝试加载相同的图像资源，PixiJS 不会重新加载该资源，而是重用已经存在的 `BaseTexture`。这对于减少内存占用和提高加载效率非常有用。

### 4. 更新

有时你可能需要更新纹理的内容，比如动态修改图像数据。PixiJS 支持直接操作 `BaseTexture` 的图像数据，但这通常只在特殊情况下使用，例如实时视频流或摄像头输入。

### 5. 销毁

当不再需要某个纹理时，应该调用其 `destroy()` 方法来释放相关资源。这包括解除与 `BaseTexture` 的关联，并释放 GPU 资源。对于不再使用的 `BaseTexture`，也需要调用 `destroy()` 方法。

```javascript
texture.destroy(); // 销毁Texture
baseTexture.destroy(); // 销毁BaseTexture
```

需要注意的是，如果一个 `BaseTexture` 被多个 `Texture` 共享，那么只有当所有相关的 `Texture` 都被销毁后，`BaseTexture` 才能安全地被销毁。

### 6. 垃圾回收

在销毁之后，如果没有其他引用指向这些纹理，它们将变为垃圾收集器的目标，最终从内存中移除。确保正确管理和及时销毁不再需要的纹理，可以帮助避免内存泄漏，特别是在长时间运行的应用程序中。

### 生命周期管理的重要性

正确管理纹理的生命周期是优化应用性能的关键之一。不恰当的管理可能导致内存泄漏、过度的内存使用以及不必要的 CPU 或 GPU 负载。通过合理利用缓存机制、及时销毁不再使用的资源，可以有效地提升应用的响应速度和稳定性。

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

### **Assets**开箱即用，可以加载以下资源类型，无需外部插件：

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