---
title: "Redux学习"
date: 2021-05-24T20:42:39+08:00
toc: true
images:
tags: 
  - React
  - ReactNative
---
yarn global add create-react-app

create-react-app demo0

yarn add antd

yarn add redux

mkdir src/store



redux dev chrome插件 开发用，在GitHub上redux项目看开发环境配置方式

```js
const store = createStore(reducer,
    // window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
                          
                          //如果浏览器有这个方法，就执行它。
    )
```

```js
export default (state = defaultState, action)=>{
    console.log(state,action);
    // ** Reducer里只能接受state ，不能改变state 
    if (action.type === 'changeInput') {
        // 所以用一个深拷贝接受state
        let newState = JSON.parse(JSON.stringify(state))
        newState.inputValue=action.value
        return newState // 这里返回给store，让store修改变量，reducer不干这事
    }
    return state
}
```

```js
// 监听绑定，新版本不用写也可以监听，但是视图层没有同步更新数据，所以还是要写这个
this.storeChange=this.storeChange.bind(this)
store.subscribe(this.storeChange)

value={this.state.inputValue}

storeChange(){
        this.setState(store.getState())
}
```

小技巧

```js
// file actionTypes.js
// action 配置文件
// 便于找错和code复用
export const CHANGE_INPUT = 'changeInput'
export const CHANGE_ADD = 'addItem'
export const CHANGE_DELETE = 'deleteItem'
```

redux三个小坑

- store必须是唯一的，多个store是坚决不允许的，只能有一个store空间
- 只有store能改变自己的内容，Reducer不能改变
- Reducer必须是纯函数

先来看什么是纯函数，纯函数定义：

> 如果函数的调用参数相同，则永远返回相同的结果。它不依赖于程序执行期间函数外部任何状态或数据的变化，必须只依赖于其输入参数。

比如传入date作为参数就不叫纯函数

工程化

TODOListUI.js UI 分离

无状态组件，不用class 使用方法 props参数，因为没有class的state所以性能会高一点

最大的特点就是只有UI

```js
const TodoListUI=(props)=> {
    return (
        <div style={{margin:'10px'}}
      value={props.inputValue}>
        </div>
    );
}
```

Easy mock 接口测试 自定义数据 yapi

axios api请求

异步方法建议放在中间件中做

## 中间件

redux-thuck

thunk的作用是将函数处理为对象

saya 和thunk类似的中间件
