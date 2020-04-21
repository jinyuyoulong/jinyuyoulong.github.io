---
title: package.json中scripts的使用方法
author: fan
type: post
date: 2018-04-05T15:49:56+00:00
url: /package-json中scripts的使用方法/
categories:
  - Nodejs
tags:
  - nodejs
format: aside

---
scripts是npm的脚本编辑的地方，不是node的

所以在package.json中scripts的命令行使用方式是这样的，如下

npm run start

      "scripts": {
        "start": "node ./bin/www"
      },


详细使用方法请参考http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html