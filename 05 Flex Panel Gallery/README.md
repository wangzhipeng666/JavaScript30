# 过程指南
## CSS 部分
CSS 在这个过程中占了重点，运用 flex 可以使各个元素按一定比例占据页面。在调试的时候，可以把边框显示出来方便查看效果。（border: 1px solid #f00;）
1. 将 .panels 设置为 display:flex
2. 设定每个子 panel 的 flex 值为 1
3. 针对每个子 panel，设为 display:flex，设置其 flex 主轴方向
4. 控制 .panle 的子元素 <p> 中的文字垂直、水平居中（单独看每个 panel，其中的文字也可以用 flex 的思路来使其三等分后居中）
    - 设置为 display:flex
    - 设置 flex 值
    - 设置其子元素的布局方式：垂直水平居中（沿主轴、侧轴居中）
5. 设定点击图片后文字移动的样式
6. 设定点击图片展开后的图片的 flex 值

## JS 部分
1. 获取所有类名为 panel 的元素
2. 为其添加 click 事件监听，编写触发事件调用的函数（给触发的 DOM 元素添加/去掉样式，实现拉伸/压缩的效果）
3. 为其添加 transitionend 事件监听，编写调用的函数（添加/去掉样式，实现文字的飞入/飞出效果）

# 基础知识
## CSS
### 针对 Flex items 的特性
flex-grow：伸展值
flex-shrink：可接受的压缩值
flex-basis：元素默认的尺寸值
flex：以上三个值按顺序的缩写

# 延伸思考
在 index-01.html 的解决方案中，用了两种 class 值来分别控制 div 元素和 p 元素的动画，这就会造成一个问题，当快速点击两下时，会出现相反的组合（图片缩小 + 上下文字出现）。

那为什么还要将文字的移动动画用 .open-actived 这个类来控制，同时还多加上了一个 transitionend 的事件监听，而不是直接用 .open 控制文字的移动，并且只采用一个 click 事件监听呢？
我试了一下，发现如果将要触发的文字移动（transform）用 .open 来控制，那么会出现有点不协调的状况。

### 解决方案：
去掉对于 transitionend 的事件监听
```
.panel > * {
	/* ... */
	transition:transform 0.5s 0.7s;
}

/* 修改 .open-actived -> .open*/
.panel.open p:first-child {
	transform: translateY(0);
}

.panel.open p:last-child {
	transform: translateY(0);
}
const panels = document.querySelectorAll('.panel');

function toggleOpen(e) {
    this.classList.toggle('open');
}
panels.forEach( panel => panel.addEventListener('click', toggleOpen, false));
```
