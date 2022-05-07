# quick_learning_MySQL
quick notes for MySQL Crash Course  
2022-05-07：在迅速看完Sams Teach Yourself SQL in 10 Minutes （中文版《SQL必知必会》，人民邮电出版社出版）的基础上，把《MySQL必知必会》看完作为温习吧。据说大面积重复。  
从简单的数据检索开始，逐步进入一些复杂的内容，包括联结的使用、子查询、正则 表达式和基于全文本的搜索、存储过程、游标、触发器、表约束，等等。  
其中比较高级的内容，如触发器、游标、存储过程、访问控制、事务等，是《SQL必知必会》中为顾及SQL在不同DBMS中可移植性而省略的部分。  

-------------------

#### 服务器搭建
注:mysql-workbench-community-8.0.28-winx64.msi不够，要下载安装mysql-installer-community-8.0.28.0.msi  
workbench只是工作区，server不在里面。需要装community的时候configure

没用虚拟机的话，本地服务器应该就一个。  
确定数据库的名称，端口等都维持了默认，密码设好。

之前为《SQL必知必会》的样例建了一个模式tysql，现在再为《MySQL必知必会》建了一个模式mysqlcrashcourse。本来想用驼峰命名法的，但提示数据库启用了表格和模式名小写要求。
样例表的生成，直接使用了https://forta.com/books/0672327120/ 的SQL脚本文件。内容看得懂，但是自己写还是生疏。
