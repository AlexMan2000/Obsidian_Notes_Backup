# Overview
## Index
> [!concept]
> ![](File_Index_Management.assets/image-20240124134301771.png)![](File_Index_Management.assets/image-20240124134309949.png)



# B-plus Tree Index
## Key Idea
> [!important]
> ![](File_Index_Management.assets/image-20240124145420327.png)![](File_Index_Management.assets/image-20240124145503359.png)


## B Tree Nodes
> [!concept] Interior Node
> ![](File_Index_Management.assets/image-20240124141940616.png)

> [!concept] Leaf Nodes
> Note: Leaf node's entry keeps the pointer to a particular record.
> ![](File_Index_Management.assets/image-20240124145034442.png)





## B Tree Properties
> [!property] Occupant Invariant
> ![Figure 1](File_Index_Management.assets/image-20240124142205540.png)
> **B+ Tree Invariant(Order):** each interior node is full beyond a certain minimum: in this case [and typically], at least half full:
> - This minimum, d, is called the **order** of the tree.
> - In Figure 1, max # of entries = 4(page 9). Thus d = 2.
> - **Guarantee:** d <= # entries <= 2d. In this tree, 2 <= # entries <= 4.
> 
> ![](File_Index_Management.assets/image-20240124142814568.png)![](File_Index_Management.assets/image-20240124142828828.png)
> **Several Properties of B+ Tree:**
> - The number d is the order of a B+ tree. Each node (**with the exception of the root node**) must have d ≤ x ≤ 2d entries **assuming no deletes happen** (it’s possible for leaf nodes to end up with < d entries if you delete data). **The entries within each node must be sorted.**
> - In between each entry of an inner node, there is a pointer to a child node. Since there are at most 2d entries in a node, inner nodes may have at most 2d + 1 child pointers. This is also called the **tree’s fanout**. 
> - The keys in the children to the left of an entry must be less than the entry while the keys in the children to the right must be **greater than or equal to** the entry

> [!property] Non-sequential Page Storage
> ![Figure 2](File_Index_Management.assets/image-20240124143516577.png)
> Leaf pages at bottom need not be stored in sequence in logical order.
> - In figure 2, we have page 2, 3 at the leaf node, but page 4 being the parent, which indicates that page doesn't have to be stored in sequential order.
> - Next and prev. pointers help examining them in sequence.



## B Tree and Scale 
> [!concept]
> ![](File_Index_Management.assets/image-20240124143755633.png)![](File_Index_Management.assets/image-20240124143802066.png)
> **Note:** Tree geight starts from 0 from leaf node of the B+ tree.
> 
> ![](File_Index_Management.assets/image-20240124144452195.png)



# B Plus Tree Operations
## Searching
> [!important]
> ![](File_Index_Management.assets/image-20240124150259808.png)![](File_Index_Management.assets/image-20240124150308596.png)![](File_Index_Management.assets/image-20240124150336307.png)
> This is the benefit brought by the doubly linked list at the leaf level.









## Insertion




## Deletion