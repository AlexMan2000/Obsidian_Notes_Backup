[lab02.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/12393765/1673601816828-17a04eba-5285-4f29-b661-dc8b680d5f6d.zip)


# Q1 Donations
> ![image.png](./Lab_02__SQL.assets/20230302_2122096193.png)


## Q1a LIKE Trump
> ![image.png](./Lab_02__SQL.assets/20230302_2122098828.png)

```python
query_q1a='''
SELECT
    cmte_id, 
    transaction_amt,
    name
FROM indiv_sample_nyc
WHERE name LIKE '%TRUMP%'
AND name LIKE '%DONALD%'
'''

res_q1a = pd.read_sql(query_q1a, engine)
res_q1a
```
**SQL Output**![image.png](./Lab_02__SQL.assets/20230302_2122091055.png)

## Q1b NOT LIKE President
> ![image.png](./Lab_02__SQL.assets/20230302_2122094193.png)

```python
query_q1b = '''
SELECT
    cmte_id, 
    transaction_amt,
    name
FROM indiv_sample_nyc
WHERE name LIKE '%TRUMP%'
AND name LIKE '%DONALD%'
AND name NOT LIKE '%PRESIDENT%'
'''

res_q1b = pd.read_sql(query_q1b, engine)
res_q1b
```
**SQL Output**![image.png](./Lab_02__SQL.assets/20230302_2122105401.png)


## Q1c Aggregation
> ![image.png](./Lab_02__SQL.assets/20230302_2122106608.png)

```python
query_q1c = '''
SELECT
    cmte_id, 
    sum(transaction_amt) as total_amount,
    count(*) as num_donations
FROM indiv_sample_nyc
WHERE name LIKE '%TRUMP%'
AND name LIKE '%DONALD%'
AND name NOT LIKE '%PRESIDENT%'
GROUP BY cmte_id
ORDER BY total_amount
DESC
'''


res_q1c = pd.read_sql(query_q1c, engine)
res_q1c
```
**SQL Output**![image.png](./Lab_02__SQL.assets/20230302_2122103811.png)
![image.png](./Lab_02__SQL.assets/20230302_2122108976.png)

## Q1d Join& Nested Queries⭐⭐⭐
> ![image.png](./Lab_02__SQL.assets/20230302_2122103709.png)![image.png](./Lab_02__SQL.assets/20230302_2122109821.png)
> **本题提供两种解法:**
> 1. 使用`JOIN`建立从`cmte_id`到`cmte_nm`的映射。
> 2. 使用`subqueries`找出符合`cmte_id`的`cmte_nm`。

```python
query_q1d = '''
SELECT
    s.cmte_id, 
    sum(s.transaction_amt) as total_amount,
    count(*) as num_donations,
    c.cmte_nm 
FROM indiv_sample_nyc as s
LEFT JOIN comm as c ON c.cmte_id = s.cmte_id
WHERE s.name LIKE '%TRUMP%'
AND s.name LIKE '%DONALD%'
AND s.name NOT LIKE '%PRESIDENT%'
GROUP BY s.cmte_id
ORDER BY total_amount
DESC
'''


res_q1d = pd.read_sql(query_q1d, engine)
res_q1d
```
```python
query_q1d = '''
SELECT
    cmte_id, 
    sum(transaction_amt) as total_amount,
    count(*) as num_donations,
    (SELECT cmte_nm 
        FROM comm
        WHERE comm.cmte_id = s.cmte_id) as cmte_nm
FROM indiv_sample_nyc as s
WHERE name LIKE '%TRUMP%'
AND name LIKE '%DONALD%'
AND name NOT LIKE '%PRESIDENT%'
GROUP BY cmte_id
ORDER BY total_amount
DESC
'''


res_q1d = pd.read_sql(query_q1d, engine)
res_q1d
```
**SQL Output**![image.png](./Lab_02__SQL.assets/20230302_2122108292.png)


# Q2 Candidates
## Q2a Community Ending in 5
> ![image.png](./Lab_02__SQL.assets/20230302_2122105957.png)

```python
query_q2a='''
SELECT
    cmte_id AS committee_id,
    sum(transaction_amt) AS total_amount,
    count(cmte_id) AS count
FROM indiv_sample_nyc
WHERE cmte_id LIKE "%5"
GROUP BY cmte_id
ORDER BY count
DESC
LIMIT 5
'''


res_q2a = pd.read_sql(query_q2a, engine)
res_q2a
```
**SQL Output**![image.png](./Lab_02__SQL.assets/20230302_2122107334.png)

## Q2b INNER JOIN
> ![image.png](./Lab_02__SQL.assets/20230302_2122116575.png)![image.png](./Lab_02__SQL.assets/20230302_2122113145.png)![image.png](./Lab_02__SQL.assets/20230302_2122116202.png)

```python
query_q2b='''
SELECT c1.cand_name as cand_name, c2.cmte_nm as cmte_nm
FROM cand c1 INNER JOIN comm c2 ON c1.cand_id = c2.cand_id
ORDER BY cand_name
DESC
LIMIT 5
'''


res_q2b = pd.read_sql(query_q2b, engine)
res_q2b
```
**SQL Output**![image.png](./Lab_02__SQL.assets/20230302_2122116353.png)


## Q2c LEFT JOIN
> ![image.png](./Lab_02__SQL.assets/20230302_2122115907.png)

```python
query_q2c='''
SELECT c1.cand_name as cand_name, c2.cmte_nm as cmte_nm
FROM cand c1 LEFT JOIN comm c2 ON c1.cand_id = c2.cand_id
ORDER BY cand_name
DESC
LIMIT 5
'''


res_q2c = pd.read_sql(query_q2c, engine)
res_q2c
```
**SQL Output**![image.png](./Lab_02__SQL.assets/20230302_2122112950.png)
