# Function Overloading
> [!concept]
> ![](Functions%20and%20Lambdas.assets/image-20231229115523399.png)![](Functions%20and%20Lambdas.assets/image-20231229115527996.png)


# Template/Generic Functions in C++
## Define generic functions
> [!important]
> ![](Template%20Functions.assets/image-20231230101340324.png)![](Template%20Functions.assets/image-20231230101345844.png)![](Template%20Functions.assets/image-20231230101350976.png)![](Template%20Functions.assets/image-20231230101358499.png)![](Template%20Functions.assets/image-20231230101409068.png)![](Template%20Functions.assets/image-20231230101324460.png)
> The process of creating templating functions is like you don't know the parameter type when the function is defined and know it when it is called by clients. In other words, you are deferring the parameter type to the function calling stage.




## Default Types
> [!concept]
> ![](Functions%20and%20Lambdas.assets/image-20231229115709517.png)




## Call Template Functions
### Explicit Instantiation
> [!code]
> Consider the following template function:
```C++
template <typename T>
pair<T, T> my_minmax(T a, T b) {
    if (a < b) return {a, b};
    else return {b, a};
}


void myMinMaxTestExplicit() {
    auto [min1, max1] = my_minmax<double>(4.2, -7.9);
    printMinAndMax(min1, max1);
    auto [min2, max2] = my_minmax<string>("Avery","Anna");
    printMinAndMax(min2, max2);
    auto [min3, max3] = my_minmax<int>(3, 3);
    printMinAndMax(min3, max3);
    auto [min4, max4] = my_minmax<double>(2, 2.3);
    printMinAndMax(min4, max4);
    auto [min5, max5] = my_minmax<vector<int>>({1, 2}, {3, 1});
//    printMinAndMax(min5, max5);   This won't compile
}


int main() {
	myMinMaxTestExplicit();
}
```
> [!important]
> ![](Functions%20and%20Lambdas.assets/image-20231230111440436.png)![](Functions%20and%20Lambdas.assets/image-20231230111449504.png)







### Implicit Instantiation
> [!code]
> Consider the following template function:
```C++
template <typename T>
pair<T, T> my_minmax(T a, T b) {
    if (a < b) return {a, b};
    else return {b, a};
}

void myMinMaxTestImplicit() {
    auto [min1, max1] = my_minmax(4.2, -7.9);
    auto [min2, max2] = my_minmax("Avery","Anna");  // This does not work, compiler deduces "Avery" to be C-string, which cannot be compared. A quick fix is making C-string a C++ string like string("Avery") and string("Anna")
    auto [min3, max3] = my_minmax(3, 3);
    auto [min4, max4] = my_minmax(2, 2.3);            // No matching function error
    auto [min5, max5] = my_minmax({1, 2}, {3, 1});    // No matching function error
}
```
> [!important]
> As we see, in the first three cases, the compiler is smart enough to correctly deduce the input type, but for the last two cases, the compiler raises an error where it cannot find a function template to match the input type.
> ![](Functions%20and%20Lambdas.assets/image-20231230111606843.png)![](Functions%20and%20Lambdas.assets/image-20231230111621928.png)




### Behind the Instantiation
> [!important]
> ![](Functions%20and%20Lambdas.assets/image-20231230103459903.png)



## Summary
> [!summary]
> ![](Functions%20and%20Lambdas.assets/image-20231231171452584.png)



# Advanced Template - Concept Lifting
> [!def]
> Concept lifting is about eliminating assumptions(e.g. parameter type that you explicitly specify) about the functions through templating process.
> ![](Functions%20and%20Lambdas.assets/image-20231230112648330.png)



## Eliminating Assumptions
> [!concept]
> Suppose we want to write a generic function for the following task:
> ![](Functions%20and%20Lambdas.assets/image-20231230113102845.png)
> And we start from this basic function, which clearly has lots of assumptions:
> 
> ![](Functions%20and%20Lambdas.assets/image-20231230113125402.png)
> **The easy-to-see unnecessary assumptions are:**
> 1. Collection type is specified to be `vector<int>&`
> 2. Data type is specified to be `int`
> 
> **So we use template to eliminate these assumptions:**
> ![](Functions%20and%20Lambdas.assets/image-20231230115309792.png)
> Notice that the following code adds an assumption about the iterator. When we do point arithmetic like the following, we are assuming that the iterator has the ability to randomly access. So we have to change the way we update the iterator as follows:
> 
> ![](Functions%20and%20Lambdas.assets/image-20231230114754702.png)
> But there is still one last assumption not very easy to spot, which is that **we assume that we are counting over the entire collection**, but the last two tasks say that we may be traversing only half of the collection. So we could further eliminate the assumptions about the iterators' range:
> 
> ![](Functions%20and%20Lambdas.assets/image-20231230115120558.png)
> So finally we could call the generic function to complete all the task but the last one:
> 
> ![](Functions%20and%20Lambdas.assets/image-20231230115715964.png)



## Implicit Interfaces
> [!important] Implicit Interface Concepts
> ![](Functions%20and%20Lambdas.assets/image-20231230155930831.png)
> Here before compilation, the code looks like the following to the g++:
> 
> ![](Functions%20and%20Lambdas.assets/image-20231230160008742.png)
> After compilation, the codes look like the following:
> 
> ![](Functions%20and%20Lambdas.assets/image-20231230160124399.png)
> 
> But each template parameter must have the operations the function assumes it has:
> ![](Functions%20and%20Lambdas.assets/image-20231230160539531.png)
> **In other words, a template function defines an implicit interface that each template parameter must satisfy.**
> 

> [!example] Implicit Interface Example
> ![](Functions%20and%20Lambdas.assets/image-20231230212116314.png)
> The answer should be:
> 1. The `Collection Type` must have a `size()` method that returns an integer.
> 2. `Collection` must support the subscript operator. (In other words, it should support random access).
> 3. `DataType` must be comparable to the return type of the subscript operator of the `Collection`.



## Overload Resolution
> [!concept]
> ![](Functions%20and%20Lambdas.assets/image-20231230213200186.png)





## Constraints and Concepts - C++ 20




# Building Templates



# Template Metaprogramming




# Predicates and Lambdas
## Predicate Functions
> [!concept]
> ![](Functions%20and%20Lambdas.assets/image-20231230213528477.png)
> Suppose now we are given a task that asks us to count the number of elements that satisfy some conditions within some range of a collection.
> 
> ![](Functions%20and%20Lambdas.assets/image-20231230213726495.png)
> We could rephrase the above task into the following:
> 
> ![](Functions%20and%20Lambdas.assets/image-20231230213821880.png)
> In other words, if we want to find how many 3 are there in the range of collection, we can equivalently find how many elements in the range of collection are equal to 3. Here `equal to 3` is a predicate function that takes in one argument `x`, and return a boolean `x == 3`, now the function changes into the following abstraction:
> 
> ![](Functions%20and%20Lambdas.assets/image-20231230214021223.png)
> Now say we want to find all the elements that are less than 5 across the entire collection, we could do the following:
> 
> ![](Functions%20and%20Lambdas.assets/image-20231230214227223.png)
> Now what if instead of fixing our upper bound to be 5, we want to find all the elements that are less than some `limit` across the entire collection. Since the way we use `predicate` function in the above code imposes two implicit interfaces on our predicate function:
> 1. It has to be `uniary predicate`, we cannot add more than one parameters to the predicate function
> 2. The function should return a `bool`, which is immediately satisfies given the definition of predicate function
> 
> Thus we will need help from `lambda` function.
> 
> ![](Functions%20and%20Lambdas.assets/image-20231230214515955.png)![](Functions%20and%20Lambdas.assets/image-20231230214524827.png)![](Functions%20and%20Lambdas.assets/image-20231230214536206.png)



## Lambda Functions
### Capture Clause
> [!def]
> ![](Functions%20and%20Lambdas.assets/image-20231230215520195.png)![](Functions%20and%20Lambdas.assets/image-20231230215602447.png)![](Functions%20and%20Lambdas.assets/image-20231230215706753.png)
> Whenever C++ compiler sees `[]()`, it is compiled as a lambda.
> 
> Behind the scene, the lambda function is actually a class object.



### Lazy Capture
> [!concept]
> ![](Functions%20and%20Lambdas.assets/image-20231230215620170.png)
> We don't recommend this use since it wil make every outside of the function usable in the function, which makes the behavior of the function complicated.
> 
> Generally don't capture anything. Be selective, only capture the variable that you need.



### Default Capture
> [!def]
> We can also do default capture as follows:
> 
> `auto func = [limit = 0](auto val) { return val < limit }`, where we set `limit = 0` by default if there is no variable outside of the function as `limit`.




## Applications
### Count Number of Elements
> [!important]
> Suppose now we want to tackle the task mentioned before: count the number of elements that are less than `limit` within the collection, we have two ways of doing this:
> 
> The first approach is to use the `lambda` function directly as follows:
> ![](Functions%20and%20Lambdas.assets/image-20231230214751728.png)
> The second approach is to use the `lambda` function as the adapter to the predicate that already exists but cannot be passed directly into our `countOccurences` function due to non-uniarity, as shown below:
> 
> ![](Functions%20and%20Lambdas.assets/image-20231230220411451.png)
> Here, `isLessThenLimit` is not unary since it takes two arguments. But we can use a unary `lambda` function as its wrapper, as follows:
> 
> ![](Functions%20and%20Lambdas.assets/image-20231230220506306.png)![](Functions%20and%20Lambdas.assets/image-20231230220530443.png)




### Execution Counter
> [!code]
> Consider the following linear time recursive program, where the function `factorial(10)` should be called 10 times during execution, and we write a lambda function to count the number of times it is executed.
> 
```C++
template <typename Monitor>
int factorial(int val, Monitor& func) {

    func();
    if (val == 1 || val == 0) {
        return val;
    }

    return val * factorial(val - 1, func);
}

int main() {
	int num_of_time = 0; 
	// Important Application: Capture by Reference
    auto functionMonitor = [&num_of_time]() {
        num_of_time++;
    };

    factorial(10, functionMonitor);
    std::cout << num_of_time << std::endl;  // 10
}

```








