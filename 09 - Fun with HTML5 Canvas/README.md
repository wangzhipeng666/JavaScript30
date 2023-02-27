# HTML5 Canvas 实现彩虹画笔绘画板

## 涉及特性
Canvas：

基本属性
getContext() 获取渲染的上下文
strokeStyle 线条描边的颜色
fillStyle 填充的颜色
lineCap 笔触的形状，有 round | butt | square 圆、平、方三种
lineJoin 线条相交的方式，有 round | bevel | miter 圆交、斜交、斜接三种
lineWidth 线条的宽度

路径绘制
beginPath() 新建一条路径
stroke() 绘制轮廓
moveTo() 路径起点
lineTo() 路径终点

鼠标事件处理
mousemove
mousedown
mouseup
mouseout

## 彩虹渐变颜色——HSL
如何实现彩虹的渐变效果？我们需要利用 HSL 色彩模式，首先可以去这个网站 http://mothereffinghsl.com 感受一下 HSL 不同色彩值对应的效果。

- H代表色调（色相）取值为0~360
- S代表饱和度（掺杂进去的灰度值）取值为0~1 或者百分比
- L代表亮度 取值为0~1 或者百分比

H 值从 0 到 360 的变化代表了色相的角度的值域变化，利用这一点就可以实现绘制时线条颜色的渐变了，只需要在它的值超过 360 时恢复到 0 重新累加即可。
```
let hue = 0;

ctx.strokeStyle = `hsl(${ hue }, 100%, 50%)`;	
if(hue >= 360) hue = 0;
hue++;
```
除此之外，如果想实现黑白水墨的颜色，可以将颜色设置为黑色，通过透明度的改变来实现深浅不一的颜色。

## 过程指南
1. 获取 HTML 中的 <canvas> 元素，并设定宽度和高度
2. getContext('2d') 获取上下文
3. 设定 ctx 基本属性
    - 描边和线条颜色
    - 线条宽度
    - 线条末端形状
4. 绘画效果
设定一个用于标记绘画状态的变量
鼠标事件监听，不同类型的事件将标记变量设为不同值
编写发生绘制时触发的函数，设定绘制路径起点、终点
5. 线条彩虹渐变效果（运用 hsl 的 h 值的变化，累加）
6. 线条粗细渐变效果（设定一个范围，当超出这个范围时，线条粗细进行逆向改变)