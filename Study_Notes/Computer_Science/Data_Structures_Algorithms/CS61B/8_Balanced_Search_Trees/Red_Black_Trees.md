[cs61b 2019 lec18 ds4 balanced search trees.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1676002780207-f5ee7d1a-2acc-43e8-b700-6ccae01a46f6.pdf)
# Recap
> ![image.png](Red_Black_Trees.assets/20230324_1528168848.png)



# Tree Rotation
> ![image.png](Red_Black_Trees.assets/20230324_1528169086.png)



## Definition
### rotateLeft
> ![image.png](Red_Black_Trees.assets/20230324_1528167363.png)![image.png](Red_Black_Trees.assets/20230324_1528176133.png)


### rotateRight
> ![image.png](Red_Black_Trees.assets/20230324_1528173044.png)![image.png](Red_Black_Trees.assets/20230324_1528174928.png)



## BST Exercise
> ![image.png](Red_Black_Trees.assets/20230324_1528175637.png)![image.png](Red_Black_Trees.assets/20230324_1528175493.png)



## Rotation for Balanace
> ![image.png](Red_Black_Trees.assets/20230324_1528173421.png)

**Demo**![image.png](Red_Black_Trees.assets/20230324_1528171377.png)![image.png](Red_Black_Trees.assets/20230324_1528178466.png)![image.png](Red_Black_Trees.assets/20230324_1528176413.png)![image.png](Red_Black_Trees.assets/20230324_1528186563.png)![image.png](Red_Black_Trees.assets/20230324_1528182429.png)![image.png](Red_Black_Trees.assets/20230324_1528184621.png)![image.png](Red_Black_Trees.assets/20230324_1528183368.png)![image.png](Red_Black_Trees.assets/20230324_1528185439.png)![image.png](Red_Black_Trees.assets/20230324_1528187025.png)![image.png](Red_Black_Trees.assets/20230324_1528198580.png)

## Simplified Implementation
> ![image.png](Red_Black_Trees.assets/20230324_1528198040.png)

```java
private Node rotateRight(Node h) {
    // assert (h != null) && isRed(h.left);
    Node x = h.left;
    h.left = x.right;
    x.right = h;
    return x;
}
```
```java
// make a right-leaning link lean to the left
private Node rotateLeft(Node h) {
    // assert (h != null) && isRed(h.right);
    Node x = h.right;
    h.right = x.left;
    x.left = h;
    return x;
}
```


# Red Black Tree
## Goal
> ![image.png](Red_Black_Trees.assets/20230324_1528197355.png)


## 2-3 Tree as BST
> ![image.png](Red_Black_Trees.assets/20230324_1528195365.png)



### Dummy Node
> ![image.png](Red_Black_Trees.assets/20230324_1528193303.png)


### Glue Links - LLRB
> ![image.png](Red_Black_Trees.assets/20230324_1528197602.png)


## LLRB Definition
### Definition
> ![image.png](Red_Black_Trees.assets/20230324_1528209234.png)


### LLRB Exercises⭐⭐⭐⭐
#### Construct LLRB from 2-3 Tree
> ![image.png](Red_Black_Trees.assets/20230324_1528201528.png)

**Solution**![image.png](Red_Black_Trees.assets/20230324_1528202860.png)![image.png](Red_Black_Trees.assets/20230324_1528207412.png)


#### Correspondence to 2-3 Tree
> ![image.png](Red_Black_Trees.assets/20230324_1528203859.png)

**Solution**![image.png](Red_Black_Trees.assets/20230324_1528201458.png)
#### 
## LLRB Properties
> ![image.png](Red_Black_Trees.assets/20230324_1528216286.png)


### LLRB Height
#### Specific Example
> ![image.png](Red_Black_Trees.assets/20230324_1528213090.png)

**Solution**![image.png](Red_Black_Trees.assets/20230324_1528216384.png)


#### Maximum Height
> ![image.png](Red_Black_Trees.assets/20230324_1528217484.png)

**Solution**![image.png](Red_Black_Trees.assets/20230324_1528214047.png)

### Other handy properties
> ![image.png](Red_Black_Trees.assets/20230324_1528211532.png)![image.png](Red_Black_Trees.assets/20230324_1528213006.png)


### Summary
> ![image.png](Red_Black_Trees.assets/20230324_1528219217.png)


## LLRB Construction
> ![image.png](Red_Black_Trees.assets/20230324_1528226165.png)



# Red Black Tree Insertion
## Design Principle
> ![image.png](Red_Black_Trees.assets/20230324_1528228972.png)


## 1 Left Insertion(Red Link)
> ![image.png](Red_Black_Trees.assets/20230324_1528221228.png)

**Solution**![image.png](Red_Black_Trees.assets/20230324_1528222637.png)
因为这是一颗`2-3 Tree`, 所以所有`Node`要有`0`或者大于等于`2`个子节点。于是我们不能在左边加入一个`Black Link`而是要加入一个`Red Link`表示`2-3 Tree`的`Root Node`是`2 3`。

## 2 Right Insertion(RotateLeft)
> ![image.png](Red_Black_Trees.assets/20230324_1528225993.png)

**Solution**![image.png](Red_Black_Trees.assets/20230324_1528227342.png)
> 🔔: 本质上因为我们是`LLRB`（`Left Leaning Red Black Tree`）, 所以任何`Red Link`都必须是朝左斜向下的。


## 3 Double Left Insertion(RotateRight)
> ![image.png](Red_Black_Trees.assets/20230324_1528228100.png)![image.png](Red_Black_Trees.assets/20230324_1528222734.png)

**Solution**![image.png](Red_Black_Trees.assets/20230324_1528232667.png)


## 4 Splitting 4-Node(Color Flip)
> ![image.png](Red_Black_Trees.assets/20230324_1528231858.png)

**Solution**![image.png](Red_Black_Trees.assets/20230324_1528235091.png)
要确保所有到`Leaf Nodes`的`Black Edges`数量都一致。因为`A,C`节点在`Split`之后的`B-Tree`中的深度为`1`，于是从根节点出发到`A`或者`C`最多只能有一个`Black Edge`, 换句话说就是`BA`,`BC`都得是`Black Edge`，且`BG`中只能是`Red Line`。

## Design Summary
> ![image.png](Red_Black_Trees.assets/20230324_1528231963.png)



## Cascading Balance Example
> ![image.png](Red_Black_Trees.assets/20230324_1528234033.png)![image.png](Red_Black_Trees.assets/20230324_1528237619.png)



# LLRB Runtime
## Basics
> ![image.png](Red_Black_Trees.assets/20230324_1528239495.png)




## Implementation
> ![image.png](Red_Black_Trees.assets/20230324_1528233864.png)

```java
private Node put(Node h, Key key, Value val) {
    if (h == null) { return new Node(key, val, RED); }

    int cmp = key.compareTo(h.key);
    if (cmp < 0)      { h.left  = put(h.left,  key, val); }
    else if (cmp > 0) { h.right = put(h.right, key, val); }
    else              { h.val   = val;                    }

    if (isRed(h.right) && !isRed(h.left))      { h = rotateLeft(h);  }
    if (isRed(h.left)  &&  isRed(h.left.left)) { h = rotateRight(h); }
    if (isRed(h.left)  &&  isRed(h.right))     { flipColors(h);      } 

    return h;
}
```


# Search Tree ummary
> ![image.png](Red_Black_Trees.assets/20230324_1528248660.png)![image.png](Red_Black_Trees.assets/20230324_1528247220.png)


