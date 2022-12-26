# 步骤分解
1. 表盘上指针的样式：旋转的效果
2. 获取实时的时间
3. 每一秒改变一次指针状态

# 基础语法
## CSS
1. 调整指针的初始位置以及旋转的轴点 transform-origin
```
transform-origin: 100%; // 或者可以用 right
```
2. 调整时钟指针跳动时的过渡效果
```
transition: all .5s;
```
3. 设置指针成为回弹的形式 设置 transition-time-function 的值，以实现秒针“滴答滴答”的效果

## JS 部分

## 延伸思考
此处存在一个小瑕疵，当秒针旋转一圈之后回到初始位置，开始第二圈旋转，角度值的变化时 444° → 90° → 96° .... 这个过程中，指针会先逆时针从 444° 旋转至 90°，再继续我们期望的顺时针旋转，由于秒针变换时间只有 0.05s，所以呈现的效果就是秒针闪了一下，如果想要观察细节，可以将 .second 设为 transition: all 1s。要解决这个问题，目前找到了两种解决办法：
#### 方法一
在这个特殊点将指针的 transition 属性去掉，由于距离短、时间短，将逆时针回旋的过程瞬间完成。
```
if (secondDeg === 90) secHand.style.transition = 'all 0s';
else secHand.style.transition = 'all 0.05s';

if (minDeg === 90) minHand.style.transition = 'all 0s';
else minHand.style.transition = 'all 0.1s';
```
#### 方法二
既然引发问题的是角度的大小变化，那就可以对这个值进行处理。此前的代码中，每秒都会重新 new 一个 Date 对象，用来计算角度值，但如果让这个角度值一直保持增长，也就不会出现逆时针回旋的问题了。

只在页面第一次加载时 new 一次 Date 对象，此后每秒直接更新角度值。
```
let secondDeg = 0,
minDeg = 0,
hourDeg = 0;

function initDate() {
	const date = new Date();
	const second = date.getSeconds();
	secondDeg = 90 + (second / 60) * 360;
	const min = date.getMinutes();
	minDeg = 90 + (min / 60) * 360 + ((second / 60) / 60) * 360;
	const hour = date.getHours();
	hourDeg = 90 + (hour / 12) * 360 + ((min / 60) / 12) * 360 + (((second / 60) / 60) / 12) * 360;
}

function updateDate() {
	secondDeg += (1 / 60) * 360;
	minDeg += ((1 / 60) / 60) * 360;
	hourDeg += (((1 / 60) / 60) / 12);
	
	secHand.style.transform = `rotate(${ secondDeg}deg)`;
	minHand.style.transform = `rotate(${ minDeg }deg)`;
	hourHand.style.transform = `rotate(${ hourDeg }deg)`;
}

initDate();
setInterval(updateDate, 1000);
```