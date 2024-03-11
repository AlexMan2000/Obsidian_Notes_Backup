# lvalues and rvalues
> [!important]
> ![](Move_Semantics.assets/image-20240118203131503.png)![](Move_Semantics.assets/image-20240118204415284.png)

> [!example] Example 1
> ![](Move_Semantics.assets/image-20240118203227984.png)
> 1. `2` is a rvalue, `val` is a lvalue
> 2. `0x02248837` is an rvalue, `int* ptr` is a lvalue.
> 3. `v1` is a lvalue
> 4. `v1` is a lvalue, it is a name(identity), can find the address. `v2` is also a lvalue for the same reason. `v1 + v2` returns a temporary vector, which is an rvalue. `v4` is a lvalue.
> 5. both `v1` and `v4` are lvalue.
> 6. `size` is lvalue. `v.size()` is rvalue(integer returned by a function)
> 7. `static_cast<int>(size)` is an rvalue. `val` is lvalue.
> 8. `v1[1]` is lvalue since we can find its address. Alternative explanation would be that `v1[1]` call the `operator[]` that returns a reference, which is a name(variable that points to something).
> 9. `&val` is an rvalue. `ptr` is lvalue.
> 10. `v1[2]` is a lvalue(explained above), `*ptr` is lvalue since we can do such thing as `*ptr = 2`.
> 
> ![](Move_Semantics.assets/image-20240118204633822.png)


# lvalue/rvalue references
## Reference Recap
> [!important]
> ![](Move_Semantics.assets/image-20240118214808299.png)



## lvalue vs rvalue references
> [!concept]
> ![](Move_Semantics.assets/image-20240118211217693.png)![](Move_Semantics.assets/image-20240118211315768.png)

> [!example] Example 1
> ![](Move_Semantics.assets/image-20240118204648132.png)
> Can only bind lvalue to lvalue reference and rvalue to rvalue reference.
> 
> **Can also bind  rvalue to const lvalue reference.**
> ![](Move_Semantics.assets/image-20240118211412547.png)

> [!example] Example 2
> ![](Move_Semantics.assets/image-20240118211143520.png)


> [!example] Example 3: r-value reference is lvalue
> ![](Move_Semantics.assets/image-20240118211541316.png)


## Summary
> [!summary]
> ![](Move_Semantics.assets/image-20240118211557114.png)





# Move Semantics
## Motivation
> [!motiv] Motivation






## Key Idea
> [!important]
> 



> [!important]
> ![](Move_Semantics.assets/image-20240118210913753.png)![](Move_Semantics.assets/image-20240118211702175.png)
> By moving from obj2 to obj1, we are promising not to use the name obj2 ever and obj1 takes control of the variable.



## std::move
> [!def]
> ![](Move_Semantics.assets/image-20240307153550861.png)

> [!important]
> Inside `<utility>` library.
> 
> Consider the following implementation of move assignment member function, we see some inefficiencies here:
> ![](Move_Semantics.assets/image-20240118213220013.png)![](Move_Semantics.assets/image-20240118213230098.png)![](Move_Semantics.assets/image-20240118213315164.png)
> One way of doing this is using casting:
> 
> ![](Move_Semantics.assets/image-20240118213338565.png)
> But C++ provides more powerful built-in algorithm to do this:
> 
> ![](Move_Semantics.assets/image-20240118213358477.png)
> More on `std::move`:
> 
> ![](Move_Semantics.assets/image-20240118213725557.png)![](Move_Semantics.assets/image-20240118213737328.png)![](Move_Semantics.assets/image-20240118213752982.png)


## Move Construct/Assign
> [!def]
> ![](Move_Semantics.assets/image-20240307153906169.png)
> Note that here there is no `const` for the parameter.



### Move Constructor
> [!def]
> ![](Move_Semantics.assets/image-20240307154251295.png)![](Move_Semantics.assets/image-20240307154451448.png)
> An equivalent way of setting up `pi` field is to use `std::exchange`:
> 
> ![](Move_Semantics.assets/image-20240307154501840.png)
> `ptr(std::exchange(new_ptr, null_ptr))`, set `ptr` to `new_ptr` and `new_ptr` to `nul_ptr`.

> [!important]
> It creates new from existing rvalue. Note that r-value reference is an l-value.
> 
> The inefficient implementation would be:
> ![](Move_Semantics.assets/image-20240118213543381.png)
> Using `std::move` we have:
> 
> ![](Move_Semantics.assets/image-20240118213609556.png)
> 
> Note that here we are using initializer list syntax.





### Move Assignment
> [!important]
> It overwrites existing from existing r-value.
> ![](Move_Semantics.assets/image-20240118213539165.png)
> Using `std::move` we have:
> 
> ![](Move_Semantics.assets/image-20240118213627265.png)


## Core Guideline C.64 - Valid State
> [!def]
> ![](Move_Semantics.assets/image-20240307160306227.png)![](Move_Semantics.assets/image-20240307160336392.png)![](Move_Semantics.assets/image-20240307160759811.png)
> If field `pi` is using `unique_ptr`, then phase 2 can be omitted:
> 
> ![](Move_Semantics.assets/image-20240307160845957.png)








### Core Guideline C.66 - noexcept
> [!def]
> ![](Move_Semantics.assets/image-20240307154706946.png)
> ![](Move_Semantics.assets/image-20240307155250506.png)
> `noexcept` basically means no exception. Adding it will not affect the correctness of the code while improve the performance.
> 
> ![](Move_Semantics.assets/image-20240307155437287.png)
> Here `push_back` gives you **strong exception safety guarantee** such that if any exceptions is thrown from `push_back` function, it acts like nothing has happened at all. Much like the rolling back of commit in database.



## Vector Example
> [!code]
> ![](Move_Semantics.assets/image-20240308201636524.png)



## Quick Quiz
> [!problem]
> ![](Move_Semantics.assets/image-20240118214037725.png)![](Move_Semantics.assets/image-20240118220552262.png)![](Move_Semantics.assets/image-20240118220558632.png)![](Move_Semantics.assets/image-20240118220617001.png)



## Applications
> [!example] Example 1: Boost Efficiency
> ![](Move_Semantics.assets/image-20240118213908260.png)![](Move_Semantics.assets/image-20240118213919089.png)![](Move_Semantics.assets/image-20240118213936192.png)![](Move_Semantics.assets/image-20240118214000925.png)


> [!example] Example 2: Generic Swap Function
> ![](Move_Semantics.assets/image-20240118214428849.png)
> Using Reference(all the ='s are copy constructor/assignment).
> 
> ![](Move_Semantics.assets/image-20240118215930345.png)
> Using `std::move`(all the ='s are move constructor/assignment):
> 
> ![](Move_Semantics.assets/image-20240118220005884.png)
























