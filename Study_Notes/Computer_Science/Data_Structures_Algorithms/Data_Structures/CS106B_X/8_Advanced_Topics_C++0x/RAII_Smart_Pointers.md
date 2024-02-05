# RAII
## Principles
> [!concept]
> ![](Exceptions.assets/image-20240124123615482.png)![](Exceptions.assets/image-20240124123635344.png)

## RAII Compliant
> [!example] Stream
> ![](Exceptions.assets/image-20240124123758813.png)![](Exceptions.assets/image-20240124123912793.png)
> The fact that stream is RAII compliant make sure once the stream is opened, even if the program throws exceptions in the middle, the stream will finally be closed. So from the user's perspective, we don't actually have to explicitly call `close()`.


# Smart Pointers
> [!overview]
> ![](Exceptions.assets/image-20240124124126870.png)
> Smart pointers are all RAII-compliant.





## std::unique_ptr
> [!concept]
> ![](RAII_Smart_Pointers.assets/image-20240124125033237.png)
> If we are able to copy, it will cause double free problem:
> 
> ![](RAII_Smart_Pointers.assets/image-20240124125205341.png)![](RAII_Smart_Pointers.assets/image-20240124125221140.png)![](RAII_Smart_Pointers.assets/image-20240124125229433.png)![](RAII_Smart_Pointers.assets/image-20240124125324263.png)



## std::shared_ptr
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

