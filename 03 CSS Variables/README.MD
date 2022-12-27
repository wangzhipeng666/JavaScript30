# 步骤分解
1. 声明全局（:root）的 CSS 变量
2. 将变量应用到页面中对应元素 <img>
3. 处理标题的 CSS 值
4. 获取页面中 input 元素
5. 给每个input添加change监听事件和鼠标滑动事件
6. 更改:root中对应CSS变量的值
# 基础语法
## HTML
1. HTML5自定义属性
HTML5 中可以为元素添加非标准的自定义属性，只需要加上 data- 前缀，可以随便添加和命名。添加之后，可以通过元素的 dataset 属性来访问这些值，dataset 的值是 DOMStringMap 的一个实例化对象，其中包含之前所设定的自定义属性的“名-值”对。
2. document.documentElement
document.documentElement代表文档根元素，即html标签。
## CSS
1. var()定义css变量（IE 和 Edge 目前都还不支持）
命名写法是 --变量名，在引用这个变量时写法是 var(--变量名)。
2. :root伪类
这个伪元素匹配的是文档的根元素，也就是 <html> 标签。
所以常用于声明全局的 CSS 变量：
```
:root {
  --color: #fff;
}
```
```
img {
  background: var(--base);
}
```
3. CSS 滤镜 filter
## JS
NodeList 和 Array 的区别
可以根据控制台查看__proto__原型上的方法。NodeList只具有少数方法，例如forEach()、keys()等。
