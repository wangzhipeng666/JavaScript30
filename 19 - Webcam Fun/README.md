# Webcam Fun 中文指南
## 挑战任务
在index-start.html中提供了一个名为Take Photo的按钮，该按钮的点击事件会触发takePhoto()函数，并提供了一组标有RGBmin/max标记的range类型input元素，一个canvas元素，一个video元素，以及带有strip类名的空div元素。
本次的编程任务：
1. 通过编写javascript代码，请求调用用户的网络摄像头;
2. 在页面上展示来自webcam的数据流信息;
3. 并允许用户保存展示的照片;
4. 及使用滑块来改变图像的色彩。

## 相关知识
1. window.navigator对象
window.navigator对象上有很多有趣的属性和方法，通过调用相应的方法可以查看到有关当前脚本运行环境(多为浏览器)的相关信息，并使用一些扩展功能。对此不熟悉的开发者可以浏览MDN中相关API的介绍，例如使用getBattery()可以获取电池状态。
https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator
2. navigator.getUserMedia方法
getUserMedia方法为我们提供了访问网络摄像头或麦克风的权限，该方法接受一个对象作为参数，通过该对象即可获得来自多媒体设备的数据。
3. canvas标签
HTML5强大的扩展功能之一，提供了丰富的图像绘制方法，也是HTML可以作为游戏开发工具的原因之一，本次开发中使用canvas.getContext('2d')提供的图像操作方法.
4. 像素数组
使用canvas绘图上下文中的getImageData()获得的像素信息为一个定型数组，每个像素点的rgba色彩信息分别存放在数组中，故数据的格式为：[第一像素r值，第一像素g值，第一像素b值，第一像素a值，第二像素r值，第二像素g值......]，通过各类函数公式对像素数据进行处理即可获得各类不同的滤镜效果。

## 基本思路
1. 调用navigator.getUserMedia()方法，若调用成功则返回数据流，若调用失败则在控制台打印相关信息;
2. 成功调用网络摄像头后，将返回的数据对象绑定至video标签的srcObject属性(注意此处getUserMedia()方法成功调用时触发的回调函数中会传递一个stream对象,该对象直接赋值给video.src是没有作用的)，并当流数据开始传递时，视频自动播放;
3. 点击takePhoto()函数时调用canvas绘图上下文中的drawImage()方法将视频中当前帧的图像绘制在canvas上，该方法第一个参数可以为图像或视频，其余参数与绘图区域尺寸相关;
4. 滤色：在全局中保存滤色范围的上下限，每次滑块数据发生改变后，使用canvas绘图上下文中的getImageData()获得画布上指定区域内各像素点的颜色数据，数据被保存在返回对象的data属性中，通过遍历修改像素色彩数组中的数据改变图像的表现，修改后调用putImageData()方法将像素点重新绘制在canvas上。