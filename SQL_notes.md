# SQL
## Creating tables
### Key commands
- create table table name (column name, column name)
- add column: alter table table name add column name
- update table:
-- UPDATE table_name
   SET column1 = value1, column2 = value2,
   WHERE condition;
-  delete rows: delete from table name where condition        --  -what you want deleted-
-   PK & FK: manual = designer -> relationships but code below
    CREATE TABLE orders
    ```
    (OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID));
    ```
- insert data: insert into table name (column name,       column name) values (value1, value2)

## Selecting data from tables

#### Gross total and net total
- select unitprice, quantity, discount,
  unitprice * Quantity as 'Gross Total',
  unitprice * quantity * (1- discount) as 'Net Total'
  from [Order Details]

#### CHARINDEX
- SELECT column name as "alias" from table_name where CHARINDEX('what you are looking for', "columnname")
- example looking for single aposrophes:
  SELECT productname as "single quote" from products where CHARINDEX('''', "ProductName") > 0
#### Datediff
- datediff(measurement,dob,GETDATE()) as alias from table
- example datediff(year,BirthDate,GETDATE()) as BirthDate from employees
#### Making new column
- CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END as 'new column name'
- example:
CASE
    WHEN (datediff(year,BirthDate,GETDATE())) >65 THEN 'Retired'
    WHEN (datediff(year,BirthDate,GETDATE())) >60 THEN 'Retirement Plan'
    ELSE 'More than 5 years to go'
END as 'Retirement Plan'
from table;

#Big sums
- select
sum(column) as 'Total on Order',
avg(column) as 'AVG on Order',
max(column) as 'Max on Order',
min(column) as 'min on Order'
from table
- example
select CategoryID , avg(ReorderLevel) as 'AVG order'
from products
group by categoryID
order by 'AVG order' desc

- select column 2,
sum(column1) as 'Total on Order',
avg(column1) as 'AVG on Order',
max(column1) as 'Max on Order',
min(column1) as 'min on Order'
from table
group by column 2
having max(column1)
