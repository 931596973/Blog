# new

## new 做的事情

经过new创造的实例可以访问构造函数中的属性和构造函数prototype中的属性   
因为new是关键字，所以用一个函数来模拟实现

## verson 1
```js
function objectFactory() {
  let obj = {}
  let Constructor = [].shift.call(arguments)
  obj._proto_ = Constructor.prototype
  Constructor.apply(obj, arguments)
  return obj
}
```
## 返回值效果实现

JavaScript构造函数一般没有return语句，如果返回基本数据类型，则会忽略，如果返回对象，则返回该对象   
```js
function objectFactory() {
  let obj = {}
  let Constructor = Array.prototype.shift(arguments)
  obj._proto_ = Constructor.prototype
  let ret = Constructor.apply(obj, arguments)
  return typeof ret === 'object'? ret: obj
}
```
