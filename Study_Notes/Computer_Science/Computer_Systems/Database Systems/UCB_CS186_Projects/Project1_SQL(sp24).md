# Basic Setup
## Run Sqlite3
> Navigate to the folder that contains `proj1.sql`, then start a new terminal and run `sqlite3 lahman.db
> `
> To exit sqlite3, run `CTRL+C X`


## Run Python Test
> In the same folder, run `python test.py`


# Task 1: Basic Syntax
> [!task]
> ![](Project1_SQL(sp24).assets/image-20240124120135353.png)
> **Note:** This task only requires `people` table.

> [!code]
> Lesson here is that varchar/char type should be embraced by `' '` not `" "`.
```sql
-- Question 0
CREATE VIEW q0(era)
AS
  -- solution you provide
	SELECT MAX(era)
	FROM pitching;
;

-- Question 1i
CREATE VIEW q1i(namefirst, namelast, birthyear)
AS
  SELECT nameFirst, nameLast, birthYear 
  FROM people
  WHERE weight > 300;
;

-- Question 1ii
CREATE VIEW q1ii(namefirst, namelast, birthyear)
AS
  SELECT nameFirst, nameLast, birthYear 
  FROM people
  WHERE nameFirst LIKE '% %'   -- Attention here, string is closed by '' instead of "".
  ORDER BY nameFirst ASC, nameLast ASC;
;

-- Question 1iii
CREATE VIEW q1iii(birthyear, avgheight, count)
AS
  SELECT birthYear, AVG(height), COUNT(*)
  FROM people 
  GROUP BY birthYear
  ORDER BY birthYear ASC;
;

-- Question 1iv
CREATE VIEW q1iv(birthyear, avgheight, count)
AS
  SELECT birthYear, AVG(height), COUNT(*)
  FROM people 
  GROUP BY birthYear 
  HAVING AVG(height) > 70
  ORDER BY birthYear ASC;
;
```


# Task 2: Multiple Tables
> [!task]
> ![](Project1_SQL(sp24).assets/image-20240124120308225.png)
> **Note:** This task requires `people`, `HallofFame`, `CollegePlaying`,`schools` Table. 
> 

> [!code]
> The lesson here is that when we are doing multiple joins, we precede by sequence. For example:
> 
> `A inner join B left join T` will be processed as we first join `A` and `B` and then join the resulting table with `T`.
> 
> We can also use `CTE` to structure our code to be more readable.
> 
> Also, when using multiple WITH, the second CTE and further ones should be omitted.
> 
```sql
-- Question 2i
CREATE VIEW q2i(namefirst, namelast, playerid, yearid)
AS
  SELECT p.nameFirst, p.nameLast, p.playerID, h.yearid 
  FROM people as p INNER JOIN HallofFame as h
  ON p.playerID = h.playerID
  WHERE h.inducted == 'Y'
  ORDER BY h.yearid DESC, p.playerid ASC
;

-- Question 2ii
CREATE VIEW q2ii(namefirst, namelast, playerid, schoolid, yearid)
AS

  -- Here one player could be appearing in the same school multiple years
  -- For test, we don't have to add DISTINCT here.
  WITH playerSchool(playerID, schoolID) AS
  (SELECT c.playerID, c.schoolID
  FROM CollegePlaying AS c LEFT JOIN schools AS s
  ON c.schoolID = s.schoolID
  WHERE s.schoolState == 'CA')
  
  
  SELECT p.nameFirst, p.nameLast, p.playerID, ps.schoolID, h.yearid 
  FROM people AS p INNER JOIN HallofFame AS h
  ON p.playerID = h.playerID
  INNER JOIN playerSchool AS ps 
  ON p.playerID = ps.playerID
  WHERE h.inducted == 'Y'
  ORDER BY h.yearid DESC, ps.schoolID ASC, p.playerID ASC
;

-- Question 2iii
CREATE VIEW q2iii(playerid, namefirst, namelast, schoolid)
AS

  WITH playerSchool(playerID, schoolID) AS
  (SELECT c.playerID, c.schoolID
  FROM CollegePlaying AS c LEFT JOIN schools AS s
  ON c.schoolID = s.schoolID),
  
  playerHall(nameFirst, nameLast, playerID) AS
  (SELECT p.nameFirst, p.nameLast, p.playerID
  FROM people AS p INNER JOIN HallofFame AS h
  ON p.playerID = h.playerID
  WHERE h.inducted == 'Y')
  
  SELECT ph.playerID, ph.nameFirst, ph.nameLast, ps.schoolID
  FROM playerHall AS ph LEFT JOIN playerSchool AS ps
  ON ph.playerID = ps.playerID
  ORDER BY ph.playerID DESC, ps.schoolID ASC
;
```


# Task 3: SQL Statistics
> [!overview]
> The tables that are used in this problem is `people` and `Batting`

## Task 3.1 SLG
> [!task]
> ![](Project1_SQL(sp24).assets/image-20240205173208963.png)![](Project1_SQL(sp24).assets/image-20240205162152473.png)![](Project1_SQL(sp24).assets/image-20240205163345649.png)

> [!code]
> The lesson here is that we could do type-casting in SQL by `CAST(variable as Type)`
> 
> In order to correctly perform integer division, we have to cast either the numerator or the denominator to be float type using the above syntax.
```sql
CREATE VIEW q3i(playerid, namefirst, namelast, yearid, slg)
AS
  SELECT p.playerID, p.nameFirst, p.nameLast, b.yearID
  , CAST(b.H + b.H2B + 2 * b.H3B + 3 * b.HR AS FLOAT) / AB AS slg
  FROM people AS p 
  INNER JOIN Batting AS b
  ON p.playerID = b.playerID
  WHERE b.AB > 50
  ORDER BY slg DESC, b.yearID ASC, p.playerID ASC
  LIMIT 10
;
```


## Task 3.2 Lifetime SLG
> [!task]
> ![](Project1_SQL(sp24).assets/image-20240205162336220.png)

> [!code]
```sql
CREATE VIEW q3ii(playerid, namefirst, namelast, lslg)
AS
  WITH LTSLG(playerID, LH, LAB, LH2B, LH3B, LHR) AS
  (SELECT playerID, SUM(H) AS LH
  , SUM(AB) AS LAB
  , SUM(H2B) AS LH2B
  , SUM(H3B) AS LH3B
  , SUM(HR) AS LHR 
  FROM Batting 
  GROUP BY playerID 
  HAVING SUM(AB) > 50
  )
  
  SELECT p.playerID, p.nameFirst, p.nameLast 
  , CAST(b.LH + b.LH2B + 2 * b.LH3B + 3 * b.LHR AS FLOAT) / LAB AS lslg
  FROM people AS p 
  INNER JOIN LTSLG AS b
  ON p.playerID = b.playerID
  ORDER BY lslg DESC, p.playerID ASC
  LIMIT 10
;
```



## Task 3.3 Lifetime SLG Part 2
> [!task]
> ![](Project1_SQL(sp24).assets/image-20240205162351563.png)

> [!code]
> Lesson here is that we can compute the statistics correctly just within the group.
```sql
CREATE VIEW q3iii(namefirst, namelast, lslg)
AS
  WITH LTSLG(playerID, LSLG) AS
  (SELECT playerID
  , (CAST(SUM(H) + SUM(H2B) + 2 * SUM(H3B) + 3 * SUM(HR) AS FLOAT)) / SUM(AB) AS LSLG
  FROM Batting
  GROUP BY playerID 
  HAVING SUM(AB) > 50
  )
  
  SELECT  p.nameFirst, p.nameLast, b.LSLG AS lslg
  FROM people AS p 
  INNER JOIN LTSLG AS b
  ON p.playerID = b.playerID
  WHERE LSLG > (SELECT LSLG FROM LTSLG WHERE playerID == 'mayswi01')
  ORDER BY LSLG DESC, p.playerID ASC
;
```


# Task 4: Salaries

## Task 4.1: Aggregation
> [!task]
> ![](Project1_SQL(sp24).assets/image-20240205174829234.png)
> The table used in this problem is `Salaries`

> [!code]
```sql
CREATE VIEW q4i(yearid, min, max, avg)
AS
  SELECT yearID, MIN(salary) AS min, MAX(salary) AS max, AVG(salary) AS avg
  FROM salaries 
  GROUP BY yearID
  ORDER BY yearID ASC
;
```


## Task 4.2 Histogram
> [!task]
> ![](Project1_SQL(sp24).assets/image-20240205174921739.png)
> The table used in this problem is `People` and `Salaries`

> [!code]
> The lesson here is that in order to use nested query, we have to use parathesis to bracket it! Otherwise, sqlite3 will flag an error that reads `no such table` even if you have everything else settled up.
> 
> Here the idea is that if your data is distibuted across $[a,b]$, then we can calculate the following quantities:
> 1. Binwidth: $\frac{b-a}{n}$ where $n$ is the number of bins.
> 2. [low, high] : for $i-th$ bin, the $low = a + i * n$, $high=a+(i+1)*n$
> 3. Salary map to binid: If $salary==b$, then $bin(salary)=\frac{salary-a}{binWidth}-1$ otherwise $\frac{salary-a}{binWidth}$.
```sql
CREATE VIEW q4ii(binid, low, high, count)
AS

  WITH salaryIn2016(salary) AS
  (SELECT salary 
  FROM salaries 
  WHERE yearID == 2016),

  binWidth(binW) AS 
  (SELECT (MAX(salary) - MIN(salary)) / (SELECT count(binid) FROM binids) AS binW
  FROM salaryIn2016),

  -- Basically this is a mapping table from salary to the binid 
  salaryToBin(salary, binid) AS
  (SELECT salary
  ,CASE WHEN salary == (SELECT MAX(salary) from salaryIn2016) 
		THEN CAST((salary - (SELECT MIN(salary) FROM salaryIn2016)) / (SELECT binW from binWidth) AS INT) - 1
        ELSE CAST((salary - (SELECT MIN(salary) FROM salaryIn2016)) / (SELECT binW from binWidth) AS INT)
		END 
	AS binid
  FROM salaryIn2016)

  -- Construct the final result
  -- Note [low, high] is not the actual data, but predetermined by binWidth.
  SELECT b.binid
  , (SELECT MIN(salary) FROM salaryIn2016) + b.binid * (SELECT binW from binWidth)
  , (SELECT MIN(salary) FROM salaryIn2016) + (b.binid + 1) * (SELECT binW from binWidth)
  , count(salary) AS count 
  FROM binids AS b 
  LEFT JOIN salaryToBin AS mapping
  ON mapping.binid = b.binid
  GROUP BY b.binid
;
```


## Task 4.3 Year-over-Year Change
> [!task]
> ![](Project1_SQL(sp24).assets/image-20240205175025743.png)
> The table used in this problem is `Salaries`

> [!code]
> The key takeaway is that nested query can happen everywhere, even in SELECT statement where we could still utilize the `correlation` between inner and outer query to perform some really cool operations.
```sql
CREATE VIEW q4iii(yearid, mindiff, maxdiff, avgdiff)
AS
  WITH yearlyStat(yearID, minSalary, maxSalary, avgSalary) AS
  (SELECT yearID, MIN(salary), MAX(salary), AVG(salary)
  FROM salaries
  GROUP BY yearID
  )

-- Neat Trick Using Nested Queries
  SELECT a.yearID
  ,a.minSalary - (SELECT b.minSalary FROM yearlyStat as b WHERE b.yearID + 1 = a.yearID)
  ,a.maxSalary - (SELECT b.maxSalary FROM yearlyStat as b WHERE b.yearID + 1 = a.yearID)
  ,a.avgSalary - (SELECT b.avgSalary FROM yearlyStat as b WHERE b.yearID + 1 = a.yearID)
  FROM yearlyStat AS a
  WHERE a.yearID != (SELECT MIN(yearID) FROM yearlyStat)
;
```



## Task 4.4 Argmax
> [!task]
> ![](Project1_SQL(sp24).assets/image-20240205175033699.png)
> The table used in this problem is `People` and `Salaries`

> [!code] Naive Approach
```sql
CREATE VIEW q4iv(playerid, namefirst, namelast, salary, yearid)
AS
  WITH maxYearlySalary(yearID, maxSalary) AS
  (SELECT yearID, MAX(salary)
  FROM salaries 
  GROUP BY yearID)
  
  SELECT p.playerID, p.nameFirst, p.nameLast, s.salary, s.yearID
  FROM people as p
  LEFT JOIN salaries as s
  ON p.playerID = s.playerID
  WHERE (s.yearID = 2000 and s.salary = (SELECT maxSalary FROM maxYearlySalary WHERE yearID = 2000))
  OR (s.yearId = 2001 and s.salary = (SELECT maxSalary FROM maxYearlySalary WHERE yearID = 2001))
;
```

> [!code] Using Window Function
```sql

```


## Task 4.5 Group Average Difference
> [!task]
> ![](Project1_SQL(sp24).assets/image-20240205175042425.png)
> The table used in this problem is `people`, `AllStarFull` and `teams`

> [!code]
```sql
CREATE VIEW q4v(team, diffAvg) AS

  SELECT a.teamid, max(salary) - min(salary)
  FROM allstarfull as a
  INNER JOIN salaries as s 
  ON a.playerid = s.playerid and a.yearid = s.yearid 
  WHERE a.yearid = 2016
  GROUP BY a.teamid
;

```



