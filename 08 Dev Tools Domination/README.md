# console 调试技巧指南

## 给页面标签添加断点
在 Elements 选项卡之中，选择页面的某个标签（以 <p>为例），右键 → Break on → Attributes modifications。

## .log 的更多用法
console.log("输出一个字符串 %s ", "log"); // 输出一个字符串 log
console.log("输出一个整数是 %d ", 1.23); // 输出一个整数是 1
console.log("输出一个小数是 %f ", 1.23); // 输出一个小数是 1.23
console.log("%c不同样式的输出效果", "color: #00fdff; font-size: 2em;");

## 不同样式的输出
// warning!
console.warn("三角感叹号图标，淡黄色背景");
// Error :|
console.error("红叉图标，红字红色背景");
// Info
console.info("蓝色圆形感叹号图标");

## 打印输出 DOM 元素
获取 DOM 元素之后，也可以打印输出。
```
const p = document.querySelector('p');
console.log(p);
console.dir(p);
```
不同的地方在于，log 输出这个 DOM 的 HTML 标签，而 dir 则会输出这个 DOM 元素的属性列表。

## 清空 console 面板输出内容
要清空已经打印输出的内容，有两种方式，一种是 JavaScript 语句： console.clear()。另一个是快捷键 Ctrl ＋ L。

## assert方法进行测试
接受一个表达式作为参数，如果参数返回值是 false，则会输出第二个参数中的内容。
```
console.assert(1 ===1, "（这句发布时删除）");
console.assert(1 ===0, "看看看，失策了吧");
console.assert(p.innerHTML.match("她"), "我这儿才没有她这个人");
```

## 以更清晰的形式输出数据
```
console.table(dogs);
console.table(dogs, ["age"]);
```

除了按表格，还可以将数据分组展示，直接看例子：
```
const dogs = [{ name: 'Snickers', age: 2 }, { name: 'hugo', age: 8 }];
dogs.forEach(dog => {
	console.group();		
//	console.groupCollapsed();  // 收起列表
	console.log(`${dog.name}`);
	console.log(`${dog.age}`);
	console.log(`${dog.name} 有 ${dog.age} 岁了`);
	console.groupEnd();
});
```

## count 计数
这里的计数对象仅限于由 count() 输出的内容（判断内容是否一致），并非所有 console 中的输出。

## time 计时
用 time("name") 和 timeEnd("name") 分别控制开始点和结束点，它们两的参数表示当前计时的名称，可以自定义但需要保持相同。所以如果想看异步获取数据花了多长时间，可以这样写：

console.time('fetch my data');
fetch("https://api.github.com/users/soyaine")
  .then(data => data.json())
  .then(data => {
  console.timeEnd('fetch my data');
  console.log(data);
});
如果 timeEnd 中的名称如果和上面不一样，得到的数据是系统当前时间换算后的毫秒值。