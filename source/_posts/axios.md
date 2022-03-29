---
title: promise
date: 2022-03-19 21:33:04
tags: 
---

###Why promise?
####传统回调函数
setTimeout
看上去在和主程序并发执行
但他们都运行在同一个主线程中
虽然不会像多线程一样产生资源竞争
####但如果有多层嵌套，你的程序将会是这个样子:
```bath
SetTimeout(()=>{
    console.log('wait 3s');
    setTimeout(()=>{
        console.log('wait 3s')
    },3000)
},3000)
```
会产生可读性差，回调地狱等问题
####而promise的链式调用，会让你的程序是这个样子
```bath
fetch("https://...")
    .then(...)
    .then(...)
```
####promise提供了finally方法，会在promise链结束之后调用,而.catch方法会保证在promise的任意一个阶段发生了错误后执行，并且之后的then将不会被触发

####可以使用finally结束加载动画!
#async await
####(Syntactic sugar)
###async:用来标记一个函数为异步函数，代码如下:
```bath
async function hello(){

}
hello()//always Promise Object
```
###await:替换.then，使代码更加简洁:
```bath
async function f(){
    const response = await fetch("https://...")
}
```
###陷阱1:
```bath
async function f(){
    const a = await fetch("http//")
    const b = await fetch("http//")
}
//会打破fetch()操作的并行,会先a后b
```
###修改一下:
```bath
async function f(){
    const promiseA = fetch("http://")
    const promiseB = fetch("http://")
    const[a,b] = await Promise.all([promiseA,promiseB])
}
```
###陷阱2
####foreach不会暂停等到所有异步操作都执行完毕,即使我们使用了await

###注意点:await只能在异步函数中有效


###ajax

优点: 在无刷新的情况下请求数据并更新
缺点: 存在跨域问题 






