# SQL REVISION SHEET 03
## BASE / AGGREGATE FUNCTIONS
<br>


they are mostly used with the ```SELECT``` and ```GROUP BY``` statments to help further filter them

***Aggregate functions all ignore the ```NULL``` values except for the ```COUNT()``` function

<br>

____________________
<br>

________
### 01.00 COUNT()
________________

it returns the ```number of rows``` that matches a condition

*** careful : when * is remplaced by a specific column, all ```NULL``` values will be ignored like the other aggregate fucntions 

```SQL
SELECT COUNT(*)
    FROM table01;
--it will not return the values but rather the number of records the table holds
```

<br>

#### 01.01 COUNT() ... WHERE

the ```WHERE``` condition can be added to filter the records returned
```SQL
SELECT COUNT(column01)
    FROM table01
    WHERE condition;
```
<br>

#### 01.02 COUNT() ... DISTINCT

to ignore the duplicates in a table, we can use the ```DISTINC``` keyword
```SQL
SELECT COUNT(DISTINCT column01)
    FROM table01;
```

<br>

#### 01.03 COUNT() ... AS

to use an alias for the returned column name, we use the ```AS``` keyword
```SQL
SELECT COUNT(*) AS aliasName
    FROM table01;
```

<br>

#### 01.04 COUNT() ... GROUP BY

it returns the number of records in each category of the specified condition

```SQL
SELECT COUNT(*)
    FROM table01
    GROUP BY category;
```


<br>
<br>

________
### 02.00 MIN()
__________

it returns the smallest value from the table of the selected column

```SQL
SELECT MIN(column01)
    FROM table01;
```

<br>
<br>

________
### 03.00 MAX()
_________

it returns the biggest value from the table of the selected column

```SQL
SELECT MAX(column01) 
    FROM table01;
```

<br>
<br>

________
### 04.00 SUM()
___________

it returns the total sum of a ```NUMERIC``` column

```SQL
SELECT SUM(numeric_column)
    FROM table01;
```

we can also add some maths to it to change the output result

```SQL
SELECT SUM(numeric_column * x)
    FROM table01;
```

<br>

#### 04.01 SUM() ... WHERE

to filter the result, we can add the ```WHERE``` condition
```SQL
SELECT SUM(numeric_column)
    FROM table01
    WHERE condition;
```

<br>

#### 04.02 SUM() ... AS

to use an alias for the returned column name, we use the ```AS``` keyword
```SQL
SELECT SUM(numeric_column) AS [complex aliaName]
    FROM table01;
```

<br>

#### 04.03 SUM() ... GROUP BY

the ```GROUP BY``` statment helps categorize the returned sums

```SQL
SELECT SUM(numeric_column)
    FROM table01
    GROUP BY condition;
```

<br>
<br>

________
### 05.00 AVG()
__________

it returns the average of a ```NUMERIC``` column

```SQL
SELECT AVG(column01)
    FROM table01
    WHERE condition;
```

<br>

#### 05.01 AVG() ... AS

to use an alias for the returned column name, we use the ```AS``` keyword
```SQL
SELECT AVG(numeric_column) AS "complex aliaName"
    FROM table01;
```

<br>

#### 05.02 AVG() ... GROUP BY

the ```GROUP BY``` statment helps categorize the returned averages

```SQL
SELECT AVG(numeric_column)
    FROM table01
    GROUP BY condition;
```

#### 05.03 AVG() IN SUB QUERY
we can use the average of a numeric column as a "variable" to set a condition in a sub query

```SQL
SELECT * FROM table01
    WHERE column01 > (
        SELECT AVG(column01) 
        FROM table01
    );

-- it will return every record where the value of column01 is smaller than the average of itself
```

<br>
<br>

________
### 05.00 ISNULL() 
__________

in other SQL servers, there is other functions that will achieve similar or the same results, like ```IFNULL()```, ```COALESCENCE()```, ```NVL()```

in MS Access, the function ```ISNULL()``` will return ```TRUE``` or ```-1``` is the expression is a ```NULL``` value, or ```FALSE``` or ```0``` if it is not

```SQL
SELECT column01 * (column02 + IF(ISNULL(column03), 
                                        0, 
                                        column03))
    FROM table01;
```






