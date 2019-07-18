---
title: .gitignore文件使用说明
tags:
  - 收藏
id: 213
categories:
  - other technology其他技术
date: 2015-10-09 13:25:58
---

一般我们总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表。通常都是些自动生成的文件，像是日志或者编译过程中创建的等等。我们可以创建一个名为&nbsp;<wbr />`.gitignore`&nbsp;<wbr />的文件，列出要忽略的文件模式，来看一个简单的例子：
<pre style="white-space: normal; background-color: rgb(247, 247, 247); border: 0px; margin-top: 0px; margin-bottom: 1.625em; padding: 0.75em 1.625em; vertical-align: baseline; font-family: &#39;Courier 10 pitch&#39;, Courier, monospace; color: rgb(55, 55, 55); line-height: 1.5; font-size: 13px; outline: 0px; overflow: auto;" class="brush:cpp;toolbar:false;">$&nbsp;cat&nbsp;.gitignore&nbsp;*.[oa]&nbsp;*~</pre>

第一行告诉 Git 忽略所有以 .o 或 .a 结尾的文件。一般这类对象文件和存档文件都是编译过程中出现的，我们用不着跟踪它们的版本。第二行告诉 Git 忽略所有以波浪符（~）结尾的文件，许多文本编辑软件（比如 Emacs）都用这样的文件名保存副本。此外，你可能还需要忽略 log，tmp 或者 pid 目录，以及自动生成的文档等等。要养成一开始就设置好&nbsp;<wbr />`.gitignore`&nbsp;<wbr />文件的习惯，以免将来误提交这类无用的文件。

文件&nbsp;<wbr />`.gitignore`&nbsp;<wbr />的格式规范如下：

*   所有空行或者以注释符号 ＃ 开头的行都会被 Git 忽略。

*   可以使用标准的 glob 模式匹配。

*   匹配模式最后跟反斜杠（/）说明要忽略的是目录。

*   要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。

所谓的 glob 模式是指 shell 所使用的简化了的正则表达式。星号（*）匹配零个或多个任意字符；[abc] 匹配任何一个列在方括号中的字符（这个例子要么匹配一个 a，要么匹配一个 b，要么匹配一个 c）；问号（?）只匹配一个任意字符；如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）。

我们再看一个&nbsp;<wbr />`.gitignore`&nbsp;<wbr />文件的例子：
<pre style="white-space: normal; background-color: rgb(247, 247, 247); border: 0px; margin-top: 0px; margin-bottom: 1.625em; padding: 0.75em 1.625em; vertical-align: baseline; font-family: &#39;Courier 10 pitch&#39;, Courier, monospace; color: rgb(55, 55, 55); line-height: 1.5; font-size: 13px; outline: 0px; overflow: auto;" class="brush:cpp;toolbar:false;">#&nbsp;此为注释&nbsp;–&nbsp;将被&nbsp;Git&nbsp;忽略&nbsp;
*.a&nbsp;#&nbsp;忽略所有&nbsp;.a&nbsp;结尾的文件&nbsp;
!lib.a&nbsp;#&nbsp;但&nbsp;lib.a&nbsp;除外&nbsp;
/TODO&nbsp;#&nbsp;仅仅忽略项目根目录下的&nbsp;TODO&nbsp;文件，不包括&nbsp;subdir/TODO&nbsp;
build/&nbsp;#&nbsp;忽略&nbsp;build/&nbsp;目录下的所有文件&nbsp;
doc/*.txt&nbsp;#&nbsp;会忽略&nbsp;doc/notes.txt&nbsp;但不包括&nbsp;doc/server/arch.txt</pre>