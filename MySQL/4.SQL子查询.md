嵌套SELECT语句也叫子查询，一个 SELECT 语句的查询结果能够作为另一个语句的输入值。子查询不但能够出现在Where子句中，也能够出现在from子句中，作为一个临时表使用，也能够出现在select list中，作为一个字段值来返回。

#### 1.单行子查询
单行子查询是指子查询的返回结果只有一行数据。当主查询语句的条件语句中引用子查询结果时可用单行比较符号（＝, >, <, >=, <=, <>）来进行比较。

例：
`sql> select ename,deptno,sal
from emp 
where deptno=(select deptno from dept where loc='NEW YORK')；`

#### 2.多行子查询
多行子查询即是子查询的返回结果是多行数据。当主查询语句的条件语句中引用子查询结果时必须用多行比较符号（IN，ALL,ANY）来进行比较。其中，IN的含义是匹配子查询结果中的任一个值即可（"IN" 操作符，能够测试某个值是否在一个列表中），ALL则必须要符合子查询的所有值才可，ANY要符合子查询结果的任何一个值即可。而且须注意ALL 和ANY 操作符不能单独使用，而只能与单行比较符（=、>、< 、>= 、<= 、<>）结合使用。

例：
##### 2.1多行子查询使用IN操作符号
例子：查询选修了老师名叫Rona(假设唯一)的学生名字

`sql> select stName 
from Student 
where stId in(selectdistinct stId from score where teId=(select teId from teacher where teName='Rona'));`

查询所有部门编号为A的资料：

`SELECT ename,job,sal
 FROM EMP 
 WHERE deptno in ( SELECT deptno FROM dept WHERE dname LIKE 'A%')；`

##### 2.2多行子查询使用ALL操作符
例子：查询有一门以上的成绩高于Kaka的最高成绩的学生的名字:

`sql> select stName
from Student
where stId in(select distinct stId from score where score >all(select score from score where stId=(select stId from Student where stName= 'Kaka') ));`

##### 2.3多行子查询使用ANY操作符号
例子：查询有一门以上的成绩高于Kaka的任何一门成绩的学生的名字:

`sql> select stName
from Student
where stId in(select distinct stId from score where score >any(select score from score where stId=(select stId from Student where stName='Kaka')));`

#### 3.多列子查询
当是单行多列的子查询时，主查询语句的条件语句中引用子查询结果时可用单行比较符号（＝, >, <, >=, <=, <>）来进行比较；当是多行多列子查询时，主查询语句的条件语句中引用子查询结果时必须用多行比较符号（IN，ALL,ANY）来进行比较。

例：
`SELECT deptno,ename,job,sal
FROM EMP
WHERE (deptno,sal) IN (SELECT deptno,MAX(sal) FROM EMP GROUP BY deptno)；`

#### 4.内联视图子查询

例：
(1)
`SELECT ename,job,sal,rownum
FROM (SELECT ename,job,sal FROM EMP ORDER BY sal)；`

(2)
`SELECT ename,job,sal,rownum
FROM ( SELECT ename,job,sal FROM EMP ORDER BY sal)
WHERE rownum<=5；`

#### 5.在HAVING子句中使用子查询

例：
`SELECT deptno,job,AVG(sal) FROM EMP GROUP BY deptno,job HAVING AVG(sal)>(SELECT sal FROM EMP WHERE ename='MARTIN')；`

让我们再看看一些具体的实例，

##### 5.1给出人口多于Russia(俄国)的国家名称

`SELECT name FROM bbc
WHERE population>
(SELECT population FROM bbc
WHERE name='Russia')`

##### 5.2给出'India'(印度), 'Iran'(伊朗)所在地区的任何国家的任何信息

`SELECT * FROM bbc
WHERE region IN
(SELECT region FROM bbc
WHERE name IN ('India','Iran'))`

##### 5.3给出人均GDP超过'United Kingdom'(英国)的欧洲国家.

`SELECT name FROM bbc
WHERE region='Europe' AND gdp/population >
(SELECT gdp/population FROM bbc
WHERE name='United Kingdom')`

#### 6.查考资料：

[深入浅出SQL教程之子查询语句](http://www.west263.com/info/html/wangluobiancheng/Mysql/20080225/32087.html)

[Sql子查询](http://blog.csdn.net/rboyxxx/archive/2009/08/17/4455757.aspx)

#### 7.SQL子查询总结：

许多包含子查询的 Transact-SQL 语句都可以改用联接表示。在 Transact-SQL 中，包含子查询的语句和语义上等效的不包含子查询的语句在性能上通常没有差别。但是，在一些必须检查存在性的情况中，使用联接会产生更好的性能。否则，为确保消除重复值，必须为外部查询的每个结果都处理嵌套查询。所以在这些情况下，联接方式会产生更好的效果。
以下示例显示了返回相同结果集的Select子查询和Select联接：

`Select Name  
FROM AdventureWor ks.Production.Product  
Where ListPrice =  
     (Select ListPrice  
     FROM AdventureWor ks.Production.Product  
     Where Name = ’Chainring Bolts’ )`  
  
`Select Prd1. Name  
FROM AdventureWor ks.Production.Product AS Prd1  
     JOIN AdventureWor ks.Production.Product AS Prd2  
       ON (Prd1.ListPrice = Prd2.ListPrice)  
Where Prd2. Name = ’Chainring Bolts’`

##### 7.1嵌套在外部Select语句中的子查询包括以下组件：

●包含常规选择列表组件的常规Select查询。
●包含一个或多个表或视图名称的常规 FROM 子句。
●可选的 Where 子句。
●可选的 GROUP BY 子句。
●可选的 HAVING 子句。

子查询的Select查询总是使用圆括号括起来。它不能包含COMPUTE 或 FOR BROWSE 子句，如果同时指定了 TOP 子句，则只能包含 or DER BY 子句。

子查询可以嵌套在外部 Select，Insert，Update 或 Delete语句的 Where 或 HAVING 子句内，也可以嵌套在其他子查询内。尽管根据可用内存和查询中其他表达式的复杂程度的不同，嵌套限制也有所不同，但嵌套到 32 层是可能的。个别查询可能不支持 32 层嵌套。任何可以使用表达式的地方都可以使用子查询，只要它返回的是单个值。

如果某个表只出现在子查询中，而没有出现在外部查询中，那么该表中的列就无法包含在输出（外部查询的选择列表）中。

包含子查询的语句通常采用以下格式中的一种：

●Where expression [NOT] IN (subquery)
●Where expression comparison_operator [ANY | ALL] (subquery)
●Where [NOT] EXISTS (subquery)

在某些 Transact-SQL 语句中，子查询可以作为独立查询来计算。从概念上说，子查询结果会代入外部查询（尽管这不一定是 Microsoft SQL Server 2005 实际处理带有子查询的 Transact-SQL 语句的方式）。

有三种基本的子查询。它们是：

●在通过 IN 或由 ANY 或 ALL 修改的比较运算符引入的列表上操作。
●通过未修改的比较运算符引入且必须返回单个值。
●通过 EXISTS 引入的存在测试。

###### 1.带in的嵌套查询

select emp.empno,emp.ename,emp.job,emp.sal from scott.emp where sal in (select sal from scott.emp where ename=’’WARD’’);
上述语句完成的是查询薪水和WARD相等的员工，也可以使用not in来进行查询。

###### 2.带any的嵌套查询
通过比较运算符将一个表达式的值或列值与子查询返回的一列值中的每一个进行比较，只要有一次比较的结果为TRUE，则ANY测试返回TRUE。

select emp.empno,emp.ename,emp.job,emp.sal from scott.emp where sal >any(select sal from scott.emp where job=’’MANAGER’’);
等价于下边两步的执行过程：
（1）执行“select sal from scott.emp where job=’’MANAGER’’”
（2）查询到3个薪水值2975、2850和2450，父查询执行下列语句：
select emp.empno,emp.ename,emp.job,emp.sal from scott.emp where sal >2975 or sal>2850 or sal>2450;


###### 3.带some的嵌套查询

select emp.empno,emp.ename,emp.job,emp.sal from scott.emp where sal =some(select sal from scott.emp where job=’’MANAGER’’);
等价于下边两步的执行过程：
（1）子查询,执行“select sal from scott.emp where job=’’MANAGER’’”。
（2）父查询执行下列语句。
select emp.empno,emp.ename,emp.job,emp.sal from scott.emp where sal =2975 or   sal=2850 or sal=2450;
带【any】的嵌套查询和【some】的嵌套查询功能是一样的。早期的SQL仅仅允许使用【any】，后来的版本为了和英语的【any】相区分，引入了【some】，同时还保留了【any】关键词。

###### 4.带all的嵌套查询
通过比较运算符将一个表达式的值或列值与子查询返回的一列值中的每一个进行比较，只要有一次比较的结果为FALSE，则ALL测试返回FALSE。
select emp.empno,emp.ename,emp.job,emp.sal from scott.emp where sal >all(select sal from scott.emp where job=’’MANAGER’’);
等价于下边两步的执行过程：
（1）子查询,执行“select sal from scott.emp where job=’’MANAGER’’”。
（2）父查询执行下列语句。
select emp.empno,emp.ename,emp.job,emp.sal from scott.emp where sal >2975 and sal>2850 and sal>2450;

###### 5.带exists的嵌套查询

select emp.empno,emp.ename,emp.job,emp.sal from scott.emp,scott.dept where exists (select * from scott.emp where scott.emp.deptno=scott.dept.deptno);

###### 6.并操作的嵌套查询

并操作就是集合中并集的概念。属于集合A或集合B的元素总和就是并集。
(select deptno from scott.emp) union (select deptno from scott.dept);

###### 7.交操作的嵌套查询

交操作就是集合中交集的概念。属于集合A且属于集合B的元素总和就是交集。

(select deptno from scott.emp) intersect (select deptno from scott.dept);

###### 8.差操作的嵌套查询

差操作就是集合中差集的概念。属于集合A且不属于集合B的元素总和就是差集。
(select deptno from scott.dept) minus (select deptno from scott.emp);
注意：并、交和差操作的嵌套查询要求属性具有相同的定义，包括类型和取值范围。

左手边是一个标量表达式列表．右手边可以是一个等长的标量表达式的列表，或者一个圆括弧括起来的子查询，该查询必须返回很左手边表达式书目完全一样的字段．另外，该子查询不能返回超过一行的数量．(如果它返回零行， 那么结果就是 NULL．)左手边逐行与右手边的子查询结果行，或者右手边 表达式列表进行比较．目前，只允许使用 = 和 <> 操作符进行逐行比较．如果两行分别是相等或者不等，那么结果为真．

通常，表达式或者子查询行里的 NULL 是按照 SQL 布尔表达式的一般规则进行组合的．如果两个行对应的成员都是非空并且相等，那么认为这两行 相等；如果任意对应成员为非空且不等，那么该两行不等；否则这样的行比较的结果是未知(NULL)．


