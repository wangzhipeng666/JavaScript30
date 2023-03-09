# Speech Synthesis 阅读器

## 挑战任务
初始文档index-start.html提供了一个阅读器，你需要完成如下编程任务：
1. 使用相应的WebAPI接口获得浏览器支持的语言种类列表，并填充至页面的下拉菜单中，选择中文;
2. 在文本域中输入对应语言的文字，点击speak按钮后浏览器会阅读输入的文字；
3. 在浏览器阅读时，点击stop按钮，浏览器会停止阅读；
4. 拖动rate和pitch滑块可改变阅读速度和音高。

## 相关知识
1. SpeechSynthesisUtterance接口
本接口用于设置阅读器阅读的配置参数，包括语言，阅读速度，语调等，实例化SpeechSynthesisUtterance后，可以通过为其属性赋值来完成参数配置，详细信息请直接参考MDN中的SpeechSynthesisUtterance接口说明。
2. SpeechSynthesis接口
本接口用于控制阅读器行为，包括获取浏览器支持的朗读语言，文本朗读，暂停，停止等，接口属性中定义有paused,speaking等只读属性来表明当前的状态,详细使用方式请参考MDN中的SpeechSynthesis接口说明。

