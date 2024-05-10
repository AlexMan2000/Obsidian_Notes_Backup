# The rule of Three
> [!thm]
> ![](Special%20Member%20Functions.assets/image-20240118155548944.png)


# Copy Construction
> [!def]
> The reason for copy constructor is to avoid double freeing problem in C++. Also part of the Rule of Three. 


## Default Copy Constructor
> [!important]
> If we don't provide our own copy constructor, C++ *__sometimes__* will create a default one for us. But **the default one only do shallow copy**, which means it only copies the primitive types correctly, as shown below:
> ![](Special%20Member%20Functions.assets/image-20240118155220353.png)
> 
> Any reference type, pointer, object are not guaranteed to be deep copied. In this case, if we have `Obj obj1 = obj2`, when obj1's internal state is modified, obj2's will also be subjective to change, as the example below shows:
> ![](Special%20Member%20Functions.assets/image-20240118155159798.png)


## When C++ doesn't provide Default Constructor
> [!important]
> There are a few circumstances where C++ does not automatically provide default copy constructors and assignment operators. If your class contains a reference or const variable as a data member, your class will not automatically get an assignment operator. Similarly, if your class has a data member that doesn't have a copy constructor or assignment operator (for example, an ifstream ), your class won't be copyable.
> 
> There is one other case involving inheritance where C++ won't automatically create the copy functions for you, and in the chapter on inheritance we'll see how to exploit this to disable copying.


## Write good copy constructor
> [!important]
> There are two ways to write the copy constructor, the first way is the following:
> ![](Special%20Member%20Functions.assets/image-20240118160329017.png)
> Note that here we are accessing `Vector`'s private field through an object. This is legal because of sibling access feature in C++, which is that:
> 
> **A class can access both its private fields and private fields of other objects of the same type. This is called sibling access and is true of any member function, not just the copy constructor. If the copy constructor were not a member of Vector or if other were not a Vector , this code would not be legal.**
> 
> An alternative means for copying data over from the other object uses the STL copy algorithm. Recall that copy takes three parameters – two delineating an input range of iterators and one denoting the beginning of an output range – then copies the specified iterator range to the destination. 
> ![](Special%20Member%20Functions.assets/image-20240118160524340.png)


## Doubling Freeing Problem
> [!important]
> Consider the following codes, which is very problematic:
> ![](Special%20Member%20Functions.assets/image-20240118161224063.png)
> **There are two things that is bug-prone:**
> 1. `vector<int> copy = vec` calls the default copy constructor from C++ standard library, where since `vec` contains `int * elems` field, the deault copy constructor would just shallow copy it, resulting in referencing issues.
> 2. When the function is returned, `vec`'s destructor, `copy`'s destructor is invoked, which means `int* elems` is freed at least twice. In other words, when the vectors go out of scope, their destructor tries to free the array.





# Copy Assignment
> [!def]
> Copy assignment is used to deal with both double freeing and resource freeing.
> ![](Special%20Member%20Functions.assets/image-20240307151517032.png)




## Write good assignment operator
> [!important]
> There are three things we need to pay attention when writing assignment operator:
> 1. We must clear up the memory of the current object.
> 2. We must check for self-assignment. That is, if `other` refers to the same object as the caller object of `operator=(const Obj& other)`, we should not do anything.
> 3. We must support the following syntax `one = (two = three)`, which means our assignment operator function must have a return value.
> 
> With all of the three things in mind, we have the follow canonical implementation:
> ![](Special%20Member%20Functions.assets/image-20240118212204144.png)![](Special%20Member%20Functions.assets/image-20240118212155561.png)![](Special%20Member%20Functions.assets/image-20240118160919254.png)


