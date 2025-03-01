---
title: Canvas笔记
author: pzc
date: 2025-03-01
cover: /assets/images/jpg/145.jpg
categories: [html]
tags: [Canvas]
---

## 来源

笔记来源：[PixiJs学前篇（一）：Canvas基础【绘制篇】🔥🔥面对网页性能要求越来越高的今天，项目性能优化已经成了项目开发 - 掘金 (juejin.cn)](https://juejin.cn/post/7161696893695688740?searchId=202502271231541CC85DB1CD50F5A46993)

## 上下文

canvas.getContext(contextType, contextAttributes)

## 描边和填充

```
stroke()` 和 `fill()
```

## 样式设置

### strokeStyle

描边的样式

### fillStyle

填充的样式

## 直线

直线的绘制就是设置两个点，然后连接这两个点形成一条直线，那么这两个点如何设置呢？

### moveTo(x, y)

设置初始位置，参数为初始位置x和y的坐标点

### lineTo(x, y)

设置指定位置，参数为指定位置x和y的坐标点

直线的样式可以通过一系列属性来设置，

#### lineWidth

#### lineCap

设置直线端点显示的样式。可选值为：butt，round 和 square。默认是 butt。

#### lineJoin

设置两线段连接处所显示的样子。可选值为：round, bevel 和 miter。默认是 miter。

#### miterLimit

设置当两条线相交时交接处最大长度；所谓交接处长度（斜接长度）是指线条交接处内角顶点到外角顶点的长度。

线段之间夹角比较大时，交点不会太远，但随着夹角变小，交点距离会呈指数级增大。

如果交点距离大于miterLimit值，连接效果会变成了 lineJoin = bevel 的效果。

## 三角形

```js
const canvas = document.getElementById('canvas'); // 获取Canvas
  const ctx = canvas.getContext('2d'); // 获取绘制上下文
  ctx.strokeStyle = "#f00" // 描边样式设置为红色
  ctx.fillStyle = "#00f" // 填充样式设置为蓝色
  ctx.lineWidth = 5
  // 绘制一个三角形
  ctx.moveTo(50, 100) 
  ctx.lineTo(50, 400)
  ctx.lineTo(400, 400)
  ctx.lineTo(50, 100) 
  ctx.stroke();
  // 如果是填充一个三角形，则只需两条直线就行，它会默认闭合。
  ctx.beginPath()
  ctx.movTo(200, 200) 
  ctx.lineTo(400, 200)
  ctx.lineTo(400, 370)
  ctx.fill();
```

## 矩形

// 矩形描边
rect(x, y, width, height)

// 绘制矩形
strokeRect(x, y, width, height)

// 填充矩形
fillRect(x, y, width, height)

上述的三个方法都可以用来绘制矩形，他们的传参都是一样的，其中x和y是起始点的x坐标和y坐标，width为矩形的宽，height为矩形的高。

```js
    const canvas = document.getElementById('canvas'); // 获取Canvas
    const ctx = canvas.getContext('2d'); // 获取绘制上下文
    ctx.strokeStyle = "#f00" // 描边样式设置为红色
    ctx.fillStyle = "#00f" // 填充样式设置为蓝色
    ctx.lineWidth = 5

    // 先创将矩形路径，再描边矩形
    ctx.rect(50, 50, 300, 100)
    ctx.fill()

    ctx.beginPath()

    // 直接创建矩形路径并描边
    ctx.fillRect(50, 300, 300, 100)
```

## 圆形

ctx.arc(x, y, radius, startAngle, endAngle, anticlockwise);

x，y 为圆弧中心或圆的圆心坐标、

radius 为圆弧的半径或圆的半径、

startAngle 为圆弧或圆的起始点，从x轴方向开始计算，且单位为弧度、

endAngle 为圆弧或圆的终点，单位也是为弧度

anticlockwise 是一个可选参数，可选值为Boolean类型，用它来表示圆弧或圆的绘制方向，默认为false，顺时针绘制圆弧或圆。

角度转弧度的公式为：`弧度 = 角度 * Math.PI / 180`

```js
    //圆弧
	const canvas = document.getElementById('canvas'); // 获取Canvas
    const ctx = canvas.getContext('2d'); // 获取绘制上下文
    ctx.strokeStyle = "#f00" // 描边样式设置为红色
    ctx.fillStyle = "#00f" // 填充样式设置为蓝色
    ctx.lineWidth = 5,

    // 顺时针绘制一段90度的圆弧
    ctx.arc(100, 100, 50, 0, 90 * Math.PI /180 ); 
    ctx.stroke();

    // 逆时针绘制一段90度的圆弧
    ctx.beginPath();
    ctx.arc(300, 100, 50, 0, 90 * Math.PI /180, true ); 
    ctx.stroke();
```

## 椭圆

```
ellipse(x, y, radiusX, radiusY, rotation, startAngle, endAngle, anticlockwise)
```

- x、y：椭圆的圆心坐标
- radiusX：x轴的半径大小
- radiusY：y轴的半径大小
- rotation：椭圆的旋转角度，也是以弧度表示
- startAngle：开始绘制点
- endAngle：结束绘制点
- anticlockwise：可选参数，表示绘制的方向（默认顺时针）。

```js
    // 获取 canvas 元素
    var canvas = document.getElementById('canvas');
    // 通过判断getContext方法是否存在来判断浏览器的支持性
    if(canvas.getContext) {
      // 获取绘图上下文
      var ctx = canvas.getContext('2d');
      ctx.beginPath();
      ctx.ellipse(100, 150, 50, 100, 0, 0, 2 * Math.PI);
      ctx.stroke();
      ctx.beginPath();
      ctx.ellipse(400, 150, 50, 100, 0, 0, 2 * Math.PI);
      ctx.stroke();
      ctx.beginPath();
      ctx.ellipse(250, 350, 50, 100, Math.PI/2, 0, 2 * Math.PI); // 旋转90°
      ctx.fill();
    }
```

## 贝塞尔曲线

### 二次贝塞尔曲线

如图就是一个二次贝塞尔曲线，他的绘制需要一个控制点来控制曲线，具体的语法为：

```
quadraticCurveTo(cp1x, cp1y, x, y)
```

参数：

- cp1x和cp1y为控制点坐标
- x和y为结束点坐标

```js 
    id="canvas"
    width="500" 
    height="500" 
    style="box-shadow: 0px 0px 5px #ccc; border-radius: 8px;">
    当前浏览器不支持canvas元素，请升级或更换浏览器！
  </canvas>
  <script>
    const canvas = document.getElementById('canvas'); // 获取Canvas
    const ctx = canvas.getContext('2d'); // 获取绘制上下文
    ctx.strokeStyle = "#333";
    ctx.beginPath();
    ctx.moveTo(100, 250);
    ctx.quadraticCurveTo(250, 100, 400, 250);
    ctx.stroke();
```

### 三次贝塞尔曲线

三次贝塞尔曲线和二次贝塞尔曲线不同的是三次贝塞尔曲线有两个控制点。具体的语法为：

```
ctx.bezierCurveTo(cp1x,cp1y, cp2x,cp2y, x, y)
```

参数为：

- cp1x和cp1y为第一个控制点坐标
- cp2x和cp2y为第二个控制点坐标
- x和y为结束点坐标

```js
    const canvas = document.getElementById('canvas'); // 获取Canvas
    const ctx = canvas.getContext('2d'); // 获取绘制上下文
    ctx.lineWidth = 6;
    ctx.strokeStyle = "#333";
    ctx.beginPath();
    ctx.moveTo(100, 250);
    ctx.bezierCurveTo(150, 100, 350, 100, 400, 250);
    ctx.stroke();
```

## 渐变

### 线性渐变

```
createLinearGradient(x1, y1, x2, y2)
```

- x1, y1为起点的坐标
- x2, y2为终点的坐标

在渐变的设置中还需要一个方法来添加渐变的颜色，语法为：`gradient.addColorStop(offset, color)`，其中color就是颜色，offset 则是颜色的偏移值，只为0到1之间的数。

```js
    const canvas = document.getElementById('canvas'); // 获取Canvas
    const ctx = canvas.getContext('2d'); // 获取绘制上下文
    ctx.strokeStyle = "#f00" // 描边样式设置为红色
    ctx.fillStyle = "#00f" // 填充样式设置为蓝色
    ctx.lineWidth = 5
  
    // 创建渐变
    var gradient1 = ctx.createLinearGradient(10, 10, 400, 10);
    gradient1.addColorStop(0, "#000000");
    gradient1.addColorStop(1, "#ffffff");
    var gradient2 = ctx.createLinearGradient(10, 10, 400, 10);
    // 从0.5的位置才开始渐变
    gradient2.addColorStop(0.5, "#000000");
    gradient2.addColorStop(1, "#ffffff");
    ctx.beginPath()
    ctx.fillStyle = gradient1;
    ctx.fillRect(10, 10, 400, 100);
    ctx.beginPath();
    ctx.fillStyle = gradient2;
    ctx.fillRect(10, 150, 400, 100);
```

### 径向渐变

**径向渐变**是从起点到终点颜色从内到外进行圆形的渐变

#### 语法

```
ctx.createRadialGradient(x0, y0, r0, x1, y1, r1)
```

参数：

- x0, y0为开始圆的坐标
- r0为开始圆的半径
- x1, y1为结束圆的坐标
- r1为结束圆的半径

```js
    const canvas = document.getElementById('canvas'); // 获取Canvas
    const ctx = canvas.getContext('2d'); // 获取绘制上下文
    ctx.strokeStyle = "#f00" // 描边样式设置为红色
    ctx.fillStyle = "#00f" // 填充样式设置为蓝色
    ctx.lineWidth = 5
  
    // 创建渐变
    // 结束坐标为点
    var gradient1 = ctx.createRadialGradient(100, 100, 100, 100, 100, 0);
    gradient1.addColorStop(0, "#000000");
    gradient1.addColorStop(1, "#ffffff");
    // 结束坐标为半径30的圆
    var gradient2 = ctx.createRadialGradient(320, 100, 100, 320, 100, 30); 
    gradient2.addColorStop(0, "#000000");
    gradient2.addColorStop(1, "#ffffff");
    // 从0.5的位置才开始渲染
    var gradient3 = ctx.createRadialGradient(100, 320, 100, 100, 320, 0); 
    gradient3.addColorStop(0.5, "#000000"); 
    gradient3.addColorStop(1, "#ffffff");
    // 开始坐标和结束坐标不一样
    var gradient4 = ctx.createRadialGradient(320, 320, 100, 250, 250, 0);
    gradient4.addColorStop(0, "#000000");
    gradient4.addColorStop(1, "#ffffff");
    ctx.beginPath();
    ctx.fillStyle = gradient1;
    ctx.fillRect(10, 10, 200, 200);
    ctx.beginPath();
    ctx.fillStyle = gradient2;
    ctx.fillRect(220, 10, 200, 200);
    ctx.beginPath();
    ctx.fillStyle = gradient3;
    ctx.fillRect(10, 220, 200, 200);
    ctx.beginPath();
    ctx.fillStyle = gradient4;
    ctx.fillRect(220, 220, 200, 200);
```

## 图案样式

`createPattern(image, type)` 参数为：

- Image 参数可以是一个 Image 对象，也可以是一个 canvas 对象
- Type 为图案绘制的类型，可用的类型分别有：repeat，repeat-x，repeat-y 和 no-repeat。

```js
    // 获取 canvas 元素
    var canvas = document.getElementById('canvas');
    // 通过判断getContext方法是否存在来判断浏览器的支持性
    if(canvas.getContext) {
      // 获取绘图上下文
      var ctx = canvas.getContext('2d');
      // 创建一个 image对象
      var img = new Image();
      img.src = "./image.png";
      img.onload = function() {
        // 图片加载完以后
        // 创建图案
        var ptrn = ctx.createPattern(img, 'no-repeat');
        ctx.fillStyle = ptrn;
        ctx.fillRect(0, 0, 500, 500);
      }
    }
```

## 文本

### 轮廓绘制和填充绘制

strokeText()方法是以描边的方式绘制文字的

### 语法：

```
ctx.strokeText(txt, x, y, maxWidth)
```

### 参数：

- txt：是绘制的文本内容
- x、y：为绘制文本的起始位置坐标
- maxWidth：可选参数，为文本绘制的最大宽度。

```js
  const canvas = document.getElementById('canvas'); // 获取Canvas
    const ctx = canvas.getContext('2d'); // 获取绘制上下文
    // 设置字号为:30px 字体为:Arial
    ctx.font = "30px Arial";
    // 在（50,50）的位置绘制一段文本
    ctx.strokeText("携手创作，共同成长，你好，掘金。", 50, 50);

    // 在（50,100）的位置绘制一段文本,并限制最大宽度为350
    ctx.strokeText("携手创作，共同成长，你好，掘金。", 50, 100, 350);

     // 在（50,150）的位置以填充的方式绘制一段文本,并限制最大宽度为350
     ctx.fillText("携手创作，共同成长，你好，掘金。", 50, 150, 350);
```

### fillText()方法是以填充的方式绘制文字的

### 语法：

```
ctx.fillText(txt, x, y, maxWidth)
```

### 参数：

- txt：是绘制的文本内容
- x、y：为绘制文本的起始位置坐标
- maxWidth：可选参数，为文本绘制的最大宽度。

### 文本样式

​    ctx.font = "20px Arial"; 

### 对齐方式

`textAlign`属性的设置可以改变文本对齐的方式。默认值是 `start`，可选值有：`left`、`right`、`center`、`start`和`end`。

### 文字方向

`direction`属性可以设置文本的方向。默认值是 `inherit`， 可选值为：`ltr`（文本方向从左向右）、`rtl`（文本方向从右向左）、`inherit`（根据情况继承 Canvas元素或者 Document 。）。

![image.png](/assets/extend/canvas1.awebp)	

### 基线对齐

`textBaseline`属性设置基于基线对齐的文字垂直方向的对齐方式。默认值是`alphabetic`，可选值为：`top`、`hanging`、`middle`、`alphabetic`、`ideographic`和`bottom`。

![image.png](/assets/extend/canvas2.awebp)

### 阴影

#### shadowOffsetX

shadowOffsetX属性用于设置阴影在 X轴 上的延伸距离，默认值为0，如设置为10，则表示延 X轴 向右延伸10像素的阴影，也可以为负值，负值表示阴影会往反方向（向左）延伸。

#### shadowOffsetY

shadowOffsetY属性用于设置阴影在 Y轴 上的延伸距离，默认值为0，如设置为10，则表示延 Y轴 向下延伸10像素的阴影，也可以为负值，负值表示阴影会往反方向（向上）延伸。

#### shadowBlur

shadowBlur属性用于设置阴影的模糊程度，默认为 0。

#### shadowColor

shadowColor属性用于设置阴影的颜色，默认为全透明的黑色。

## 绘制图像

`drawImage`，并且 `drawImage`方法会根据不同的传参实现不同的功能：绘制图像、缩放图像、裁剪图像。

### 语法：

```
drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight)
```

### 参数：

- image：绘制的元素（图像）。
- sx、sy：裁剪框左上角的坐标。
- sWidth、sHeight：裁剪框的宽度和高度。
- dx、dy：绘制元素（图像）时左上角的坐标。
- dWidth、dHeight：绘制元素（图像）的宽度和高度。如果不设置，则在绘制时image宽度和高度不会缩放。

```js
    const canvas = document.getElementById('canvas'); // 获取Canvas
    const ctx = canvas.getContext('2d'); // 获取绘制上下文

    var img = new Image();
    img.src = 'https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9f56ebb2a6674e1fbd55a3d92df042bd~tplv-k3u1fbpfcp-watermark.image';
    img.onload = function(){
      ctx.drawImage(img, 0, 150, 1650, 700, 0, 0, 550, 500);
    }
```

## 动画

### 移动

移动就是把元素从一个地方移动到另外一个地方。

语法：`translate(x, y)`，其中 x 是左右偏移量，y 是上下偏移量。

## 旋转

了解了移动以后，旋转也比较好理解，就是把元素顺时针旋转一定的弧度。

语法：`rotate(angle)`，其中 angle 是旋转的角度，以弧度为单位，顺时针旋转。

```js
    const canvas = document.getElementById('canvas'); // 获取Canvas
    const ctx = canvas.getContext('2d'); // 获取绘制上下文
    for (let i = 0; i < 9; i++) {
      ctx.fillStyle=`#${i}${i}${i}`
      // 旋转弧度设置，角度和弧度的转换公式：1° = Math.PI / 180
      ctx.rotate(i * 2 * Math.PI / 180);
      // 在（0,0）坐标点绘制一个宽：200，高：100的矩形
      ctx.fillRect(100, 0, 200, 100)
    }
```

### 缩放

了解了移动和旋转以后，缩放也就更好理解了，就是把元素按一定的比例整体缩小或放大。

语法：`scale(x, y)`，其中 x 为水平缩放的值，y 为垂直缩放得值。x和y的值小于1则为缩小，大于1则为放大。默认值为 1。

## 状态的保存和恢复

状态的保存和恢复 用到的方法是 `save()` 和 `restore()`， 分别是保存和恢复。方法不需要参数，直接调用就OK。

绘画的状态有哪些呢（就是我们可以保存和恢复的状态有哪些）？我们列举一下：

- 应用的变形：移动、旋转、缩放、strokeStyle、fillStyle、globalAlpha、lineWidth、lineCap、lineJoin、miterLimit、lineDashOffset、shadowOffsetX、shadowOffsetY、shadowBlur、shadowColor、globalCompositeOperation、font、textAlign、textBaseline、direction、imageSmoothingEnabled等。
- 应用的裁切路径（clipping path）

## 正式动画

Canvas呈现的东西都是绘制完了以后才能看到，因此想通过Canvas自己提供的Api来实现动画是做不到的。

那么想在 Canvas 中实现动画就得借助别的东西，那么借助啥呢？

在我们的 windows 对象上有三个方法：

- setInterval(function, delay) ：定时器，当设定好间隔时间后，function 会定期执行。
- setTimeout(function, delay)：延时器，在设定好的时间之后执行函数
- requestAnimationFrame(callback)：告诉浏览器你希望执行一个动画，并在重绘之前，请求浏览器执行一个特定的函数来更新动画。

```js
    // 获取Canvas
    const canvas = document.getElementById('canvas'); 
    // 获取绘制上下文
    const ctx = canvas.getContext('2d'); 
    // globalCompositeOperation 属性设置或返回如何将一个源（新的）图像绘制到目标（已有的）的图像上。
    // 这里主要是为了让飞机压在运行轨迹上
    ctx.globalCompositeOperation = 'destination-over';
    const width = canvas.width
    const height = canvas.height
    let num = 0
    ctx.strokeStyle = "#ccc"
    const img = new Image()
    img.src="../images/plane.png"
    img.onload = ()=>{
      requestAnimationFrame(planeRun);
    }
    function planeRun(){
      // 清空画布
      ctx.clearRect(0, 0, width, height)

      // 保存画布状态
      ctx.save();

      // 把原心移到画布中间
      ctx.translate(250, 250); 

      // 绘制飞机和飞机动画
      num += 0.01
      ctx.rotate(-num);
      ctx.translate(0, 200);
      ctx.drawImage(img, -20, -25, 40, 40);

      // 恢复状态
      ctx.restore();

      // 飞机运行的轨迹
      ctx.beginPath();
      ctx.arc(250, 250, 200, 0, Math.PI * 2, false);
      ctx.stroke();

      // 执行完以后继续调用
      requestAnimationFrame(planeRun);
    }
```

## 画布清空

在我们的Canvas中其实它本身已经提供了这样的方法：`clearRect()`

语法：`clearRect(x, y, width, height)`

参数：

- x为要清除的矩形区域左上角的x坐标，
- y为要清除的矩形区域左上角的y坐标
- width为要清除的矩形区域的宽度

## transform

`transform`不仅能实现`移动`、`旋转`和`缩放`，还能实现`斜切`。

### 语法：

`transform(a, b, c, d, e, f)`，

### 参数：

- a：水平缩放，不缩放为1
- b：水平倾斜，不倾斜为0
- c：垂直倾斜，不倾斜为0
- d：垂直缩放，不缩放为1
- e：水平移动，不移动为0
- f：垂直移动，不移动为0

因此不设置参数的时候，默认参数为`transform(1, 0, 0, 1, 0, 0)

### 旋转

```js
    // 获取Canvas
    const canvas = document.getElementById('canvas'); 
    // 获取绘制上下文
    const ctx = canvas.getContext('2d'); 
    // 填充颜色
    ctx.fillStyle="orange"

    // 旋转30度
    const deg = Math.PI/180;
    const c3 = Math.cos(30*deg)
    const s3 = Math.sin(30*deg)
    ctx.transform(c3, s3, -s3, c3, 0, 0)
    ctx.fillRect(0, 0, 200, 200);
```

![image.png](/assets/extend/canvas3.awebp)

## 鼠标事件

click（点击）

dblclick（双击）

mouseover（鼠标移入）支持事件冒泡

mouseout（鼠标移出）支持事件冒泡

mouseenter（鼠标移入）不支持事件冒泡

mouseleave（鼠标移出）不支持事件冒泡

mousedown（鼠标按下）

mouseup（鼠标抬起）

mousemove（鼠标移动）

mousewheel（鼠标滚轮）

## 键盘事件

- keydown（键盘按下）
- keyup（键盘抬起）
- keypress（键盘按下）

## 事件的添加和移除

给Canvas中的元素添加事件我们用的是：`addEventListener()`方法，移除事件用的是`removeEventListener()`方法，也可以通过window添加监测canvas

## 内部元素添加事件

转至pixi.js

## 图片保存

### 所需方法

### toDataURL

`toDataURL()`方法可以返回一个包含图片的`Data URL`。

`Data URL`也就是前缀为 `data:` 协议的URL，其允许内容创建者向文档中嵌入小文件。

语法：
 `toDataURL(type, encoderOptions)`

参数：

- type：`type`为图片格式，默认为`image/png`，也可指定为：`image/jpeg`、`image/webp`等格式
- encoderOptions：`encoderOptions`为图片的质量，默认值 `0.92`。在指定图片格式为 `image/jpeg` 或 `image/webp` 的情况下，可以从 `0` 到 `1` 的区间内选择图片的质量。如果不在这个范围内，则使用默认值 `0.92`。

```js
// 点击截图函数
function clickFn(){
  // 将canvas转换成base64的url
  let url = canvas.toDataURL("image/png"); 
  // 把Canvas 转化为图片
  Img.src = url;
  // 将base64转换为文件对象
  let arr = url.split(",")
  let mime = arr[0].match(/:(.*?);/)[1] // 此处得到的为文件类型
  let bstr = atob(arr[1]) // 此处将base64解码
  let n = bstr.length
  let u8arr = new Uint8Array(n);
  while (n--) {
    u8arr[n] = bstr.charCodeAt(n);
  }
  // 通过以下方式将以上变量生成文件对象，三个参数分别为文件内容、文件名、文件类型
  let file = new File([u8arr], "filename", { type: mime });
  // 将文件对象通过a标签下载
  let aDom = document.createElement("a"); // 创建一个 a 标签
  aDom.download = file.name; // 设置文件名
  let href = URL.createObjectURL(file); // 将file对象转成 UTF-16 字符串
  aDom.href = href; // 放入href
  document.body.appendChild(aDom); // 将a标签插入 body
  aDom.click(); // 触发 a 标签的点击
  document.body.removeChild(aDom); // 移除刚才插入的 a 标签
  URL.revokeObjectURL(href); // 释放刚才生成的 UTF-16 字符串
};
```

## 滤镜

### 所需方法

### getImageData()

`getImageData()`方法可以返回一个`ImageData`对象。

```
ImageData`对象用来描述`canvas`区域隐含的像素数据，此区域通过矩形表示，起始点为`(sx, sy)`、宽为`sw`、高为`sh
```

语法：
 `getImageData(sx, sy, sw, sh)`

参数：

- sx：将要被提取的图像数据矩形区域的左上角 x 坐标。
- sy：将要被提取的图像数据矩形区域的左上角 y 坐标。
- sw：将要被提取的图像数据矩形区域的宽度。
- sh：将要被提取的图像数据矩形区域的高度。

### putImageData()

`putImageData()`方法和`getImageData()`方法正好相反，可以将数据从已有的`ImageData`对象绘制为位图。如果提供了一个绘制过的矩形，则只绘制该矩形的像素。

语法：
 `putImageData(imagedata, dx, dy, dirtyX, dirtyY, dirtyWidth, dirtyHeight)`

参数：

- ImageData：包含像素值的数组对象。
- dx：源图像数据在目标画布中 x 轴方向的偏移量。
- dy：源图像数据在目标画布中 y 轴方向的偏移量。
- dirtyX：可选参数，在源图像数据中，矩形区域左上角的位置。默认是整个图像数据的左上角（x 坐标）。
- dirtyY：可选参数，在源图像数据中，矩形区域左上角的位置。默认是整个图像数据的左上角（y 坐标）。
- dirtyWidth：可选参数，在源图像数据中，矩形区域的宽度。默认是图像数据的宽度。
- dirtyHeight：可选参数，在源图像数据中，矩形区域的高度。默认是图像数据的高度。

知道了这两个方法以后，下面我们简单编写两个方法来做两个主题（滤镜）效果。

## 黑白主题

`blackWhite`函数来实现，具体是减掉颜色的最大色值255来实现

```js
const blackWhite = function() {
    ctx.drawImage(img, 0, 0, 450, 800);
    const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
    const data = imageData.data;
    for (var i = 0; i < data.length; i += 4) {
      var avg = (data[i] + data[i + 1] + data[i + 2]) / 3;
      data[i]     = avg; // red
      data[i + 1] = avg; // green
      data[i + 2] = avg; // blue
    }
    ctx.putImageData(imageData, 0, 0);
};
```

## 曝光主题

黑白主题咱们用一个：`blackWhite`函数来实现，具体是减掉颜色的最大色值255来实现

```js
const exposure = function() {
    ctx.drawImage(img, 0, 0, 450, 800);
    const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
    const data = imageData.data;
    for (var i = 0; i < data.length; i += 4) {
      data[i]     = 255 - data[i];     // red
      data[i + 1] = 255 - data[i + 1]; // green
      data[i + 2] = 255 - data[i + 2]; // blue
    }
    ctx.putImageData(imageData, 0, 0);
};
```

## 拾色器

使用getImageData()

```js
 // 获取 canvas 元素
    var canvas = document.getElementById('canvas');
    // 通过判断getContext方法是否存在来判断浏览器的支持性
    if(canvas.getContext) {
      // 获取绘图上下文
      var ctx = canvas.getContext('2d');
      var img = new Image();
      img.crossOrigin = 'anonymous';
      img.src = 'https://img1.baidu.com/it/u=4141276181,3458238270&fm=253&fmt=auto&app=138&f=JPEG';
      img.onload = function() {
        ctx.drawImage(img, 0, 0, 450, 800);
        img.style.display = 'none';
      };
      var hoveredColor = document.getElementById('hovered');
      var selectedColor = document.getElementById('selected');
      
      canvas.addEventListener('mousemove', function(event) {
        pickColor('move', event, hoveredColor);
      });
      canvas.addEventListener('click', function(event) {
        pickColor('click', event, selectedColor);
      });

      function pickColor(type, event, destination) {
        var x = event.layerX;
        var y = event.layerY;
        var pixel = ctx.getImageData(x, y, 1, 1);
        var data = pixel.data;
        const rgba = `rgba(${data[0]}, ${data[1]}, ${data[2]}, ${data[3] / 255})`;
        destination.style.background = rgba;
        if(type === 'move') {
          destination.textContent = "划过的颜色为：" + rgba;
        } else {
          destination.textContent = "选中的颜色为：" + rgba;
        }
        return rgba;
      }
    }
```

## 签名

canvas.addEventListener

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>canvas - 签名</title>
  <style>
    /* 给画布增加一个阴影和圆角的样式 */
    canvas {
        box-shadow: 0px 0px 5px #ccc;
        border-radius: 8px;
    }
    div {
        width: 450px;
        box-shadow: 0px 0px 5px #ccc;
        border-radius: 8px;
        text-align: center;
    }
  </style>
</head>
<body>
  <canvas id="canvas" width="450" height="300">
      当前浏览器不支持canvas元素，请升级或更换浏览器！
  </canvas>
  <div id="clear">清空画布</div>
  <script>
    // 获取 canvas 元素
    var canvas = document.getElementById('canvas');
    var clear = document.getElementById('clear');
    const ctx = canvas.getContext("2d");
    canvas.addEventListener('mouseenter', () => {
        canvas.addEventListener('mousedown', (e) => {
            ctx.beginPath()
            ctx.moveTo(e.offsetX, e.offsetY)
            canvas.addEventListener('mousemove', draw)
        })
        canvas.addEventListener('mouseup', () => {
            canvas.removeEventListener('mousemove', draw)
        })
    })
    function draw(e) {
        ctx.lineTo(e.offsetX, e.offsetY)
        ctx.stroke()
    }
    clear.addEventListener('click', () => {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
    })

</script>
</body>
</html>

```

## 刮刮奖

使用globalCompositeOperation

语法：`globalCompositeOperation = type`，属性值 type 表示是要使用的合成或混合模式操作的类型。

type属性为不同值时，绘制显示将会不同，具体的类型值我们列一下：

| 属性类型         | 表现形式                                                     |
| ---------------- | ------------------------------------------------------------ |
| source-over      | 默认。在目标图像上显示源图像                                 |
| source-atop      | 在目标图像顶部显示源图像。源图像位于目标图像之外的部分是不可见的。 |
| source-in        | 在目标图像中显示源图像。只有目标图像内的源图像部分会显示，目标图像是透明的。 |
| source-out       | 在目标图像之外显示源图像。只会显示目标图像之外源图像部分，目标图像是透明的。 |
| destination-over | 在源图像上方显示目标图像。                                   |
| destination-atop | 在源图像顶部显示目标图像。源图像之外的目标图像部分不会被显示。 |
| destination-in   | 在源图像中显示目标图像。只有源图像内的目标图像部分会被显示，源图像是透明的。 |
| destination-out  | 在源图像外显示目标图像。只有源图像外的目标图像部分会被显示，源图像是透明的。 |
| lighter          | 显示源图像 + 目标图像。                                      |
| copy             | 显示源图像。忽略目标图像。                                   |
| xor              | 使用异或操作对源图像与目标图像进行组合。                     |

![globalCompositeOperation.jpg](/assets/extend/canvas4.awebp)

## 擦玻璃

使用高斯模糊

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>canvas - 刮刮奖</title>
  <style>
    /* 给画布增加一个阴影和圆角的样式 */
    canvas {
      background-image: url("https://gimg2.baidu.com/image_search/src=http%3A%2F%2Ffile.moyublog.com%2Fd%2Ffile%2F2021-05-29%2Ff8b2a20556774afebed8fd91ccbe0497.jpg&refer=http%3A%2F%2Ffile.moyublog.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1672406341&t=a0b71fded87dd696982c1632cc015397");
      background-size: cover;
      background-position: center;
      box-shadow: 0px 0px 5px #ccc;
      border-radius: 8px;
      float: left;
    }
  </style>
</head>
<body>
  <canvas id="canvas" width="1000" height="500">
    当前浏览器不支持canvas元素，请升级或更换浏览器！
  </canvas>
  <script>
    // 获取 canvas 元素
    var canvas = document.getElementById('canvas');
   
    // 通过判断getContext方法是否存在来判断浏览器的支持性
    if(canvas.getContext) {
      // 获取绘图上下文
      var ctx = canvas.getContext('2d');
      const imageUrl = "https://gimg2.baidu.com/image_search/src=http%3A%2F%2Ffile.moyublog.com%2Fd%2Ffile%2F2021-05-29%2Ff8b2a20556774afebed8fd91ccbe0497.jpg&refer=http%3A%2F%2Ffile.moyublog.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1672406341&t=a0b71fded87dd696982c1632cc015397";

      // 设置画笔
      ctx.lineCap = 'round'
      ctx.lineJoin = 'round'
      ctx.lineWidth = 50

      // 为canvas添加鼠标按下事件
      canvas.addEventListener("mousedown", mousedownFn, false)
      let downX,downY
      // 鼠标按下触发的方法
      function mousedownFn(e) {
        e.preventDefault()
        downX = e.pageX
        downY = e.pageY
        drawLine({startX: downX, startY: downY})
        // 为canvas添加鼠标移动和鼠标抬起事件
        canvas.addEventListener("mousemove", mousemoveFn, false)
        canvas.addEventListener("mouseup", mouseupFn, false)
      }

      // 鼠标移动触发
      function mousemoveFn(e) {
        e.preventDefault()
        const moveX = e.pageX
        const moveY = e.pageY
        drawLine({endX: moveX, endY: moveY})
        downX = moveX
        downY = moveY
      }

      // 鼠标抬起触发
      function mouseupFn() {
        // 鼠标抬起以后移除事件
        canvas.removeEventListener("mousemove", mousemoveFn, false)
        canvas.removeEventListener("mouseup", mouseupFn, false)
      }
        

      // 画线
      function drawLine(position) {
        const { startX, startY, endX, endY } = position
        ctx.beginPath()
        ctx.moveTo(startX, startY)
        ctx.lineTo(endX || startX, endY || startY)
        ctx.stroke()
      }

      drawImage(imageUrl)
      function drawImage(src) {
        const img = new Image()
        img.crossOrigin = ''
        img.src = src
        img.onload = () => {
          const imageAspectRatio = img.width / img.height
          const canvasAspectRatio = canvas.width / canvas.height
          ctx.drawImage( img, 0, 0, canvas.width, canvas.height )

          // 把像素数据模糊化
          var canvasData = ctx.getImageData(0, 0, canvas.width, canvas.height);
          var tempData = gaussBlur(canvasData, 20);
          ctx.putImageData(tempData,0,0);

          // 设置绘制类型
          ctx.globalCompositeOperation = 'destination-out'
        }
      }

      function gaussBlur(imgData) {
        const pixes = imgData.data;
        const width = imgData.width;
        const height = imgData.height;
        const gaussMatrix = [];
        let gaussSum = 0;
        let x;
        let y;
        let r;
        let g;
        let b;
        let a;
        let i;
        let j;
        let k;
        let len;
        const radius = 10;
        const sigma = 20;
        a = 1 / (Math.sqrt(2 * Math.PI) * sigma);
        b = -1 / (2 * sigma * sigma);
        // 生成高斯矩阵
        for (i = 0, x = -radius; x <= radius; x++, i++) {
          g = a * Math.exp(b * x * x);
          gaussMatrix[i] = g;
          gaussSum += g;
        }

        // 归一化, 保证高斯矩阵的值在[0,1]之间
        for (i = 0, len = gaussMatrix.length; i < len; i++) {
          gaussMatrix[i] /= gaussSum;
        }

        // x 方向一维高斯运算
        for (y = 0; y < height; y++) {
          for (x = 0; x < width; x++) {
            r = g = b = a = 0;
            gaussSum = 0;
            for (j = -radius; j <= radius; j++) {
              k = x + j;
              if (k >= 0 && k < width) {
                // 确保 k 没超出 x 的范围
                // r,g,b,a 四个一组
                i = (y * width + k) * 4;
                r += pixes[i] * gaussMatrix[j + radius];
                g += pixes[i + 1] * gaussMatrix[j + radius];
                b += pixes[i + 2] * gaussMatrix[j + radius];
                // a += pixes[i + 3] * gaussMatrix[j];
                gaussSum += gaussMatrix[j + radius];
              }
            }
            i = (y * width + x) * 4;
            // 除以 gaussSum 是为了消除处于边缘的像素, 高斯运算不足的问题
            // console.log(gaussSum)
            pixes[i] = r / gaussSum;
            pixes[i + 1] = g / gaussSum;
            pixes[i + 2] = b / gaussSum;
            // pixes[i + 3] = a ;
          }
        }

        // y 方向一维高斯运算

        for (x = 0; x < width; x++) {
          for (y = 0; y < height; y++) {
            r = g = b = a = 0;
            gaussSum = 0;
            for (j = -radius; j <= radius; j++) {
              k = y + j;
              if (k >= 0 && k < height) {
                // 确保 k 没超出 y 的范围
                i = (k * width + x) * 4;
                r += pixes[i] * gaussMatrix[j + radius];
                g += pixes[i + 1] * gaussMatrix[j + radius];
                b += pixes[i + 2] * gaussMatrix[j + radius];
                // a += pixes[i + 3] * gaussMatrix[j];
                gaussSum += gaussMatrix[j + radius];
              }
            }
            i = (y * width + x) * 4;
            pixes[i] = r / gaussSum;
            pixes[i + 1] = g / gaussSum;
            pixes[i + 2] = b / gaussSum;
          }
        }
        return imgData
      }
    }
  </script>
</body>
</html>

```

