# Generics
> [!concept]
> ![](Generics_Function_Pointers.assets/image-20231211151258065.png)


# Swap Elements
## Swap two ints
> [!code]
> ![](Generics_Function_Pointers.assets/image-20231211151327004.png)


## Swap two shorts
> [!code]
> ![](Generics_Function_Pointers.assets/image-20231211151353659.png)



## Swap two strings
> [!code]
> ![](Generics_Function_Pointers.assets/image-20231211151408815.png)



# Generic Swap - void*/memcpy/memmove
> [!important]
> ![](Generics_Function_Pointers.assets/image-20231211151447156.png)
> The goal is this chapter is to create just ==one== generic function(using function pointers) that could handle all the cases above instead of writing individual pieces of code to consider for all input cases.


## Step 1: Change method signature
> [!code]
> ![](Generics_Function_Pointers.assets/image-20231211151534636.png)
> So that we want to transform our code into the following:
> 
> ![](Generics_Function_Pointers.assets/image-20231211151606848.png)
> For these three lines, we have to tackle two problems:
> - Line 1: Each type may need a different size temp.
> - Line 2: Each type needs to copy a different amount of data.
> - Line 3: Each type needs to copy a different amount of data.
> 
> ![](Generics_Function_Pointers.assets/image-20231211151853330.png)
> C knows the size of `temp`, inferring from its static type, and knows how many bytes to replicate, because of the variable types. But is there a way to make a version that doesn't care about the variable types?
> 
> The answer in that we could use `void*` as the pointer to data, `void *` doesn't make any assumption on the size of the data, and thus we cannot use static typing to infer the size of data. So we should introduce a new parameter that indicates the size of the data we are dealing with, which gives the following codes:
> ![](Generics_Function_Pointers.assets/image-20231211152217595.png)



## Step 2: Change function body - memcpy/memmove
> [!code]
> Now the second problem is that we want to first copy the data 1 to some temporary variable. Doing this requires:
> 1. We have someplace to store data 1. Since data1 is of `nbytes`, we could create a buffer `char buf[nbytes]` to hold data1.
> 2. We have to read data 1. The first thought would be dereferencing the `data1ptr`, but note that `void*` could indicate any data types and thus may access arbitrary amount/location of memory space, which may cause segment fault. **Moreover, C doesn’t know what it points to! Therefore, it doesn’t know how many bytes there it should be looking at.**
> 
> The solution turns out to be rather simple, just using the `memcpy/memmove` function provided by standard C library.
> ![](Generics_Function_Pointers.assets/image-20231211152811177.png)![](Generics_Function_Pointers.assets/image-20231211152902132.png)![](Generics_Function_Pointers.assets/image-20231211152921589.png)
> Finally, our code becomes:
> 
> ![](Generics_Function_Pointers.assets/image-20231211153031146.png)




## Design of memcpy and memmove
> [!concept]
> ![](Generics_Function_Pointers.assets/image-20231211153214396.png)



## Void* Pitfalls
> [!important]
> ![](Generics_Function_Pointers.assets/image-20231211153313226.png)![](Generics_Function_Pointers.assets/image-20231211153317624.png)



# Generic Swap Array Elements
## Generic Implementation - Type Casting
> [!motiv] Motivation
> ![](Generics_Function_Pointers.assets/image-20231212150326628.png)
> Now we can use the swap element function written above and replace the body of swap_ends_int():
> 
> ![](Generics_Function_Pointers.assets/image-20231212150508854.png)
> Other version of the swap looks like the following:
> 
> ![](Generics_Function_Pointers.assets/image-20231212150559622.png)


> [!code]
> We want to rewrite the following function to support any types:
> ![](Generics_Function_Pointers.assets/image-20231212150922980.png)
> The first idea that comes up should be using `void *`, since it can potentially be any types, it's just that we don't know exactly which type it will be. So let's modify the first argument type to be statically `void*`:
> 
> ![](Generics_Function_Pointers.assets/image-20231212151033025.png)
> It is generic for sure, but it doesn't work. Since in the function we have `arr + nelems - 1` which means we are doing pointer arithmetics. But pointer arithmetics depends on the type of data being pointed to, with `void*` we will lose that information. So we need to know the element size, which prompt us to add a paramter as follows:
> 
> ![](Generics_Function_Pointers.assets/image-20231212151225337.png)
> Now in order to get to the last element of the arr, we would have to perform certain kind of pointer arithmetics, like `arr + some bytes`, since we already know the total number of elements in the array and the size of each elements. If we could move one byte at a time, the pointer arithmetic would be `arr + (nelems - 1) * elem_bytes`. So the last missing piece of the function should be to make the pointer access the memory one byte when we perform `arr + 1`, which can be realized using type casting feature:
> 
> ![](Generics_Function_Pointers.assets/image-20231212151911045.png)![](Generics_Function_Pointers.assets/image-20231212151944669.png)![](Generics_Function_Pointers.assets/image-20231212151956348.png)![](Generics_Function_Pointers.assets/image-20231212152002483.png)



## Array Rotations
> [!example]
> ![](Generics_Function_Pointers.assets/image-20231212152313970.png)![](Generics_Function_Pointers.assets/image-20231212152318591.png)![](Generics_Function_Pointers.assets/image-20231212152324546.png)


# Integer Bubble Sort - Function Pointer
## Integer Version
> [!concept] Implementation Idea
> ![](Generics_Function_Pointers.assets/image-20231212153000606.png)![](Generics_Function_Pointers.assets/image-20231212153104252.png)![](Generics_Function_Pointers.assets/image-20231212153116397.png)


## Generic on Swap
> [!important]
> ![](Generics_Function_Pointers.assets/image-20231212153227337.png)![](Generics_Function_Pointers.assets/image-20231212153441428.png)
> So our function should look like this:
> 
> ![](Generics_Function_Pointers.assets/image-20231212153501371.png)
> Back to the bubble sort function, we could do the following modifications:
> 
> ![](Generics_Function_Pointers.assets/image-20231212153554797.png)![](Generics_Function_Pointers.assets/image-20231212153617747.png)
> If we want to sort the element according to there absolute value, then we can do the following:
> 
> ![](Generics_Function_Pointers.assets/image-20231212153710343.png)


## Function Pointer Details
> [!concept]
> ![](Generics_Function_Pointers.assets/image-20231212153744686.png)![](Generics_Function_Pointers.assets/image-20231212153751143.png)


## Comparison Functions
> [!important]
> ![](Generics_Function_Pointers.assets/image-20231212153826499.png)![](Generics_Function_Pointers.assets/image-20231212153831862.png)![](Generics_Function_Pointers.assets/image-20231212153854197.png)




# Generic Bubble Sort
> [!motiv] Motivation
> ![](Generics_Function_Pointers.assets/image-20231212154003849.png)![](Generics_Function_Pointers.assets/image-20231212154012093.png)


## Generic Parameters
> [!concept]
> ![](Generics_Function_Pointers.assets/image-20231212154053187.png)![](Generics_Function_Pointers.assets/image-20231212154129953.png)



## Generify Bubble Sort
> [!important]
> Given the original function:
> ![](Generics_Function_Pointers.assets/image-20231212154246355.png)
> We first generify the element type by making arr type arbitrary, setting to `void *`:
> 
> ![](Generics_Function_Pointers.assets/image-20231212154258670.png)
> In order to call our generic version of `swap_array_element`, we need to match its parameter static type as follows:
> 
> ![](Generics_Function_Pointers.assets/image-20231212154441902.png)
> Then, let's generify the comparater function as follows:
> 
> ![](Generics_Function_Pointers.assets/image-20231212154635118.png)
> Finally, the comparator function:
> 
> ![](Generics_Function_Pointers.assets/image-20231212155010620.png)![](Generics_Function_Pointers.assets/image-20231212155023334.png)![](Generics_Function_Pointers.assets/image-20231212155038583.png)![](Generics_Function_Pointers.assets/image-20231212155105654.png)


## Function Pointer Pitfalls
> [!important]
> ![](Generics_Function_Pointers.assets/image-20231212155217449.png)![](Generics_Function_Pointers.assets/image-20231212155516807.png)
> It wil return the wrong answer, since the logic of comparison is different from other types.


































