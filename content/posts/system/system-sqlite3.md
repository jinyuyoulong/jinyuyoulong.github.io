---
title: sqlite3的使用
categories: [数据库]
date: 2015-08-07 23:38:47
tags:
---

<span style="background-color: rgb(255, 250, 165);-evernote-highlight:true;"></span><span style="font-family: Arial; background-color: rgb(255, 255, 255);">新建数据库</span>

<span style="font-family: Arial; background-color: rgb(255, 255, 255);">sqlite3 databasefilename</span>

<span style="font-family: Arial; background-color: rgb(255, 255, 255);">检查databasefilename是否存在，如果不存在就创建并进入数据库（如果直接退出，数据库文件不会创建）&nbsp;&nbsp;如果已经存在直接进入数据库 对数据库进行操作</span>

<span style="font-family: Arial;"><span style="background-color: rgb(255, 255, 255);">
</span></span>

<span style="background-color: rgb(255, 250, 165);-evernote-highlight:true;">创建表</span>：

<span style="font-size: 12px; font-family: Menlo; color: rgb(195, 195, 0);">create table if not exists UserList(id integer primary key autoincrement,firstName[not null],lastName[not null],sex,birthday,remark[not null],resumeNum[not null])</span>

<span style="font-family:&#39;Helvetica Neue&#39;;font-size:14px;"></span>

该表已经创建了主键，可以自增ID

<span style="font-family:&#39;Helvetica Neue&#39;;font-size:14px;"></span>

terminal命令行使用sqlite3

打开或创建：进入到文件所在目录下，输入sqlite3 filename

1、显示数据库中所有的表：.tables

<span style="font-family:&#39;Helvetica Neue&#39;;font-size:14px;"></span>

2、显示表头：.head on 然后执行 select * from tableName

sqlite中命令:
以.开头,大小写敏感（数据库对象名称是大小写不敏感的）
.exit
.help 查看帮助 针对命令
.database 显示数据库信息；包含当前数据库的位置
.tables 或者 .table 显示表名称 &nbsp;没有表则不显示
.schema 命令可以查看创建数据对象时的SQL命令；
.schema databaseobjectname查看创建该数据库对象时的SQL的命令；如果没有这个数据库对象就不显示内容，不会有错误提示

.read FILENAME 执行指定文件中的SQL语句
.headers on/off &nbsp;显示表头 默认off

.mode list|column|insert|line|tabs|tcl|csv &nbsp; 改变输出格式，具体如下

sqlite&gt; .mode list
sqlite&gt; select * from emp;
7369|SMITH|CLERK|7902|17-12-1980|800||20
7499|ALLEN|SALESMAN|7698|20-02-1981|1600|300|30
如果字段值为NULL 默认不显示 也就是显示空字符串

sqlite&gt; .mode column
sqlite&gt; select * from emp;
7369 &nbsp; &nbsp; &nbsp; &nbsp;SMITH &nbsp; &nbsp; &nbsp; CLERK &nbsp; &nbsp; &nbsp; 7902 &nbsp; &nbsp; &nbsp; &nbsp;17-12-1980 &nbsp;800 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 20 &nbsp; &nbsp; &nbsp; &nbsp;
7499 &nbsp; &nbsp; &nbsp; &nbsp;ALLEN &nbsp; &nbsp; &nbsp; SALESMAN &nbsp; &nbsp;7698 &nbsp; &nbsp; &nbsp; &nbsp;20-02-1981 &nbsp;1600 &nbsp; &nbsp; &nbsp; &nbsp;300 &nbsp; &nbsp; &nbsp; &nbsp; 30 &nbsp; &nbsp; &nbsp; &nbsp;
7521 &nbsp; &nbsp; &nbsp; &nbsp;WARD &nbsp; &nbsp; &nbsp; &nbsp;SALESMAN &nbsp; &nbsp;7698 &nbsp; &nbsp; &nbsp; &nbsp;22-02-1981 &nbsp;1250 &nbsp; &nbsp; &nbsp; &nbsp;500 &nbsp; &nbsp; &nbsp; &nbsp; 30&nbsp;

sqlite&gt; .mode insert
sqlite&gt; select * from dept;
INSERT INTO table VALUES(10,&#39;ACCOUNTING&#39;,&#39;NEW YORK&#39;);
INSERT INTO table VALUES(20,&#39;RESEARCH&#39;,&#39;DALLAS&#39;);
INSERT INTO table VALUES(30,&#39;SALES&#39;,&#39;CHICAGO&#39;);
INSERT INTO table VALUES(40,&#39;OPERATIONS&#39;,&#39;BOSTON&#39;);

sqlite&gt; .mode line
sqlite&gt; select * from dept;
DEPTNO = 10
&nbsp;DNAME = ACCOUNTING
&nbsp; &nbsp;LOC = NEW YORK

DEPTNO = 20
&nbsp;DNAME = RESEARCH
&nbsp; &nbsp;LOC = DALLAS

DEPTNO = 30
&nbsp;DNAME = SALES
&nbsp; &nbsp;LOC = CHICAGO

DEPTNO = 40
&nbsp;DNAME = OPERATIONS
&nbsp; &nbsp;LOC = BOSTON

sqlite&gt; .mode tabs
sqlite&gt; select * from dept;
10<span style="white-space: pre;"> </span>ACCOUNTING<span style="white-space: pre;"> </span>&nbsp;NEW YORK
20<span style="white-space: pre;"> </span>RESEARCH<span style="white-space: pre;"> </span>&nbsp;DALLAS
30<span style="white-space: pre;"> </span>SALES<span style="white-space: pre;"> </span>&nbsp;CHICAGO
40<span style="white-space: pre;"> </span>OPERATIONS<span style="white-space: pre;"> </span>&nbsp;BOSTON

sqlite&gt; .mode tcl
sqlite&gt; select * from dept;
&quot;10&quot;<span style="white-space: pre;"> </span>&quot;ACCOUNTING&quot;<span style="white-space: pre;"></span>&quot;NEW YORK&quot;<span style="white-space: pre;"></span>
&quot;20&quot;<span style="white-space: pre;"> </span>&quot;RESEARCH&quot;<span style="white-space: pre;"></span>&quot;DALLAS&quot;<span style="white-space: pre;"></span>
&quot;30&quot;<span style="white-space: pre;"> </span>&quot;SALES&quot;<span style="white-space: pre;"> </span>&nbsp;&quot;CHICAGO&quot;<span style="white-space: pre;"> </span>
&quot;40&quot;<span style="white-space: pre;"> </span>&quot;OPERATIONS&quot;<span style="white-space: pre;"></span>&quot;BOSTON&quot;<span style="white-space: pre;"></span>

sqlite&gt; .mode csv
sqlite&gt; select * from dept;
10,ACCOUNTING,&quot;NEW YORK&quot;
20,RESEARCH,DALLAS
30,SALES,CHICAGO
40,OPERATIONS,BOSTON

.separator &quot;X&quot; 更改分界符号为X
sqlite&gt; .separator &#39;**&#39; &nbsp;
sqlite&gt; select * from dept;
10**ACCOUNTING**&quot;NEW YORK&quot;
20**RESEARCH**DALLAS
30**SALES**CHICAGO
40**OPERATIONS**BOSTON

.dump ?TABLE? &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;生成形成数据库表的SQL脚本
.dump 生成整个数据库的脚本在终端显示
.output stdout &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 将输出打印到屏幕 &nbsp;默认
.output filename &nbsp;将输出打印到文件（.dump &nbsp;.output 结合可将数据库以sql语句的形式导出到文件中）
.nullvalue STRING &nbsp; &nbsp; &nbsp; &nbsp;查询时用指定的串代替输出的NULL串 默认为.nullvalue &#39;&#39;

字段类型：

数据库中存储的每个值都有一个类型,都属于下面所列类型中的一种,(被数据库引擎所控制)
NULL: 这个值为空值
INTEGER: 值被标识为整数,依据值的大小可以依次被存储为1,2,3,4,5,6,7,8个字节
REAL: 所有值都是浮动的数值,被存储为8字节的IEEE浮动标记序号.
TEXT: 文本. 值为文本字符串,使用数据库编码存储(TUTF-8, UTF-16BE or UTF-16-LE).
BLOB: 值是BLOB数据,如何输入就如何存储,不改变格式.

值被定义为什么类型只和值自身有关,和列没有关系,和变量也没有关系.所以sqlite被称作 弱类型 数据库
数据库引擎将在执行时检查、解析类型，并进行数字存储类型(整数和实数)和文本类型之间的转换.
SQL语句中部分的带双引号或单引号的文字被定义为文本,
如果文字没带引号并没有小数点或指数则被定义为整数,
如果文字没带引号但有小数点或指数则被定义为实数,&nbsp;
如果值是空则被定义为空值.
BLOB数据使用符号X&#39;ABCD&#39;来标识.

但实际上，sqlite3也接受如下的数据类型：&nbsp;
smallint 16位的整数。&nbsp;
interger 32位的整数。&nbsp;
decimal(p,s) 精确值p是指全部有几个十进制数,s是指小数点后可以有几位小数。如果没有特别指定，则系统会默认为p=5 s=0 。&nbsp;
float &nbsp;32位元的实数。&nbsp;
double &nbsp;64位元的实数。&nbsp;

char(n) &nbsp;n 长度的字串，n不能超过 254。&nbsp;
varchar(n) 长度不固定且其最大长度为 n 的字串，n不能超过 4000。&nbsp;
graphic(n) 和 char(n) 一样，不过其单位是两个字节， n不能超过127。这个形态是为了支持两个字节长度的字体，如中文字。&nbsp;
vargraphic(n) 可变长度且其最大长度为n的双字元字串，n不能超过2000&nbsp;
date &nbsp;包含了 年份、月份、日期。&nbsp;
time &nbsp;包含了 小时、分钟、秒。&nbsp;
timestamp 包含了 年、月、日、时、分、秒、千分之一秒。

SQLite包含了如下时间/日期函数：&nbsp;
datetime() 产生日期和时间 &nbsp; &nbsp;无参数表示获得当前时间和日期
sqlite&gt; select datetime();
2012-01-07 12:01:32
有字符串参数则把字符串转换成日期
sqlite&gt; select datetime(&#39;2012-01-07 12:01:30&#39;);&nbsp;
2012-01-07 12:01:30

select date(&#39;2012-01-08&#39;,&#39;+1 day&#39;,&#39;+1 year&#39;);
2013-01-09

select datetime(&#39;2012-01-08 00:20:00&#39;,&#39;+1 hour&#39;,&#39;-12 minute&#39;);
2012-01-08 01:08:00

select datetime(&#39;now&#39;,&#39;start of year&#39;);
2012-01-01 00:00:00

select datetime(&#39;now&#39;,&#39;start of month&#39;);
2012-01-01 00:00:00

select datetime(&#39;now&#39;,&#39;start of day&#39;);
2012-01-08 00:00:00

select datetime(&#39;now&#39;,&#39;start of week&#39;);错误

select datetime(&#39;now&#39;,&#39;localtime&#39;);
结果：2006-10-17 21:21:47

date()产生日期 &nbsp; &nbsp;
sqlite&gt; select date(&#39;2012-01-07 12:01:30&#39;);&nbsp;
2012-01-07
同理 有参和无参
select date(&#39;now&#39;,&#39;start of year&#39;);
2012-01-01

select date(&#39;2012-01-08&#39;,&#39;+1 month&#39;);
2012-02-08

time() 产生时间&nbsp;
select time();
03:14:30

select time(&#39;23:18:59&#39;);
23:18:59

select time(&#39;23:18:59&#39;,&#39;start of day&#39;);
00:00:00

select time(&#39;23:18:59&#39;,&#39;end of day&#39;);错误

在时间/日期函数里可以使用如下格式的字符串作为参数：&nbsp;
YYYY-MM-DD&nbsp;
YYYY-MM-DD HH:MM&nbsp;
YYYY-MM-DD HH:MM:SS&nbsp;
YYYY-MM-DD HH:MM:SS.SSS&nbsp;
HH:MM&nbsp;
HH:MM:SS&nbsp;
HH:MM:SS.SSS&nbsp;
now&nbsp;
其中now是产生现在的时间。

日期不能正确比较大小,会按字符串比较，日期默认格式 dd-mm-yyyy
select hiredate from emp order by hiredate;

17-11-1981
17-12-1980
19-04-1987
20-02-1981
22-02-1981

strftime() 对以上三个函数产生的日期和时间进行格式化
strftime()函数可以把YYYY-MM-DD HH:MM:SS格式的日期字符串转换成其它形式的字符串。 strftime(格式, 日期/时间, 修正符, 修正符, …) &nbsp;select strftime(&#39;%d&#39;,datetime());
它可以用以下的符号对日期和时间进行格式化：&nbsp;
%d 在该月中的第几天, 01-31&nbsp;
%f 小数形式的秒，SS.SSS&nbsp;
%H 小时, 00-23&nbsp;
%j 算出某一天是该年的第几天，001-366&nbsp;
%m 月份，00-12&nbsp;
%M 分钟, 00-59&nbsp;
%s 从1970年1月1日到现在的秒数&nbsp;
%S 秒, 00-59&nbsp;
%w 星期, 0-6 (0是星期天)&nbsp;
%W 算出某一天属于该年的第几周, 01-53&nbsp;
%Y 年, YYYY&nbsp;
%% 百分号

select strftime(&#39;%Y.%m.%d %H:%M:%S&#39;,&#39;now&#39;);&nbsp;
select strftime(&#39;%Y.%m.%d %H:%M:%S&#39;,&#39;now&#39;,&#39;localtime&#39;);&nbsp;
结果：2006.10.17 21:41:09

select hiredate from emp&nbsp;
order by strftime(&#39;%Y.%m.%d %H:%M:%S&#39;,hiredate); 正确

select strftime(&#39;%Y.%m.%d %H:%M:%S&#39;,hiredate) from emp&nbsp;
order by strftime(&#39;%Y.%m.%d %H:%M:%S&#39;,hiredate); 错误

算术函数&nbsp;
abs(X) 返回给定数字表达式的绝对值。&nbsp;
max(X,Y[,...]) 返回表达式的最大值。 &nbsp;组函数 max(列名)
sqlite&gt; select max(2,3,4,5,6,7,12);
12

min(X,Y[,...]) 返回表达式的最小值。&nbsp;
random() 返回随机数。
sqlite&gt; select random();
3224224213599993831
&nbsp;
round(X[,Y]) 返回数字表达式并四舍五入为指定的长度或精度。&nbsp;

字符处理函数&nbsp;
length(X) 返回给定字符串表达式的字符个数。&nbsp;
lower(X) 将大写字符数据转换为小写字符数据后返回字符表达式。&nbsp;
upper(X) 返回将小写字符数据转换为大写的字符表达式。&nbsp;
substr(X,Y,Z) 返回表达式的一部分。 &nbsp;从Y开始读Z个字符 &nbsp;Y最小值1
sqlite&gt; select substr(&#39;abcdef&#39;,3,3); &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
cde

quote(A) 给字符串加引号
&nbsp;sqlite&gt; select quote(&#39;aaa&#39;);
&#39;aaa&#39;

条件判断函数&nbsp;
ifnull(X,Y) &nbsp;如果X为null 返回Y
select ifnull(comm,0) from emp;
0
300
500
0
1400

集合函数&nbsp;
avg(X) 返回组中值的平均值。&nbsp;
count(X) 返回组中项目的数量。&nbsp;
max(X) 返回组中值的最大值。&nbsp;
min(X) 返回组中值的最小值。&nbsp;
sum(X) 返回表达式中所有值的和。&nbsp;

其他函数&nbsp;
typeof(X) 返回数据的类型。&nbsp;
sqlite&gt; select typeof(111);
integer
sqlite&gt; select typeof(&#39;233&#39;);
text
sqlite&gt; select typeof(&#39;2012-12-12&#39;);
text
sqlite&gt; select typeof(&#39;223.44&#39;);
text
sqlite&gt; select typeof(223.44);
real

last_insert_rowid() 返回最后插入的数据的ID。&nbsp;
sqlite_version() 返回SQLite的版本。&nbsp;
sqlite&gt; select sqlite_version();
3.7.9

change_count() 返回受上一语句影响的行数。&nbsp;
last_statement_change_count()

create table emp_bak select * from EMP;不能在sqlite中使用

插入记录
insert into table_name values (field1, field2, field3...);
查询
select * from table_name;查看table_name表中所有记录；
select * from table_name where field1=&#39;xxxxx&#39;; 查询符合指定条件的记录；

select .....&nbsp;<span style="white-space: pre;"></span>
from table_name[,table_name2,...]
where .....<span style="white-space: pre;"> </span>
group by....<span style="white-space: pre;"> </span>
having ....<span style="white-space: pre;"> </span>
order by ...

select .....&nbsp;<span style="white-space: pre;"></span>
from table_name &nbsp;inner join | left outer join | right outer join table_name2
on ...
where .....<span style="white-space: pre;"> </span>
group by....<span style="white-space: pre;"> </span>
having ....<span style="white-space: pre;"> </span>
order by ...

子查询：
select *&nbsp;
from EMP m
where SAL&gt;
(select avg(SAL) from EMP where DEPTNO=m.DEPTNO);<span style="white-space: pre;"> </span>&nbsp;

支持case when then 语法
update EMP
set SAL=
(
case
when DEPTNO=10 and JOB=&#39;MANAGER&#39; then SAL*1.1
when DEPTNO=20 and JOB=&#39;CLERK&#39; then SAL*1.2
when DEPTNO=30 &nbsp;then SAL*1.1
when DEPTNO=40 &nbsp;then SAL*1.2
else SAL
END
);

select ENAME,&nbsp;
case DEPTNO
when 10 then &#39;后勤部&#39;
when 20 then &#39;财务部&#39;
when 30 then &#39;内务部门&#39;
else &#39;其他部门&#39;
end as dept
from EMP;

支持关联子查询 &nbsp;in后面的语法中可以有limit（mysql不可以）
select *
from emp e
where e.EMPNO in&nbsp;
(
select empno &nbsp;
from EMP
where deptno=e.DEPTNO
order by SAL desc
limit 0,2
);

支持表和表之间的数据合并等操作
union 去重复 &nbsp;union all 不去掉重复
select deptno from emp
union&nbsp;
select deptno from dept;

select deptno from emp
union all
select deptno from dept;

在列名前加distinct也是去重复
sqlite&gt; select distinct deptno from emp;

删除
delete from table_name where ...

删除表
drop table_name; &nbsp; &nbsp; 删除表；
drop index_name; &nbsp; &nbsp; 删除索引；

修改
update table_name
set xxx=value[, xxx=value,...]
where ...

建立索引

如果资料表有相当多的资料，我们便会建立索引来加快速度。好比说：

create index film_title_index on film(title);
意思是针对film资料表的name字段，建立一个名叫film_name_index的索引。这个指令的语法为

CREATE [ UNIQUE ] &nbsp;NONCLUSTERED &nbsp;INDEX index_name
&nbsp; &nbsp; ON { table | view } ( column [ ASC | DESC ] [ ,...n ] )
create index index_name on table_name(field_to_be_indexed);
一旦建立了索引，sqlite3会在针对该字段作查询时，自动使用该索引。这一切的操作都是在幕后自动发生的，无须使用者特别指令。

其他sqlite的特别用法

sqlite可以在shell底下直接执行命令：
sqlite3 film.db &quot;select * from emp;&quot;

输出 HTML 表格：
sqlite3 -html film.db &quot;select * from film;&quot;
将数据库「倒出来」：

sqlite3 film.db &quot;.dump&quot; &gt; output.sql
利用输出的资料，建立一个一模一样的数据库（加上以上指令，就是标准的SQL数据库备份了）：

sqlite3 film.db &lt; output.sql
在大量插入资料时，你可能会需要先打这个指令：

begin;
插入完资料后要记得打这个指令，资料才会写进数据库中：
commit;

sqlite&gt; begin;
sqlite&gt; insert into aaaa values(&#39;aaa&#39;,&#39;333&#39;);
sqlite&gt; select * from aaaa;
2|sdfds
sdfsd|9
2012-12-12|13:13:13
aaa|333
sqlite&gt; rollback;
sqlite&gt; select * from aaaa;
2|sdfds
sdfsd|9
2012-12-12|13:13:13

创建和删除视图
CREATE VIEW view_name AS
SELECT column_name(s)
FROM table_name
WHERE condition
DROP VIEW view_name

create view &nbsp;e as
select avg(SAL) avgsal,DEPTNO
from EMP
group by DEPTNO;

select ENAME,EMP.DEPTNO,SAL,avgsal
from EMP inner join e
on EMP.DEPTNO=e.DEPTNO
where SAL&gt;avgsal;

练习员工表：

PRAGMA foreign_keys=OFF;
BEGIN TRANSACTION;
CREATE TABLE DEPT
(
DEPTNO int(2) not null,
DNAME varchar(14),
LOC &nbsp; &nbsp;varchar(13)
);
INSERT INTO &quot;DEPT&quot; VALUES(10,&#39;ACCOUNTING&#39;,&#39;NEW YORK&#39;);
INSERT INTO &quot;DEPT&quot; VALUES(20,&#39;RESEARCH&#39;,&#39;DALLAS&#39;);
INSERT INTO &quot;DEPT&quot; VALUES(30,&#39;SALES&#39;,&#39;CHICAGO&#39;);
INSERT INTO &quot;DEPT&quot; VALUES(40,&#39;OPERATIONS&#39;,&#39;BOSTON&#39;);
CREATE TABLE EMP
(
EMPNO &nbsp; &nbsp;int(4) not null,
ENAME &nbsp; &nbsp;varchar(10),
JOB &nbsp; &nbsp; &nbsp;varchar(9),
MGR &nbsp; &nbsp; &nbsp;int(4),
HIREDATE date,
SAL &nbsp; &nbsp; &nbsp;int(7 ),
COMM &nbsp; &nbsp; int(7 ),
DEPTNO &nbsp; int(2)
);
INSERT INTO &quot;EMP&quot; VALUES(7369,&#39;SMITH&#39;,&#39;CLERK&#39;,7902,&#39;17-12-1980&#39;,800,NULL,20);
INSERT INTO &quot;EMP&quot; VALUES(7499,&#39;ALLEN&#39;,&#39;SALESMAN&#39;,7698,&#39;20-02-1981&#39;,1600,300,30);
INSERT INTO &quot;EMP&quot; VALUES(7521,&#39;WARD&#39;,&#39;SALESMAN&#39;,7698,&#39;22-02-1981&#39;,1250,500,30);
INSERT INTO &quot;EMP&quot; VALUES(7566,&#39;JONES&#39;,&#39;MANAGER&#39;,7839,&#39;02-04-1981&#39;,2975,NULL,20);
INSERT INTO &quot;EMP&quot; VALUES(7654,&#39;MARTIN&#39;,&#39;SALESMAN&#39;,7698,&#39;28-09-1981&#39;,1250,1400,30);
INSERT INTO &quot;EMP&quot; VALUES(7698,&#39;BLAKE&#39;,&#39;MANAGER&#39;,7839,&#39;01-05-1981&#39;,2850,NULL,30);
INSERT INTO &quot;EMP&quot; VALUES(7782,&#39;CLARK&#39;,&#39;MANAGER&#39;,7839,&#39;09-06-1981&#39;,2450,NULL,10);
INSERT INTO &quot;EMP&quot; VALUES(7788,&#39;SCOTT&#39;,&#39;ANALYST&#39;,7566,&#39;19-04-1987&#39;,3000,NULL,20);
INSERT INTO &quot;EMP&quot; VALUES(7839,&#39;KING&#39;,&#39;PRESIDENT&#39;,NULL,&#39;17-11-1981&#39;,5000,NULL,10);
INSERT INTO &quot;EMP&quot; VALUES(7844,&#39;TURNER&#39;,&#39;SALESMAN&#39;,7698,&#39;08-09-1981&#39;,1500,0,30);
INSERT INTO &quot;EMP&quot; VALUES(7876,&#39;ADAMS&#39;,&#39;CLERK&#39;,7788,&#39;23-05-1987&#39;,1100,NULL,20);
INSERT INTO &quot;EMP&quot; VALUES(7900,&#39;JAMES&#39;,&#39;CLERK&#39;,7698,&#39;03-12-1981&#39;,950,NULL,30);
INSERT INTO &quot;EMP&quot; VALUES(7902,&#39;FORD&#39;,&#39;ANALYST&#39;,7566,&#39;03-12-1981&#39;,3000,NULL,20);
INSERT INTO &quot;EMP&quot; VALUES(7934,&#39;MILLER&#39;,&#39;CLERK&#39;,7782,&#39;23-01-1982&#39;,1300,NULL,10);
CREATE TABLE SALGRADE
(
GRADE int,
LOSAL int,
HISAL int
);
INSERT INTO &quot;SALGRADE&quot; VALUES(1,700,1200);
INSERT INTO &quot;SALGRADE&quot; VALUES(2,1201,1400);
INSERT INTO &quot;SALGRADE&quot; VALUES(3,1401,2000);
INSERT INTO &quot;SALGRADE&quot; VALUES(4,2001,3000);
INSERT INTO &quot;SALGRADE&quot; VALUES(5,3001,9999);
COMMIT;