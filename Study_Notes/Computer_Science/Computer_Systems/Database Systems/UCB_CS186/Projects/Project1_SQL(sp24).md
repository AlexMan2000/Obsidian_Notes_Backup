# Basic Setup
## Run Sqlite3
> Navigate to the folder that contains `proj1.sql`, then start a new terminal and run `sqlite3 lahman.db`


## Run Python Test
> In the same folder, run `python test.py`


# Task 1: Basics
> [!task]
> ![](Project1_SQL(sp24).assets/image-20240124120135353.png)
> **Note:** This task only requires `people` table.

> [!code]
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


# Task 2: Intermediate
> [!task]
> ![](Project1_SQL(sp24).assets/image-20240124120308225.png)
> **Note:** This task requires `people` and `HallofFame` Table.

> [!code]
```sql

```