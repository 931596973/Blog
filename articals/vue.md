# Vue

## v-show 与 v-if 的区别

+ v-show只是CSS级别的display:none 和display:block之间的切换，v-if是动态的向DOM树中添加删除DOM元素
+ 对于频繁操作显隐的情况下使用v-show，对于一次渲染完的使用v-if
+ v-if 的性能优化：v-if = "false" 时，对应的组件是不会渲染的，所以可以将在特定条件下才需要渲染的组件设置为false，需要时（或异步，比如$nextTrick）在设置为true

## computed 和 watch 的区别

+ computed 是自动监听依赖值的变化， watch 是一个过程，在监听的值变化时，触发一个回调，并做一些事情
+ 只需要动态值时用 computed, 需要知道值改变后的业务逻辑，用 watch

## vue响应式原理

根据Object.defineProperty设置getter、setter来追踪变化。   
对于一个属性name，我们需要当name变化时，所有用到name的地方都更新，所以要先收集依赖，每当用到name 属性的时候都会触发getter，   
所以在getter中收集依赖，在setting中触发依赖，（即知道name属性发生了变化）   
每一个属性都有一个Dep数组用来存储依赖（即所有用到那么的地方都是Dep数组的一项，那么这每一项又究竟是什么呢？就是Watcher   

## vue检测变化注意事项

vue无法检测property的添加或移除，因为用Object.defineProperty将属性转化为可监测的过程是在vue初始化的过程中进行的，所以property必须在 data 对象上   
存在，vue才能将它转换为响应式的。

对于数组，不能检测一下数组的变动   
1、通过索引直接设置一个数组项时  
2、修改数组的长度时   
因为监测数组的变化采用的方式是通过拦截原型的方式实现的

## vue的data为什么必须是函数

每一个vue组件都是一个vue实例，而vue中的data是原型上的属性，且属于引用类型，一个实例修改了data，会对别的实例产生影响

## vue-router 的history和hash模式的区别
+ 默认情况下是hash模式，且hash模式下，url中带有#号，hash模式跳转是window监听onhashchange事件进行的
+ history模式下，url中没有#，跳转利用的是history.pushstate的API，来替换url，但服务器没有重新请求页面，所以如果F5刷新页面，   
页面会显示404，解决办法将不存在的路径请求重定向到入口文件
