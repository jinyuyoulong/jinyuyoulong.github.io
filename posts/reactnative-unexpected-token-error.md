---
title: 'react-native:unexpected token error'
categories: [iOS]
date: 2016-03-22 17:11:47
---

react-native新建的项目默认使用ES6写法，所以如果你在用到
 componentWillMount:function()这样的代码时会运行出错
   解决：改成ES6写法componentWillMount(){}
     其他几种方式都改为ES6写法
   如果你是使用这种方式
   class wyq extends Component {}定义一个组件
   那么应该这样定义方法：componentWillMount(){}
   如果使用这种方式定义组件
   var MovieScreen =  React.createClass({}）
   那么应该使用这种方式定义方法：render: function() {}

请使用ES6的新写法