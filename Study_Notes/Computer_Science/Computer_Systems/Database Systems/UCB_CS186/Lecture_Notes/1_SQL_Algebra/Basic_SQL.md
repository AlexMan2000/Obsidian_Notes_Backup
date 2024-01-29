# Relation Language
## Relational Terminology
> [!def]
> ![](Basic_SQL.assets/image-20231205203036766.png)![](Basic_SQL.assets/image-20231205203040690.png)


## Relational Tables
> [!summary]
> ![](Basic_SQL.assets/image-20231205203221203.png)




## Concept Check
> [!example]
> ![](Basic_SQL.assets/image-20231205215246718.png)
> Since the second row doesn't satisfy the scheme. Very obvious visually.
> 
> ![](Basic_SQL.assets/image-20231205215406603.png)
> Two columns have the same name. Attributes have to be unique.
> 
> ![](Basic_SQL.assets/image-20231205215446234.png)
> Table is not flat. Addr is not as primitive type.




## Table Implementation
> [!concept]
> ![](Basic_SQL.assets/image-20231205215039489.png)![](Basic_SQL.assets/image-20231205215044489.png)![](Basic_SQL.assets/image-20231205215051679.png)




## First Normal Form
> [!concept]
> ![](Basic_SQL.assets/image-20231205215554402.png)![](Basic_SQL.assets/image-20231205215559989.png)



## Sets, Relations and Tables
> [!concept]
> ![](Basic_SQL.assets/image-20240119114231727.png)


# Operators with Set Semantics
## Sets and Bags Analogy
> [!concept]
> ![](Basic_SQL.assets/image-20240119142550954.png)![](Basic_SQL.assets/image-20240119142807132.png)





## Sets Operations
> [!concept]
> ![](Basic_SQL.assets/image-20240119142634066.png)


## Bags Operations

### ALL
> [!concept]
> ![](Basic_SQL.assets/image-20240119142645884.png)



### UNION ALL
> [!concept]
> ![](Basic_SQL.assets/image-20240119142700393.png)


### INTERSECT ALL
> [!concept]
> ![](Basic_SQL.assets/image-20240119142711866.png)



### EXCEPT ALL
> [!concept]
> ![](Basic_SQL.assets/image-20240119142720926.png)




# Basic SQL
> [!important]
> ![](Basic_SQL.assets/image-20240118222037698.png)



## SQL DDL


## SQL DML


## SQL DQL: Basic Single-Table Queries
> [!important]
> ![](Basic_SQL.assets/image-20240118221751615.png)![](Basic_SQL.assets/image-20240119113948486.png)





# Intermediate SQL
## Set-Oriented Operations
> [!concept]
> ![](Basic_SQL.assets/image-20240119142944860.png)
> Here, UNION is like performing set operations by treating each tuple(row) as set. We know that set operation automatically disallow for duplicates.
> 
> ![](Basic_SQL.assets/image-20240119143454604.png)





## Joins
### Cross Join
> [!concept]
> ![](Basic_SQL.assets/image-20240119145559676.png)![](Basic_SQL.assets/image-20240119145628557.png)![](Basic_SQL.assets/image-20240119145634991.png)



### Inner/Natural Join
> [!concept]
> ![](Basic_SQL.assets/image-20240119145734494.png)


### Outer Join
#### Left Outer Join
> [!concept]
> ![](Basic_SQL.assets/image-20240119145813612.png)![](Basic_SQL.assets/image-20240119150040141.png)



#### Right Outer Join
> [!concept]
> ![](Basic_SQL.assets/image-20240119145819571.png)![](Basic_SQL.assets/image-20240119150211965.png)



#### Full Outer Join
> [!concept]
> ![](Basic_SQL.assets/image-20240119145824687.png)![](Basic_SQL.assets/image-20240119150217069.png)



### Summary
> [!summary]
> ![](Basic_SQL.assets/image-20240119114433312.png)![](Basic_SQL.assets/image-20240119145425826.png)





## Aliasing



## String Comparison
> [!important]
> ![](Basic_SQL.assets/image-20240119114507130.png)




## Arithmetic Expression in SELECT



## NULL Values
### Arithmetic Rules
> [!important]
> ![](Basic_SQL.assets/image-20240119114843259.png)
> The use of NULL can be boiled down to the following rules:
> - If you do anything with NULL, you’ll just get NULL. For instance if x is NULL, then x > 3, 1 = x, and x + 4 all evaluate to NULL. Even x = NULL would evaluate to NULL; if you want to check whether x is NULL, then write x IS NULL or x IS NOT NULL instead. 
> - NULL is falsey, meaning that WHERE NULL is just like WHERE FALSE. The row in question does not get included. 
> - NULL short-circuits with boolean operators. That means a boolean expression involving NULL will evaluate to: 
> 	- TRUE, if it’d evaluate to TRUE regardless of whether the NULL value is really TRUE or FALSE
> 	- FALSE, if it’d evaluate to FALSE regardless of whether the NULL value is really TRUE or FALSE
> 	- NULL, if it depends on the NULL value.
> 
> 


### NULL in WHERE clause
> [!example]
> ![](Basic_SQL.assets/image-20240119115158865.png)


### Detect NULL
> [!example] 
> ![](Basic_SQL.assets/image-20240119142101613.png)


### NULL and Aggregation
> [!example]
> ![](Basic_SQL.assets/image-20240119142127328.png)


### Summary
> [!summary]
> ![](Basic_SQL.assets/image-20240119142136625.png)



## Fa20 Discussion 1 Exercises
### Single Table Query
> [!example]
> ![](Basic_SQL.assets/image-20240119144516228.png)![](Basic_SQL.assets/image-20240119144523373.png)

> [!solution]
> ![](Basic_SQL.assets/image-20240119144929221.png)![](Basic_SQL.assets/image-20240119144934805.png)



### Multi Table Query
> [!example]
> ![](Basic_SQL.assets/image-20240119145211879.png)![](Basic_SQL.assets/image-20240119145218549.png)![](Basic_SQL.assets/image-20240119145224228.png)

> [!solution]
> ![](Basic_SQL.assets/image-20240119152436094.png)![](Basic_SQL.assets/image-20240119152443507.png)![](Basic_SQL.assets/image-20240119152452009.png)




# Advanced SQL
## Nested Queries
### IN
> [!concept]
> ![](Basic_SQL.assets/image-20240119155026361.png)



### NOT IN
> [!concept]
> ![](Basic_SQL.assets/image-20240119155031990.png)


### Correlated Subqueries
> [!concept]
> Suppose we have two following table schema:
> courses (<u>num</u>, name), enrollment (<u>c_num</u>, students)
> ![](Basic_SQL.assets/image-20240119155746764.png)
> ![](Basic_SQL.assets/image-20240119155423555.png)![](Basic_SQL.assets/image-20240119155104314.png)

> [!example] Tough Example
> ![](Basic_SQL.assets/image-20240119155236573.png)



### Subqueries in FROM 
> [!example]
> ![](Basic_SQL.assets/image-20240119155935922.png)![](Basic_SQL.assets/image-20240119155940840.png)


### Set-Comparison Operators
> [!concept]
> ![](Basic_SQL.assets/image-20240119155127799.png)![](Basic_SQL.assets/image-20240119162343686.png)![](Basic_SQL.assets/image-20240119162350157.png)




## Views
> [!concept]
> ![](Basic_SQL.assets/image-20240119162414152.png)![](Basic_SQL.assets/image-20240119162423945.png)




## Common Table Expressions
> [!concept]
> ![](Basic_SQL.assets/image-20240119162501800.png)![](Basic_SQL.assets/image-20240119162512227.png)![](Basic_SQL.assets/image-20240119162543402.png)









# Appendix(Tips and Tricks)
> [!important]
> ![](Basic_SQL.assets/image-20240119154321594.png)


## How to write max?
> [!example]
> Suppose we have the following schema called `countries`: (<u>country</u>, gdp) and we want to select the countries with the highest gdp, we have the following ways to write the SQL:
> 1. Using ALL and max(if the country's gdp is bigger than any other ones'): 
> 	`SELECT name FROM countries where gdp >= ALL(SELECT max(gdp) FROM countries)`
> 1. Using Subqueries(if there is no countries with bigger gdp, then it is the max-gdp country): 
>	`SELECT name FROM countries WHERE NOT EXISTS (SELECT name FROM countries as countries2 WHERE countries2.gdp>countries.gdp)`


## How to write more than once?
> [!example]
> 
