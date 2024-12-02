# SQL REVISION SHEET 09
## BACKUP & RECOVERY
<br>

________
### 01.00 FILES
__________

| TYPE | FILE | STORES |
|------|------|------|
| DATA FILE | ```MDF``` | all the data <br> database objects |
| TRANSACTION LOG FILE | ```LDF``` | all the modifications to the database |

<br>

#### 01.01 TRANSACTION LOG FILE

it is the record of all the changes made in the database by each transaction

it is the database equivalent of ```CTRL-C``` - ```CTRL-V``` in case of failure

the basic idea is to have : 

| ID | TIME | OPERATION | OLD VALUES | NEW VALUES | STATUS |
|----|------|-----------|------------|------------|--------|

usually it contains something like 

| ID | REVERSE POINTER | FORWARD POINTER | TIME | OPERATION | OBEJCT | OLD VALUES | NEW VALUES | STATUS |
|----|---|---|------|-----------|------------|------------|--------|---|

<br>
<br>

________
### 02.00 RECOVERY MODELS
__________

there are different kinds of recovery which all tell the database what data to keep in the transaction log file and for how long

each database can only have **one** recovery model

<br>

#### 02.01 SIMPLE RECOVERY

the most basic recovery model

the transaction data is kept until another transaction is made\

when use it :
* data is not critical
* data can be re-created
* data is static (not changing)
* losing any or all transactions since last backup is fine


<br>

#### 02.02 FULL RECOVERY

all transaction data is kept in the transaction log until 
* log backup
* log truncated

```POINT IN TIME RECOVERY``` : it is always possible to ```CTRL-Z``` from all recent points since everything is kept

when use it : 
* data is critical
* minimize data loss
* need of point in time recovery

<br>

#### 02.03 BULK-LOGGED RECOVERY

it is the same as a full recovery if there is no bulk operation

```BULK OPERATION``` : brings all the data from the application to the database server at once to then being processed
* it maximizes the performance

when use it : 
* data is critical 
* minimize data loss
* no need to log large bulk operations
* need of point in time recovery


<br>
<br>

________
### 03.00 BACKUP MODELS
__________

| NAME | DESC | FILE SIZE | RESTORATION | PREREQUISITE |
|------|------|-----------|-------------|--------------|
| FULL | the simplest type of backup <br> complete copy of the database | large | at a fixed point | none |
| DIFFERENCIAL | contains the data changed since the last FULL backup | depends | at a fixed point | FULL BACKUP |
| TRANSACTION LOG | copy in a backup file all the logs inserted in the LDF file since last FULL backup | depends | any point within the backup | FULL BACKUP |
