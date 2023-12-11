# Header and Source File
> [!concept]
> ![](Class_Design.assets/image-20231209224004418.png)


# Class Design
> [!concept]
> ![](Class_Design.assets/image-20231209224025586.png)


## Constructor
### How to Define
> [!important]
> ![](Class_Design.assets/image-20231209224118153.png)![](Class_Design.assets/image-20231209224157095.png)![](Class_Design.assets/image-20231209224220608.png)![](Class_Design.assets/image-20231209224254366.png)![](Class_Design.assets/image-20231209224318263.png)![](Class_Design.assets/image-20231209224324188.png)


### Constructor Overload
> [!concept]
> ![](Class_Design.assets/image-20231209224413363.png)


### Implement Member Functions
> [!concept]
> ![](Class_Design.assets/image-20231209224452645.png)![](Class_Design.assets/image-20231209224500297.png)


## Operator Overloading
> [!important]
> 



## Destructor
> [!concept]
> ![](Class_Design.assets/image-20231209224535359.png)



## this keyword - name conflict
> [!concept]
> ![](Class_Design.assets/image-20231209225325074.png)
> **Remarks:**
> 1. Getter functions don't have naming conflict with the parameter since typically they don't have input parameters.
> 2. Setter functions can have naming conflicts so we need to use `this` to fully specify.
> 3. Alternative way to avoid name conflict is to add a subscript before the member variables.



## Type Casting
> 



## Class Design Examples
### Car Class
> [!task]
> ![](Class_Design.assets/image-20231210091750677.png)

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
> ![](Class_Design.assets/image-20231210091825049.png)




# Class Hierarchy
## Inheritance
> [!concept]
> 



# Template Classes and Const Correctness
## Template Classes
### Header File Definition
> [!concept]
> ![](Class_Design.assets/image-20231209225523337.png)![](Class_Design.assets/image-20231209225528569.png)![](Class_Design.assets/image-20231209225535380.png)


## CPP File Implementation
> [!concept]
> ![](Class_Design.assets/image-20231209225650387.png)![](Class_Design.assets/image-20231209225658848.png)![](Class_Design.assets/image-20231209230030745.png)


> [!bug]
> ![](Class_Design.assets/image-20231209225925437.png)![](Class_Design.assets/image-20231209225921010.png)![](Class_Design.assets/image-20231209225915465.png)


## Const Correctness
> [!concept]
> ![](Class_Design.assets/image-20231209230224057.png)![](Class_Design.assets/image-20231209230218479.png)![](Class_Design.assets/image-20231209230305368.png)


## Const Interface
> [!important]
> ![](Class_Design.assets/image-20231209230345065.png)



# Static in C++



# CONST in C++









