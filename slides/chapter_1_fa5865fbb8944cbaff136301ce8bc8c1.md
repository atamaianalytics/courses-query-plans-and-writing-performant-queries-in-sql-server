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
## Final Slide

```yaml
type: "FinalSlide"
key: "5c909e8ad9"
```

`@script`


