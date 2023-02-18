---
### 必要基础知识
 - HTML5 https://www.runoob.com/html/html-tutorial.html
 - JavaScript https://www.runoob.com/js/js-variables.html
 - css https://www.runoob.com/css/css-tutorial.html
 - typeScript https://www.runoob.com/typescript/ts-tutorial.html
### 开发工具
vscode

### 开发环境
node.js

---

### react 基础
#### 概要
     相较于传统的H5,开发更迅速的单页面应用(single page application)框架.
     优点:
     1.根据数据驱动页面显示
     2.组件化开发(conponent概念浓厚)
     3.跨平台性优秀,不仅可以用来开发网页,还可以开发手机APP(react native)
     4.有过spa开发经验的人上手很快,有更简单的语法
     
     缺点:
     1.相较于传统H5,比较笨重,需要build.(spa框架通病)
     
     版本:随着react的更新,现在分两种版本
       1.class component
       2.function component
     两者语法截然不同,生命周期管理也不相同.现今大多数公司已经不再使用class component.本次仅做function component的介绍

#### 开始
##### 构造
<img width="287" alt="WechatIMG351" src="https://user-images.githubusercontent.com/41722601/219898779-f1a4225b-c182-4a30-9814-19e00eab99ac.png">

|文件|作用|
|---|---|
|public/index.html|单页面应用的唯一页面,项目的template|
|src/index.js|react的入口,其中使用react-dom取得template中的id为root的div,并利用render函数挂载后续开发内容(provider以及App component)|
|src/App.js|项目最外层component,route通常定义在此处|
|package.json|项目中是用的lib, 以及一些npm script定义在此处|
|package-lock.json|lib版本锁|
|其他文件以及目录|根据不同项目的架构设计略有不同|

##### command
|command|作用|
|---|---|
|npm start|debug模式启动项目|
|npm build|build生产模式产物|

#### react知识(基本)

##### JSX语法

```javascript

//JSX基本用法
export defalut const Page = () = {

 const title = "标题"
 const list = [{data:"data1"},{data:"data2"}] 
 
 return (
  <div>
   <h5>{title}</h5>
   {!list.length ? (
    <div>这个数组是空的</div>
   ):(
     <ul>
    {list.map((item)=>{
     <li>{item.data}</li>
    })}
    </ul>
   )}
  </div>
 )

}

```
##### 组件化

```javascript

//创建名为sample的组件
const Sample = () = {

 return (
  <div>
   这是一个组件!
  </div>
 )

}

//在page中使用组件
export defalut const Page = () = {

 return (
  <div>
   <Sample/>
  </div>
 )

}

```
##### 父子组件传参

```javascript

//创建名为sample的组件
const Sample = (props) = {
 
 //useEffect具体用法 hook讲解中详细讲解
 useEffect(()=>{
  props.onMsg('给父组件的消息')
 })
 
 return (
  <div>
   {props.msg}
  </div>
 )

}

//在page中使用组件
export defalut const Page = () = {

 return (
  <div>
   <Sample msg={`给子组件的消息`} onMsg={msg=>console.log(msg)}/>
  </div>
 )

}

```

##### css用法
```scss
.sample {
  background-color: red;
 }
```
```javascript

import "./sample.scss"

export defalut const Page = () = {

 const title = "标题"
 const list = [{data:"data1"},{data:"data2"}] 
 
 return (
  <div className="sample">
   css的使用方法 className的prop处写上对应class名即可
  </div>
 )

}

```
#### hook
     先解释下hook,hook其实就是react中一种函数规范,以useXXX的形式命名,返回值通常是obj或者数列,hook本质其实就是把业务模块化
     react提供的方法基本都是hook的形式,现在流行useCase的编程思想,我们每个useCase也可以编写为useXXXUseCase的hook.
     
     以下介绍两个重中之重的hook的作用和用法
1. useState
```
当前component内用来存取数据状态用,数据驱动画面的核心
```
```JavaScript
import { useState } from "react";
export defalut const Page = () = {
 //数列中data是名为data的State的get方法,setData是set方法,''为默认值
 const [data,setData] = useState('')
 
 return (
  <div>
   <div className="title">{data}</div>
   {/* 触发setData后,data的值会发生改变,页面将被立即被重新渲染*/}
   <button onclick={()=>{setData('state的set方法')}}>change title</button>
  </div>
 )

}
```
2. useEffect
```
当前component每次被渲染时被调用的hook,引入useEffect概念让生命周期变得异常的简单
```
```JavaScript
import { useEffect, useState } from "react";
export defalut const Page = () = {

 const [data,setData] = useState('')
 
 const [data2,setData2] = useState('')
 
 useEffect(()=>{
 //页面只要被数据刷新就会调用
 return ()=>{
  //useEffect中的return的函数是component将要销毁时调用的函数(也就是消失的生命周期)
 }
 },[])
 
 useEffect(()=>{
 //data发生改变时才会调用
 },[data])
 
 useEffect(()=>{
 //data2发生改变时才会调用
 },[data2])
 
 useEffect(()=>{
 //data和data2发生改变时才会调用
 },[data,data2])
 
 
 
 return (
  <div>
   <div className="title">{data}</div>
   <button onclick={()=>{setData('1')}}>change title</button>
   <button onclick={()=>{setData2('2')}}>change title2</button>
  </div>
 )

}
```


### react 进阶
```
以上看完并尝试后,进入现场的轻微改修的工作足以胜任,接下来我们看看一些开发时常用到的Lib
```
|库|作用|
|---|---|
|axios|出色的网络异步请求的JS库,并非react专用|
|react-router-dom|react开发必备,用来做画面跳转的路由|
|styled|css-in-js的库,非必须,但有的项目会用到|
|react-query|非常出色的异步处理的库,具有缓存机能,提升性能用,常常配合axios让网络请求更丝滑|
|moment|大家都在用的时间处理工具|
|....|很多很多,不一一赘述|
