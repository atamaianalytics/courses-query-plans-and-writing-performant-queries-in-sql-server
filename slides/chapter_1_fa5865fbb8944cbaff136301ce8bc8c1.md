---
title: Insert title here
key: fa5865fbb8944cbaff136301ce8bc8c1

---
## The Right Order

```yaml
type: "TitleSlide"
key: "e872f3528d"
```

`@lower_third`

name: Dean Smith
title: Geologist, Atamai Analytics


`@script`



---
## NORTHWIND Tables

```yaml
type: "FullSlide"
key: "081c294c7c"
```

`@part1`
![](http://assets.datacamp.com/production/repositories/3898/datasets/f4427279612b14dff1d8a673bf3ac0809bac65d2/Orders.jpg)


`@script`
I want to start by looking at the ordering of SQL syntax in the construction of a query verses the processing order of the query in the database.  In the following examples I will be using the Orders and Order Details tables from the NORTHWIND database.


---
## Query Order

```yaml
type: "FullCodeSlide"
key: "c2b599326d"
```

`@part1`
```sql
SELECT OrderID,CustomerID,ShipCity -- 1. SELECT
FROM Orders                        -- 2. FROM
WHERE ShipCountry = 'France'       -- 3. WHERE
ORDER BY ShipCity,CustomerID       -- 4. ORDER BY
```

**SELECT** rows in the columns _OrderID_,_CustomerID_ and _ShipCity_ **FROM** the Orders table, **WHERE** values in the column _ShipCountry_ = _France_,
then **ORDER BY** values in the _ShipCity_ and _CustomerID_
Columns.


`@script`
Here is a simple query.  The SQL syntax is in the correct order and when executed will return the desired results.  If I write the query out in a sentence it will be something like SELECT rows in the columns OrderID, CustomerID and ShipCity FROM the Orders table, WHERE values in the column ShipCountry = France, then ORDER BY values in the ShipCity and CustomerID Columns. The order of the SQL syntax in the query is SELECT, FROM WHERE and ORDER BY.


---
## Processing Order

```yaml
type: "FullCodeSlide"
key: "c8cf5fde51"
```

`@part1`
```sql
SELECT OrderID,CustomerID,ShipCity -- 3. SELECT
FROM Orders                        -- 1. FROM
WHERE ShipCountry = 'France'       -- 2. WHERE
ORDER BY ShipCity,CustomerID       -- 4. ORDER BY
```

**FROM** the table _Orders_, **WHERE** values in the column _ShipCountry_ = _France_,
**SELECT** rows in the columns _OrderID_, _CustomerID_ and _ShipCity_,
then **ORDER BY** values in the _ShipCity_ and _CustomerID_ Columns.


`@script`



---
## Ordering Example 1.

```yaml
type: "FullCodeSlide"
key: "cfc6ffc6f0"
```

`@part1`
```sql
SELECT OrderID,CustomerID,ShipTown
FROM Order
WHERE ShipArea = 'France'
ORDER BY ShipCity,Customer
```
```
Incorrect syntax near the keyword 'Order'.        --1. FROM
```

```sql
SELECT OrderID,CustomerID,ShipTown
FROM Orders
WHERE ShipArea = 'France'
ORDER BY ShipCity,Customer
```
```
Invalid column name 'ShipArea'.                  --2. WHERE
Invalid column name 'ShipTown'.                  --3. SELECT
Invalid column name 'Customer'.                  --4. ORDER BY
```


`@script`
Let’s look at an example of this.  I’m using the same query, the ordering of the SQL syntax is correct but I have some typo errors in the table and column names. 
When I execute the query, FROM is processed first – I get an error because the table Order is not part of the database.  When I execute again, after fixing the error to the correct table name, which is Orders, I get addition errors listed in order of the processing order.  WHERE cannot process ShipArea, SELECT cannot process ShipTown and ORDER BY cannot process Customer because none of these are columns in the table Orders.  They should by ShipCountry, ShipCity and CustomerID respectively.


---
## Logical Processing Order

```yaml
type: "FullCodeSlide"
key: "33e2171dec"
```

`@part1`
```sql
FROM        --1
ON          --2
JOIN        --3
WHERE       --4
GROUP BY    --5
HAVING      --6
SELECT      --7
DISTINCT    --8
ORDER BY    --9
TOP         --10
```


`@script`
Here is the Logical Processing Order for the most commonly used SQL Syntax in the SELECT Statement.  Note how far down the order SELECT occurs.  You can imaging that all the processing before SELECT is concerned with finding, merging, aggregating and filtering the data and that processing after SELECT is concerned with actions on the final data extracted.  Steps after SELECT tend to be quite expensive to process and should only be used where necessary.  As a data scientist, working with real world large data sets, having an understanding of the processing order can help determine why a query will not execute and also help to look at ways to optimize the query for performance.


---
## Final Slide

```yaml
type: "FinalSlide"
key: "5c909e8ad9"
```

`@script`


