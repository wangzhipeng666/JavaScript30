# Click And Drag 

## 挑战任务
初始文档index-start.html中提供了一组条幅，本次的编程任务需要实现的效果是当鼠标拖动画面移动时，条幅同步向水平方向移动。

## 延伸思考
/*透视距离，即视点位于垂直距离屏幕的距离，数值越大，离的越远，变形效果看起来越微小*/
.items{perspective: 500px;}
/*所有奇数序号的子元素沿X轴放大，并绕Y轴旋转（相当于人绕柱子转一定角度）*/
.item:nth-child(even) { transform: scaleX(1.31) rotateY(40deg); }
/*所有奇数序号的子元素沿X轴放大，并绕Y轴逆向旋转（相当于人绕柱子反转一定角度）*/
.item:nth-child(odd) { transform: scaleX(1.31) rotateY(-40deg); }