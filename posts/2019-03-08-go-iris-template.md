---
title: Go-如何选择合适的Web模板引擎
author: fan
type: post
date: 2019-03-08T09:29:09+00:00
excerpt: Iris 支持五个开箱即用的模板引擎:标准HTML，Django，Pug(jade)，Handlebars,Amber
url: /go-iris-template/
categories:
  - Go

---
所谓模板引擎，则将模板和数据进行渲染的输出格式化后的字符程序。对于go，执行这个流程大概需要三步。
  
创建模板对象
  
加载模板字串
  
执行渲染模板
  
其中最后一步就是把加载的字符和数据进行格式化。其过程可以总结下图：
  
[![模板引擎][1]][1]
  
模板引擎一般有两种实现方式，一种是解析 html 语法树，然后根据一定的规则动态的拼接，是非预编译生成Go代码的模板引擎。另外一种是把模板预编译生成Go代码的模板引擎，渲染模板时调用相关的函数即可。这一类模板引擎由于先天优势，性能将更为出色一些，是否采用这类引擎，要看你项目的需求来权衡。这类引擎的佼佼者是hero，也是一位国人开发的Go语言模板引擎库。
  
Go 内置的 template 包使用的是第一种方式，很多开源项目使用的是第二种方式。
  
Iris 支持五个开箱即用的模板引擎，所有这五个模板引擎都具有通用API的共同特征，如布局，模板功能，特定于派对的布局，部分渲染等。
  
Iris 其实是用了Go语言模板引擎库是go-template，它更像一个模板引擎适配器，它的最大特色是同时支持standard html/template、amber、django、handlebars、pug(jade)、markdown六种模板引擎。

> 标准的html,它的模板解析器就是 [golang.org/pkg/html/template/][2] 

<pre><code class="line-numbers">file name :  xxx.html
{{ define "layout" }}
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8"&gt;
    &lt;title&gt;layout&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;h3&gt;This is layout&lt;/h3&gt;
    template data: {{ . }}
    {{ if . }}
      Number is greater than 5!
    {{ else }}
      Number is 5 or less!
    {{ end }}
  &lt;/body&gt;
&lt;/html&gt;
{{ end }}
</code></pre>

> Django,它的模板解析器就是 [github.com/flosch/pongo2][3] 

<pre><code class="line-numbers">file name : xxx.html
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
&lt;meta charset="utf-8"&gt;
&lt;title&gt;my title&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;h1&gt;Hello World!&lt;/h1&gt;
    &lt;p&gt;Django 测试。&lt;/p&gt;
    {% block mainbody %}
       &lt;p&gt;original&lt;/p&gt;
    {% endblock %}
&lt;/body&gt;
&lt;/html&gt;
</code></pre>

> Pug(Jade),它的模板解析器就是 [github.com/Joker/jade][4]
    
> 为什么要引入pug? 在后期维护和修改时，一不小心少了一个尖括号，或者某个标签的开始和闭合没有对应上，就会导致DOM结构的混乱甚至是错误。所以，有人发明了HAML，它最大的特色就是使用缩进排列来代替成对标签。受HAML的启发，pug进行了javascript的实现。
    
> Pug有它本身的缺点——可移植性差，调试困难，性能并不出色，但使用它可以加快开发效率。 

<pre><code class="line-numbers">file name : xxx.pug
html
    head
        title aaa
    body
    &lt; var user = { description: 'foo bar baz' }&gt;
    &lt; var authorised = false&gt;
    #user
    if user.description
        h2.green 描述
        p.description= user.description
    else if authorised
        h2.blue 描述
        p.description.
            用户没有添加描述。
            不写点什么吗……
    else
        h2.red 描述
        p.description 用户没有描述
</code></pre>

> Handlebars, 它的模板解析器 [github.com/aymerick/raymond][5]
    
> Handlebars 是 JavaScript 一个语义模板库，通过对view和data的分离来快速构建Web模板。它采用&#8221;Logic-less template&#8221;（无逻辑模版）的思路，在加载时被预编译，而不是到了客户端执行到代码时再去编译， 这样可以保证模板加载和运行的速度。 

<pre><code class="line-numbers">file name : xxx.html
div class="demo"&gt;
    &lt;h1&gt;{{name}}&lt;/h1&gt;
    &lt;p&gt;{{content}}&lt;/p&gt;
&lt;/div&gt;
{{#if list}}
&lt;ul id="list"&gt;
    {{#each list}}
        &lt;li&gt;{{this}}&lt;/li&gt;
    {{/each}}
&lt;/ul&gt;
{{else}}
    &lt;p&gt;{{error}}&lt;/p&gt;
{{/if}}
</code></pre>

> Amber, 它的模板解析器 [github.com/eknkc/amber][6]
    
> 灵感来自 HAML 和Jade,那为什么不用 Pug。 

<pre><code class="line-numbers">html
    head
        title Page Title
    body
        div#content
            p
                | This is a long page content
                | These lines are all part of the parent p
                a[href="/"] Go To Main Page
</code></pre>

 [1]: https://upload-images.jianshu.io/upload_images/11043-d8ed7fda8ee06555.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/606/format/webp "模板引擎"
 [2]: https://golang.org/pkg/html/template/
 [3]: https://github.com/flosch/pongo2
 [4]: https://github.com/Joker/jade
 [5]: https://github.com/aymerick/raymond
 [6]: https://github.com/eknkc/amber