---
title: npm-scripts.md
date: 2018-07-17 16:47:27
tags: [nodejs]
categorise: [Nodejs]
---

scripts是npm的脚本编辑的地方，不是node的
所以在package.json中scripts的命令行使用方式是这样的，如下
npm run start

```
  "scripts": {
    "start": "node ./bin/www"
  },
```
详细使用方法请参考http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html