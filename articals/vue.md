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

