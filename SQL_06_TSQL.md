# SQL REVISION SHEET 06
## TRANSACT-SQL
<br>

transaction SQL always has 4 parts

DECLARE
    <variables>
BEGIN
    <actual code>
EXCEPTION
    <exception handling>
END;

________
### 01.00 LOOPS
__________

they are the control flow statments of TSQL

#### 01.01 CASE

the ```CASE``` expression creates multiple conditions and 'results' or actions to do. It is accompanied of the ```ELSE``` keyword, for when none of the conditions expressed are ```TRUE```.

the ```CASE``` statment alone 
```SQL
CASE
    WHEN condition01 THEN result01
    WHEN condition02 THEN result02
    WHEN condition03 THEN result03
    ELSE defaultResult
END;
```

with the rest of a SQL statment
```SQL
SELECT column01, column02, column03
    FROM table01
    ORDER BY (
        CASE
            WHEN column01 IS NULL THEN result01
            WHEN condition02 THEN 'result02'
            ELSE defaultResult
        END;
    )

```


#### 01.02 IF ELSE

it is the same as all the programming languages

```SQL
IF (condition01)
    SQLstatement
ELSE BEGIN
    SQLstatement
END;
```

with the rest of a SQL statment
```SQL
SELECT column01, column02, column03
    FROM table01

IF (column01 > condition01)
    PRINT 'column01 is greater than XXX'
ELSE 
    PRINT 'column01 is smaller than XXX'
END;
```

#### 01.03 WHILE

same as always, make sure to declare a counter to avoid infinite loops

```SQL
BEGIN 
DECLARE
    @counter NUMERIC = 1;

    BEGIN
        WHILE @counter < 5
            BEGIN
                PRINT @counter
                SET @counter = @counter + 1 --INCREMENTATION
            END
        PRINT 'END'
    END;
END; -- not sure if we actually need that one
```


