[released_lab_lab13_lab13.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/12393765/1673000074813-c375e4f1-1448-4622-b64e-3de92d4b1afe.zip)
[released_lab_sol-lab13_lab13.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/12393765/1673000074850-dc02eb9d-15e6-4d9e-9850-4ac3324f56ce.zip)
[Lab 13_ SQL (Optional) _ CS 61A Fall 2022.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673000110449-7e29859c-3455-49f7-ab9b-0f79b8cd5005.pdf)


> Refer to the `data.sql` in the folder when completing this lab.



# Berkeley Students
## Q1 What would SQL print?
> ![image.png](Lab_13__SQL(Optional).assets/20230302_1025021693.png)

**Solution**![image.png](Lab_13__SQL(Optional).assets/20230302_1025022438.png)![image.png](Lab_13__SQL(Optional).assets/20230302_1025027285.png)![image.png](Lab_13__SQL(Optional).assets/20230302_1025022963.png)


## Q2 Go Bears? (And Dogs?)
**Description**![image.png](Lab_13__SQL(Optional).assets/20230302_1025035030.png)![image.png](Lab_13__SQL(Optional).assets/20230302_1025037270.png)
```sql
CREATE TABLE bluedog AS
  SELECT color, pet FROM students WHERE color = 'blue' AND pet = 'dog';

CREATE TABLE bluedog_songs AS
  SELECT color, pet, song FROM students WHERE color = 'blue' AND pet = 'dog';

```


## Q3 The Smallest Unique Positive Integer
> ![image.png](Lab_13__SQL(Optional).assets/20230302_1025035390.png)
> 就是只被提交了一次的`smallest-int`, 所以`group by smallest-int`

```sql
CREATE TABLE matchmaker AS
  SELECT "REPLACE THIS LINE WITH YOUR SOLUTION";
```
```sql
CREATE TABLE smallest_int_having AS
  SELECT time, smallest from students group by smallest having count(*) = 1;
```



## Q4 Matchmaker - Join with itself
> ![image.png](Lab_13__SQL(Optional).assets/20230302_1025035185.png)

```sql
CREATE TABLE matchmaker AS
  SELECT "REPLACE THIS LINE WITH YOUR SOLUTION";
```
```sql
CREATE TABLE matchmaker AS
  SELECT s1.pet as pet, s2.song as song, s1.color as color1, s2.color as color2
  from students as s1, students as s2
    where s1.pet = s2.pet
    and s1.time < s2.time   -- 保证不会选到自己和自己一对
    and s1.song = s2.song;
```


## Q5 Sevens
> ![image.png](Lab_13__SQL(Optional).assets/20230302_1025038231.png)

```sql
CREATE TABLE sevens AS
  SELECT "REPLACE THIS LINE WITH YOUR SOLUTION";
```
```sql
CREATE TABLE sevens AS
  SELECT seven from students, numbers
    where students.time = numbers.time
    and students.number = 7
    and numbers."7" = "True";
```



# Cyber Monday
## Q6 Price Check
> ![image.png](Lab_13__SQL(Optional).assets/20230302_1025034946.png)
> **MSRP: **建议零售价, the price at which its manufacturer notionally recommends that a retailer sell the product.

```sql
CREATE TABLE average_prices AS
  SELECT "REPLACE THIS LINE WITH YOUR SOLUTION";
```
```sql
CREATE TABLE average_prices AS
  SELECT category, avg(MSRP) as average_price
    from products group by category;
```

## Q7 The Price is Right
> ![image.png](Lab_13__SQL(Optional).assets/20230302_1025031220.png)

```sql
CREATE TABLE lowest_prices AS
  SELECT "REPLACE THIS LINE WITH YOUR SOLUTION";

```
```sql
CREATE TABLE lowest_prices AS
  SELECT store, item, min(price) as lowest_price
    from inventory group by item;
```


## Q8 Bang for your Buck ⭐⭐⭐⭐⭐
> ![image.png](Lab_13__SQL(Optional).assets/20230302_1025044526.png)
> `having`可以只跟`MIN(...)`

```sql
CREATE TABLE shopping_list AS
  SELECT "REPLACE THIS LINE WITH YOUR SOLUTION";
```
```sql
CREATE TABLE shopping_list AS
  SELECT item, store from lowest_prices, products
    where item = name
    group by category having MIN(MSRP/rating)
  ;

```



## Q9 Driving the Cyber Highways
> ![image.png](Lab_13__SQL(Optional).assets/20230302_1025047108.png)

```sql
CREATE TABLE total_bandwidth AS
  SELECT "REPLACE THIS LINE WITH YOUR SOLUTION";

```
```sql
CREATE TABLE total_bandwidth AS
  SELECT SUM(s.mbs) FROM stores AS s, shopping_list AS sl WHERE s.store = sl.store;
```
