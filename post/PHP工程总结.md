---
title: PHP工程总结
date: 2018-07-02
categories: [PHP]
---



PHP工程总结

1. 使用session需要调用session_start()手动开启环境，`session_start()调用之前页面不允许输出任何内容，包括空格`
2. sql语句 执行exec(),查询使用query()
3. order不能作为表名称，这是关键字
4. 获取最后一条插入数据 id使用PHP内置的方法调用:  $db->lastInsertRowID();插入一条数据后获取此条数据id。
5. $\sum_{i=1}^{n}\sqrt{i+\sin(i)}$
6. **include 和 require 除了处理错误的方式不同之外，在其他方面都是相同的：**
   - require 生成一个致命错误（E_COMPILE_ERROR），在错误发生后脚本会停止执行。
   - include 生成一个警告（E_WARNING），在错误发生后脚本会继续执行。
7. 增
8. 删
9. 改updateRow(tablename, id, key-values )
10. 查 
```mysql
单表查询:
select * from A where to_days(A.create_time)=to_days('2018-10-09')

两表联查:
select * from A inner join user on A.uid=B.uid where to_days(A.create_time)=to_days('2018-10-09')

三表联查:
select * from ((A left join B on A.orderId = B.id) left join C  on B.uid=C.uid)  where to_days(A.create_time)=to_days('2018-10-09')

三生万物，只有推到3，才能找到规律，推及万物
```
11. 遇到问题： unable to open database file ，
 ```
 原因为:当前文件夹的文件权限，需要为可读可写.
 原理为：当sqlite进行写操作时，会先 生成缓存文件，然后对缓存文件进行操作，而缓存文件的默认权限为当前文件夹的权限。
 ```

12. sqlite 中 inner outer 的区别：inner是两个表的交集，outer是一个表+另一个表不够补null的并集
13. array 插入
```
 // 第一种方式
        $childArr[$i]['name'] = $name;
        $childArr[$i]['number'] = $number;
        $childArr[$i]['unit'] = $unit;

        // 第二种方式
//        $childArr[] = $subArrItem;

        // 第三种方式，差评！
        //竟然需要两个参数, 不直观
//        array_push($childArr,$subArrItem);
```
14. 空值判断
```
empty

如果 变量 是非空或非零的值，则 empty() 返回 FALSE。
换句话说，""、0、"0"、NULL、FALSE、array()、var $var、未定义; 以及没有任何属性的对象都将被认为是空的，如果 var 为空，则返回 TRUE。

isset

如果 变量 存在(非NULL)则返回 TRUE，否则返回 FALSE(包括未定义）。
变量值设置为：null，返回也是false;unset一个变量后，变量被取消了。注意，isset对于NULL值变量，特殊处理。

is_null

检测传入值【值，变量，表达式】是否是null,只有一个变量定义了，且它的值是null，它才返回TRUE . 其它都返回 FALSE 【未定义变量传入后会出错！】.

参考: www.cnblogs.com/chengmo/archive/2010/10/18/1854258.html
```
15. 数据库
```
数据类型
blob 二进制大数据块
real 4字节浮点数->类float
binary 指定字节长度的二进制数据
timestamp 时间戳，MySQL自动添加当前时间
参考http://dcx.sap.com/1201/zh/dbreference/dtnu.html
```
16. MySQL中的timestamp数据类型不能直接用PHP时间和日期函数读取，先用strtotime函数将字符串转换成时间
```
	$birthday = $ROW['user_birthday'];
    $birthday = strtotime($birthday);
    $birthday  = date('n月j日',$birthday);
    echo $birthday/r/n;        //输出如“12月5日”的日期格式

    date formate时间格式化： http://php.net/manual/zh/function.date.php
```
17. phpstrom破解
```
目前遇到的最好的PHP开发IDE：集成数据库，编程规范检查警告（包括PHP，HTML，SQL，数据库配置）

若资金允许，请点击https://www.jetbrains.com/idea/buy/购买正版，谢谢合作 
学生凭学生证可免费申请正版授权 | 创业公司可5折购买正版授权
若资金不足，请尽量给予工具作者捐赠，支持作者&以后还可以获得帮助。
使用工具来源：http://idea.lanyus.com/
1. 下载工具
2. 修改配置文件
3. 移动破解工具到指定目录下
4. 运行软件，弹出软件注册激活激活窗口，Enterkey->Activate license with->Activation code:随意输入激活码文本内容->OK

2) phpstrom的配置文件为 /Application/PhpStorm.app/Contents/bin/phpstorm.vmoptions,
修改这里添加破解包路径：
-javaagent:/Applications/PhpStorm.app/Contents/bin/JetbrainsCrack.jar
3) 下载的破解工具JetbrainsCrack添加到上面配置的路径下
tips: 破解版本请不要轻易升级，以免升级使用后软件破解失效。
```
18. 集合数据不能使用数字作为key，会直接赋值到对应的数组下标中，不会作为字典处理。
19. ajax使用标签button请求，不能使用a标签，会造成事件冲突。
20. phpstrom使用
    alt+enter 为拼写检查添加忽略单词，需要光标放在单词位置
21. MySQL联合查询语法（内联、左联、右联、全联）
```sql
T1表结构（用户名,密码）   userid   username password
                    1   jack   jackpwd   
                    2   owen   owenpwd  
T2表结构（积分,等级）   userid   jifen    dengji 
                    1   20   3   
                    3   50   6   
1. 内联（inner  join）：取T1，T2的交集
SQL语句：select * from T1 inner join T2 on T1.userid=T2.userid
运行结果   T1.userid   username   password   T2.userid   jifen   dengji   
        1   jack   jackpwd   1   20   3   
2. 左联（left outer join）:以T1为参考表，取T1,T2的并集，T2数据不足补null
SQL语句：select * from T1 left outer join T2 on T1.userid=T2.userid
运行结果   T1.userid   username   password   T2.userid   jifen   dengji   
        1   jack   jackpwd   1   20   3   
        2   owen   owenpwd   NULL   NULL   NULL   
3. 右联（right outer join）:以T2为参考表，取T1,T2的并集，T1数据不足补null
SQL语句：select * from T1 right outer join T2 on T1.userid=T2.userid
运行结果   T1.userid   username   password   T2.userid   jifen   dengji   
        1   jack   jackpwd   1   20   3   
        NULL   NULL   NULL   3   50   6   
4. 全联（full outer join）：取T1,T2的并集，凡是数据不足的都补null
SQL语句：select * from T1 full outer join T2 on T1.userid=T2.userid
运行结果   T1.userid   username   password   T2.userid   jifen   dengji   
        1   jack   jackpwd   1   20   3   
        2   owen   owenpwd   NULL   NULL   NULL   
        NULL   NULL   NULL   3   50   6   
```


