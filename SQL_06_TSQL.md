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


<br>
<br>

________
### 02.00 EXCEPTION HANDLING
__________

exception handling comes in when a certain code *might* cause an error

it is enclosed with the keyowrds ```TRY``` and ```CATCH``` in the coding part of a T-SQL statement

this is an example of division, where the exception would come in when it gets divided by 0

```SQL
BEGIN
DECLARE 
    @value01 NUMERIC, @value02 NUMERIC, @value03 NUMERIC;
    BEGIN TRY --TRY keyword
        @value03 = @value01 / @value02;
        PRINT @value03;
    END TRY

    BEGIN CATCH --CATCHING keyword
        PRINT 'division by 0 is impossible';
    END CATCH;
END;
```


