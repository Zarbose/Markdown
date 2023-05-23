# BD et Big Data

Document qui rasemble les commandes sql les plus courantes : [Documentation](https://sql.sh/) (23.05.2023)

### SELECT et FROM
```sql
SELECT studentID, FirstName, LastName, FirstName + ' ' + LastName AS FullName
FROM student;
```

### CREATE TABLE
```sql
CREATE TABLE table_name (
    column_1 datatype,
    column_2 datatype,
    column_3 datatype
);
```

### ALTER TABLE
```sql
ALTER TABLE table_name
ADD column_name datatype;
```

### CHECK
```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CHECK (Age>=18)
);
```
```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255),
    CONSTRAINT CHK_Person CHECK (Age>=18 AND City='Sandnes')
);
```

### WHERE
```sql
Select studentID, FullName, sat_score, recordUpdated
FROM student
WHERE (studentID BETWEEN 1 AND 5 OR studentID = 8)
        AND
        sat_score NOT IN (1000, 1400);
```

### UPDATE
```sql
UPDATE table_name
SET column1 = value1, 
    column2 = value2, ...
WHERE condition;
```

### GROUP BY
```sql
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name;
```

### HAVING
```sql
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name
HAVING COUNT(*) > value;
```

### AVG()
```sql
SELECT groupingField, AVG(num_field)
FROM table1
GROUP BY groupingField
```

### AS
```sql
SELECT user_only_num1 AS AgeOfServer, (user_only_num1 - warranty_period) AS NonWarrantyPeriod FROM server_table
```

### ORDER By
```sql
SELECT studentID, FullName, sat_score
FROM student
ORDER BY FullName DESC;
```

### COUNT
```sql
SELECT count(*) AS studentCount FROM student; 
```

### DELETE
```sql
DELETE FROM table_name
WHERE condition;
```

### INNER JOIN
```sql
SELECT * FROM A x JOIN B y ON y.aId = x.Id
```

### LEFT JOIN
```sql
SELECT * FROM A x LEFT JOIN B y ON y.aId = x.Id
```

### RIGHT JOIN
```sql
SELECT * FROM A x RIGHT JOIN B y ON y.aId = x.Id
```

### INSERT
```sql
INSERT INTO table_name (column_1, column_2, column_3) 
VALUES (value_1, 'value_2', value_3);
```

### LIKE
```sql
SELECT studentID, FullName, sat_score, rcd_updated
FROM student 
WHERE 
    FullName LIKE 'Monique%' OR 
    FullName LIKE '%Greene'; 
```

```sql
SELECT studentID, FullName, sat_score, rcd_updated
FROM student 
WHERE FullName NOT LIKE '%cer Pau%' AND FullName NOT LIKE '%"Ted"%';
```
