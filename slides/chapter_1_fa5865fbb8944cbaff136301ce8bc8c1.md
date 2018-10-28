---
title: Insert title here
key: fa5865fbb8944cbaff136301ce8bc8c1

---
## Order Matters

```yaml
type: "TitleSlide"
key: "e872f3528d"
```

`@lower_third`

name: Dean Smith
title: Geologist, Atamai Analytics


`@script`



---
## NBA Player Statistics 2007-2018

```yaml
type: "FullSlide"
key: "081c294c7c"
```

`@part1`
```sql
SELECT * FROM NBAPlayer_17_18
```
![](http://assets.datacamp.com/production/repositories/3898/datasets/bbdfe735ba09931a69fa7898831038f91c3eaaa1/NBA.jpg)


`@script`
In this lesson I will be looking at the ordering of SQL syntax in the construction of a query verses the processing order of the query in the database. For this, I will be using a selection of player statistics from the 2017 and 2018 NBA basketball season.


---
## Query Order

```yaml
type: "FullCodeSlide"
key: "c2b599326d"
```

`@part1`
```sql
SELECT PlayerName,Team,Points  -- 1. SELECT
FROM FROM NBAPlayer_17_18      -- 2. FROM
WHERE Position = 'PG'          -- 3. WHERE
ORDER BY Points DESC           -- 4. ORDER BY
```{{1}}
```
PlayerName                     Team Points
------------------------------ ---- -----------
Russell Westbrook              OKC  2028
Damian Lillard                 POR  1962
Kemba Walker                   CHO  1770
Kyrie Irving                   BOS  1466
Jamal Murray                   DEN  1352
Stephen Curry                  GSW  1346
........
(142 row(s) affected)
```{{2}}
![](http://assets.datacamp.com/production/repositories/3898/datasets/81bb932e0391abaf675dbd7d77a77cd2a09e2064/OrderSentence1.jpg) {{3}}


`@script`
Here is a simple query.  The SQL syntax is in the correct order and when executed will return the desired results.  If I write the query out in a sentence it will be something like SELECT rows in the columns PlayerName, Team and Points FROM the NBAPlayer_17_18  table, WHERE values in the Column Position = PG (for Point Guard), then ORDER BY values in the Points column descending. The order of the SQL syntax in the query is SELECT, FROM, WHERE and ORDER BY.


---
## Processing Order

```yaml
type: "FullCodeSlide"
key: "c8cf5fde51"
```

`@part1`
```sql
SELECT PlayerName,Team,Points  -- 3. SELECT
FROM FROM NBAPlayer_17_18      -- 1. FROM
WHERE Position = 'PG'          -- 2. WHERE
ORDER BY Points DESC           -- 4. ORDER BY
```{{1}}
```
PlayerName                     Team Points
------------------------------ ---- -----------
Russell Westbrook              OKC  2028
Damian Lillard                 POR  1962
Kemba Walker                   CHO  1770
Kyrie Irving                   BOS  1466
Jamal Murray                   DEN  1352
Stephen Curry                  GSW  1346
........
(142 row(s) affected)
```
![](http://assets.datacamp.com/production/repositories/3898/datasets/16f74425f1ff07b6930577c581e911668774f0c9/OrderSentence2.jpg) {{2}}


`@script`



---
## Ordering Example 1.

```yaml
type: "FullCodeSlide"
key: "cfc6ffc6f0"
```

`@part1`
```sql
SELECT Name,Team,Points
FROM NBAPlayer1718
WHERE Pos = 'PG'
ORDER BY Pts DESC
```{{1}}
```
Invalid object name 'NBAPlayer1718'.        --1. FROM
```{{2}}

```sql
SELECT Name,Team,Points
FROM NBAPlayer_17_18
WHERE Pos = 'PG'
ORDER BY Pts DESC
```{{3}}
```
Invalid column name 'Pos'.                  --2. WHERE
Invalid column name 'Name'.                 --3. SELECT
Invalid column name 'Pts'.                  --4. ORDER BY
```{{4}}


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
## Ordering Example 2.

```yaml
type: "FullCodeSlide"
key: "624b19780f"
```

`@part1`
```sql
SELECT PlayerName,Team,(DRebound+ORebound) AS TotalRebounds
FROM NBAPlayer_17_18
WHERE TotalRebounds > 1000
ORDER BY TotalRebounds DESC
```{{1}}
```
Invalid column name 'TotalRebounds'.
```{{2}}

```sql
SELECT PlayerName,Team,TotalRebounds
FROM
      (SELECT PlayerName,Team,(DRebound+ORebound) AS TotalRebounds
       FROM NBAPlayer_17_18) tr
WHERE TotalRebounds > 1000
ORDER BY TotalRebounds DESC
```{{3}}
```
PlayerName                     Team TotalRebounds
------------------------------ ---- -------------
Andre Drummond                 DET  1247
DeAndre Jordan                 LAC  1171
Karl-Anthony Towns             MIN  1012
Dwight Howard                  CHO  1012
(4 row(s) affected)
```{{4}}


`@script`



---
## Ordering Example 3.

```yaml
type: "FullCodeSlide"
key: "727d24fa99"
```

`@part1`
```sql
SELECT Team, SUM(Points) AS TotalPoints
FROM NBAPlayer_17_18
GROUP BY Team
HAVING (MinutesPlayed/GamesPlayed) > 20
ORDER BY TotalPoints DESC
```{{1}}
```
Column 'NBAPlayer_17_18.MinutesPlayed' is invalid in the HAVING clause 
because it is not contained in either an aggregate function or the 
GROUP BY clause.
```{{2}}

```sql
SELECT Team, SUM(Points) AS TotalPoints
FROM NBAPlayer_17_18
WHERE (MinutesPlayed/GamesPlayed) > 20
GROUP BY Team
ORDER BY TotalPoints DESC
```{{3}}
```
Team TotalPoints
---- -----------
HOU  8550
LAL  7911
IND  7781
……………………….
(30 row(s) affected)
```{{4}}


`@script`



---
## HAVING the Correct Order

```yaml
type: "FullCodeSlide"
key: "4c57ab90fe"
```

`@part1`
```sql
SELECT Team, SUM(Points) AS TotalPoints
FROM NBAPlayer_17_18
WHERE (MinutesPlayed/GamesPlayed) > 20
GROUP BY Team
HAVING AVG(MinutesPlayed/GamesPlayed) > 30
ORDER BY TotalPoints DESC
```{{1}}
```
Team TotalPoints
---- -----------
MIN  6495
DEN  6468
OKC  6455

(3 row(s) affected)
```{{2}}


`@script`



---
## Final Slide

```yaml
type: "FinalSlide"
key: "5c909e8ad9"
```

`@script`


