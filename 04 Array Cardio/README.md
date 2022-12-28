# 调试技巧
>     console.table()  // 可以在控制台输出表格

# 步骤分解
1. 筛选 16 世纪出生的发明家
2. 展示他们的姓和名
3. 把他们按照出生日期从大到小进行排序
4. 计算所有的发明家加起来一共活了多少岁
5. 按照他们活了多久来进行排序
6. 筛选出一个网页里含有某个词语的标题
7. 按照姓氏来进行排序
8. 统计给出数组中各个物品的数量

# 相关知识
## filter
筛出运行结果是 true 的组成数组返回。
```
const fifteen = inventors.filter(inventor => inventor.year >= 1500 && inventor.year < 1600);
console.table(fifteen);
```
## map
把数组中的每个元素进行处理后，返回一个新的数组。
```
const fullNames = inventors.map(inventor => inventors.first + ' ' + inventor.last);
console.log(fullNames);
```
## sort
默认情况下，Array.prototype.sort() 会将数组以字符串的形式进行升序排列（10 会排在 2 之前），但 sort 也可以接受一个函数作为参数。
```
const ordered = inventors.sort((a, b) => a.year > b.year ? '1' : '-1');
console.table(ordered);
```
## reduce
归并数组的方法，它接受一个函数作为参数（这个函数可以理解成累加器）。
```
const totalYears = inventors.reduce((total, inventor) => {
    return total + (inventor.passed - inventor.year);
}, 0);
console.log(totalYears);
```