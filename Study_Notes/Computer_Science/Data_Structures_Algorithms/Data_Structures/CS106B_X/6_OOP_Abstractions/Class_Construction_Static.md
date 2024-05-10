# How C++ Construct Objects - pp266 ~ 269 
## Without Initializer List
> [!important]
> ![](Class_Construction_Static.assets/image-20240118112713620.png)

### Step 1: Allocate Memory
> [!concept]
> ![](Class_Construction_Static.assets/image-20240118112748196.png)



### Step 2: Call Members' Default Constructors
> [!concept]
> C++ will call default constructor for each non-primitive types and initilize their values while leaving primitive type field unchanged.
> ![](Class_Construction_Static.assets/image-20240118112850034.png)

### Step 3: Call Object's Constructor
> [!concept]
> ![](Class_Construction_Static.assets/image-20240118112909558.png)![](Class_Construction_Static.assets/image-20240118112916022.png)



## With Member Initializer List
> [!concept]
> ![](Class_Construction_Static.assets/image-20240118113006643.png)


### Step 1: Allocate Memory
> [!concept]
> ![](Class_Construction_Static.assets/image-20240118113025896.png)


### Step 2: Call Members' Constructors with parameters
> [!concept]
> ![](Class_Construction_Static.assets/image-20240118113121745.png)![](Class_Construction_Static.assets/image-20240118113125596.png)
> This step turns out to be extremely useful when the field doesn't have default constructor.


### Step 3: Call Object's Constructor
> [!concept]
> ![](Class_Construction_Static.assets/image-20240118113144284.png)



## Passing Parameters in Member Initializer Lists - pp269 ~ 270
> [!important]
> ![](Class_Construction_Static.assets/image-20240118113419476.png)![](Class_Construction_Static.assets/image-20240118113426560.png)


# When Initializer Lists are Mandatory
## Case 1: Initialize Const Variable
> [!important]
> ![](Class_Construction_Static.assets/image-20240118113631968.png)![](Class_Construction_Static.assets/image-20240118113642808.png)

 
## Case 2: Field without Default Constructor
> [!important]
> ![](Class_Construction_Static.assets/image-20240118114011281.png)



## Multiple Constructors Caveasts
> [!important]
> ![](Class_Construction_Static.assets/image-20240118114137788.png)


# std::initializer_list
>[!important] 
>![](Class_Construction_Static.assets/image-20240121113617855.png)![](Class_Construction_Static.assets/image-20240121113621773.png)







# Static Keyword in Class
## Static Data Members



## Static Member Functions