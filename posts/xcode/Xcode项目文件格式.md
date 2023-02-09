---
title: "Xcode项目文件格式"
date: 2021-05-24T20:19:16+08:00
toc: true
images:
tags: 
  - Xcode
---

原文：http://www.monobjc.net/xcode-project-file-format.html

译者：chai2010

译文：https://www.jianshu.com/p/bd4e3c1a7276

#### 简介 xxx.xcodeproj -> project.pbxproj

> Xcode工程文件采用的是老式风格的plist文件（Next公司采用的格式，现在新的plist文件采用xml格式），它使用花括弧来组织结构化的数据。文件的开头是一个显式的编码信息，通常是采用utf8编码。这意味着它不支持带bom(Byte Ordering Mark)头的utf8格式文件，因为在开头的bom部分解析时就会失败。

注意： 文档以下的部分只是基于 `*.pbxproj `

文件和元素推断的结果。本文并不是对真实的代码做逆向的分析，因此可能有不准确的地方。

#### 唯一标识码
文件中的每个元素均由一个24个字符，每个字符对应十六进制的4bit，共96bit的唯一标识码表示。即使是不同的文档之间，唯一标识码依然是唯一的（和UUID的原理类似）。

Xcode生成唯一标识码的算法可能引入了日期、序列和其它一些预定义的值，但是并没有确切的文档说明具体的生成过程。一个合理的推测，跨文档的唯一标识码也基本是唯一的（应该不会出现两个不同元素对应相同唯一标识码的情绪）。

下面的链接是关于CMake对Xcode的支持的讨论（还有其它一些文章），或许可以提供一些信息：
```
CMake Apple XCode support A brief look at the Xcode project format More on the Xcode project format Xcode project object UUIDs
```
#### 元素

以下这些是工程文件中包含的元素类型：

根节点
```
PBXBuildFile
PBXBuildPhase
PBXAppleScriptBuildPhase
PBXCopyFilesBuildPhase
PBXFrameworksBuildPhase
PBXHeadersBuildPhase
PBXResourcesBuildPhase
PBXShellScriptBuildPhase
PBXSourcesBuildPhase
PBXContainerItemProxy
PBXFileElement
PBXFileReference
PBXGroup
PBXVariantGroup
PBXTarget
PBXAggregateTarget
PBXLegacyTarget
PBXNativeTarget
PBXProject
PBXTargetDependency
XCBuildConfiguration
XCConfigurationList
```
根节点 根节点包含通用的信息。
```
属性  类型  值   注释
archiveVersion  数字  1   默认值
classes 列表  空
objectVersion   数字  参考 XcodeCompatibilityVersion 枚举值
objects 字典  字典  字典的key是前面讲到的唯一标识码
rootObject  引用  一个元素的引用 每个 object 对应一个 PBXProject 元素的引用
```
例子:
```
// !$<em>UTF8</em>$!
{
    archiveVersion = 1;
    classes = {
    };
    objectVersion = 45;
    objects = {
	...
};
rootObject = 0867D690FE84028FC02AAC07 /* Project object */;
}
```
PBXAggregateTarget 不同构建目标的集合（含依赖关系）。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXAggregateTarget  空
buildConfigurationList  引用  元素的引用   对应 XCConfigurationList 类型
buildPhases 列表  元素引用的列表 列表元素对应 PBXBuildPhase 类型
dependencies    列表  元素引用的列表 列表元素对应 PBXTargetDependency 类型
name    字符串 目标的名字
productName 字符串 产品的名字   ?
```
例子:
```
4DA521A6115A00AF007C19C3 /* documentation <em>/ = {
    isa = PBXAggregateTarget;
    buildConfigurationList = 4DA521AE115A00ED007C19C3 /</em> Build configuration list for PBXAggregateTarget "documentation" <em>/;
    buildPhases = (
        4DA521A5115A00AF007C19C3 /</em> ShellScript <em>/,
    );
    dependencies = (
        4DA521AA115A00BC007C19C3 /</em> PBXTargetDependency */,
    );
    name = documentation;
    productName = documentation;
};
```
PBXBuildFile 文件元素，被PBXBuildPhase等作为文件包含或被引用的资源。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXBuildFile    空
fileRef 引用  元素引用    对应PBXFileReferenc元素
settings    字典  扩展的配置信息，对应 key/value 字典 ?
```
```
例子:
4D05CA6B1193055000125045 /* xxx.c in Sources <em>/ = {
    isa = PBXBuildFile;
    fileRef = 4D05CA411193055000125045 /</em> xxx.c */;
};
```
PBXBuildPhase 一个抽象的构建阶段，最终需有对应到具体化的构建对象。

PBXContainerItemProxy 目标对象的容器。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXContainerItemProxy   空
containerPortal 引用  元素的引用   引用 PBXProject 元素
proxyType   数字  1
remoteGlobalIDString    引用  元素的引用   使用全局唯一的ID引用
remoteInfo  字符串     ?
```
例子:
```
4D22DC0C1167C992007AF714 /* PBXContainerItemProxy <em>/ = {
    isa = PBXContainerItemProxy;
    containerPortal = 08FB7793FE84155DC02AAC07 /</em> Project object */;
    proxyType = 1;
    remoteGlobalIDString = 87293EBF1153C114007AFD45;
    remoteInfo = xxx;
};
```
PBXCopyFilesBuildPhase 构建阶段复制文件信息。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXCopyFilesBuildPhase  空
buildActionMask 数字  2^32-1
dstPath 字符串 目标文件的路径
dstSubfolderSpec    数字
files   列表  元素引用的列表 对应 PBXBuildFile 元素
runOnlyForDeploymentPostprocessing  数字  0   ?
```
例子:

MISSING

PBXFileElement 抽象类型，对应具体化的文件和group组元素。

PBXFileReference 用于跟踪项目引用的每一个外部文件，比如源代码文件、资源文件、库文件、生成目标文件等。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXFileReference    空
fileEncoding    数字  参考 PBXFileEncoding
explicitFileType    字符串 参考 the PBXFileType
lastKnownFileType   字符串 参考 PBXFileType
name    字符串 文件名
path    字符串 文件名路径
sourceTree  字符串 参考 PBXSourceTree    ?
```
例子:
```
87293F901153D870007AFD45 /* monobjc.mm */ = {
    isa = PBXFileReference;
    fileEncoding = 4;
    lastKnownFileType = sourcecode.cpp.objcpp;
    name = monobjc.mm;
    path = sources/monobjc.mm;
    sourceTree = "";
};
```
PBXFrameworksBuildPhase 用于framewrok构建的链接阶段。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXFrameworksBuildPhase 空
buildActionMask 数字  2^32-1
files   列表  元素引用的列表 对应 PBXBuildFile 类型
runOnlyForDeploymentPostprocessing  数字  0   ?
```
例子:
```
4D05CA2C119304BD00125045 /* Frameworks */ = {
    isa = PBXFrameworksBuildPhase;
    buildActionMask = 2147483647;
    files = (
    );
    runOnlyForDeploymentPostprocessing = 0;
};
```
PBXGroup 用于打组文件，或者嵌套组。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXGroup    空
children    列表  元素引用的列表 对应 PBXFileElement 元素类型
name    字符串 The filename.
sourceTree  字符串 参考 PBXSourceTree    ?
```
例子:
```
4DA521A2115A003E007C19C3 /* scripts <em>/ = {
    isa = PBXGroup;
    children = (
    4D22DBAF116742DE007AF714 /</em> fix_references.sh <em>/,
    4DA521A1115A0032007C19C3 /</em> generate_descriptors.sh */,
    );
    name = scripts;
    sourceTree = "";
};
```
PBXHeadersBuildPhase 用于framewrok构建的链接阶段。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXHeadersBuildPhase    空
buildActionMask 数字  2^32-1
files   列表  元素引用的列表 对应 PBXBuildFile 元素类型
runOnlyForDeploymentPostprocessing  数字  0   ?
```
例子:
```
87293EBC1153C114007AFD45 /* Headers */ = {
    isa = PBXHeadersBuildPhase;
    buildActionMask = 2147483647;
    files = (
    );
    runOnlyForDeploymentPostprocessing = 0;
};
```
PBXLegacyTarget MISSING

PBXNativeTarget 对应生成可执行的二进制程序或库文件的本地构建目标对象。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXNativeTarget 空
buildConfigurationList  引用  元素引用    对应 XCConfigurationList 类型
buildPhases 列表  元素引用的列表 对应 PBXBuildPhase 元素类型
dependencies    列表  元素引用的列表 对应 PBXTargetDependency 元素类型
name    字符串 目标的名字
productInstallPath  字符串 产品的安装路径
productName 字符串 产品的名字
productReference    引用  元素的引用   对应 PBXFileReference 元素类型
productType 字符串 参考 PBXProductType   ?
```
例子:
```
8D1107260486CEB800E47090 /* XXX <em>/ = {
    isa = PBXNativeTarget;
    buildConfigurationList = C01FCF4A08A954540054247B /</em> Build configuration list for PBXNativeTarget "XXX" <em>/;
    buildPhases = (
        8D1107290486CEB800E47090 /</em> Resources <em>/,
        8D11072C0486CEB800E47090 /</em> Sources <em>/,
        8D11072E0486CEB800E47090 /</em> Frameworks <em>/,
    );
    buildRules = (
    );
    dependencies = (
    );
    name = XXX;
    productInstallPath = "$(HOME)/Applications";
    productName = TrackIt;
    productReference = 8D1107320486CEB800E47090 /</em> XXX.app */;
    productType = "com.apple.product-type.application";
};
```
PBXProject 工程，对应构建可执行的二进制目标程序或库。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXProject  空
buildConfigurationList  引用  元素的引用   对应 XCConfigurationList 类型
compatibilityVersion    字符串 XcodeCompatibilityVersion 对应的字符串表示
developmentRegion   字符串 开发者所在区域
hasScannedForEncodings  数字  0 or 1  是否已经扫描了文件编码信息
knownRegions    列表  字符串列表   不同区域的本地资源文件列表
mainGroup   引用  元素的引用   对应 PBXGroup 类型
productRefGroup 引用  元素的引用   对应 PBXGroup 类型
projectDirPath  字符串 相对工程的相对路径
projectReferences   字典列表    列表中的每个字典元素包含 ProductGroup和ProjectRef两个成员
projectRoot 字符串 根目录路径（相对路径）
targets 列表  元素引用的列表 对应 PBXTarget 元素类型
```
例子:
```
29B97313FDCFA39411CA2CEA /* Project object <em>/ = {
        isa = PBXProject;
        buildConfigurationList = C01FCF4E08A954540054247B /</em> Build configuration list for PBXProject "XXX" <em>/;
        compatibilityVersion = "Xcode 2.4";
        developmentRegion = English;
        hasScannedForEncodings = 1;
        knownRegions = (
                English,
                Japanese,
                French,
                German,
                en,
        );
        mainGroup = 29B97314FDCFA39411CA2CEA /</em> XXX<em>/;
        projectDirPath = "";
        projectRoot = "";
        targets = (
             8D1107260486CEB800E47090 /</em> XXX*/,
        );
};
```
PBXResourcesBuildPhase 构建阶段需要复制的资源文件。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXResourcesBuildPhase  空
buildActionMask 数字  2^32-1
files   列表  元素引用的列表 对应 PBXBuildFile 元素类型
runOnlyForDeploymentPostprocessing  数字  0   ?
```
例子:
```
8D1107290486CEB800E47090 /* Resources <em>/ = {
        isa = PBXResourcesBuildPhase;
        buildActionMask = 2147483647;
        files = (
                535C1E1B10AB6B6300F50231 /</em> ReadMe.txt in Resources <em>/,
                533B968312721D05005E617D /</em> Credits.rtf in Resources <em>/,
                533B968412721D05005E617D /</em> InfoPlist.strings in Resources <em>/,
                533B968512721D05005E617D /</em> MainMenu.nib in Resources <em>/,
                533B968612721D05005E617D /</em> TableEdit.nib in Resources <em>/,
                533B968712721D05005E617D /</em> TestWindow.nib in Resources */,
        );
        runOnlyForDeploymentPostprocessing = 0;
};
```
PBXShellScriptBuildPhase 用于构建阶段复制资源文件的shell脚本。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXShellScriptBuildPhase    空
buildActionMask 数字  2^32-1
files   列表  元素引用的列表 对应 PBXBuildFile 类型
inputPaths  列表  字符串列表   输入的路径列表
outputPaths 列表  字符串列表   输出的路径列表
runOnlyForDeploymentPostprocessing  数字  0
shellPath   字符串 shell解释器程序的路径
shellScript 字符串 shell脚本程序的内容    ?
```
例子:
```
4D22DBAE11674009007AF714 /* ShellScript */ = {
        isa = PBXShellScriptBuildPhase;
        buildActionMask = 2147483647;
        files = (
        );
        inputPaths = (
        );
        outputPaths = (
        );
        runOnlyForDeploymentPostprocessing = 0;
        shellPath = /bin/sh;
        shellScript = "./fix_references.sh";
};
```
PBXSourcesBuildPhase 构建阶段中编译源文件。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXSourcesBuildPhase    空
buildActionMask 数字  2^32-1
files   列表  元素引用的列表 对应 PBXBuildFile 类型
runOnlyForDeploymentPostprocessing  数字  0   ?
```
例子:
```
4DF8B22D1171CFBF0081C1DD /* Sources <em>/ = {
        isa = PBXSourcesBuildPhase;
        buildActionMask = 2147483647;
        files = (
                4DF8B23E1171D0310081C1DD /</em> test.mm in Sources */,
        );
        runOnlyForDeploymentPostprocessing = 0;
};
```
PBXTarget 抽象对象，对应具体化的构建目标。

PBXTargetDependency 目标的外部依赖管理。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXTargetDependency 空
target  引用  元素引用    对应 PBXNativeTarget 类型
targetProxy 引用  元素引用    对应 PBXContainerItemProxy 类型
```
例子:
```
4D22DC0D1167C992007AF714 /* PBXTargetDependency <em>/ = {
        isa = PBXTargetDependency;
        target = 87293EBF1153C114007AFD45 /</em> libXXX <em>/;
        targetProxy = 4D22DC0C1167C992007AF714 /</em> PBXContainerItemProxy */;
};
```
PBXVariantGroup 对不同地区资源文件的引用管理。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa PBXVariantGroup 空
children    列表  元素引用的列表 对应 PBXFileElement 类型
name    字符串 文件名
sourceTree  字符串 参考 PBXSourceTree    ?
```
例子:
```
870C88031338A77600A69309 /* MainMenu.xib <em>/ = {
        isa = PBXVariantGroup;
        children = (
                870C88041338A77600A69309 /</em> en */,
        );
        name = MainMenu.xib;
        sourceTree = "";
};
```
XCBuildConfiguration 构建配置元素。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa XCBuildConfiguration    空
baseConfigurationReference  字符串 xcconfig文件的路径
buildSettings   字典  构建配置信息的字典
name    字符串 配置名 ?
```
例子:
```
870C88151338ABB600A69309 /* Debug <em>/ = {
        isa = XCBuildConfiguration;
        buildSettings = {
                PRODUCT_NAME = "$(TARGET_NAME)";
        };
        name = Debug;
};
870C88161338ABB600A69309 /</em> Release */ = {
        isa = XCBuildConfiguration;
        buildSettings = {
                PRODUCT_NAME = "$(TARGET_NAME)";
        };
        name = Release;
};
```
XCConfigurationList 构建配置相关元素的列表。
```
属性  类型  值   注释
reference   UUID    96bit的表示码
isa XCConfigurationList 空
buildConfigurations 列表  引用对象的列表 每个引用对象对应一个 XCBuildConfiguration 元素
defaultConfigurationIsVisible   数字  0
defaultConfigurationName    字符串 配置文件的默认名称   ?
```
例子:
```
870C87E41338A77600A69309 /* Build configuration list for PBXProject "CocoaApp" <em>/ = {
        isa = XCConfigurationList;
        buildConfigurations = (
                870C88061338A77600A69309 /</em> Debug <em>/,
                870C88071338A77600A69309 /</em> Release */,
        );
        defaultConfigurationIsVisible = 0;
        defaultConfigurationName = Release;
};
```