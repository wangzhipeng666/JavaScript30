# Speech Detection 语音侦测
## 挑战任务
本次的挑战任务，是利用浏览器内置Web speech API,将自己所说的话输出在页面上,仅chrome浏览器支持。
说明：由于只有chrome浏览器实现了该接口，而语音识别需要将捕捉到的信息发送至google服务器进行处理，故本文档只提供解决思路和参考代码。

## 相关知识
有关语音识别接口SpeechRecognition的说明，可查看MDN中的相关解释。
https://developer.mozilla.org/zh-CN/docs/Web/API/SpeechRecognition

## 基本思路
1. 新建语音识别对象;
2. 开启语音识别服务;
3. 通过监听result事件，实时获取捕获到的语音信息;
4. 通过监听end事件，当一次语音捕获结束后，重新开启该功能，实现持续的语音监听功能。

## 过程指南
1. 由于目前只有chrome浏览器实现了此功能，故直接使用带有前缀的构造函数来构建一个语音识别对象。
var speech = new webkitSpeechRecognition();

2. 设置语音识别对象的基本属性，并开启该功能。
```
speech.interimResults = true;
// 返回即时语音，即时语音是指SpeechRecognitionResult.isFinal 为false时捕获到的信息。
speech.lang = 'en-US';//设置语音识别类别为英语
speech.start();//开启功能
```

3. 监听收到结果事件，将语音识别结果输出在DOM元素上。
```
speech.addEventListener('result', (e) => {
    const results = Array.from(e.results) 
    // e.results中保存的是识别的结果，本来并不是数组，需要将其转换为数组，方便使用其map、join等方法。
    .map(result => result[0])
    .map(result => result.transcript) // 获取到每一段话，是一个数组类型
    .join(''); // 将每一段话连接成字符串
    // 将结果输出在页面上
    words.innerHTML = results;
}
```