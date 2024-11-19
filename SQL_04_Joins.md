# SQL REVISION SHEET 03
## JOINS
<br>

_________
### 01.00 INNER JOIN
_____________

all the matching values in both tables

```SQL
SELECT table01.column01, table02.column02
    FROM table01
    INNER JOIN table02 
    ON table01.column02 = table02.column02;
```

<br>

#### 01.01 INNER JOIN ... ON 3 TABLES

```SQL
SELECT table01.column01, table02.column02, table03.column03
    FROM ((table01
    INNER JOIN table02 ON table01.column02 = table02.column02)
    INNER JOIN table03 ON table01.column03 = table03.column03);
```



<br>
<br>

___________
### 02.00 LEFT JOIN
__________

all the records from the left table and the matching records from the right

```SQL
SELECT lt.column01, rt.column02
    FROM left_table AS lt, 
    LEFT JOIN right_table AS rt
    ON lt.column02 = rt.column02;
```

<br>
<br>

___________
### 03.00 RIGHT JOIN
__________

all the records from the right table and the matching records from the left

```SQL
SELECT lt.column01, rt.column02
    FROM left_table AS lt, 
    RIGHT JOIN right_table AS rt
    ON lt.column02 = rt.column02;
```

<br>
<br>

___________
### 04.00 FULL OUTER JOIN
__________

all the records that have a match from the left and right table

```SQL
SELECT table01.column01, table02.column02
    FROM table01
    FULL OUTER JOIN table02
    ON table01.column02 = table02.column02;
--A WHERE clause should be added to filter the results as the output of such join can be very long
```

<br>
<br>

___________
### 05.00 SELF JOIN
__________

```SQL
SELECT T1.column01 AS c1, T2.column01 AS c2
    FROM table01 T1, table01 T2;
--A WHERE condition should be added to further filter the resutls
```


