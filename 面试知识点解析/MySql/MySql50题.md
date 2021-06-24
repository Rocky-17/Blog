# 建表  

表结构如下：  
course 

| 列名称 | 字段类型 | 是否为空 | 键 | 默认值 | 备注 |
| ----- | -------- | ------- | -- | ----- | ---- |
| c_id | varchar(20) | NO | PRI | None |  |
| c_name | varchar(20) | NO |  |  |  |
| t_id | varchar(20) | NO |  | None |  |

score 

| 列名称 | 字段类型 | 是否为空 | 键 | 默认值 | 备注 |
| ----- | -------- | ------- | -- | ----- | ---- |
| s_id | varchar(20) | NO | PRI | None |  |
| c_id | varchar(20) | NO | PRI | None |  |
| s_score | int(3) | YES |  | None |  |

student 

| 列名称 | 字段类型 | 是否为空 | 键 | 默认值 | 备注 |
| ----- | -------- | ------- | -- | ----- | ---- |
| s_id | varchar(20) | NO | PRI | None |  |
| s_name | varchar(20) | NO |  |  |  |
| s_birth | varchar(20) | NO |  |  |  |
| s_sex | varchar(10) | NO |  |  |  |

teacher 

| 列名称 | 字段类型 | 是否为空 | 键 | 默认值 | 备注 |
| ----- | -------- | ------- | -- | ----- | ---- |
| t_id | varchar(20) | NO | PRI | None |  |
| t_name | varchar(20) | NO |  |  |  |
  


```
-- 学生表
-- Student（s_id，s_name，s_birth，s_sex）
-- 学生编号,学生姓名, 出生年月,学生性别
CREATE TABLE `Student`(
`s_id` VARCHAR(20),
`s_name` VARCHAR(20) NOT NULL DEFAULT '',
`s_birth` VARCHAR(20) NOT NULL DEFAULT '',
`s_sex` VARCHAR(10) NOT NULL DEFAULT '',
PRIMARY KEY(`s_id`)
);

-- 课程表
-- Course(c_id,c_name,t_id) 
-- 课程编号, 课程名称, 教师编号
CREATE TABLE `Course`(
`c_id` VARCHAR(20),
`c_name` VARCHAR(20) NOT NULL DEFAULT '',
`t_id` VARCHAR(20) NOT NULL,
PRIMARY KEY(`c_id`)
);

-- 教师表
-- Teacher(t_id,t_name)
-- 教师编号,教师姓名
CREATE TABLE `Teacher`(
`t_id` VARCHAR(20),
`t_name` VARCHAR(20) NOT NULL DEFAULT '',
PRIMARY KEY(`t_id`)
);

-- 成绩表
-- Score(s_id,c_id,s_s_score) 
-- 学生编号,课程编号,分数
CREATE TABLE `Score`(
`s_id` VARCHAR(20),
`c_id` VARCHAR(20),
`s_score` INT(3),
PRIMARY KEY(`s_id`,`c_id`)
)
```

# 插入数据  
```
-- 学生表数据
insert into Student values('01' , '赵雷' , '1990-01-01' , '男');
insert into Student values('02' , '钱电' , '1990-12-21' , '男');
insert into Student values('03' , '孙风' , '1990-05-20' , '男');
insert into Student values('04' , '李云' , '1990-08-06' , '男');
insert into Student values('05' , '周梅' , '1991-12-01' , '女');
insert into Student values('06' , '吴兰' , '1992-03-01' , '女');
insert into Student values('07' , '郑竹' , '1989-07-01' , '女');
insert into Student values('08' , '王菊' , '1990-01-20' , '女');

-- 课程表数据
insert into Course values('01' , '语文' , '02');
insert into Course values('02' , '数学' , '01');
insert into Course values('03' , '英语' , '03');

-- 教师表数据
insert into Teacher values('01' , '张三');
insert into Teacher values('02' , '李四');
insert into Teacher values('03' , '王五');

-- 成绩表数据
insert into Score values('01' , '01' , 80);
insert into Score values('01' , '02' , 90);
insert into Score values('01' , '03' , 99);
insert into Score values('02' , '01' , 70);
insert into Score values('02' , '02' , 60);
insert into Score values('02' , '03' , 80);
insert into Score values('03' , '01' , 80);
insert into Score values('03' , '02' , 80);
insert into Score values('03' , '03' , 80);
insert into Score values('04' , '01' , 50);
insert into Score values('04' , '02' , 30);
insert into Score values('04' , '03' , 20);
insert into Score values('05' , '01' , 76);
insert into Score values('05' , '02' , 87);
insert into Score values('06' , '01' , 31);
insert into Score values('06' , '03' , 34);
insert into Score values('07' , '02' , 89);
insert into Score values('07' , '03' , 98);
```

# 题目  

1.查询课程编号为‘01’的课程比‘02’的课程成绩高的所有学生的学号、姓名和各自‘01’‘02’课程成绩  
```
SELECT student.s_id ,student.s_name,res1.s_score,res2.s_score FROM 
(SELECT s_id,s_score FROM score WHERE c_id='01') AS res1
INNER JOIN
(SELECT s_id,s_score FROM score WHERE c_id='02') AS res2 ON res1.s_id = res2.s_id
INNER JOIN
student ON res1.s_id = student.s_id
WHERE res1.s_score > res2.s_score
```
| s_id | s_name | 01 | 02 |
|------|--------|----|----|
| 02   | 钱电     | 70 | 60 |
| 04   | 李云     | 50 | 30 |
  
2.查询平均成绩大于60分的学生的学号、姓名和平均成绩
```
SELECT student.s_id,student.s_name,avg_score
FROM student,
(SELECT score.s_id,round(avg(score.s_score)) as avg_score 
FROM score
GROUP BY score.s_id
HAVING avg(score.s_score) > 60) as res
WHERE student.s_id = res.s_id
```
| s_id | s_name | avg_score |
|------|--------|-----------|
| 01   | 赵雷     | 90        |
| 02   | 钱电     | 70        |
| 03   | 孙风     | 80        |
| 05   | 周梅     | 82        |
| 07   | 郑竹     | 94        |

3.查询所有学生的学号、姓名、选课数、总成绩  
```
SELECT student.s_id,student.s_name,COUNT(score.c_id) as count_course,SUM(IFNULL(score.s_score,0)) as sum_score
FROM student
LEFT JOIN score
ON student.s_id=score.s_id
GROUP BY s_id
```
| s_id | s_name | conut_course | sum_score |
|------|--------|-------------------|--------------------------------|
| 01   | 赵雷     | 3                 | 269                            |
| 02   | 钱电     | 3                 | 210                            |
| 03   | 孙风     | 3                 | 240                            |
| 04   | 李云     | 3                 | 100                            |
| 05   | 周梅     | 2                 | 163                            |
| 06   | 吴兰     | 2                 | 65                             |
| 07   | 郑竹     | 2                 | 187                            |
| 08   | 王菊     | 0                 | 0                              |
