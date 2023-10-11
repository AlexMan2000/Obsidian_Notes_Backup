> **Ch6:** [https://learningds.org/ch/06/pandas_intro.html](https://learningds.org/ch/06/pandas_intro.html)



# 1 Pandas Basics
[5. Pandas 1.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673679057375-839051f8-ed5e-43e7-a13c-933f6412e611.pdf)
[lec05.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/12393765/1673679824936-4422b1a3-55db-4f83-86ef-f9af77f21523.zip)


## DataFrames& Series & Indices
### Basics
:::info
![image.png](./Lectures_Readings.assets/20230302_2123071648.png)![image.png](./Lectures_Readings.assets/20230302_2123087945.png)![image.png](./Lectures_Readings.assets/20230302_2123089383.png)![image.png](./Lectures_Readings.assets/20230302_2123082985.png)![image.png](./Lectures_Readings.assets/20230302_2123083684.png)
`Pandas`会自动区分那些重复的`column_names`，比如创建新的`column_alias`
:::

### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2123085879.png)
:::


## Indexing
### Index by Columns
:::info
![image.png](./Lectures_Readings.assets/20230302_2123096845.png)![image.png](./Lectures_Readings.assets/20230302_2123099170.png)
:::


### Index by Rows
:::info
![image.png](./Lectures_Readings.assets/20230302_2123099495.png)![image.png](./Lectures_Readings.assets/20230302_2123095371.png)
:::
**Exercise**⭐⭐⭐⭐⭐![image.png](./Lectures_Readings.assets/20230302_2123091401.png)

### Summary
:::info
![image.png](./Lectures_Readings.assets/20230302_2123094532.png)
:::


### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2123103086.png)![image.png](./Lectures_Readings.assets/20230302_2123106699.png)
:::



## Boolean Array Selection
:::info
Used to select the rows
:::
### Using Raw Boolean
:::info
![image.png](./Lectures_Readings.assets/20230302_2123105364.png)
:::


### Using Boolean Expressions
:::info
![image.png](./Lectures_Readings.assets/20230302_2123107748.png)![image.png](./Lectures_Readings.assets/20230302_2123107358.png)![image.png](./Lectures_Readings.assets/20230302_2123107428.png)
:::


### isin
:::info
![image.png](./Lectures_Readings.assets/20230302_2123113003.png)
:::


### query
:::info
![image.png](./Lectures_Readings.assets/20230302_2123113781.png)
:::



### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2123114339.png)![image.png](./Lectures_Readings.assets/20230302_2123119593.png)
:::

## 
## Loc
### Basics
:::info
![image.png](./Lectures_Readings.assets/20230302_2123114085.png)
:::

### Loc with Lists
:::info
![image.png](./Lectures_Readings.assets/20230302_2123117041.png)![image.png](./Lectures_Readings.assets/20230302_2123112438.png)
:::


### Loc with Slices
:::info
![image.png](./Lectures_Readings.assets/20230302_2123126678.png)![image.png](./Lectures_Readings.assets/20230302_2123121040.png)
:::

### Loc with Single Values
:::info
![image.png](./Lectures_Readings.assets/20230302_2123122510.png)![image.png](./Lectures_Readings.assets/20230302_2123126838.png)![image.png](./Lectures_Readings.assets/20230302_2123128297.png)![image.png](./Lectures_Readings.assets/20230302_2123131974.png)![image.png](./Lectures_Readings.assets/20230302_2123133312.png)
:::


### Loc with Boolean Array
:::info
![image.png](./Lectures_Readings.assets/20230302_2123132391.png)![image.png](./Lectures_Readings.assets/20230302_2123139030.png)
:::


### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2123132392.png)
:::


## iloc
### Basics
:::info
![image.png](./Lectures_Readings.assets/20230302_2123133118.png)
**注意: **`**iloc slicing**`**是**`**exclusive**`**的。**
:::

### Challenges
:::info
![image.png](./Lectures_Readings.assets/20230302_2123147250.png)
:::
**Solution**![image.png](./Lectures_Readings.assets/20230302_2123148213.png)


### Samples
:::info
![image.png](./Lectures_Readings.assets/20230302_2123148677.png)
:::


### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2123142234.png)![image.png](./Lectures_Readings.assets/20230302_2123145351.png)
:::



## Pandas Utility Functions
### Numpy Operations
:::info
![image.png](./Lectures_Readings.assets/20230302_2123145063.png)![image.png](./Lectures_Readings.assets/20230302_2123151008.png)
:::


### head/size/shape/describe
:::info
![image.png](./Lectures_Readings.assets/20230302_2123153942.png)![image.png](./Lectures_Readings.assets/20230302_2123152136.png)
:::


### DataFrame.index/column
:::info
![image.png](./Lectures_Readings.assets/20230302_2123157644.png)![image.png](./Lectures_Readings.assets/20230302_2123156681.png)
:::


### sort_values
:::info
![image.png](./Lectures_Readings.assets/20230302_2123152770.png)![image.png](./Lectures_Readings.assets/20230302_2123153469.png)
:::

### Series.value_counts
:::info
![image.png](./Lectures_Readings.assets/20230302_2123165886.png)
:::


### Series.unique
:::info
![image.png](./Lectures_Readings.assets/20230302_2123163476.png)
`DataFrame`没有`unique`。
:::


### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2123164746.png)![image.png](./Lectures_Readings.assets/20230302_2123164940.png)
`DataFrame`没有`value_counts()`方法，所以报错。
:::


# 2 Pandas Advanced
[6. Pandas 2.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673679069244-b505f346-52aa-4d76-9d00-2c5b95176c59.pdf)
[lec06.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/12393765/1673679844016-a5376919-aade-4e0b-b795-d5afb8475d9b.zip)


## Data
:::info
![image.png](./Lectures_Readings.assets/20230302_2123166903.png)
:::

## Pandas String Methods
### Intro Example
:::info
![image.png](./Lectures_Readings.assets/20230302_2123163021.png)![image.png](./Lectures_Readings.assets/20230302_2123171506.png)
:::



### Str Methods
:::info
![image.png](./Lectures_Readings.assets/20230302_2123179803.png)![image.png](./Lectures_Readings.assets/20230302_2123178406.png)![image.png](./Lectures_Readings.assets/20230302_2123175900.png)
:::


### Challenges
:::info
![image.png](./Lectures_Readings.assets/20230302_2123179033.png)![image.png](./Lectures_Readings.assets/20230302_2123187656.png)
:::


### Quick Check
:::info
**Guide:** [series.str.split](https://pandas.pydata.org/pandas-docs/stable/user_guide/text.html#splitting-and-replacing-strings)
:::
:::info
![image.png](./Lectures_Readings.assets/20230302_2123186292.png)![image.png](./Lectures_Readings.assets/20230302_2123181498.png)
:::

## Sort columns
### Approach 1: Create Temporary Columns
#### Sort the name length
> ![image.png](./Lectures_Readings.assets/20230302_2123185976.png)

:::info
![image.png](./Lectures_Readings.assets/20230302_2123181816.png)![image.png](./Lectures_Readings.assets/20230302_2123186678.png)![image.png](./Lectures_Readings.assets/20230302_2123191582.png)
:::


#### Sort arbitrary substr
:::info
![image.png](./Lectures_Readings.assets/20230302_2123192207.png)
:::



### Approach 2: Create a sorted Index with loc
:::info
![image.png](./Lectures_Readings.assets/20230302_2123195411.png)![image.png](./Lectures_Readings.assets/20230302_2123191907.png)![image.png](./Lectures_Readings.assets/20230302_2123198973.png)
:::



### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2123207474.png)
:::



## Aggregation
### Goal
:::info
![image.png](./Lectures_Readings.assets/20230302_2123204016.png)![image.png](./Lectures_Readings.assets/20230302_2123209132.png)
:::


### For Loop(Bad)
:::info
![image.png](./Lectures_Readings.assets/20230302_2123201728.png)![image.png](./Lectures_Readings.assets/20230302_2123205704.png)
**Access variables in python within queries:  **`**@variable**`** **
![image.png](./Lectures_Readings.assets/20230302_2123215727.png)
:::


### Groupby and agg
:::info
![image.png](./Lectures_Readings.assets/20230302_2123217134.png)![image.png](./Lectures_Readings.assets/20230302_2123216070.png)![image.png](./Lectures_Readings.assets/20230302_2123213863.png)![image.png](./Lectures_Readings.assets/20230302_2123213393.png)
:::


### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2123215535.png)![image.png](./Lectures_Readings.assets/20230302_2123222664.png)
:::


## Groupby Puzzles
### Puzzle 1 Changed Intention
:::info
![image.png](./Lectures_Readings.assets/20230302_2123229530.png)
这个本质上求的是，`Difference between the least popular name and the most popular name`
:::


### Puzzle 2 Independent Calculations
:::info
![image.png](./Lectures_Readings.assets/20230302_2123222577.png)![image.png](./Lectures_Readings.assets/20230302_2123229821.png)
:::


### Puzzle 3 Independent Calculations
:::info
![image.png](./Lectures_Readings.assets/20230302_2123224608.png)![image.png](./Lectures_Readings.assets/20230302_2123236131.png)
:::


### Puzzle 4 Against the Independence⭐⭐⭐⭐⭐
:::info
![image.png](./Lectures_Readings.assets/20230302_2123232466.png)![image.png](./Lectures_Readings.assets/20230302_2123231357.png)
:::



### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2123234876.png)![image.png](./Lectures_Readings.assets/20230302_2123241135.png)
:::



## Other groupby Features
### return type of groupby()
:::info
![image.png](./Lectures_Readings.assets/20230302_2123241217.png)
:::



### .size()⭐⭐⭐⭐
:::info
![image.png](./Lectures_Readings.assets/20230302_2123247333.png)![image.png](./Lectures_Readings.assets/20230302_2123241725.png)
注意, `.size()`返回的是`Series`类型的数据。
:::



### filter by group⭐⭐⭐⭐
:::info
![image.png](./Lectures_Readings.assets/20230302_2123248031.png)![image.png](./Lectures_Readings.assets/20230302_2123245661.png)![image.png](./Lectures_Readings.assets/20230302_2123252491.png)![image.png](./Lectures_Readings.assets/20230302_2123255028.png)
`filter`最终的结果不是以组别为单位的， 而是以`row`为单位的。即，如果某个组别满足某些条件，则这个组别内的所有`rows`都会出现在结果集中。
:::


### Simplification⭐⭐
:::info
![image.png](./Lectures_Readings.assets/20230302_2123254546.png)
:::


### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2123254137.png)![image.png](./Lectures_Readings.assets/20230302_2123258926.png)![image.png](./Lectures_Readings.assets/20230302_2123262590.png)
:::


## Group by multiple columns
### Multi-Index
:::info
![image.png](./Lectures_Readings.assets/20230302_2123265176.png)
本质上`Multi-index`会列出所有的`Cartesian Product of multi-indices`
:::


### Pivot Tables
:::info
![image.png](./Lectures_Readings.assets/20230302_2123268830.png)![image.png](./Lectures_Readings.assets/20230302_2123262332.png)![image.png](./Lectures_Readings.assets/20230302_2123268167.png)
:::


### Multi-index vs Pivot Tables
:::info
![image.png](./Lectures_Readings.assets/20230302_2123261318.png)
:::



### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2123265852.png)![image.png](./Lectures_Readings.assets/20230302_2123279563.png)![image.png](./Lectures_Readings.assets/20230302_2123273785.png)![image.png](./Lectures_Readings.assets/20230302_2123279889.png)
:::


## Joins
:::info
![image.png](./Lectures_Readings.assets/20230302_2123274224.png)![image.png](./Lectures_Readings.assets/20230302_2123277277.png)
:::


### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2123275039.png)
![image.png](./Lectures_Readings.assets/20230302_2123273579.png)![image.png](./Lectures_Readings.assets/20230302_2123277373.png)
:::
