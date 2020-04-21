---
title: react-native:unexpected token error
author: fan
type: post
date: 2016-03-22T09:11:47+00:00
url: /react-nativeunexpected-token-error/
duoshuo_thread_id:
  - 6278603406185595649
  - 6278603406185595649
categories:
  - iOS

---
react-native新建的项目默认使用ES6写法，所以如果你在用到
   
componentWillMount:function()这样的代码时会运行出错
     
解决：改成ES6写法componentWillMount(){}
       
其他几种方式都改为ES6写法
     
如果你是使用这种方式
     
class wyq extends Component {}定义一个组件
     
那么应该这样定义方法：componentWillMount(){}
     
如果使用这种方式定义组件
     
var MovieScreen = React.createClass({}）
     
那么应该使用这种方式定义方法：render: function() {}
  
请使用ES6的新写法