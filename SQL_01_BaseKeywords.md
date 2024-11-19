# SQL REVISION SHEET 01
## BASE KEYWORDS
<br>

### 01.00 SELECT
___________

keyword used to select from a table

```SQL   
SELECT column01, column02, column03 
    FROM table_01;
```
```SQL
SELECT * FROM table_01;
```

<br>

#### 01.01 SELECT + DISTINCT
when we add ```DISTINCT```, we want to see every different otpion for a certain column

```SQL
SELECT DISTINCT column01 FROM table_01;
```
<br>

#### 01.02 SELECT + DISTINCT + COUNT
the ```COUNT``` keyword counts the number of distinct possibilities

```SQL
SELECT COUNT(DISTINCT column01) 
    FROM table_01;
```

<br>

#### 01.03 SELECT INTO

the ```INTO``` keyword makes it so it copies data from the table to another

when the table is in the same DB
```SQL
SELECT column01, column02
    INTO newTable
    FROM table01;
```

when the table is in a different DB
```SQL
SELECT column01, column02
    INTO newTable IN externalDB
    FROM table01;
```

<br>

<br>

_______
### 02.00 ORDER BY
________

The ```ORDER BY``` keyword is used to sort the result by a condition
If it is not a numeric condition, it will always order the condition alaphabetically

```SQL
SELECT column01, column02
    FROM table_01
    ORDER BY column03;
```
<br>

#### 02.01 ORDER BY + ASC
Sorts by ascending values
```SQL
SELECT column01, column02
    FROM table_01
    ORDER BY column03 ASC;
```
<br>

#### 02.02 ORDER BY + DESC
Sorts by descending values
```SQL
SELECT column01, column02
    FROM table_01
    ORDER BY column03 DESC;
```

<br>
<br>

__________
### 03.00 GROUP BY
__________

the ```GROUP BY``` statment groups records that have the same groupping values into summary rows


it is often used with aggregate funcitons to help further filter and order the information

<br>

```SQL
SELECT column01, column02
    FROM table01
    WHERE condition
    GROUP BY column01;
```


<br>
<br>

__________
### 04.00 WHERE
__________

the ```WHERE``` keyword is used to filter certain records. It only shows records where a specific condition is met.
```SQL
SELECT column01, column02, column03
    FROM table_01
    WHERE column = condition;
```
```SQL
UPDATE column01
    FROM table_01
    WHERE column = condition;
```
<br>

#### 04.01 WHERE + OPERATORS

```SQL
SELECT column01, column02, column03
    FROM table_01
    WHERE column >= condition;
```

<br>
<br>

_____
### 05.00 INSERT INTO
_____
is used to insert new records to a table

```SQL
INSERT INTO table_01
    VALUES (column01_value, column02_value, column03_value);
```
```SQL
INSERT INTO table_01 (column01, column02, column03)
    VALUES (column01_value, column02_value, column03_value);
```

<br>

#### 05.01 INSERT SPECIFIC COLUMNS

you can also insert into specific columns, not as the table is made.
For example, if there is the table ```Customers``` with the records ```Name```, ```Address```, ```City```, ```PostalCode```, ```Country```
but you only want to insert a Customer with ```Name``` and ```Country```, you can specify it
The rest of the values will be assigned ```NULL``` until they are filled manually.

```SQL
INSERT INTO Customers (Name, Country)
    VALUES ('RandName', 'NewCountry');
```
<br>

#### 05.01 INSERT MULTIPLE COLUMNS

It is also possible to insert multiple columns at the same time

```SQL
INSERT INTO table_01 (column01, column02, column03)
    VALUES 
        (column01_value, column02_value, column03_value),
        (column01_value, column02_value, column03_value),
        (column01_value, column02_value, column03_value);
```
<br>
<br>

<br>

#### 05.03 INSERT INTO + SELECT

its a statments that copies data from one table and then copies it to another table

**it requires that the data types in the source and target table matches**

```SQL
INSERT INTO table02 (column01, column02, column03)
    SELECT column01, column02, column03 
        FROM table01
        WHERE condition01;
```

___________
### 06.00 UPDATE
__________

the ```UPDATE``` keyword is used to modify existing records from a table.

the ```WHERE``` condition prevents all the records from the table to be updated (without the condition, all the table is updated according to the ```UPDATE``` and ```SET``` statment)

```SQL
UPDATE table01
    SET column01 = value01, column02 = value02, column03 = value03,
    WHERE condition;
```

<br>
<br>

_________
### 07.00 DELETE
__________

the ```DELETE``` keyword deletes records from a table without deleting the table itself

```SQL
DELETE FROM table01;
```

the ```WHERE``` condition prevents all the records from the table to be delted (without the condition, all the records in the table are deleted according to the ```DELETE```statment)

```SQL
DELETE FROM table01
    WHERE condition;
```
<br>
<br>

_________
### 08.00 DROP TABLE
__________

the ```DROP TABLE``` statment deletes a table and its contents in its entirety

```SQL
DROP TABLE table01;
```

<br>
<br>

_________
### 09.00 SELECT TOP
____________

the ```SELECT TOP``` statment is used to select a specific number of records instead of selecting all of them

*** there is different syntax for each SQL Database Systems, here is only the one for MS Access and SQL Server

```SQL
SELECT TOP number_or_percentage column01
    FROM table01;
```
to select with a percentage, the ```PERCENT``` keyword needs to be used

```SQL
SELECT TOP x PERCENT column01
    FROM table01;
```
<br>

#### 09.01 SELECT TOP ... WHERE
it is also possible to add a condition to further the filtering

```SQL
SELECT TOP number_or_percentage column01
    FROM table01
    WHERE condition;
```
<br>

#### 09.02 SELECT TOP ... ORDER BY
to sort the result returned

```SQL
SELECT TOP number_or_percentage column01, column02, column03
    FROM table01
    ORDER BY column01 ASC;
```


<br>
<br>

_________
### 10.00 AS
____________

we use aliases to make the code shorter or the output more user-friendly

```SQL
SELECT column01 AS alias
    FROM table01;
```

to have more complex aliases (like when there is spaces in the alias), we can use ```[ ]``` or ```" "``` to declare the name


```SQL
SELECT column01 AS [alias]
    FROM table01;
```


```SQL
SELECT column01 AS "alias"
    FROM table01;
```

#### 10.01 AS FOR MULTIPLE COLUMNS

when we want to concat multiple columns in the same to have fewer output than input columns, we can join (or concat) the columns in the alias


```SQL
SELECT column01, column02 + ', ' + column03 + ', ' + column04 
    AS alias
    FROM table01;
```