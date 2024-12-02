# SQL REVISION SHEET 05
## STORED SQL
<br>

________
### 01.00 STORED PROCEDURES
__________

it is an SQL statment that will be saved in the database so you can reuse it later on by calling it

it is also possible to pass on parameters in a procedure

```SQL
CREATE PROCEDURE procedureName
    AS
        SQLstatment
    GO;

EXEC procedureName;
```

#### 01.01 PROCEDURES WITH PARAMETERS

one parameter 

```SQL
CREATE PROCEDURE procedureName 
    @variable01 varType
    
    AS
        SELECT column01, column02, column03
            FROM table01
            WHERE condition = @variable01
    GO;

EXEC procedureName @variable01 = value01;
```

multiple parameters

```SQL
CREATE PROCEDURE procedureName 
    @variable01 varType
    @variable02 varType

    AS
        SELECT column01, column02, column03
            FROM table01
            WHERE condition01 = @variable01 
                AND condition02 = @variable02
    GO;

EXEC procedureName @variable01 = value01, @variable02 = value02;
```



<br>
<br>

________
### 02.00 INDEXES
__________

it is a special data structure that improves the speed of data retrieval by creating pointers to records

it is an alternative with the longer full table scan

```SQL
CREATE INDEX table01_column01_IDX
    ON table01 (column01);
```

index on multiple columns
```SQL
CREATE INDEX table01_column01_column02_IDX
    ON table01 (column01, column02);
```

<br>

#### 02.01 CLUSTERED INDEX

is used when a ```PRIMARY KEY``` is defined

it is automatically created by the DB server

it regroups the primary key into nodes, which are used (often via a B-tree structure)
    for example, with an ID INT composed of XXXX, it will regroup the primary keys through the thousand, then the hundred values.

    root >   
        > 0000 - 0999
            > 0000 - 0999
            > 0100 - 0199
            > 0200 - 0299
            ...
        > 1000 - 1999
            > 1000 - 1999
            > 1100 - 1199
            > 1200 - 1299
            ...
        > 2000 - 2999
            > 2000 - 2999
            > 2100 - 2199
            > 2200 - 2299
            ...

if the table does not have a primary key, it is possible to create one throught he ```UNIQUE INDEX``` statment

```SQL
CREATE UNIQUE INDEX table01_column01_IDX
    ON table01 (column01);
```


<br>

#### 02.02 NON-CLUSTERED INDEX

is an index that contains index key values and pointers to actual data rows

the pointers are refered as ```ROWID```, a pseudocolumn

multiple non-clustered indexes can be created on a single table since they do not alter the order of the data in the table, compared to the clustered index

they are useful with columns that are frequently used in search operations but are not used to sort the table data in the table itself


<br>
<br>

________
### 03.00 VIEWS
__________

it is used like a procedure, to hide the code from the end-user and to be able to reuse the code multiple time, without having to re-write it

```SQL
CREATE VIEW view01 
    AS SELECT
    SQLstatment;
```

it is possible to have a ```CHECK``` option 
```SQL
CREATE VIEW view01 
    AS SELECT
    SQLstatment
    WITH CHECK OPTION;
```

```SQL
CREATE VIEW view01 (column01, column02, column03)
    AS SELECT
    SQLstatment
    WITH CHECK OPTION;
```


to use it, we use a ```SELECT``` statement

```SQL
SELECT * FROM viewName;
```

to modify the view, we use the ```ALTER``` statement

```SQL
ALTER VIEW view01 
    AS SELECT
    SQLstatment;
```


to remove it, we use the ```DROP``` statement

```SQL
DROP VIEW viewName;
```

#### 03.01 VIEW + INSERT

we can use a view to insert data into a table

```SQL
CREATE VIEW view01
    AS SELECT column01, column02
    FROM table01;

GO
INSERT INTO view01 VALUES (valueColumn01, valueColumn02);
```



<br>
<br>

________
### 04.00 TRANSACTIONS
__________

it is a sequence if operations that need to be fully executed or it will be aborted

when it is fully executed, it makes a transaction ```COMMIT``` which marks the end of the transaction

it there is an error, it will ```ROLLBACK``` and all the changes will be undone

transaction need to bring the DBMS from one consitent state to another, respecting all business and integrity rules

each transaction must display ```ACID```
* **A**tomicity
* **C**onsistency
* **I**solation
* **D**urability

```ATOMICITY``` : all the steps of the transaction cannot be subdivided <br>

```CONSITENCY``` : after the transaction all data must be left in a consistent state <br>

```ISOLATION``` : transactions are isolated from one another and their effects are not visible to each other until they commit or rollback <br>

```DURABILITY``` : commited changes cannot be reversed and are consistent, even through system crashes <br>
