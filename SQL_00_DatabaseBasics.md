# SQL REVISION SHEET 00
## DATABASE BASICS
<br>

________
### 01.00 DATABASE
__________

#### 01.01 CREATE

```SQL
CREATE DATABASE database01;
```

#### 01.02 SHOW

```SQL
SHOW DATABASES;
```

#### 01.03 BACKUP

```SQL
BACKUP DATABASE database01
    TO DISK = 'filepath'; --ex. 'C:\Documents\database01.bak'
```
<br>

backup only the new changes 
```SQL
BACKUP DATABASE database01
    TO DISK = 'filepath'
    WITH DIFFERENTIAL;
```


#### 01.04 DROP

**there is no CTRL-Z in databses, DO NOT USE ```DROP``` without being VERY SURE of the consequences**

```SQL
DROP DATABASE database01;
```

<br>
<br>

________
### 02.00 TABLE
__________

#### 02.01 CREATE

```SQL
CREATE TABLE table01 (
    column01 dataType,
    column02 dataType,
    column03 dataType
);
```
from another, existing table (it is also possible to use it with conditions)

```SQL
CREATE TABLE table02 
    AS SELECT column01, column02, column03 
        FROM table01;
```

#### 02.02 ALTER

it is used to add, delete or modify columns and constraints in an existing table

<br>

ADD COLUMN
```SQL
ALTER TABLE table01
    ADD column04 dataType;
```

DROP COLUMN
```SQL
ALTER TABLE table01
    DROP COLUMN column04;
```

RENAME COLUMN
```SQL
ALTER TABLE table01
    RENAME COLUMN column04 TO column05;
```

MODIFY COLUMN DATABASE

this syntax changes depending on the SQL server used

```SQL
ALTER TABLE table01
    ALTER COLUMN column04 newDataType;
```


#### 02.03 DROP

**there is no CTRL-Z in databses, DO NOT USE ```DROP``` without being VERY SURE of the consequences**

```SQL
DROP TABLE table01;
```

#### 02.04 TRUNCATE

is the same as ```DROP``` except it only deletes the data, not the table itself

```SQL
TRUNCATE TABLE table01;
```


<br>
<br>

________
### 03.00 CONSTRAINTS
__________

they are the rules for the tables in the database

all of them can be defined at the column level except for composite PK

the general convention for naming constraints is ```table_column_constraint```

<br>

ADD CONSTRAINT
```SQL
ALTER TABLE table01
    ADD CONSTRAINT constraint01;
```

DROP CONSTRAINT
```SQL
ALTER TABLE table01
    DROP CONSTRAINT constraint01;
```

<br>


|CONSTRAINT| ABREVIATION | |
--------|-------|--------|
|```NOT NULL```| ```NN``` | no ```NULL``` values accepted in the column|
|```UNIQUE```| ```UK``` | every value in a column needs to be different|
|```CHECK```| ```CC``` | all values in a column meets a condition |
|```DEFAULT```| | sets a default value for a column if no other value is set|
|```PRIMARY KEY```| ```PK``` | ```NOT NULL``` + ```UNIQUE```|
|```FOREIGN KEY```| ```FK``` | used to link two tables, prevents actions that would destroy links between tables|
|```CREATE INDEX```|```INDX```| used to create and retrieve data from a DB quickly|

<br>

#### 03.01 NOT NULL

the column cannot accept ```NULL``` values

```SQL
CREATE TABLE table01 (
    column01 dataType 
        CONSTRAINT table01_column01_NN NOT NULL,
    column02 dataType,
    column03 dataType,

    CONSTRAINT table01_column02_NN 
        NOT NULL (column02)
);
```
```SQL
ALTER TABLE table01
    ALTER COLUMN column01 
        CONSTRAINT table01_column01_NN NOT NULL;
```

<br>

#### 03.02 UNIQUE

the column cannot accept two values that are the same

```SQL
CREATE TABLE table01 (
    column01 dataType,
    column02 dataType
            CONSTRAINT table01_column02_UK UNIQUE,
    column03 dataType,

    CONSTRAINT table01_column01_UK
        UNIQUE (column01);
);
```

```SQL
ALTER TABLE table01
    ALTER COLUMN column01 
        CONSTRAINT table01_column01_UK UNIQUE;
```
<br>

#### 03.03 CHECK

it defines a condition that every record MUST meet


```SQL
CREATE TABLE table01 (
    column01 dataType
            CONSTRAINT table01_column01_CC
                CHECK (column01 condition01),
    column02 dataType,
    column03 dataType,

    CONSTRAINT table01_column02_CC
        CHECK (column02 condition02 AND column02 condition03);
);
```

```SQL
ALTER TABLE table01
    ALTER COLUMN column01 
        CONSTRAINT table01_column01_CC CHECK (column01 condition01);
```

<br>

#### 03.04 DEFAULT

it defines a default value when no other value is specified when entering the data

```SQL
CREATE TABLE table01 (
    column01 dataType,
    column02 dataType 
        CONSTRAINT table01_column02_DF DEFAULT defaultValue,
    column03 dataType,
);
```

```SQL
ALTER TABLE table01
    ALTER COLUMN column01 
        CONSTRAINT table01_column01_DF SET DEFAULT defaultValue;
```

<br>

#### 03.05 PRIMARY KEY

it is the unique ID of a record in a table
it cannot be ```NULL``` and has to be ```UNIQUE```

```SQL
CREATE TABLE table01 (
    column01 dataType
            CONSTRAINT table01_column01_PK PRIMARY KEY,
    column02 dataType,
    column03 dataType,

    --OR : CONSTRAINT table01_column01_PK PRIMARY KEY (column01);
);
```

a composite primary key
```SQL
CREATE TABLE table01 (
    column01 dataType,
    column02 dataType,
    column03 dataType,

    CONSTRAINT table01_column01_column02_PK 
        PRIMARY KEY (column01, column02);
);
```

```SQL
ALTER TABLE table01
    ALTER COLUMN column01 
        CONSTRAINT table01_column01_PK PRIMARY KEY;
```

<br>

#### 03.06 FOREIGN KEY

a foreign key is a field that references the same field which is a primary key in another table.

```SQL
CREATE TABLE table01 (
    column01 dataType,
    column02 dataType
        CONSTRAINT table01_column02_FK 
            FOREIGN KEY REFERENCES table02 (column01),
    column03 dataType,

    --OR : CONSTRAINT table01_column02_FK 
    --          FOREIGN KEY (column02) REFERENCES table02 (column01);
);
```

```SQL
ALTER TABLE table01
    ADD CONSTRAINT table01_column02_FK
    FOREIGN KEY (column02) 
    REFERENCES table02 (column01);
```

<br>

#### 03.07 INDEX

see revision sheet #05 > section 03

<br>
<br>

________
### 04.00 REFERENTIAL INTEGRITY
__________

when we update or delete records in a table, all records that reference the updated / deleted record must also change

to change them, there is three methods, two with the ```CASCADE``` keyword

#### 04.01 ON DELETE CASCADE

it will delete all the records which references the parent record

```SQL
CREATE TABLE table01 (
    column01 dataType,
    column02 dataType,
    column03 dataType,

    CONSTRAINT table01_column02_FK 
        FOREIGN KEY (column02) REFERENCES table02 (column01) 
        ON DELETE CASCADE,
);
```

#### 04.02 ON DELETE SET NULL

it will set to ```NULL``` all the records which references the parent record

```SQL
CREATE TABLE table01 (
    column01 dataType,
    column02 dataType,
    column03 dataType,

    CONSTRAINT table01_column02_FK 
        FOREIGN KEY (column02) REFERENCES table02 (column01) 
        ON DELETE SET NULL,
);
```


#### 04.02 ON UPDATE CASCADE

it will update with the new value(s) all the records which reference the parent record

```SQL
CREATE TABLE table01 (
    column01 dataType,
    column02 dataType,
    column03 dataType,

    CONSTRAINT table01_column02_FK 
        FOREIGN KEY (column02) REFERENCES table02 (column01) 
        ON UPDATE CASCADE,
);
```


