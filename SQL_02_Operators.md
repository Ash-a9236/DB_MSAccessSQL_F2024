# SQL REVISION SHEET 02

## OPERATORS

<br>

____________________

|OPERATOR | MEANING||OPERATOR | MEANING|
---------- |---------|---------|-------|-------|
||
| **ARITHMETIC** ||| **BITWISE** | |
|+| Add |           |&| AND|
|-| Substract|      |&#124;| OR |
|*| Multiply |      |^| exclusive OR |
|/| Divide |
|%| Modulo |
||
| **COMPARISON** | || **COMPOUND** | |
| = | Equal|        |+=| Add equals |
|< | Greater|       |-=| Substract equals |
|>| Less|           |*=| Multiply equals |
|>=|Greater or equal||/=| Divide equals |
|<=|Less or equal|  |%=| Modulo equals |
|<> OR !=| Not equal||&=| AND equals |
|   |             | |^-=| EXCLUSIVE equals |
|   |             | |&#124;*=| OR equals |
||
| **LOGICAL** | || **LOGICAL** | |
|```BETWEEN```| Between range||```ANY```| returns ```TRUE``` if any value meets the condition| 
|```LIKE```| Search for a pattern||```ALL```| returns ```TRUE``` if all value meets the condition(s)|
|```IN```| To specify multiple possible values for a column||```AND```| returns ```TRUE``` if all conditions separated by ```AND``` are true|
|```UNION```| Combine the result of two or more ```SELECT```||```NOT```| Displays a record if the conditions are ```NOT TRUE``` |
|```EXISTS``` | To check if a records exists or not ||```OR```| returns ```TRUE``` if any condition separated by ```OR``` is true|
|```SOME```| returns ```TRUE``` if any subquery meets the condition |

<br>
<br>

____________
### 01.00 DATE
_____________

MS Access support multiple ```DATE``` formats

```SQL
DATE() --Returns the current date

'yyyy-mm-dd'

#yyyy-mm-dd# OR #yyyy/mm/dd#

```


<br>
<br>

____________
### 02.00 AND
_____________

The ```AND``` operator allows to add more conditions to statements
It will only return the records where all conditions are ```TRUE```

```SQL
SELECT *
    FROM table_01
    WHERE condition01 AND condition02 
```
<br>
<br>

____________
### 03.00 OR
___________

The ```OR``` operator allows to add more conditions to statments. The difference with the ```AND``` operator is that not both conditions must be true for the records to be returned.


```SQL
SELECT *
    FROM table_01
    WHERE condition01 OR condition02 
```
<br>

#### 03.01 COMBINATION OF AND & OR

```SQL
SELECT *
    FROM table_01
    WHERE condition01 
    AND (condition02 OR condition03);
```
<br>
<br>

____________
### 04.00 NOT
____________

It gives the 'negative' or 'opposite' result

```SQL
SELECT *
    FROM table_01
    WHERE NOT condition01;
```
you can add other operators to ```NOT```

```SQL
SELECT *
    FROM table_01
    WHERE NOT condition01 LIKE xxx;
```
```SQL
SELECT *
    FROM table_01
    WHERE NOT condition01 BETWEEN xxx AND yyy;
```
```SQL
SELECT *
    FROM table_01
    WHERE NOT condition01 > xxx;
```

<br>
<br>

____________
### 05.00 LIKE
____________

the ```LIKE``` operator is used in a ```WHERE``` condition to search for a specific pattern

it is often associated with different wildcards to specify the pattern type


|WILDCARD | MEANING|
---------- |---------|
| % | zero or more characters |
| _ | single character |
| [ ] | single character within the brackets |
| - | single character within a specified range <br> it helps to specify the range with the ```[]``` wildcard |
| |
| **MS ACCESS ONLY** ||
| |
| * | zero or more characters |
| ? | single character like ```_``` |
| ! | any character NOT in the ```[]``` |
| # | single numeric character |

<br>

```SQL
SELECT * FROM table01
    WHERE condition LIKE 'pattern';
```

<br>

#### 05.01 LIKE '. . .  % . . .'

the wildcard ```%``` represents any number of character before or after.

```SQL
SELECT * FROM table01
    WHERE condition LIKE '%pattern';

-- it will return all the patterns with anything before 'pattern' itself
```

```SQL
SELECT * FROM table01
    WHERE condition LIKE 'pattern%';

-- it will return all the patterns with anything that starts with 'pattern'
```

```SQL
SELECT * FROM table01
    WHERE condition LIKE '%pattern%';

-- it will return all the patterns with anything that includes 'pattern'
```

```SQL
SELECT * FROM table01
    WHERE condition LIKE 'a%' AND condition LIKE '%b';

-- it will return all the patterns with anything that starts with 'a' AND 'b'
```


<br>

#### 05.02 LIKE '. . .  _'

the wildcard ```_``` represents a single character

```SQL
SELECT * FROM table01
    WHERE condition LIKE '_attern';

-- it will return all the patterns that starts with any character then followed by 'attern'
```
```SQL
SELECT * FROM table01
    WHERE condition LIKE 'pa__ern';

-- it will return all the patterns that starts with 'pa' followed by any 2 character, then ending with 'ern'
```

```SQL
SELECT * FROM table01
    WHERE condition LIKE 'pa__%';

-- it will return all the patterns that starts with 'pa' followed by any 2 character, and any ending
```

<br>

#### 05.03 LIKE '. . .  [ ]'

the ```[ ]``` wildcard returns the results if any of the characters inside it have a match

```SQL
SELECT * FROM table01
    WHERE condition LIKE '[pat]%';

-- it will return all the patterns that starts with either 'p', 'a', or 't'
```

<br>

#### 05.04 LIKE '. . .  -'

the ```-``` wildcard specifies a range in a condition

```SQL
SELECT * FROM table01
    WHERE condition LIKE '[a-d]%';

-- it will return all the patterns that starts with either 'a', 'b', 'c', or 'd'
```

<br>
<br>

_______

### 06.00 IN
_______

it is a shortcut for multiple ```OR``` conditions

it helps to specify multiple values, especially with the ```WHERE``` condition

```SQL
SELECT * FROM table01
    WHERE condition IN ('example01', 'example02', 'example03');

```

<br>
<br>

_______
### 07.00 NOT IN
________

it returns all the records where the specified condition is not true

```SQL
SELECT * FROM table01
    WHERE condition NOT IN ('example01', 'example02', 'example03');

```
<br>
<br>

_______

### 08.00 IN + SUB QUERY
_________

<br>

```SQL
SELECT * FROM table01
    WHERE column01 IN (
        SELECT column01 FROM table02)
```


<br>
<br>

_______
### 09.00 NULL
_______

the ```NULL``` keyword is a placeholder when there is no value inserted for a certain field

We cannot test for ```NULL``` values with normal operators such as ```=```, ```<```, ```>```, etc. Instead, we use ```IS NULL```, or ```IS NOT NULL```.

<br>

#### 09.01 IS NULL
```SQL   
SELECT column01, column02, column03 
    FROM table_01
    WHERE column01 IS NULL;
```
<br>

#### 09.02 IS NOT NULL
```SQL   
SELECT column01, column02, column03 
    FROM table_01
    WHERE column01 IS NOT NULL;
```

<br>
<br>

_______
### 10.00 BETWEEN
_______

the ```BETWEEN``` operator selects inclusively values (number, text, or date) within a range

```SQL
SELECT * FROM table01
    WHERE column01 BETWEEN value01 AND value02;
```

<br>

#### 10.01 BETWEEN ...IN

it helps further specify the condition to filter the result better

```SQL
SELECT * FROM table01
    WHERE column01 BETWEEN value01 AND value02
    AND column02 IN (value03, value04, value05);
```

<br>

#### 10.02 BETWEEN ...DATE

SQL recognizes dates and therefore we can have a ```BETWEEN DATE AND DATE``` statment

```SQL
SELECT * FROM table01
    WHERE column01 
    BETWEEN #2024/02/01# AND #2024/05/01#;
```


<br>
<br>

_______
### 11.00 UNION
_______

the ```UNION``` operator is used to combine the result-set of two or more ```SELECT``` statments

**CONDITIONS**<br><br>
- Every ```SELECT``` statment within ```UNION``` needs to have the  same number of columns
- Similar column data types
- The columns in all the ```SELECT``` statments must be in the same order

<br>

```SQL
SELECT column01, column02, column03 FROM table01
UNION
SELECT column04, column05, column06 FROM table02
```
<br>

the difference between ```UNION``` and ```UNION ALL``` is that the first doesn't allow duplicate values

```SQL
SELECT column01, column02, column03 FROM table01
UNION
SELECT column04, column05, column06 FROM table02;
```

#### 11.01 UNION ...WHERE

```SQL
SELECT column01, column02, column03 
    FROM table01
    WHERE condition
UNION
SELECT column04, column05, column06 
    FROM table02
    WHERE condition;
```

<br>
<br>

_________
### 12.00 EXISTS
____________

the ```EXISTS``` operator tests if any records matching a condition already exists in the database
it will return ```TRUE``` if there is one or multiple matches

```SQL
SELECT column01, column02
    FROM table01
    WHERE EXISTS (
        SELECT column01, column02
        FROM table01 
        WHERE condition
    );
```


<br>
<br>

_________
### 13.00 ANY
____________

the ```ANY``` operator returns ```TRUE``` if ```ANY``` of the subquery meets the defined condition

returns a ```BOOLEAN``` value

```SQL
SELECT column01, column02
    FROM table01
    WHERE column01 > ANY -- the operator needs to be a comparison operator such as <, >, <>, !=, =, etc.
        (SELECT column03
            FROM table01
            WHERE condition);
```




