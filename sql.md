[mysql manual in chinase](http://doc.mysql.cn/mysql5/refman-5.1-zh.html-chapter/ "中文")  
[w3c mysql manual](http://www.w3school.com.cn/sql/sql_alter.asp)  
[runoob mysql manual](http://www.runoob.com/mysql/mysql-database-import.html)

### sql查找mysql安装目录
`select @@basedir;`
### sql查看链接数
`show full processlist;`
### cmd查看mysql版本
`mysql -V`
### 将MySQL 添加到服务中。

在Windows Run中输入cmd，这时上面有提示（cmd.exe），右键单击cmd.exe, 选择Run as administrator，进入路径： d:/appspace/mysql /bin>

输入  mysqld --install MySQL --defaults-file="C:\Windows\my.ini"

要指定defaults-file.

命令行中输入services.msc回车，可以看到MySQL已被添加到Services中，

Path to executable中的内容为

d:\appspace\mysql\bin\mysqld --defaults-file=C:\windows\my.ini MySQL
### 删除mysql服务
mysqld --remove Mysql
### 开启/关闭mysql服务
net start/stop mysql
### 查看字符集
`show variables like 'character%'`;

### 删除数据库
`drop database if exists drop_database`

### 创建表
```sql
CREATE TABLE `user` (
  `id` INT(32) NOT NULL,
  `name` varchar(100) DEFAULT NULL,
  `psw` varchar(100) DEFAULT NULL,
  PRIMARY KEY (`id`)
  ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

### 是在命令行中查询显示乱码（DOS不支持UTF8从MYSQL中显示），解决如下：

mysql> set names gbk;
sql 对大小写不敏感
日期
基于集合理论

## 在创建mysql数据库的时候如何支持UTF-8编码

1. 用工具  
CHARSET 选择 utf8
COLLATION 选择 utf8_general_ci
2. 用SQL语句  
GBK: CREATE DATABASE `test1` DEFAULT CHARACTER SET gbk COLLATE gbk_chinese_ci;
UTF-8: CREATE DATABASE `test2` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

## 解决cmd下，乱码问题
你也可以使用 在 windows 中 dos 中 mysql -uroot --default-character-set=gbk ...

连接方式 （注意 在Windows 下 不管你的数据是什么格式的 都得用gbk ,原因是 dos 中文只支持 gbk ）

 order by排序 返回游标不能做表达式 select atime, deathnumber, province from full_accident_tbl where (deathnumber>=5 and deathnumber<=10) and province='山东' order by 2

不同值统计 select count(distinct deathnumber) from full_accident_tbl where (deathnumber>=5 and deathnumber<=10) and province='山东';

分组统计 select province, sum(deathnumber) from full_accident_tbl where (deathnumber>=5 and deathnumber<=10) group by province;
+----------+------------------+
| province | sum(deathnumber) |
+----------+------------------+
| 上海     | 151              |
| 云南     | 1828             |
| 内蒙     | 695              |
| 北京     | 165              |
| 吉林     | 315              |
| 四川     | 1565             |
| 天津     | 84               |
| 宁夏     | 163              |
| 安徽     | 881              |
| 山东     | 1342             |
| 山西     | 1251             |
| 广东     | 1435             |
| 广西     | 966              |
| 新疆     | 818              |
| 江苏     | 569              |
| 江西     | 599              |
| 河北     | 723              |
| 河南     | 895              |
| 浙江     | 1289             |
| 海南     | 151              |
| 湖北     | 754              |
| 湖南     | 1601             |
| 甘肃     | 825              |
| 福建     | 937              |
| 西藏     | 435              |
| 贵州     | 2469             |
| 辽宁     | 772              |
| 重庆     | 915              |
| 陕西     | 957              |
| 青海     | 210              |
| 黑龙江   | 984              |
+----------+------------------+
31 rows in set
当我们选不只一个栏位，且其中至少一个栏位有包含函数的运用时，我们就需要用到 GROUP BY 这个指令。在这个情况下，我们需要确定我们有 GROUP BY 所有其他的栏位。换句话说，除了有包括函数的栏位外，我们都需要将其放在 GROUP BY 的子句中。
或者
select t1.pwd ,count(t1.pwd) from newuser t1 group by t1.pwd;

+----------+---------------+
| pwd      | count(t1.pwd) |
+----------+---------------+
| 123      |             2 |
| 123123   |             1 |
| 123456   |            15 |
| 123465   |             1 |
| 654321   |             1 |
| yr910118 |             1 |
+----------+---------------+

对函数的结果进行筛选不一定需要group子句    select province, sum(deathnumber) from full_accident_tbl where (deathnumber>=5 and deathnumber<=10) group by province having sum(deathnumber) <200
;
+----------+------------------+
| province | sum(deathnumber) |
+----------+------------------+
| 上海     | 151              |
| 北京     | 165              |
| 天津     | 84               |
| 宁夏     | 163              |
| 海南     | 151              |
+----------+------------------+
5 rows in set
或者

select t1.pwd ,count(t1.pwd) from newuser t1 group by t1.pwd having count(pwd) <= 2;
| pwd      | count(t1.pwd) |
+----------+---------------+
| 123      |             2 |
| 123123   |             1 |
| 123465   |             1 |
| 654321   |             1 |
| yr910118 |             1 |
+----------+---------------+
列别名 有空格时用‘’ 及表格别名。

当我们在 WHERE 子句或 HAVING 子句中插入另一个 SQL 语句时，我们就有一个 subquery 的架构。第一，它可以被用来连接表格。另外，有的时候 subquery 是唯一能够连接两个表格的方式。

SELECT SUM(Sales) FROM Store_Information WHERE Store_name IN (SELECT store_name FROM Geography
WHERE region_name = 'West');


UNION 指令的目的是将两个 SQL 语句的结果合并起来。从这个角度来看， UNION 跟 JOIN 有些许类似，因为这两个指令都可以由多个表格中撷取资料。 UNION 的一个限制是两个 SQL 语句所产生的列需要是同样的资料种类和个数。另外，当我们用 UNION 这个指令时，我们只会看到不同的资料值 (类似 SELECT DISTINCT)。

UNION ALL 这个指令的目的也是要将两个 SQL 语句的结果合并在一起。 UNION ALL 和 UNION 不同之处在于 UNION ALL 会将每一笔符合条件的资料都列出来，无论资料值有无重复。

和 UNION 指令类似，INTERSECT 也是对两个 SQL 语句所产生的结果做处理的。不同的地方是， UNION 基本上是一个 OR (如果这个值存在于第一句或是第二句，它就会被选出)，而 INTERSECT 则比较像 AND ( 这个值要存在于第一句和第二句才会被选出)。UNION 是联集，而 INTERSECT 是交集。
请注意，在 INTERSECT 指令下，不同的值只会被列出一次。

ifconfig eth0 192.168.254.200 netmask 255.255.255.0

网卡配置文件

mysql 命令下执行脚本

第一种方式：在未连接数据库的情况下，输入 mysql -h localhost -u root -p 123456 database < d:\book.sql 回车即可；

第二种方式：在已连接数据库的情况下，此时命令提示符为mysql>，输入 source d:\book.sql  或者 \. d:\book.sql 回车即可。

### 聚合查询`oracle`
```sql

SELECT
	DQBM_BM.province as 省,
	WKKDB_BM.WKKDBMC as 等别,
	COUNT (*) as 数量,
	SUM (
		DECODE (SFAQSCXKZ, '是', 1, 0)
	) AS 已取得安全生产许可证,
	sum(DECODE (SFAZZXJCXT, '是', 1, 0)) AS 已安装在线监测设备
FROM
	WKK
join WKKDB_BM on WKK.WKKDB = WKKDB_BM.WKKDB
JOIN DQBM_BM ON WKK.DQBM = DQBM_BM.DQBM
GROUP BY
	WKKDB_BM.WKKDBMC,
	DQBM_BM.PROVINCE;

--别名
SELECT
	QY.QYDZ AS 企业地址,
	COUNT (s.qyid) AS 企业数量,
	COUNT (S.AQSCXKZBH) AS 安全生产许可证,
	SUM (s.CYRYSL) AS 从业人员数量,
	SUM (s.yycl) AS 原油产量,
	SUM (s.trqcl) AS 天然气产量,
	SUM (s.yjsl),
	SUM (GHLYJSL) AS 高含硫油井数量
FROM
	SYK s
JOIN QYQK qy ON QY.QYID = s.QYID
WHERE
	s.syfl = 1 -- 1-> 陆油， 2-> 海油
AND s.ZYKCJZ = 1 -- 1 -> 原油, 2 -> 天然气
GROUP BY
	QY.qydz;
```
* mysqlimport
* 乱码
### EXISTS
将外查询表的每一行，代入内查询作为检验，如果内查询返回的结果取非空值，则EXISTS子句返回TRUE，这一行行可作为外查询的结果行，否则不能作为结果。
### NULL处理
* IS NULL: 当列的值是NULL,此运算符返回true。
* IS NOT NULL: 当列的值不为NULL, 运算符返回true。
* <=>: 比较操作符（不同于=运算符），当比较的的两个值为NULL时返回true。
### 正则匹配
`SELECT name FROM person_tbl WHERE name REGEXP '^[aeiou]|ok$';`

### 表sql批量导入

### sql删除列
`ALTER TABLE bying_flow	DROP COLUMN last_modify_time;`