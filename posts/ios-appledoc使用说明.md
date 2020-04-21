---
title: appledoc使用说明
<<<<<<< HEAD:posts/2018-04-04-appledoc使用说明.md
author: fan
type: post
date: 2018-04-04T07:00:34+00:00
url: /appledoc使用说明/
categories:
  - iOS
  - Mac
  - 工具
tags:
  - appledoc
format: aside
=======
tags: [appledoc]
categories: [iOS,Mac,工具]
date: 2018-04-04 07:00:34
---
>>>>>>> 9b93207d813e2b213031f967612e37c68194cf37:post/iOS-appledoc.md

---
appledoc使用说明
  
安装命令行：

  * git clone git://github.com/tomaz/appledoc.git
  * cd ./appledoc
  * sudo sh install-appledoc.sh
  * appledoc —version //检查successed

使用
  
生成HTML
  
当需要html文档时，可以加上“&#8211;no-create-docset”——

    appledoc --no-create-docset --output ~/doc --project-name "DrowRect" --company-id "com.jinyuyoulong" --project-company "jinyuyoulong" ./
    

注:
  
&#8211;output ./doc：设置输出目录为“./doc”。
  
&#8211;project-name objcdoc：设置项目名为“DrowRect”。
  
&#8211;project-company &#8220;jinyuyoulong&#8221;：设置公司名为“jinyuyoulong”。
  
&#8211;company-id &#8220;com.jinyuyoulong&#8221;：设置公司id为“com.jinyuyoulong”。
  
./：当前目录。
  
生成docset 此路不通

    appledoc --output ./doc --project-name "DrowRect" --project-company "jinyuyoulong" --company-id "com.jinyuyoulong" ./
    

* * *Xcode脚本生成文档


  
Xcode 配置</p> 

  1. add new target —>选择Other—Aggregate，命名为docText</p> 
  2. Build Phases + run script

  3. 编辑run script的内容
  4. 设置target为docText，运行Xcode
  5. 在脚本中标明的导出目录下查看生成的文档

script:

    #appledoc Xcode script
    # Start constants
    company="abc";
    companyID="com.abc";
    companyURL="http://abc.com";
    target="iphoneos";
    #target="macosx";
    outputPath="~/doc";#输出地址
    # End constants
    /usr/local/bin/appledoc \
    --project-name "${PROJECT_NAME}" \
    --project-company "${company}" \
    --company-id "${companyID}" \
    --docset-atom-filename "${company}.atom" \
    --docset-feed-url "${companyURL}/${company}/%DOCSETATOMFILENAME" \
    --docset-package-url "${companyURL}/${company}/%DOCSETPACKAGEFILENAME" \
    --docset-fallback-url "${companyURL}/${company}" \
    --output "${outputPath}" \
    --publish-docset \
    --docset-platform-family "${target}" \
    --logformat xcode \
    --keep-intermediate-files \
    --no-repeat-first-par \
    --no-warn-invalid-crossref \
    --exit-threshold 2 \
    "${PROJECT_DIR}"