---
title: 为什么析构函数要翻译成析构？
author: fan
type: post
date: 2019-01-16T05:45:39+00:00
url: /为什么析构函数要翻译成析构？/
categories:
  - 十万个为什么

---
#### 为什么析构函数要翻译成析构？

Destructuring assignment （解构赋值）
  
这个是JavaScript 1.7引入的新名词.至于用途,用过Matlab、Lua等编程脚本的人都再熟悉不过了.
  
var a = 1;
  
var b = 3;
  
[a, b] = [b, a];
  
用白话说,就是多个复制写在一行.其最主要的用途也就是返回多个返回值了,因为这类脚本既没有指针也没有引用参数.当然,也可以用来交换变量的值(如上例),循环旋转变量序列的值等.
  
JavaScript给它起了这么个怪名字,应该是由于使用了其本来的数组的形式.将一个数组赋给另一个数组,本来是引用赋值,但左边如果是右值常量,则不能赋值.于是改变语义为将每个元素的值赋到左边对应的元素.所以,才叫做解构赋值,就是解了数组的构.
  
扯得远一点,destructuring咋一看挺眼熟,象C++的destructor.既然destructor翻译成析构,为什么destructure要翻译成解构呢?查一下专业词典,便会发现destruct和destructure是不同的.destruct是破坏、粉碎;而destructure是解构.明显destructor是destruct的派生词.那么疑问就变成为什么destructor翻译成析构函数,而不是破坏函数、销毁函数什么的.析字的解释有一条分开、分散,即是分崩离析的析.这么一想,也有些道理,而且与构造共享一个构字,也便于将构造和析构联系到一起. loading&#8230;
  
引用自天涯 http://wenda.tianya.cn/question/521b090115127d96
  
单词翻译
  
destruct 自毁，为可自毁而设计的

<pre><code class="line-numbers">"to destroy," 1958, probably a back-formation from destruction in the jargon of U.S. aerospace and defense workers to refer to deliberate destruction of a missile in flight by a friendly agent; popularized 1966 in form self-destruct in the voice-over at the beginning of popular TV spy drama "Mission Impossible." OED records an isolated use of destruct from 17c., in this case probably from Latin destruct-, past participle stem of destruere.
“摧毁”，1958年，可能是美国航空航天和国防工作人员用行话破坏的反击形式，指的是友好的特工故意破坏飞行中的导弹; 在流行的电视间谍剧“不可能的任务”的开头，在画外音中以1966年的形式自我毁灭推广。 OED记录了对17c的破坏的单独使用，在这种情况下可能来自拉丁语destruct-，destruere的过去分词词干。
</code></pre>

destructor 爆炸者，破坏装置，垃圾焚毁炉
  
destructure 析构，拆解