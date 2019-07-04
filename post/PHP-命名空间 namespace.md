---
title: PHP 命名空间 namespace
date: 2018-11-12
---



PHP 命名空间 namespace

1. 声明：
 ```php
 <?php 
//     file1.php
	namespace MyProject;
	namespace MyProject\Sub\Level;  //声明分层次的单个命名空间

	namespace MyProject {
    const CONNECT_OK = 1;
    class Connection { /* ... */ }
    function connect() { /* ... */  }
        
    namespace Foo\Bar\subnamespace; 

    const FOO = 1;
	function foo() {}
	class foo
	{
    	static function staticmethod() {}
	}
}
 ?>
 ```
2. 使用
```php
<?php
    //file2.php
    namespace Foo\Bar;
	include 'file1.php';

    subnamespace\foo(); // 解析为函数 Foo\Bar\subnamespace\foo
    subnamespace\foo::staticmethod(); // 解析为类 Foo\Bar\subnamespace\foo,
                                      // 以及类的方法 staticmethod
	\Foo\Bar\foo(); // 解析为函数 Foo\Bar\foo
	\Foo\Bar\foo::staticmethod(); // 解析为类 Foo\Bar\foo, 以及类的方法 staticmethod
?>

```