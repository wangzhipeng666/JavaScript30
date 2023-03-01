# JS中的引用与复制

## 数组的浅复制
方法一：
Array.prototype.slice()
方法二：
Array.prototype.concat()
方法三：
ES6扩展语法 ...
方法四：
Array.from()

## 对象的浅复制
方法一：
Object.assign(target, sources)
方法二：
JSON.parse(JSON.stringify(sources))
