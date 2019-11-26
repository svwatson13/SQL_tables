## SQL Tables notes
#Key commands
- create table <table name> (<column name>, <column name>)
- add column: alter table <table name> add <column name>
- update table:
-- UPDATE table_name
   SET column1 = value1, column2 = value2,
   WHERE condition;
-  delete rows: delete from <table name> where <condition>    --  <what you want deleted>
-   PK & FK: manual = designer -> relationships but code below
    CREATE TABLE orders
    ```
    (OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID));
    ```
- insert data: insert into <table name> (<column name>,       <column name>) values (<value1>, <value2>)
