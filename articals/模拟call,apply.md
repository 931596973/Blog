# 模拟call,apply实现

## call

call：call() 方法在使用一个指定的 this 值和若干个指定的参数值的前提下调用某个函数或方法 
 
通俗讲就是funtion.protoype.call(obj) 相当于用obj调用function,this指向obj 

要点：1 call改变了this的指向 2 函数执行了 

思路：既然相当于obj调用了function，我们可以将function添加到obj中，然后调用function，最后在删掉function 

```js
Function.prototype.call2 = function(context) {

}
 


