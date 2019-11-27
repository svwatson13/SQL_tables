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

## Querying tables

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
- format date: format(datecolumnname,'dd/mm/yyyy')
- example:
select orderid, format(orderdate,'dd/mm/yyyy'), orderdate
from orders;
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

#### Big sums
- select
sum(column) as 'Total on Order',
avg(column) as 'AVG on Order',
max(column) as 'Max on Order',
min(column) as 'min on Order'
group by column 2
having max(column1)
from table
- example
select CategoryID , avg(ReorderLevel) as 'AVG order'
from products
group by categoryID
order by 'AVG order' desc

### JOIN
- join command automatically inner join - combines tables but matching columns are only listed once
- left join or left outer join returns all rows from left table and matched rows from right table but none extras from right
- right join or right outer join is same as left but opposite
- full join returns all matching records from both tables whether the other table matches or not. EVERYTHANG
- example
select * from table
join on lefttablecolumnname, rightcolumnname

### Subqueries
- most common in where
- example where trying to find all products with quantity over 100
```
SELECT ProductName
  FROM Product
 WHERE Id IN (SELECT ProductId
                FROM OrderItem
               WHERE Quantity > 100)
```
- also used in extra select statements
```
select orderid, productid, unitprice, quantity, discount,
	(select max(unitprice) from [Order Details]) as 'max price',
	(select avg(unitprice) from [Order Details]) as 'AVG price'
from [Order Details]
```
