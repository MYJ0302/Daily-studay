## 一、DQL的多表查询（多表联合查询）  
多表查询指的是要查询的数据存在多张表中

### 1.关系模型：表与表之间的关系
关系模型与数学的映射是类似的
一对一关系
一对多关系
多对多关系

### 2.交叉连接  
##### 2张表的交叉连接  
语法：**SELECT * FROM 表1, 表2WHERE 表1.公共列 = 表2.公共列;**  
例：查询计算机系的学生信息  
思路：  
1.分析数据的来源（需要搞清楚从哪些表中查询）  
计算机系在department中，学生信息在student中  
2.从两张表中查询数据：需要给表与表之间加上一个逗号  
SELECT * FROM student , department ;   
3.需要在查询结果的基础上进行过滤，需要加上过滤条件WHERE  
SELECT * FROM student s, department d WHERE s.did = d.did ;  
4.对系做过滤  
SELECT * FROM student s ,department d WHERE s.did = d.did AND d.dname = "计算机系";  
注意：  
1.给表名起别名之后，在SELECT/WHERE 子句中不能再使用原名  
2.如果多张表存在相同的列名，需要给列名前加上表名；如果列名是唯一的，可以加也可以不加  

##### 3张表的交叉连接  
Eg：查询计算机系学生的考试成绩  
1.分析数据来源  
计算机系存在department中，考试成绩存在score 表中，这两张表没有公共列，所以需要引入student表  
2.先用语法将多张表连接起来  
SELECT * FROM student stu ,department d , score sc WHERE stu.sid = sc.sid AND stu.did = d.did ;  
3.根据查询的结果进行分析，分析是否还需要加更多的过滤条件  
加上系名称这个过滤条件  
SELECT * FROM student stu ,department d , score sc WHERE stu.sid = sc.sid AND stu.did = d.did AND d.dname = "计算机系";  

### 3.内连接  
语法：**SELECT * FROM 表1 INNER JOIN 表2 ON 表1.公共列 = 表2.公共列;**  
说明：ON子句的作用：用来设置内连接的连接条件  
#####  2张表的内连接  
例：查询计算机系的学生名称  
1.分析数据的来源  
计算机系在department中，学生在student中  
2.将两张表连接起来  
SELECT * FROM department d INNER JOIN student s ON d.did = s.did ;  
3.根据查询的结果进行分析，分析是否还需要更多的过滤条件 
SELECT * FROM department d INNER JOIN student s ON d.did = s.did WHERE d.dname = "计算机系" ;  
总结：  
1.对于同一个题目，使用交叉连接查询和使用内连接查询结果是一样的，内连接等价于交叉连接+WHERE条件  
2.内连接查询的效率比交叉连接查询效率要高  
3.内连接查询语法中的关键字INNER可以省略  
#####  3张表的内连接  
例：使用内连接查询公共课的考试成绩，并且还需知道那些学生参加了考试  
1.course , score , student  
2.SELECT * FROM student stu JOIN score sc ON stu.sid = sc.sid JOIN course c ON c.cid = sc.cid ;  
3.SELECT * FROM student stu JOIN score sc ON stu.sid = sc.sid JOIN course c ON c.cid = sc.cid WHERE c.cname = "公共课";  
4.SELECT stu.sname 学生姓名, sc.grade 考试成绩, c.cname 课程名称 FROM student stu JOIN score sc ON stu.sid = sc.sid JOIN course c ON c.cid = sc.cid WHERE c.cname = "公共课" AND sc.grade IS NOT NULL ;  

### 4.外连接  
外连接分为左连接和右连接  
#### （1）左连接  
语法：**SELECT * FROM 表1 LIFT JOIN 表2 ON 表1.公共列= 表2.公共列;**
左连接查询结果：以左表为主，查询到两张表交集的数据，并且会把左表独有的数据查询出来  
总结：左连接先查询出左表的数据，然后再查询右表中的，如果右表中满足条件的数据正常显示出来，不满足条件的数据就显示NULL  

#### (2)右连接  
语法：**SELECT * FROM 表1 RIGHT JOIN 表2 ON 表1.公共列= 表2.公共列;**
右连接查询结果：以左表为主，查询到两张表交集的数据，并且会把左表独有的数据查询出来  
面试题：左连接与右连接的区别  
1.语法不同  
2.查询结果不同，左连接查询的结果是两张表交集的数据以及左表独有的数据；右连接查询的结果是两张表交集的数据以及右表独有的数据  
3.把两张表的顺序换一下，两者就是等价的  

### 5.嵌套查询  
定义：一个SELECT语句中的WHERE 子句中嵌套了另外一个SELECT语句的查询称之为嵌套查询。其中外层的 ELECT语句称之为外层查询（也叫 父查询），内层的SELECT语句称之为内层查询（也叫 子查询）  
使用场景：  
SELECT * FROM 表名 WHERE 列名 比较运算符 值;  
在题目中没有告诉我们要比较的值是多少，需要使用另外一个SQL把未知的值查询查询出来来代替语法中的要比较的值  
#### (1)子查询语句之查询出来一个值（只能返回一行一列值）  
语法：**SELECT * FROM 表名 WHERE 列名 比较运算符 （SELECT 列名 FROM 表名 WHERE 条件）;**  
注意事项：  
1.子查询语句一定要写在括号中，意味着再执行的时候，子查询语句会先执行  
2.子查询语句中SELECT后面只能写列名，不能写*  
#### (2)子查询语句查询出来多个值  
语法：**SELECT * FROM 表名 WHERE 列名 IN (SELECT 列名 FROM 表名 WHERE 条件);**
总结：  
1.子查询用在查询条件中，用来代替搜索值的  
2.如果子查询只查询出来一个值，就应该使用 比较运算符  
3.如果子查询查询出来多个值，就应该使用 IN  
4.因为子查询语句加了括号，所以，在执行的时候会先执行    

## 二、分组查询
分组：把具有相同特征的数据放在一起，把放在一起的数据做一个统计  
### 1.聚合函数  
聚合函数的定义：  
指的是对一组数据进行汇总的函数，输入的是一组数据，输出的是单个值  
- max() 表示统计某列的最大值  
- min() 表示统计某列的最小值  
- avg() 表示统计某列的平均值  
- sum() 表示统计某列的总和  
- count(*) 用来统计数据的总行数，会统计NULL值  
- count(列名) 用来统计数据的总行数，不会统计NULL值  

### 2.对单列进行分组  
例：查询每门课程的最高分  
1.分析数据的来源  
2.按照什么字段分组  
3.使用哪个聚合函数  
SELECT did,COUNT(*) FROM student GROUP BY did;  

### 3.对多列进行分组
语法：**SELECT * FROM 表名 GROUP BY 列名1, 列名2;**  
多列分组：先对第一列进行分组，在组中再对第二列进行分组
例”查询每一个系各年龄段的学生人数
SELECT did 系名称,sage 年龄, COUNT(*) 人数 FROM student GROUP BY did ,sage ; 
SELECT d.did 系名称,s.sage 年龄,COUNT(*) 人数 FROM student s JOIN department d ON s.did = d.did GROUP BY d.did , s.sage;     

### 4.HAVING  
HAVING的作用与WHERE 的作用是一样的：都是用来做数据的过滤，但是，HAVING 是用在分组之后做过滤，而WHERE 是用在分组之前  
SELECT did 系名称 , COUNT(*) 人数 FROM student GROUP BY did HAVING 人数 > 2; 
SELECT d.did 系名称, COUNT(*) 人数 FROM department d JOIN student s ON s.did = d.did GROUP BY d.did HAVING 人数 > 2;  

总结：DQL语句中关键字的书写顺序及执行顺序
书写顺序：SELECT -> DISTINCT -> FROM -> JOIN -> ON -> WHERE -> GROUP BY -> HAVING -> ORDER BY -> LIMIT   
执行顺序：FROM -> JOIN -> ON -> WHERE -> GROUP BY -> HAVING -> SELECT -> DISTINCT -> ORDER BY -> LIMIT  



v