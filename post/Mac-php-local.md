---
title: mac系统使用内置的 PHP
id: 172
categories:
  - PHP
date: 2015-08-18 11:19:22
tags:
---

<span class="s1">从 OS X 10.0.0 版本开始，PHP 作为 Mac 机的标准配置被提供。在默认的 web 服务器中启用 PHP，只需将 Apache 配置文件 _httpd.conf_ 中的几行配置指令最前面的注释符号去掉，而 CGI 或 CLI 默认都可使用（可以很容易的被终端程序使用）。</span>

<span class="s1">按照以下的使用说明，可以快速的建立一个本地 PHP 开发环境。_强烈建议_将 PHP 升级到最新的版本。在大多数活跃的软件中， 新的版本会修复错误和添加新的功能，PHP 也是如此。请参见相应的 Mac OS X 安装文档，以进一步了解详细的信息。以下的说明以初学者的角度来详细描述如何操作来得到一个缺省的运行环境。建议所有的用户都编译或者安装一个新的打包版本。</span>

<span class="s1">标准的安装类型为 mod_php，在 Mac OS X 的 Apache web 服务器（默认 web 服务器，可以从系统设置中访问）中启用 PHP 包含以下的步骤：</span>

<span class="s1">&nbsp;</span>

1.  <span class="s2"></span><span class="s3">找到并打开Apache的配置文件。默认情况下，这个配置文件的位置是： _/private/etc/apache2/httpd.conf_。 使用 _Finder_ 或者 _Spotlight_ 来找到这个文件可能不是很容易的事情，因为在默认情况下它一般是 _root_ 用户拥有所有权的私有文件。 </span><span class="s1">**Note**: 要打开这个文件，可以在命令行下面使用基于 Unix 的文本编辑器，例如 _nano_，因为他的属主是 _root_，所以我们需要使用 _sudo_ 来打开（以 _root_ 用户权限）。例如我们在 _Terminal_ 程序中敲入下面的指令（操作后，会提示输入密码）：_sudo nano /private/etc/apache2/httpd.conf_ 注意 nano 中的命令：_^w_（搜索），_^o_（保存），以及 _^x_（退出）。_^_ 表示 Ctrl 键。
    **Note**: 在Mac OS X 10.5之前的版本中捆绑的是旧版本的 PHP 和 Apache。因此在旧的计算机中 Apache 配置文件的位置可能是 _/etc/httpd/httpd.conf_。</span>

2.  <span class="s1">使用文本的编辑器取消注释（删除前面的 #）看起来类似于下面的行（这两行常常不在一起，需要在文件中找到这两行）：
</span><span class="s4"># LoadModule php5_module libexec/httpd/libphp5.so</span>

3.4.  <span class="s1"># AddModule mod_php5.c</span>

5.  <span class="s5"></span><span class="s1">

    注意位置／路径。如果在以后重新编译了 PHP，以上文件应被更换或者注释掉。</span>

6.  <span class="s1">确保将所需要的文件扩展名解析为 PHP（例如：.php .html 以及 .inc），否则不能正常运行。
由于以下的配置已经写入 _httpd.conf_（自 Mac Panther 版起），一旦 PHP 被启用则 _.php_ 文件会被自动解析为 PHP 脚本。
</span><span class="s6">
&lt;IfModule mod_php5.c&gt;</span>

7.  <span class="s1">&nbsp; &nbsp; # If php is turned on, we respect .php and .phps files.</span>

8.  <span class="s1">&nbsp; &nbsp; AddType application/x-httpd-php .php</span>

9.  <span class="s1">&nbsp; &nbsp; AddType application/x-httpd-php-source .phps</span>

10.11.  <span class="s1">&nbsp; &nbsp; # Since most users will want index.php to work we</span>

12.  <span class="s1">&nbsp; &nbsp; # also automatically enable index.php</span>

13.  <span class="s1">&nbsp; &nbsp; &lt;IfModule mod_dir.c&gt;</span>

14.  <span class="s1">&nbsp; &nbsp; &nbsp; &nbsp; DirectoryIndex index.html index.php</span>

15.  <span class="s1">&nbsp; &nbsp; &lt;/IfModule&gt;</span>

16.  <span class="s7"></span><span class="s8">&lt;/IfModule&gt;</span><span class="s9">
</span><span class="s8">

    </span><span class="s3">

    </span><span class="s1">**Note**:
在 OS X 10.5（Leopard）以前版本中，捆绑的是 PHP 4 而不是 PHP 5，因此上面的配置指令稍有不同，需要将 5 更改为 4。
</span>

17.  <span class="s1">确保 DirectoryIndex 加载了所需的默认索引文件。 这个也是在 _httpd.conf_ 中设置的。 通常情况下使用 _index.php_ 和 _index.html_ 。默认情况下 _index.php_ 会被启用，因为在我们上面的配置指令中写明了。根据实际情况可以做相应的调整。</span>

18.  <span class="s1">设置 _php.ini_ 的位置或者使用默认的位置。 Mac OS X 上通常默认的位置是 _/usr/local/php/php.ini_ ，调用 [<span class="s10">phpinfo()</span>](http://www.php.net/manual/zh/function.phpinfo.php) 也可以得到此信息。如果没有使用 _php.ini_，PHP 将使用所有的默认值。参见常见问题中的[<span class="s10">寻找 php.ini</span>](http://www.php.net/manual/zh/faq.installation.php#faq.installation.phpini)。</span>

19.  <span class="s1">定位或者设置 _DocumentRoot_。 这是网站所有文件的根目录。此目录中的文件由 web 服务器提供服务，从而使得 PHP 文件将在输出到浏览器之前解析为 PHP 脚本。通常情况下默认的路径是 _/Library/WebServer/Documents_，但是可以根据需要在 _httpd.conf_中设置为任何其他目录。另外，用户自己的缺省 _DocumentRoot_ 是 _/Users/yourusername/Sites_。</span>

20.  <span class="s1">创建一个 [<span class="s10">phpinfo()</span>](http://www.php.net/manual/zh/function.phpinfo.php) 文件。 [<span class="s10">phpinfo()</span>](http://www.php.net/manual/zh/function.phpinfo.php) 将会显示PHP的相关系统信息。可以在 DocumentRoot 下创建一个 PHP 文件，其代码如下：
</span><span class="s4">&lt;?php&nbsp;phpinfo();&nbsp;?&gt; </span><span class="s1">
</span>

21.  <span class="s1">重启 Apache，然后从浏览器访问上面创建的文件。 要重启Apache，可以在 shell 中执行 _sudo apachectl graceful_，也可以停止/启动 OS X 系统首选项中的“Personal Web Server”选项。默认情况下，从浏览器访问本地文件的 URL 一般类似于：_http://localhost/info.php_，或者使用：_http://localhost/~yourusername/info.php_ 来访问用户自己 DocumentRoot 中的文件。</span>

<span class="s1">CLI（或者旧版本中的 CGI）一般文件名为 _php_ ，其路径可能是 _/usr/bin/php_。打开一个终端，参考 PHP 手册中的 [<span class="s10">PHP 的命令行模式</span>](http://www.php.net/manual/zh/features.commandline.php)一章，然后执行 _php -v_ 可以检查当前运行的 PHP 的版本。调用 [<span class="s10">phpinfo()</span>](http://www.php.net/manual/zh/function.phpinfo.php) 也会显示相关的信息。</span>