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
### Common APIs
> [!important]
> **Create and Initialization:**
> 1. Default Constructor: `std::unique_ptr<int> ptr;`
> 2. Constructor with Raw Pointer: `std::unique_ptr<int> ptr(new int(5));
> 3. Using `std::make_unique(elem)` (preferred): `auto ptr = std::make_unique<int>(5)`. 
> 
> **Accessing the Managed Object:**
> 1. **Dereference** Operator: `*ptr`
> 2. Member **Access** Operator: `ptr->member_func()`
> 
> **Managing Ownership:**
> 1. **Release** Ownership: `int* rawPtr = ptr.release();`
> 2. **Reset**, it will change the raw pointer that will be managed: `ptr.reset(new int(10))` or change it to null `ptr.reset()` so that nothing will be managed by the smart pointer.
> 3. **Swap**: Swaps the managed objects of two `std::unique_ptr` instances.

### Exclusive Ownership and Movable
> [!def]
> ![](RAII_Smart_Pointers.assets/image-20240307161308927.png)![](RAII_Smart_Pointers.assets/image-20240308203826359.png)
```c++
#include <iostream>
#include <memory>

class MyClass {
public:
    MyClass() { std::cout << "MyClass constructor\n"; }
    ~MyClass() { std::cout << "MyClass destructor\n"; }
    void display() const { std::cout << "Displaying MyClass\n"; }
};

int main() {
    // Create a unique_ptr using std::make_unique
    std::unique_ptr<MyClass> ptr1 = std::make_unique<MyClass>();

    // Move construct a new unique_ptr
    std::unique_ptr<MyClass> ptr2 = std::move(ptr1);
    if (!ptr1) {
        std::cout << "ptr1 is now null after move\n";
    }
    if (ptr2) {
        ptr2->display();
    }

    // Move assign to another unique_ptr
    std::unique_ptr<MyClass> ptr3;
    ptr3 = std::move(ptr2);
    if (!ptr2) {
        std::cout << "ptr2 is now null after move\n";
    }
    if (ptr3) {
        ptr3->display();
    }

    return 0;
}

```
> [!exp]
> ![](RAII_Smart_Pointers.assets/image-20240510145550092.png)![](RAII_Smart_Pointers.assets/image-20240510145541079.png)



### Array Form 
> [!def]
> ![](RAII_Smart_Pointers.assets/image-20240308203905215.png)


### Deleter Template
> [!def]
> ![](RAII_Smart_Pointers.assets/image-20240308203941282.png)


### CS106X Slides
> [!concept]
> ![](RAII_Smart_Pointers.assets/image-20240124125033237.png)
> If we are able to copy, it will cause double free problem:
> 
> ![](RAII_Smart_Pointers.assets/image-20240124125205341.png)![](RAII_Smart_Pointers.assets/image-20240124125221140.png)![](RAII_Smart_Pointers.assets/image-20240124125229433.png)![](RAII_Smart_Pointers.assets/image-20240124125324263.png)



## std::shared_ptr
### Common APIs
> [!important]
> ![](RAII_Smart_Pointers.assets/image-20240510172759569.png)![](RAII_Smart_Pointers.assets/image-20240510172806320.png)![](RAII_Smart_Pointers.assets/image-20240510172813664.png)![](RAII_Smart_Pointers.assets/image-20240510172823742.png)



### Reference Count
> [!important]
> ![](RAII_Smart_Pointers.assets/image-20240308204242557.png)![](RAII_Smart_Pointers.assets/image-20240308204342541.png)


### Control Block
> [!def]
> ![](RAII_Smart_Pointers.assets/image-20240308204555097.png)




### CS106X Slides
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

