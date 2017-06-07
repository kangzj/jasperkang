---
title: 将Excel中的数据导出成SQL(即可导入MySQL等数据库了)
tags:
  - excel
  - mysql
id: 60
categories:
  - Others
date: 2009-03-18 07:14:17
---

=CONCATENATE("INSERT OR REPLACE into students (school,name,stuno,gender,grade,mobile)values(","'",A771,"'",",","'",A771,"'",",","'",A771,"'",",","'",A771,"'",",","'",A771,"'",",","'",A771,"'",");")

把上面的语句在单元格中输入，然后，将A771换成相应的单元格的编号即可，然后拖动就行了！