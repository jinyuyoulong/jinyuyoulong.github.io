---
title: "React学习"
date: 2021-05-24T20:37:25+08:00
toc: true
images:
tags: 
  - React
  - ReactNative
---
React学习

## 两个重要的概念：虚拟DOM，diff算法

虚拟DOM：用js对象模拟HTML的DOM树，为了方便比较，减少渲染

diff算法由3种组成：

tree diff DOM树按层对比

component diff 在每层里按组件对比

element diff：在每个组件中 按元素进行对比

## 工程启动流程：

创建webpack：npm init -y 创建dist 和 src文件夹，创建文件src/index.html src/main.js

安装webpack：`npm -i webpack -D`

`yarn add web-dev-server --dev` 自动编译js

```js
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
		"dev": "webpack-dev-server --port 8080 --hot --host"// 最佳实践
  },
```



html-webpack-plugin 将页面生成到内存中去

webpack.config.js文件中的配置

```javascript
// 向外暴露一个打包的对象
module.exports = {
    mode: 'development',// production develoment 设置压缩文件的方式
    // webpack 4.0 中约定大于配置，默认 src/index.js 是入口文件

}
```

---

**react** 专门用来创建组件和虚拟DOM，同时组件的生命周期都在这个包里

**react-dom** 专门进行DOM操作，最主要的应用场景，就是ReactDOM.rander()

实例代码：

```javascript
// 1. 导入
// 2. 创建虚拟DOM元素
// 3. 使用ReactDOM把虚拟DOM渲染到屏幕上

// 导入react的别名必须这么写
import  React  from 'react';
import  ReactDOM  from "react-dom";

// 参数1 创建的元素的类型，字符串，表示元素名称
// 参数2 一个对象或者null，表示这个DOM的属性
// 参数3 子节点 包括其他虚拟DOM获取文本子节点
// 参数n 其他子节点
// <h1 id="myh" title="这是一个h1">这是一个没有感情的h1</h1>
const myh1 = React.createElement('h1', {
    id: 'myh1',
    title: '这是一个h1'
}, "这是一个没有感情的h1")
const mdiv = React.createElement('div',null,'这是一个div',myh1)
// 参数1 目标虚拟DOM
// 参数2 指定页面的容器,一个DOM元素
ReactDOM.render(mdiv, document.getElementById('app'))
```

### JSX = js + xml

JSX 语法本质是通过babel转换成 React.createElement()形式

依赖包：babel-core babel-loader babel-plugin-transform-runtime --dev

关于语法解析的：babel-preset-env babel-preset-stage-0 babel-preset-react --dev

@babel/core、@babel/preset-env、@babel/runtime、@babel/plugin-transform-runtime、@babel/plugin-proposal-class-properties、@babel/preset-react这几个包安装一下，然后在.babelrc文件中添加{"presets":["@babel/preset-env","@babel/preset-react"], "plugins":["@babel/transform-runtime","@babel/plugin-proposal-class-properties"]}



注：react中需要把key添加给被 foreach 或map 或 for循环直接没控制的那些元素（也就是最外层的元素）

jsx 注释：jsx的{}中可以写任何合法的js代码，包括注释

```
{/* 注释单行 */}
{
// 注释多行
}
```

为jsx添加类名，需要用className代替class；htmlFor代替label的for属性

### 组件创建和使用

为组件传递数据

```jsx
// 第一种创建组件方式，组件名称首字母必须大写
function Hello(props) {// 在Props 上获取dog对象
// react 和Vue 中的 props 对象所有属性都是 只读 read only的
    console.log(props.name);
    
    // 返回一个 虚拟DOM
    return <div>这是Hello组件 -- {props.name}-- {props.age} -- {props.gander}</div>
}

{/* 直接将组件名称以标签的形式，丢到页面上 */}
<Hello name={dog.name} age={dog.age} gander={dog.gander}></Hello>
```

react chrome开发插件 react developer tools

**注：组件名称首字母必须大写**

默认不做单独的配置的话，不能省略后缀名 
可以配置webpack.config.js 省略后缀名

@代表src目录 配置webpack的alias 字段

```
import Hello from '@/components/Hello'
```

### class 属性

this.props 只读

this.state 可读可写

class 有私有属性state 和生命周期

### JSX style 样式

{*/\* jsx中的样式写法{{color: 'red'}} \*/*}

```js
css文件
.title{
    color: red;
}
-----
webpack 配置 解析css ，依赖包 style-loader css-loader
{test: /\.css$/,use: ['style-loader','css-loader?modules']}// 打包处理css样式表，从右向左 处理，css处理完交给style处理 
            // style-loader loader不嫩省略，webpack 1.0 用的是 style，后边都加-loader了，搜blog不要被误导
自定义 样式对象的名称
css-loader?modules&localIdentName=[path][name]-[local]-[hash:3]
path src-css
name 文件name
local css中的样式名称
hash 默认全length
-----
使用
import cssObj from "@/css/cssList.css";
<h1 className="title">这是评论列表组件</h1>
cssObj是全局的，整个项目都生效
```

解决样式冲突：vue `<style scoped>`

  css 模块化只针对 class和id 不作用于标签

:global 全局，不模块化

自己的样式用scss结尾

第三方的用css结尾，这样就区分了个人和其他

`sass-loader node-sass`

### 绑定事件

最佳实践

```js
<button onClick={()=>{this.myClickHandler()}}>按钮</button>
 myClickHandler = ()=>{        console.log('点击事件');       }
```

箭头函数本身是一个匿名函数，和匿名函数不同的是会改变this指针的指向，它会根据环境选择箭头外部的那个对象。

修改数据使用this.setState({msg:'改'}), 是异步执行的

### JSX注释折叠

```
//#region
// 我是JSX注释
//#endregion
```

### *实现双向数据绑定*

```jsx
 <input type="text" value={this.state.msg} onChange= {(e)=>this.txtChanged(e)} />
 
  txtChanged = (e)=>{
        // console.log(this.refs.txt.value);
        // console.log(e.target.value);

        //  实现双向数据绑定
        const newValue = e.target.value
        this.setState({
            msg: newValue
        })
    }
```

## 第三方库使用 ant

插件 react-app-rewired 替换 react-scripts 实现按需加载css

babel-plugin-import