#### MySQL Workbench常用快捷键
执行选中的SQL(如无选中则执行所有) Ctrl + Shift + Enter  
执行当前这句SQL  Ctrl + Enter  
选中SQL注释/取消注释 Ctrl + /  
格式化SQL Ctrl + B  
新开SQL编辑器 Ctrl + T

-----------

### SELECT 子句及其顺序
|子 句	|说 明|是否必须使用
|--|--|--|
|SELECT	|要返回的列或表达式	|是
|FROM	|从中检索数据的表	|仅在从表选择数据时使用
|WHERE	|行级过滤	|否
|GROUP BY	|分组说明	|仅在按组计算聚集时使用
|HAVING	|组级过滤	|否
|ORDER BY	|输出排序顺序	|否
|LIMIT	|要检索的行数	|否

多条SQL语句必须以分号（；）分隔。MySQL如同多数DBMS一样，不需要在单条SQL语句后加分号。  
**使用mysql 命令行，必须加上分号或\g来结束SQL语句。**  
SQL语句不区分大小写，许多SQL开发人员喜欢对所有SQL关键字使用大写，而对所有列和表名使用小写，以易于阅读和调试。  
处理SQL语句时，行间空格都被忽略，所以单句可单行也可转行。
#### SELECT
从一个或多个表中检索信息  
必须至少给出两条信息——想选择什么，以及从什么地方选择，即SELECT 列 FROM 表  
如果没有明确排序查询结果（下一章介绍），则返回的数据的顺序没有特殊意义。  
SQL语句一般返回原始的、无格式的数据。数据的格式化是一个表示问题，而不是一个检索问题。因此，表示（对齐和显示上面的价格值，用货币符号和逗号表示其金额）一般在显示该数据的应用程序中规定。

SELECT * FROM 表
返回表中所有列，好处是能检索出名字未知的列，但通常不要这么做。检索不需要的列通常会降低检索和应用程序的性能。  
**在Workbench中左边导航，能看到数据库里的结构信息。**

SELECT DISTINCT 列 ...
指示MySQL只返回不同的值  
其中DISTINCT 关键字必须直接放在列名的前面，且应用于所有列而不仅是前置它的列。

LIMIT子句限制结果行数  
带一个值的LIMIT 总是从第一行开始，给出的数为返回的行数。带两个值的LIMIT 可以指定从行号为第一个值的位置开始。  
**注：检索出来的第一行为行0而不是行1。**  
两种语法：LIMIT 4 OFFSET 3 意为从行3开始取4行，就像LIMIT 3,4 一样。

---------------

#### ORDER BY 子句，根据需要排序检索出的数据
用非检索的列排序数据也合法  
按多个列排序，只要指定列名，列名之间用逗号分开即可（就像选择多个列时所做的那样）  
**在按多个列排序时，排序完全按所规定的顺序进行**  
降序排序，必须指定DESC 关键字。DESC 关键字只应用到直接位于其前面的列名（区别于DISTINCT的作用域）。  
与DESC 相反的关键字是ASC，但一般没啥用。  
**在对文本性的数据进行排序时，大小写是否区分及排序顺序取决于数据库的设置。  
默认不区分大小写，必要时问数据库管理员。  
在给出ORDER BY 子句时，应该保证它位于FROM 子句之后。如果使用LIMIT ，它必须位于ORDER BY 之后。使用子句的次序不对将产生错误消息。**

#### WHERE 子句，指定搜索条件，过滤数据
只检索所需数据需要指定搜索条件（search criteria），搜索条件也称为过滤条件（filter condition）  
**在同时使用ORDER BY 和WHERE 子句时，应该让ORDER BY 位于WHERE 之后，否则将会产生错误**  
##### WHERE子句操作符
**操作符（operator） 用来联结或改变WHERE 子句中的子句的关键字。也称为逻辑操作符 （logical operator）。**  
=	等于  
<>	不等于  
!=	不等于  
<	小于  
<=	小于等于  
\>	大于  
\>=	大于等于  
BETWEEN	在指定的两个值之间，两个值用AND关键字分隔，匹配范围包括指定的开始值和结束值，  
AND  
OR  
**SQL（像多数语言一样）在处理OR 操作符前，优先处理AND 操作符。所以组合WHERE子句时建议使用圆括号明确分组。**  
IN 操作符用来指定条件范围，范围中的每个条件都可以进行匹配。IN 取合法值的由逗号分隔的清单，全都括在圆括号中。功能与OR相当。  
IN 操作符一般比OR 操作符清单执行更快；IN 的最大优点是可以包含其他SELECT 语句，使得能够更动态地建立WHERE 子句  
NOT 否定它之后所跟的任何条件。MySQL支持使用NOT 对IN 、BETWEEN 和EXISTS 子句取反。

单引号用来限定字符串

##### NULL 无值 （novalue），它与字段包含0、空字符串或仅仅包含空格不同。在一个列不包含值时，称其为包含空值NULL。
检查具有NULL 值的列，用WHERE 的 IS NULL 子句  
因为未知具有特殊的含义，数据库不知道它们是否匹配，所以在匹配过滤或不匹配过滤时都不主动返回有NULL的行。
