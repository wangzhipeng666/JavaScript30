# 步骤分解
1. 添加键盘事件监听。在 window 上添加键盘 keydown 事件。
2. 对应事件处理程序。
  - 获取键码
  - 用 querySelector 获取元素
  - 获取 data-key 为对应键码的元素
  - 处理元素。播放音频、添加样式。
3. 为所有的 div.key 添加 transitionened 事件。
  - 获取所有样式为 key 的元素
  - 为其添加事件监听
4. 去除样式的事件处理程序
# 基础语法
## CSS
### text-transform 控制文本的大小写
属性：
1. none: 默认。定义带有小写字母和大写字母的标准的文本。
2. capitalize: 文本中的每个单词以大写字母开头。
3. uppercase: 定义仅有大写字母。
4. lowercase: 定义无大写字母，仅有小写字母。

## JS
1. const 声明一个只读的常量，标识符的值只能赋值一次。
2. forEach 函数可以用来遍历NodeList对象（此对象是对于文档的实时运行的动态查询）

## 解决难点
### 如何保证按键被按住不放时，可以马上响起连续鼓点声？
每次播放音频之前，设置播放时间戳为 0：
```
var audio = document.getElementById("video"); 
audio.currentTime = 0;
audio.play();
```

