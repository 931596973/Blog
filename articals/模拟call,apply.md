# 模拟call, apply, bind实现

## call

call：call() 方法在使用一个指定的 this 值和若干个指定的参数值的前提下调用某个函数或方法 
 
通俗讲就是funtion.protoype.call(obj) 相当于用obj调用function,this指向obj 

要点：1 call改变了this的指向 2 函数执行了 

思路：既然相当于obj调用了function，我们可以将function添加到obj中，然后调用function，最后在删掉function 

```js
V1
Function.prototype.call2 = function(context) {
  // 要获取调用call的函数，用this可以获取
  // 因为函数的this是在调用时确定的
  context.fn = this
  context.fn()
  delete context.fn
}
V2
// call还有第二个参数，及要传入fn的参数
Function.prototype.call2 = function(context, ...args) {
  context.fn = this
  context.fn(...args)
  delete context.fn
}
V3
// 完善
Function.prototype.call2 = function(context = window, ...ages) {
  if ( this === Function.prototype ) {
    return undefined // 用于防止Function.prototype直接调用
  }
  const fn = Symbol()
  context[fn] = this
  const result = context[fn](...args)
  delete context[fn]
  return result
}
```
## apply

apply的实现类似call, 参数为数组

```js
Function.prototype.apply2 = function(context = window, args) {
  if (this === Function.prototype ) return undefined
  const fn = Symbol()
  context[fn] = this
  const result
  // 加一个对参数的判断
  if (Array.isArray(args)) {
    result = context[fn](...args)
  } else {
    result = context[fn]()
  }
  delete context[fn]
  return result
}
```
## bind

特点：与call不同的是，bind会返回一个函数而不是调用它,返回的这个函数的参数既可以在bind的时候传  
也可以在调用这个函数的时候传

```js
V1
Function.prototype.bind2 = function(context) {
  let self = this
  return function() {
    self.apply(context)
  }
}
V2 // c传参
Function.prototype.bind2 = function(context) {
  let self = this
  // 获取调用bind2时传的参数
  // arguments是类数组不能直接调用数组方法
  let args = Array.prototype.slice.call(arguments, 1)
  return function() {
    // 这里是获取向生成的函数传的参数
    let bindArgs = Array.prototype.slice.call(arguments)
    self.apply(context, args.contact(bindArgs))
  }
}
```
## 构造函数效果的实现

bind还有一个特点：当bind返回的函数作为构造函数使用的时候, bind时的this就会失效  
但传入的参数依然生效

```js
Function.prototype.bind2 = function(context) {
  
}