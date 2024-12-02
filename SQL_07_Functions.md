# SQL REVISION SHEET 07
## FUNCTIONS
<br>

________
### 01.00 SYSTEM DEFINED
__________

SQL server has already some ```system defined functions``` that are provided with the database to make some common tasks easier

examples of system defined functions are ```LEN()```, ```UPPER()```, ```LOWER()```, ```ROUND()```, ```GETDATE()```

<br>
<br>

________
### 02.00 USER - SCALAR
__________

```SCALAR``` functions are user-defined / created functions that will return a single column value

it always returns a value, and is generally used within a ```QUERY```

```SQL
CREATE FUNCTION function01 (@parameter01 dataType, @parameter02 dataType)
RETURNS dataType
AS
BEGIN
    SQLstatements

    RETURN outputValue
END;
```

to call a scalar function, you need to add in front of it the database schema it is associated with
in MS Access, the default one is ```dbo.```

```SQL
SELECT dbo.function01(value01);
```

```SQL
SELECT column01,
    dbo.function01(column01)
    AS name01
    FROM table01
    WHERE condition02;
```

<br>
<br>

________
### 03.00 USER - TABLE
__________

they are the same as ```SCALAR FUNCTIIONS``` but instead of returning a value, they return a table

```SQL
CREATE FUNCTION function01 (@parameter01 dataType)
RETURNS TABLE01 --doensn't return a dataType
AS
BEGIN
    RETURN 
        SELECT column01, column02, column03
            FROM table01
            WHERE column02 < @parameter01 
END;
```

<br>
<br>

________
### 04.00 CURSOR
__________

```SQL
DECLARE cursor01 CURSOR FOR
    SELECT statement01;

OPEN cursor01;
```
to stop using the cursor without deleting it  

```SQL
CLOSE cursor01;
```

to completly delete the cursor
```SQL
DEALLOCATE cursor01;
```

<br>
<br>

________
### 05.00 TRIGGER
__________

they are created and will automatically be fired by the system when a certain event 'triggers' them

the triggering event can be set with different keywords, such as ```FOR```, ```AFTER```, ```INSTEAD OF```

```FOR``` AND ```AFTER``` are triggers that fire **AFTER** the action

```INSTEAD OF``` are triggers that fire instead of an actual SQL statement

to delete a trigger, we can use the ```DROP``` statement

```SQL
DROP TRIGGER triggerName;
```

we can also disable triggers with the ```DISABLE``` keyword, and then renable them with the ```ENABLE``` keyword

```SQL
DISABLE TRIGGER triggerName
    ON table01;
```
```SQL
ENABLE TRIGGER triggerName
    ON table01;
```

```SQL
DROP TRIGGER triggerName;
```

#### 05.01 FOR

```SQL
CREATE TRIGGER trigger01
ON table01
FOR event01, event02 --AFTER, INSTEAD OF

DECLARE
    variables
AS
BEGIN
    SQLstatements

    EXCEPTION
        try_catchStatements
END;
```

#### 05.02 AFTER

```SQL
CREATE TRIGGER trigger01
ON table01
AFTER event01, event02 --FOR, INSTEAD OF

DECLARE
    variables
AS
BEGIN
    SQLstatements

    EXCEPTION
        try_catchStatements
END;
```

#### 05.03 INSTEAD OF

```SQL
CREATE TRIGGER trigger01
ON table01
INSTEAD OF event01, event02 --FOR, AFTER

DECLARE
    variables
AS
BEGIN
    SQLstatements

    EXCEPTION
        try_catchStatements
END;
```

#### 05.04 INSERTED AND DELETED

MS Access, when firing triggers, created two, temporary tables, called ```INSERTED``` and ```DELETED``` tables

they are accessible when you insert, delete, or update in a trigger

|ACTION|TABLE|EX OF USE|
-------|-------|--------|
|```AFTER INSERT```| INSERTED| update related tables <br> calculations based on new data inserted |
|```AFTER DELETE```| DELETED| logging the deletion <br> updating realted tables |
|```AFTER UPDATE```| INSERTED & DELETED| compare old and new values of records |

to call them in code, you can call them like a normal table, their name being ```INSERTED``` and ```DELETED```

