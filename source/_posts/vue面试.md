---
title: vue面试
tags: Vue
---

###MVVM
#####视图模型双向绑定 Moedel代表数据 View代表UI组件,ViewModel是View和Model层的桥梁， 数据 会绑定到viewModel层并自动将数据渲染到页面中，视图 变化时会通知ViewModel层更新数据
由DOM结构更新视图 =》 数据驱动视图


###Vue双向绑定原理
#####数据劫持 结合 发布者-订阅者模式，Observer通过Object.defineProperty() = > proxy()来劫持setter / getter ,在数据变动时发布消息给订阅者(watcher),触发相应的回调(complie)
Observer（数据监听器） : Observer的核心是通过Object.defineProprtty()来监听数据的变动，这个函数内部可以定义setter和getter，每当数据发生变化，就会触发setter。这时候Observer就要通知订阅者，订阅者就是Watcher

Watcher（订阅者） : Watcher订阅者作为Observer和Compile之间通信的桥梁，主要做的事情是：

在自身实例化时往属性订阅器(dep)里面添加自己
自身必须有一个update()方法
待属性变动dep.notice()通知时，能调用自身的update()方法，并触发Compile中绑定的回调

Compile（指令解析器） : Compile主要做的事情是解析模板指令，将模板中变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加鉴定数据的订阅者，一旦数据有变动，收到通知，更新试图

###vue生命周期

create阶段：vue实例被创建
#####beforeCreate: 创建前，此时data和methods中的数据都还没有初始化
#####created： 创建完毕，data中有值，未挂载
mount阶段： vue实例被挂载到真实DOM节点
#####beforeMount：可以发起服务端请求，去数据
#####mounted: 此时可以操作DOM
update阶段：当vue实例里面的data数据变化时，触发组件的重新渲染
#####beforeUpdate :更新前
#####updated：更新后
destroy阶段：vue实例被销毁
#####beforeDestroy：实例被销毁前，此时可以手动销毁一些方法
#####destroyed:销毁后

###发送网络请求时机
####created 阶段的优势是：请求时间比较早，页面 loading 时间相对较短；（调用异步请求最佳，用户就越早感知页面的已加载）

####mounted 阶段的优势是：页面已经渲染完成，如果想请求之后进行 DOM 操作的话，必须在 mounted 阶段发起请求

###组件生命周期
生命周期（父子组件） 父组件beforeCreate --> 父组件created --> 父组件beforeMount --> 子组件beforeCreate --> 子组件created --> 子组件beforeMount --> 子组件 mounted --> 父组件mounted -->父组件beforeUpdate -->子组件beforeDestroy--> 子组件destroyed --> 父组件updated

加载渲染过程 父beforeCreate->父created->父beforeMount->子beforeCreate->子created->子beforeMount->子mounted->父mounted

挂载阶段 父created->子created->子mounted->父mounted

父组件更新阶段 父beforeUpdate->父updated

子组件更新阶段 父beforeUpdate->子beforeUpdate->子updated->父updated

销毁阶段 父beforeDestroy->子beforeDestroy->子destroyed->父destroyed


###computed与watch

通俗来讲，既能用 computed 实现又可以用 watch 监听来实现的功能，推荐用 computed， 重点在于
#### computed 的缓存功能
computed 计算属性是用来声明式的描述一个值依赖了其它的值，当所依赖的值或者变量 改变时，计算属性也会跟着改变； watch 监听的是已经在 data 中定义的变量，当该变量变化时，会触发 watch 中的方法。

watch 属性监听 是一个对象，键是需要观察的属性，值是对应回调函数，主要用来监听某些特定数据的变化，从而进行某些具体的业务逻辑操作,监听属性的变化，需要在数据变化时执行异步或开销较大的操作时使用

computed 计算属性 属性的结果会被缓存，当computed中的函数所依赖的属性没有发生改变的时候，那么调用当前函数的时候结果会从缓存中读取。除非依赖的响应式属性变化时才会重新计算，主要当做属性来使用 computed中的函数必须用return返回最终的结果 computed更高效，优先使用。data 不改变，computed 不更新。

#####使用场景 
#####computed：当一个属性受多个属性影响的时候使用，例：购物车商品结算功能
#####watch：当一条数据影响多条数据的时候使用，例：搜索数据

#### 组件中的data为什么是一个函数？
+ 一个组件被复用多次的话，也就会创建多个实例。本质上，这些实例用的都是同一个构造函数。 2.如果data是对象的话，对象属于引用类型，会影响到所有的实例。所以为了保证组件不同的实例之间data不冲突，data必须是一个函数。

#### 为什么v-for和v-if不建议用在一起
+ 当 v-for 和 v-if 处于同一个节点时，v-for 的优先级比 v-if 更高，这意味着 v-if 将分别重复运行于每个 v-for 循环中。如果要遍历的数组很大，而真正要展示的数据很少时，这将造成很大的性能浪费
这种场景建议使用 computed，先对数据进行过滤
+ 注意：3.x 版本中 v-if 总是优先于 v-for 生效。由于语法上存在歧义，建议避免在同一元素上同时使用两者。比起在模板层面管理相关逻辑，更好的办法是通过创建计算属性筛选出列表，并以此创建可见元素。
解惑传送门 ☞ # v-if 与 v-for 的优先级对比非兼容


#### React/Vue 项目中 key 的作用


+ key的作用是为了在diff算法执行时更快的找到对应的节点，提高diff速度，更高效的更新虚拟DOM;
vue和react都是采用diff算法来对比新旧虚拟节点，从而更新节点。在vue的diff函数中，会根据新节点的key去对比旧节点数组中的key，从而找到相应旧节点。如果没找到就认为是一个新增节点。而如果没有key，那么就会采用遍历查找的方式去找到对应的旧节点。一种一个map映射，另一种是遍历查找。相比而言。map映射的速度更快。


+ 为了在数据变化时强制更新组件，以避免“就地复用”带来的副作用。
当 Vue.js 用 v-for 更新已渲染过的元素列表时，它默认用“就地复用”策略。如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序，而是简单复用此处每个元素，并且确保它在特定索引下显示已被渲染过的每个元素。重复的key会造成渲染错误。


#### vue组件的通信方式

+ Vuex
+ props
+ $emit
+ bus全局事件总线
+ ref获取组件实例调用其属性 或者方法 
+ Provide,inject / $attrs、$listeners (跨级组件通信)


####nextTick的实现

nextTick是Vue提供的一个全局API,是在下次DOM更新循环结束之后执行延迟回调，在修改数据之后使用$nextTick，则可以在回调中获取更新后的DOM；
Vue在更新DOM时是异步执行的。只要侦听到数据变化，Vue将开启1个队列，并缓冲在同一事件循环中发生的所有数据变更。如果同一个watcher被多次触发，只会被推入到队列中-次。这种在缓冲时去除重复数据对于避免不必要的计算和DOM操作是非常重要的。nextTick方法会在队列中加入一个回调函数，确保该函数在前面的dom操作完成后才调用；
比如，我在干什么的时候就会使用nextTick，传一个回调函数进去，在里面执行dom操作即可；
我也有简单了解nextTick实现，它会在callbacks里面加入我们传入的函数，然后用timerFunc异步方式调用它们，首选的异步方式会是Promise。这让我明白了为什么可以在nextTick中看到dom操作结果。

####nextTick的实现原理是什么？

在下次 DOM 更新循环结束之后执行延迟回调，在修改数据之后立即使用 nextTick 来获取更新后的 DOM。 nextTick主要使用了宏任务和微任务。 根据执行环境分别尝试采用Promise、MutationObserver、setImmediate，如果以上都不行则采用setTimeout定义了一个异步方法，多次调用nextTick会将方法存入队列中，通过这个异步方法清空当前队列。
####使用过插槽么？用的是具名插槽还是匿名插槽或作用域插槽

vue中的插槽是一个非常好用的东西slot说白了就是一个占位的 在vue当中插槽包含三种一种是默认插槽（匿名）一种是具名插槽还有一种就是作用域插槽 匿名插槽就是没有名字的只要默认的都填到这里具名插槽指的是具有名字的

####keep-alive的实现
作用：实现组件缓存，保持这些组件的状态，以避免反复渲染导致的性能问题。 需要缓存组件 频繁切换，不需要重复渲染
场景：tabs标签页 后台导航，vue性能优化
原理：Vue.js内部将DOM节点抽象成了一个个的VNode节点，keep-alive组件的缓存也是基于VNode节点的而不是直接存储DOM结构。它将满足条件（pruneCache与pruneCache）的组件在cache对象中缓存起来，在需要重新渲染的时候再将vnode节点从cache对象中取出并渲染。
