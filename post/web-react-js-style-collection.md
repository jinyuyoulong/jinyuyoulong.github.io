---
title: react JS style样式设置总结
id: 388
categories:
  - web前端
date: 2016-04-08 14:29:04
tags:
---

    const styles = StyleSheet.create({
      style_0:{
          flex:1,
          borderColor: 'red',
          borderWidth:1,
      },
    &lt;View style={styles.style_0}&gt;
    &lt;View style={[styles.view, styles.center]}&gt;&lt;Text&gt;自由摆放&lt;/Text&gt;&lt;/View&gt;
    &lt;View style={[styles.style_1, {flexDirection: 'column'}]}&gt;
    &lt;Text style={{marginTop:40, fontSize:25}}&gt;1／4高&lt;/Text&gt;
    