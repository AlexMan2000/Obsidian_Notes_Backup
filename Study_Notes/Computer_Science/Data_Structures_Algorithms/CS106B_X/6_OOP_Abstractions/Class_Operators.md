# Header and Source File
> [!concept]
> ![](Class_Operators.assets/image-20231209224004418.png)


# Class Design
> [!concept]
> ![](Class_Operators.assets/image-20231209224025586.png)


## Constructor
### How to Define
> [!important]
> ![](Class_Operators.assets/image-20231209224118153.png)![](Class_Operators.assets/image-20231209224157095.png)![](Class_Operators.assets/image-20231209224220608.png)![](Class_Operators.assets/image-20231209224254366.png)![](Class_Operators.assets/image-20231209224318263.png)![](Class_Operators.assets/image-20231209224324188.png)


### Constructor Overload
> [!concept]
> ![](Class_Operators.assets/image-20231209224413363.png)


### Implement Member Functions
> [!concept]
> ![](Class_Operators.assets/image-20231209224452645.png)![](Class_Operators.assets/image-20231209224500297.png)


## Destructor
> [!concept]
> ![](Class_Operators.assets/image-20231209224535359.png)



## this keyword - name conflict
> [!concept]
> ![](Class_Operators.assets/image-20231209225325074.png)
> **Remarks:**
> 1. Getter functions don't have naming conflict with the parameter since typically they don't have input parameters.
> 2. Setter functions can have naming conflicts so we need to use `this` to fully specify.
> 3. Alternative way to avoid name conflict is to add a subscript before the member variables.



## Type Casting
> 



## Class Design Examples
### Car Class
> [!task]
> ![](Class_Operators.assets/image-20231210091750677.png)

```c++ car.h
#include <string>

class Car {
public:
    // Constructor
    Car(std::string make, std::string model, int year, int mileage);
    
    // Getters
    std::string GetMake();
    std::string GetModel();
    int GetYear();
    int GetMileage();
    
    // Other methods
    void Drive(int distance);

    void DisplayInfo();

private:
    std::string _make;
    std::string _model;
    int _year;
    int _mileage;
};

```


```c++ cpp file
// Gotta include the .h file!!
#include "car.h"

// Best practice to include header files that are only needed for implementation 
// in the .cpp file 
#include <iostream>

Car::Car (std::string make, std::string model, int year, int mileage) {
	// To avoid name conflict
  _make = make;
  _model = model;
  _year = year;
  _mileage = mileage;
}

std::string Car::GetMake () {
  return _make;
}

std::string Car::GetModel () {
  return _model;
}

int Car::GetYear () {
  return _year;
}

int Car::GetMileage () {
  return _mileage;
}

void Car::Drive (int distance) {
  _mileage += distance;
}

void Car::DisplayInfo () {
  std::cout << "Make: " << _make << std::endl;
  std::cout << "Model: " << _model << std::endl;
  std::cout << "Year: " << _year << std::endl;
  std::cout << "Mileage: " << _mileage << std::endl;
}

```

### Dynamic Array Example
> [!task]
> ![](Class_Operators.assets/image-20231210091825049.png)




# Class Hierarchy
## Inheritance
> [!concept]
> 



# Template Classes
## Template Classes
### Header File Definition
> [!concept]
> ![](Class_Operators.assets/image-20231209225523337.png)![](Class_Operators.assets/image-20231209225528569.png)![](Class_Operators.assets/image-20231209225535380.png)



## CPP File Implementation
> [!concept]
> ![](Class_Operators.assets/image-20231209225650387.png)![](Class_Operators.assets/image-20231209225658848.png)![](Class_Operators.assets/image-20231209230030745.png)


> [!bug]
> ![](Class_Operators.assets/image-20231209225925437.png)![](Class_Operators.assets/image-20231209225921010.png)![](Class_Operators.assets/image-20231209225915465.png)




# Const Keyword
## Why Const?
### Detecting Malicious Assginment
> [!important]
> ![](Class_Operators.assets/image-20231229120843096.png)![](Class_Operators.assets/image-20231229120848781.png)
> Due to the const keyword, any attempts to modify the content of const variable will trigger **compiler errors**.



### Reasoning about function's behavior
> [!important]
> ![](Class_Operators.assets/image-20231229121143551.png)![](Class_Operators.assets/image-20231229121147763.png)
> **Notes:**
> 
> Here, all three functions will change the state of the planet object, which cannot be reasoned without the help of const keyword.



## Const in Class
> [!example]
> ![](Class_Operators.assets/image-20231229121510527.png)![](Class_Operators.assets/image-20231229121519097.png)
> So const object can only call const member functions. Any call to non-const member function will trigger **compilation error**.







## Const Correctness
> [!concept]
> The const correctness means that if we promise not to modify some object `s` by putting const keywords before tehe variable decalration, then we should make sure that any calls to the member function of `s` should also be const functions.
> ![](Class_Operators.assets/image-20231209230224057.png)![](Class_Operators.assets/image-20231209230218479.png)![](Class_Operators.assets/image-20231209230305368.png)


## Const Interface
> [!important]
> ![](Class_Operators.assets/image-20231209230345065.png)



## Const Pointer
> [!concept]
> ![](Class_Operators.assets/image-20231231223636813.png)![](Class_Operators.assets/image-20231231223654390.png)![](Class_Operators.assets/image-20231231223811168.png)




## Const Iterator
> [!concept]
> We can think of constant iterator just as constant pointer, where incrementing is not allowed but modifying the data it points to is legal. 
> ![](Class_Operators.assets/image-20231231223857794.png)![](Class_Operators.assets/image-20231231223901821.png)



## Summary
> [!summary]
> ![](Class_Operators.assets/image-20231231224319758.png)



# Iterator Class



# Operators
> [!overview]
> ![](Class_Operators.assets/image-20231231224758385.png)



## Operator Overloading
> [!concept]
> ![](Class_Operators.assets/image-20231231225055189.png)![](Class_Operators.assets/image-20231231225101324.png)![](Class_Operators.assets/image-20231231225133851.png)



## Unary Operators
> [!example] vector class +=
> ![](Class_Operators.assets/image-20240101082415578.png)![](Class_Operators.assets/image-20240101082421047.png)![](Class_Operators.assets/image-20240101082427501.png)
> **Notes:**
> 
> It is super important to return a reference type at the operator function. Since if we don't do it, we are returning a brand new object. Then if we call `("s" += "a") += "b"` and print `"s"`we will get `"sa"` instead of `"sab"`.

> [!example] vector class []
> ![](Class_Operators.assets/image-20240101092154619.png)



## Binary Operators
> [!example] vector class +
> ![](Class_Operators.assets/image-20240101091919146.png)
> 1. **Why are we returning by value instead?** 
>    We don't want to support chain calling.
> 2. **Why are both parameters const?** 
>    The arithmetic operators return copies but doesn’t change the objects themselves.
> 3. **Why did we declare these as non-member functions?**
>    We are not changing the objects of lhs.

> [!example] fraction struct <<
> ![](Class_Operators.assets/image-20240101100251736.png)![](Class_Operators.assets/image-20240101100257564.png)
> 1. **Why is the ostream parameter passed by non-const reference, and the Fraction struct passed by const reference?** 
>    Always think about const-ness of parameters. Here, we are modifying the stream, not the Fraction struct.
> 2. **Why are we returning a reference?** 
>    Return reference to support chaining << calls
> 3. **Why are we implementing this as a non-member function?**
>    Here we are overloading << so our class works as the rhs…but we can’t change the class of lhs (stream library).

> [!example] fraction class << friend keyword
> ![](Class_Operators.assets/image-20240101100900777.png)![](Class_Operators.assets/image-20240101100908440.png)![](Class_Operators.assets/image-20240101101124121.png)![](Class_Operators.assets/image-20240101101508061.png)






## Member vs Non-Member
> [!important]
> ![](Class_Operators.assets/image-20240101092017120.png)![](Class_Operators.assets/image-20240101092021653.png)
> 6. If binary operator wants to change the lhs but the lhs is a STL library function, then implement as non-member.
> 7. If a non-member operator wants to access the rhs's private variable, use friend keyword before the non-member operator in the rhs's class.



## Conversion Operators
> [!important]
> 




# Principle of Least Astonishment(POLA)
## C 160 Mimic Conventional Usage
> [!concept]
> ![](Class_Operators.assets/image-20240101101830299.png)![](Class_Operators.assets/image-20240101101837923.png)




## C.161 Non-member for symmetric operators
> [!concept]
> ![](Class_Operators.assets/image-20240101101847361.png)![](Class_Operators.assets/image-20240101101853169.png)![](Class_Operators.assets/image-20240101101856722.png)![](Class_Operators.assets/image-20240101101901155.png)














