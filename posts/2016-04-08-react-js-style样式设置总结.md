---
title: react JS style样式设置总结
author: fan
type: post
date: 2016-04-08T06:29:04+00:00
url: /react-js-style样式设置总结/
duoshuo_thread_id:
  - 6278603406902821633
  - 6278603406902821633
categories:
  - web前端

---
    const styles = StyleSheet.create({
      style_0:{
          flex:1,
          borderColor: 'red',
          borderWidth:1,
      },
    <View style={styles.style_0}>
    <View style={[styles.view, styles.center]}><Text>自由摆放</Text></View>
    <View style={[styles.style_1, {flexDirection: 'column'}]}>
    <Text style={{marginTop:40, fontSize:25}}>1／4高</Text>