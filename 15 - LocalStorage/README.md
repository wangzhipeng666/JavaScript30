# LocalStorage
## 知识点
默认情况下，在表单拥有焦点时按下 Enter 键或者点击提交按钮，会提交表单。提交时，浏览器会在发送请求给服务器之前触发 submit 事件。
解决方法：e.preventDefault()阻止默认事件