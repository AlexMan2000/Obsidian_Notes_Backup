# Behavioral Equivalence
> [!concept] Behavioral Equivalence 
> To determine ==behavioral equivalence==, our question is whether we could substitute one implementation for the other. Below are two implementations of the `find()` method.

```start-multi-column  
ID: ExampleRegion1  
number of columns: 2   
```

```java
// Find the index of an integer in an array
static int find(int[] arr, int val) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == val) return i;
    }
    return -1;
}
```

--- end-column ---

```java
// Improved Search, from both ends.
static int find(int[] arr, int val) {
    for (int i = 0, j = arr.length-1; i <= j; i++, j--) {
        if (arr[i] == val) return i;
        if (arr[j] == val) return j;
    }
    return -1;
}
```

--- end-multi-column
> [!bug] Behavioral Difference
> In turns out that the two programs don't have so-called behavioral equivalence. 
> Not only do these implementations have different performance characteristics, they actually have different behavior. 
> - If `val` happens to appear _more than once_ in the array, the original `find` always returns the lowest index at which it occurs. 
> - But the new `find` might return the lowest index or the highest index, whichever it finds first.
> 

> [!example] One Possible Specfication
> The notion of behavioral equivalence is in the eye of the beholder — that is, the client. In order to make it possible to substitute one implementation for another, and to know when this is acceptable, we need a specification that states exactly what the client depends on.
> 
> In this case, a specification that would allow these two implementations to be behaviorally equivalent might be:
> ![](Ch4_Specifications.assets/image-20231211110502572.png)
> ![](Ch4_Specifications.assets/image-20231211110817814.png)![](Ch4_Specifications.assets/image-20231211110943505.png)![](Ch4_Specifications.assets/image-20231211113532230.png)![](Ch4_Specifications.assets/image-20231211113828569.png)



# Specification Structure
> [!concept]
> Abstractly speaking, a ==_specification_== of a method has several parts:
> - A _method signature_, giving the name, parameter types, return type, and exceptions thrown
> - A _requires_ clause, describing additional restrictions on the parameters
> - An _effects_ clause, describing the return value, exceptions, and other effects of the method
> 
> Taken together, these parts form the ==_precondition_== and the ==_postcondition_== of the method.
> 
> The ==precondition== is an obligation on the ==client== (the caller of the method). It is a condition over the state in which the method is invoked. One aspect of the precondition is the number and types of the parameters in the method signature. Additional conditions are written down in the _requires_ clause, for example:
> - narrowing a parameter type (e.g. `x >= 0` to say that an `int` parameter x must actually be a nonnegative `int`)
> - interactions between parameters (e.g., `val` occurs exactly once in `arr`)
>  
> The ==postcondition== is an obligation on the ==implementer== of the method. It includes the parts that Java can statically check: the return type and declared checked exceptions. Additional conditions are written down in the _effects_ clause, including:
> - how the return value relates to the inputs
> - which exceptions are thrown, and when
> - whether and how objects are mutated
> 
> **In general, the postcondition is a condition on the state of the program _after_ the method is invoked, assuming the precondition was true _before_.**
> 
> The overall structure is a logical implication: _if_ the precondition holds when the method is called, _then_ the postcondition must hold when the method completes.
> ![](Ch4_Specifications.assets/image-20231211134733543.png)
> If the precondition does _not_ hold when the method is called, the implementation is _not_ bound by the postcondition. It is free to do anything, including never returning, throwing an exception, returning arbitrary results, making arbitrary mutations, etc.
> 
> A specification of a method ==can== talk about the parameters and return value of the method, but it ==should never== talk about _local variables_ of the method or _private fields_ of the method’s class. You should consider the implementation invisible to the reader of the spec. It’s behind the firewall as far as clients are concerned.
> 
> In Java, the source code of the method is often unavailable to the reader of your spec, because the Javadoc tool only extracts the spec comments from your code and renders them as HTML.
> ![](Ch4_Specifications.assets/image-20231211134853408.png)



> [!example] Exercise
> ![](Ch4_Specifications.assets/image-20231211133102046.png)![](Ch4_Specifications.assets/image-20231211133128070.png)


# Java Specifications
> [!concept]
> Java has a convention for documentation comments called [Javadoc](http://en.wikipedia.org/wiki/Javadoc), in which parameters are described by `@param` clauses and results are described by `@return` clauses. 
> 
> - You ==should== put the preconditions into `@param` where possible, and postconditions into `@return`. 
> 
> - You ==should not== put any static type in the spec, since it is automatically checked by Java Compiler, and don't need to occupy some place in the spec.
> 
> So a specification like this:
> ![](Ch4_Specifications.assets/image-20231211133821831.png)

> [!bug] Problematic Specifications
> ![](Ch4_Specifications.assets/image-20231211133902185.png)![](Ch4_Specifications.assets/image-20231211133911636.png)

> [!example] Concise Javadoc
> ![](Ch4_Specifications.assets/image-20231211134501767.png)![](Ch4_Specifications.assets/image-20231211134515446.png)![](Ch4_Specifications.assets/image-20231211134531216.png)

> [!example] Python Doc Example
> Python 3 typically don't haver static type checking so we expect a different form of documentation from Java.
> ![](Ch4_Specifications.assets/image-20231211134641968.png)![](Ch4_Specifications.assets/image-20231211134654048.png)



# Null References
## Why we should avoid null reference?
> [!concept]
> - Primitives cannot be `null`
> - Reference Types can be `null`
> - `null` is different from empty string `""` or empty arrays `[]` where we can call member functions and access its element. But trying to access the attributes of `null` objects will trigger `NullPointerException`.
> - Sometimes, programmers are unaware of the potential access of the member functions of `null` object. For example when we have a collection of reference type `List<String tmp` where we add a `null` to it. Then when we try to run `tmp.get(0)` , we get the `null` object and thus when we further try to access the member function in the following way: `tmp.get(0).<member_function>` we will get the `NullPointerExceptionError`.


> [!example] Exercise 1: NullPointerException
> ![](Ch4_Specifications.assets/image-20231228102245781.png)

> [!example] Exercise 2: More Null Exercises
> ![](Ch4_Specifications.assets/image-20231228102435671.png)

> [!example] Exercise 3: Null Preconditions and Postconditions
> 
> - Null values are troublesome and unsafe, so much so that most methods simply avoid them entirely. As a general convention, **null values are disallowed in parameters and return values** unless the spec explicitly says otherwise. So every method has a precondition on the object and array types in its parameters that they be non-null – including elements of collections like arrays, sets, lists, and maps. Every method that can return object or array types implicitly has a postcondition that their values are non-null, again including elements of collection types.
> - **If a method allows null values in a parameter, it needs to explicitly state it, or if it might return a null value in a result, it should explicitly state it**. But these are in general not good ideas. **Avoid `null`**.
> - To sum up, a method has an implicit precondition and postcondition that the parameters and return value cannot be null. In other words, in the method specifications, there may not be any null keywords but null are implicitly assumed to be illegal. If the method allow null value then it has to explicitly mention it in the specifications.
> 
> **Let's see the following examples of specifications:**
> 
> The first example is `String.startsWith(String str)`, we see that there is no mentioning of `null` keyword, which implies that the method doesn't allow parameters and return values to be `null`. We say that this method has a precondition that the parameters cannot be null.
> ![](Ch4_Specifications.assets/image-20231228103507289.png)
> The second example is `BigInteger(String val)`, where there is only a `NumberFormatException` and no mentioning of `null`, so same as before. We say that this method has a precondition that the parameters cannot be null.
> 
> ![](Ch4_Specifications.assets/image-20231228103757362.png)
> The third example is `File(String pathname)`, this method allows null parameters and explicitly state that `NullPointerException` will be triggered upon null input of pathname. 
> 
> ![](Ch4_Specifications.assets/image-20231228103832292.png)
> For those methods that have implicit restriction of null parameter, if it turns out that the input is null, then since the precondition of the method isn't met, the method can do anything, like the following example:
> 
> ![](Ch4_Specifications.assets/image-20231228104245654.png)













## How to avoid null?
> [!concept]
> Google has their own [discussion of `null` in Guava, the company’s core Java libraries](https://github.com/google/guava/wiki/UsingAndAvoidingNullExplained). The project explains
> 
> Careless use of `null` can cause a staggering variety of bugs. Studying the Google code base, we found that something like 95% of collections weren’t supposed to have any null values in them, and having those **fail fast*** rather than silently accept `null` would have been helpful to developers.
> 
> Additionally, `null` is unpleasantly ambiguous. It’s rarely obvious what a `null` return value is supposed to mean — for example, `Map.get(key)` can return `null` either because the value in the map is `null`, or the value is not in the map. Null can mean failure, can mean success, can mean almost anything. Using something other than `null` **makes your meaning clear**.
> 
> If you avoid using `null`, there is still sometimes a need for a parameter or return value to indicate that a value is missing. For example, what should [`Map.get(key)`](http://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/util/Map.html#get(java.lang.Object)) return when the key is not found in the map? One good tool for this problem is [`Optional<T>`](http://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/util/Optional.html). You can think of `Optional<T>` like a very constrained `List<T>` of length at most 1. It either contains just one element of type `T`, or it is empty. The `isPresent()` method tests whether or not it is empty, and `get()` and `getOrElse()` unpack the value if present. The key advantage of `Optional<T>` is that it can be used _sparingly_, only in places where it’s sensible for the spec to allow for a missing value, and it clearly expresses the intention of the spec in those cases.



## Emptiness
> [!concept]
> Recall that in Python, `None` is not the same as the empty string `""`, the empty list `[ ]`, or the empty dictionary `{ }`. These empty objects like these are _valid objects_ that simply happen to contain no elements. But you can use them with all the usual operations allowed by the type. For example, `len("")` returns 0, and `"" + "a"` returns `"a"`. That’s not true of `None` – `len(None)` and `None + "a"` both produce errors.
> 
> The same idea translates to Java. The `null` reference is not a valid string, or list, or map, or any other object. But the empty string `""` is a valid `String` value, and the empty list `List.of()` is a valid list value.
> 
> The upshot of this is that **empty values are always allowed as parameter or return values**, unless a spec explicitly disallows them.

> [!example] Vacuous Statement
> Let's see the following method, `List.of()`:
> ![](Ch4_Specifications.assets/image-20231228105328365.png)
> If we pass a sequence of strings then it will return a list of specified strings.
> ![](Ch4_Specifications.assets/image-20231228104951926.png)
> If we pass `""`(empty string), we will get `[""]` with length 1. If we pass nothing (`List.of()`), we will get `[]` with length 0.
> 
> Now consider the following problem:
> ![](Ch4_Specifications.assets/image-20231228105627509.png)![](Ch4_Specifications.assets/image-20231228105649827.png)






# Testing and Specifications
## White-Box and Black-box Testing Cannot go beyond Specs
> [!concept]
> In testing, we talk about _black box tests_ that are chosen with only the specification in mind, and _glass box tests_ that are chosen with knowledge of the actual implementation. 
> 
> But it’s important to note that **even glass box tests must follow the specification**. Your implementation may provide stronger guarantees than the specification calls for, or it may have specific behavior where the specification is undefined. 
> 
> **But your test cases should not count on that behavior. **
> 
> Test cases must be correct, obeying the contract just like every other client.
> 
> For example, suppose you are testing this specification of `find`, slightly different from the one we’ve used so far:
> ![](Ch4_Specifications.assets/image-20231228111650798.png)
> 
> This spec has:
> - A strong precondition in the sense that `val` is required to be found.
> - A fairly weak postcondition in the sense that if `val` appears more than once in the array, this specification says nothing about which particular index of `val` is returned. 
> - Even if you implemented `find` so that it always returns the lowest index, **your test case can’t assume that specific behavior:**
> ![](Ch4_Specifications.assets/image-20231228111746846.png)
> 
> - Similarly, even if you implemented `find` so that it (sensibly) throws an exception when `val` isn’t found, instead of returning some arbitrary misleading index, your test case can’t assume that behavior, because it can’t call `find()` in a way that violates the precondition.
> - So what does glass box testing mean, if it can’t go beyond the spec? **It means you are trying to find new test cases that exercise different parts of the implementation, but still checking those test cases in an implementation-independent way, following the spec.** 简单来说，就是即便你知道了函数的实现逻辑，也不能为所欲为不按照`Specifications`来设计测试用例。



## Examples - Great Common Divisors
> [!example] 
> ![](Ch4_Specifications.assets/image-20231228112206393.png)![](Ch4_Specifications.assets/image-20231228112251068.png)


# Specifications for Mutating Methods
> [!concept]
> 如果spec中没有涉及到任何关于null的字眼，那么默认情况下spec隐含不能传入null的precondition。
> 
> 类似地，如果spec中没有涉及到任何关于mutation的字眼，比如the list is modified之类，那么默认情况下spec隐含着不能mutate input的precondition。
> 
> ![](Ch4_Specifications.assets/image-20231228131842378.png)




# Exceptions
> [!concept]



