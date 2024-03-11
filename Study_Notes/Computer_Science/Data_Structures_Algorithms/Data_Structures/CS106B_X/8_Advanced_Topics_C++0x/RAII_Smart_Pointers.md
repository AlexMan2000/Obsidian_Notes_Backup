# RAII
## Definition
> [!def]
> ![](RAII_Smart_Pointers.assets/image-20240307163209883.png)



## Exception Safety
> [!example] Bad Example
> ![](RAII_Smart_Pointers.assets/image-20240307163358756.png)

> [!example] Fix
> ![](RAII_Smart_Pointers.assets/image-20240307163531299.png)




## Principles
> [!concept]
> ![](Exceptions.assets/image-20240124123615482.png)![](Exceptions.assets/image-20240124123635344.png)





## The Rule of Zero
> [!important]
> ![](RAII_Smart_Pointers.assets/image-20240308202031294.png)





## The Rule of Five
> [!important]
> ![](RAII_Smart_Pointers.assets/image-20240308202045717.png)



## The Rule of Four
> [!important]
> ![](RAII_Smart_Pointers.assets/image-20240308202911736.png)


## Vector Example
> [!important]
> ![](RAII_Smart_Pointers.assets/image-20240308202950879.png)




## RAII Compliant
> [!example] Stream
> ![](Exceptions.assets/image-20240124123758813.png)![](Exceptions.assets/image-20240124123912793.png)
> The fact that stream is RAII compliant make sure once the stream is opened, even if the program throws exceptions in the middle, the stream will finally be closed. So from the user's perspective, we don't actually have to explicitly call `close()`.


# Smart Pointers
## Rule of Smart Pointers
> [!important]
> ![](RAII_Smart_Pointers.assets/image-20240308204017251.png)![](Exceptions.assets/image-20240124124126870.png)
> Smart pointers are all RAII-compliant.


## std::unique_ptr
### Exclusive Ownership
> [!def]
> ![](RAII_Smart_Pointers.assets/image-20240307161308927.png)![](RAII_Smart_Pointers.assets/image-20240308203826359.png)



### Array Form 
> [!def]
> ![](RAII_Smart_Pointers.assets/image-20240308203905215.png)


### Deleter Template
> [!def]
> ![](RAII_Smart_Pointers.assets/image-20240308203941282.png)





> [!concept]
> ![](RAII_Smart_Pointers.assets/image-20240124125033237.png)
> If we are able to copy, it will cause double free problem:
> 
> ![](RAII_Smart_Pointers.assets/image-20240124125205341.png)![](RAII_Smart_Pointers.assets/image-20240124125221140.png)![](RAII_Smart_Pointers.assets/image-20240124125229433.png)![](RAII_Smart_Pointers.assets/image-20240124125324263.png)



## std::shared_ptr
### Reference Count
> [!important]
> ![](RAII_Smart_Pointers.assets/image-20240308204242557.png)![](RAII_Smart_Pointers.assets/image-20240308204342541.png)


### Control Block
> [!def]
> ![](RAII_Smart_Pointers.assets/image-20240308204555097.png)





> [!concept]
> ![](RAII_Smart_Pointers.assets/image-20240124125558380.png)
> When we do `p2 = p1`, we call copy constructor of `std::shared_ptr<int>`.
> 
> The implementation details revolves around `reference counting`:
> 
> ![](RAII_Smart_Pointers.assets/image-20240124125634854.png)



## std::weak_ptr
> [!concept]
> ![](RAII_Smart_Pointers.assets/image-20240124125901553.png)

