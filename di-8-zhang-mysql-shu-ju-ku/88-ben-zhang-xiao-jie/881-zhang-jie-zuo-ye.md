### 一、表关系

请创建如下表，并创建相关约束

|                 |            |           |       |             |                 |            |          |
| --------------- | ---------- | --------- | ----- | ----------- | --------------- | ---------- | -------- |
| 班级表：class       |            |           |       | 学生表：student |                 |            |          |
| cid             | caption    | grade_id  |       | sid         | sname           | gender     | class_id |
| 1               | 一年一班       | 1         |       | 1           | 乔丹              | 女          | 1        |
| 2               | 二年一班       | 2         |       | 2           | 艾弗森             | 女          | 1        |
| 3               | 三年二班       | 3         |       | 3           | 科比              | 男          | 2        |
|                 |            |           |       |             |                 |            |          |
| 老师表：teacher     |            |           |       | 课程表：course  |                 |            |          |
| tid             | tname      |           |       | cid         | cname           | teacher_id |          |
| 1               | 张三         |           |       | 1           | 生物              | 1          |          |
| 2               | 李四         |           |       | 2           | 体育              | 1          |          |
| 3               | 王五         |           |       | 3           | 物理              | 2          |          |
|                 |            |           |       |             |                 |            |          |
| 成绩表：score       |            |           |       |             | 年级表：class_grade |            |          |
| sid             | student_id | course_id | score |             | gid             | gname      |          |
| 1               | 1          | 1         | 60    |             | 1               | 一年级        |          |
| 2               | 1          | 2         | 59    |             | 2               | 二年级        |          |
| 3               | 2          | 2         | 99    |             | 3               | 三年级        |          |
|                 |            |           |       |             |                 |            |          |
| 班级任职表：teach2cls |            |           |       |             |                 |            |          |
| tcid            | tid        | cid       |       |             |                 |            |          |
| 1               | 1          | 1         |       |             |                 |            |          |
| 2               | 1          | 2         |       |             |                 |            |          |
| 3               | 2          | 1         |       |             |                 |            |          |
| 4               | 3          | 2         |       |             |                 |            |          |

### 二、操作表

1、自行创建测试数据；

2、查询学生总人数；

3、查询“生物”课程和“物理”课程成绩都及格的学生id和姓名；

4、查询每个年级的班级数，取出班级数最多的前三个年级；

5、查询平均成绩最高和最低的学生的id和姓名以及平均成绩；

6、查询每个年级的学生人数；

7、查询每位学生的学号，姓名，选课数，平均成绩；

8、查询学生编号为“2”的学生的姓名、该学生成绩最高的课程名、成绩最低的课程名及分数；

9、查询姓“李”的老师的个数和所带班级数；

10、查询班级数小于5的年级id和年级名；

11、查询班级信息，包括班级id、班级名称、年级、年级级别(12为低年级，34为中年级，56为高年级)，示例结果如下；

| 班级id | 班级名称 | 年级   | 年级级别 |
| ---- | ---- | ---- | ---- |
| 1    | 一年一班 | 一年级  | 低    |

12、查询学过“张三”老师2门课以上的同学的学号、姓名；

13、查询教授课程超过2门的老师的id和姓名；

14、查询学过编号“1”课程和编号“2”课程的同学的学号、姓名；

15、查询没有带过高年级的老师id和姓名；

16、查询学过“张三”老师所教的所有课的同学的学号、姓名；

17、查询带过超过2个班级的老师的id和姓名；

18、查询课程编号“2”的成绩比课程编号“1”课程低的所有同学的学号、姓名；

19、查询所带班级数最多的老师id和姓名；

20、查询有课程成绩小于60分的同学的学号、姓名；

21、查询没有学全所有课的同学的学号、姓名；

22、查询至少有一门课与学号为“1”的同学所学相同的同学的学号和姓名；

23、查询至少学过学号为“1”同学所选课程中任意一门课的**其他同学**学号和姓名；

24、查询和“2”号同学学习的课程完全相同的其他同学的学号和姓名；

25、删除学习“张三”老师课的score表记录；

26、向score表中插入一些记录，这些记录要求符合以下条件：①没有上过编号“2”课程的同学学号；②插入“2”号课程的平均成绩； 

27、按平均成绩从低到高显示所有学生的“语文”、“数学”、“英语”三门的课程成绩，按如下形式显示： 学生ID,语文,数学,英语,有效课程数,有效平均分；

28、查询各科成绩最高和最低的分：以如下形式显示：课程ID，最高分，最低分；

29、按各科平均成绩从低到高和及格率的百分数从高到低顺序；

30、课程平均分从高到低显示（现实任课老师）；

31、查询各科成绩前三名的记录(不考虑成绩并列情况) 

32、查询每门课程被选修的学生数；

33、查询选修了2门以上课程的全部学生的学号和姓名；

34、查询男生、女生的人数，按倒序排列；

35、查询姓“张”的学生名单；

36、查询同名同姓学生名单，并统计同名人数；

37、查询每门课程的平均成绩，结果按平均成绩升序排列，平均成绩相同时，按课程号降序排列；

38、查询课程名称为“数学”，且分数低于60的学生姓名和分数；

39、查询课程编号为“3”且课程成绩在80分以上的学生的学号和姓名； 

40、求选修了课程的学生人数

41、查询选修“王五”老师所授课程的学生中，成绩最高和最低的学生姓名及其成绩；

42、查询各个课程及相应的选修人数；

43、查询不同课程但成绩相同的学生的学号、课程号、学生成绩；

44、查询每门课程成绩最好的前两名学生id和姓名；

45、检索至少选修两门课程的学生学号；

46、查询没有学生选修的课程的课程号和课程名；

47、查询没带过任何班级的老师id和姓名；

48、查询有两门以上课程超过80分的学生id及其平均成绩；

49、检索“3”课程分数小于60，按分数降序排列的同学学号；

50、删除编号为“2”的同学的“1”课程的成绩；

51、查询同时选修了物理课和生物课的学生id和姓名；