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
