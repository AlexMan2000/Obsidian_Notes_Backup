# Operations on ADTs
> [!def]
> The operations of an abstract type are classified as follows:
> - ==**Creators**== create new objects of the type. A creator may take values of other types as arguments, but not an object of the type being constructed. 
> 	- **Factory Method Design Pattern**: Call `new T()` inside of a static method, like `List.of(...)`
> 	- Used to create ADT objects.
> - ==**Producers**== also create new objects of the type, but require one or more existing objects of the type as input. The `concat` method of `String`, for example, is a producer: it takes two strings and produces a new string representing their concatenation.
> 	- Used to produce the objects of the same type as the caller.
> - ==**Observers**== take objects of the abstract type and return objects of a different type. The `size` method of `List`, for example, returns an `int`. 
> 	- It is used to inspect some of the properties of an object.
> - ==**Mutators**== change objects. The `add` method of `List`, for example, mutates a list by adding an element to the end.
> 
> ![](8_Abstract_Data_Type.assets/image-20240208130409401.png)



# Components of ADTs
## Specifications
> [!def]
> The specification of an ADT includes:
> - The name of the class
> - The Javadoc comment just before the class
> - The specifications of its public methods and fields
> 
> These parts are the contract that is visible to a client of the class.

## Representation
> [!def]
> The representation of an ADT consists of:
> - Its fields and any assumptions or requirements about those fields.


## Implementations
> [!def]
> The implementation of an ADT consists of the method implementations that manipulate its representation.


## Example
> [!example]
> ![](8_Abstract_Data_Type.assets/image-20240208131342907.png)![](8_Abstract_Data_Type.assets/image-20240208131355539.png)



# Good ADTs Properties
## Representation Independence
> [!def]
> Critically, a good abstract data type should be ==**representation independent**==. This means that the use of an abstract type is independent of its representation (the actual data structure or data fields used to implement it), so that changes in representation have no effect on code outside the abstract type itself. 
> 
> **In other words, we can change the implementation of Tweet without affecting all the clients who are directly accessing those fields.**
> 
> For example, the operations offered by `List` are independent of whether the list is represented as a linked list or as an array.
> 
> As an implementer, you will only be able to safely change the representation of an ADT if its operations are fully specified with preconditions and postconditions, so that clients know what to depend on, and you know what you can safely change.



## String Design Example
### Specifications
> [!code]
```java
/** MyString represents an immutable sequence of characters. */
public class MyString { 

    //////////////////// Example of a creator operation ///////////////
    /**
     * @param b a boolean value
     * @return string representation of b, either "true" or "false"
     */
    public static MyString valueOf(boolean b) { ... }

    //////////////////// Examples of observer operations ///////////////
    /**
     * @return number of characters in this string
     */
    public int length() { ... }

    /**
     * @param i character position (requires 0 <= i < string length)
     * @return character at position i
     */
    public char charAt(int i) { ... }

    //////////////////// Example of a producer operation ///////////////    
    /** 
     * Get the substring between start (inclusive) and end (exclusive).
     * @param start starting index
     * @param end ending index.  Requires 0 <= start <= end <= string length.
     * @return string consisting of charAt(start)...charAt(end-1)
     */
    public MyString substring(int start, int end) { ... }

    /////// no mutator operations (why not?)
}
```

### Representation 1
> [!code]
> ![](8_Abstract_Data_Type.assets/image-20240306162622688.png)
```java
/** MyString represents an immutable sequence of characters. */
public class MyString {

	private char[] a;

    public static MyString valueOf(boolean b) {
	    MyString s = new MyString();
	    s.a = b ? new char[] { 't', 'r', 'u', 'e' } 
	            : new char[] { 'f', 'a', 'l', 's', 'e' };
	    return s;
	}

    public int length() {
	    return a.length;
	}

    public char charAt(int i) {
	    return a[i];
	}
	
	public MyString substring(int start, int end) {
		MyString that = new MyString();
		that.a = new char[end - start];
		System.arraycopy(this.a, start, that.a, 0, end - start);
		return that;
	}

}
```
> [!bug] Low Efficiency
>   One problem with this implementation is that it’s passing up an opportunity for performance improvement. Because this data type is immutable, the `substring` operation doesn’t really have to copy characters out into a fresh array. 
>   
>   It could just point to the original `MyString` object’s character array and keep track of the start and end that the new substring object represents. In some versions of Java, the built-in `String` implementation does exactly this.

### Representation 2 - Optimized
> [!code]
> ![](8_Abstract_Data_Type.assets/image-20240306162742375.png)
```java
public class MyString {

	private char[] a;
	private int start;
	private int end;
	
	public static MyString valueOf(boolean b) {
	    MyString s = new MyString();
	    s.a = b ? new char[] { 't', 'r', 'u', 'e' } 
	            : new char[] { 'f', 'a', 'l', 's', 'e' };
	    s.start = 0;
	    s.end = s.a.length;
	    return s;
	}
	
	public int length() {
	    return end - start;
	}
	
	public char charAt(int i) {
	  return a[start + i];
	}
	
	public MyString substring(int start, int end) {
	    MyString that = new MyString();
	    that.a = this.a;
	    that.start = this.start + start;
	    that.end = this.start + end;
	    return that;
	}
}
```


## Family Example
> [!example] Example 1
> ![](8_Abstract_Data_Type.assets/image-20240306163117813.png)![](8_Abstract_Data_Type.assets/image-20240306163124627.png)

> [!example] Example 2
> ![](8_Abstract_Data_Type.assets/image-20240306163153711.png)![](8_Abstract_Data_Type.assets/image-20240306163209185.png)

> [!example] Example 3
> ![](8_Abstract_Data_Type.assets/image-20240306163518388.png)


# Invariants
> [!overview]
> An ==_invariant_== is a property of a program that is always true, for every possible runtime state of the program.


## Immutibility
> [!def]
> Immutability is one crucial invariant that we’ve already encountered: once created, an immutable object should always represent the same value, for its entire lifetime.




## Rep Exposure/Independence
> [!def]
> **Representation Exposure:** Code outside the class can modify the representation directly.
>  
>  **Representation Independence:** We can safely modify how we implement a class without affecting how clients can access the class's field and the clients can trust the specifications of the class that we give them to guide the usages.

> [!example] Example 1
> ![](8_Abstract_Data_Type.assets/image-20240306170625502.png)![](8_Abstract_Data_Type.assets/image-20240306170632906.png)

> [!example] Example 2
> ![](8_Abstract_Data_Type.assets/image-20240306170655844.png)






## Statically-checked Invariants
> [!example]
> ![](8_Abstract_Data_Type.assets/image-20240306170150514.png)



# Rep Invariants and Abstraction Function
## Basic Definition
> [!def]
> ![](8_Abstract_Data_Type.assets/image-20240309094938023.png)
> - **Abstraction functions** only map those representations that satisfy rep invariant to the abstraction space. 
> - **Abstraction functions** are always surjective. But not necessarily injective. Some representations wwon't be mapped.
> - **Rep Invariants** are boolean functions.
> - We want to make sure that after any operations(creators, producers, mutators, and even including observers), the rep invariant of ADT should be maintained.
> 
> ![](8_Abstract_Data_Type.assets/image-20240309093042599.png)

> [!example] Basic Example
> ![](8_Abstract_Data_Type.assets/image-20240309095257438.png)![](8_Abstract_Data_Type.assets/image-20240309095311359.png)

> [!example] What is a valid Rep Invariant?
> ![](8_Abstract_Data_Type.assets/image-20240309100113496.png)


## Who knows what?
> [!def]
> ![](8_Abstract_Data_Type.assets/image-20240309095623327.png)



## Implementations of AF/RI Pair
> [!important]
> ![](8_Abstract_Data_Type.assets/image-20240309103023304.png)![](8_Abstract_Data_Type.assets/image-20240309103030814.png)![](8_Abstract_Data_Type.assets/image-20240309103037393.png)![](8_Abstract_Data_Type.assets/image-20240309103044891.png)


## Check the Rep Invariants
> [!code]
```java
public class RatNum {

    private final int numerator;
    private final int denominator;

    // Rep invariant:
    //   denominator > 0
    //   numerator/denominator is in reduced form,
    //       i.e. gcd(|numerator|,denominator) = 1

    // Abstraction function:
    //   AF(numerator, denominator) = numerator/denominator

    /** 
     * Make a new RatNum == n.
     * @param n value
     */
    public RatNum(int n) {
        numerator = n;
        denominator = 1;
        checkRep();
    }

    /**
     * Make a new RatNum == (n / d).
     * @param n numerator
     * @param d denominator
     * @throws ArithmeticException if d == 0
     */
    public RatNum(int n, int d) {
        // reduce ratio to lowest terms
        int g = gcd(n, d);
        n = n / g;
        d = d / g;

        // make denominator positive
        if (d < 0) {
            numerator = -n;
            denominator = -d;
        } else {
            numerator = n;
            denominator = d;
        }
        checkRep();
    }
}
```
> [!def] Checking Rep Invariants
> ![](8_Abstract_Data_Type.assets/image-20240309103410827.png)

> [!example]
> ![](8_Abstract_Data_Type.assets/image-20240309103606622.png)
> Note: `checkRep()` is a rep invariant.



## Null Check
> [!important]
> ![](8_Abstract_Data_Type.assets/image-20240309103817011.png)
> Note that any object or array reference are implicitly assumed to be `not null`. In other words, there is automatically a `!=null` in the `Rep Invariant` comment even if we don't write it out explicitly.

> [!example]
> ![](8_Abstract_Data_Type.assets/image-20240309104105329.png)![](8_Abstract_Data_Type.assets/image-20240309104116725.png)![](8_Abstract_Data_Type.assets/image-20240309104122971.png)



# Beneficent Mutation
> [!def]





# Testing of ADTs
> [!def]
> ![](8_Abstract_Data_Type.assets/image-20240208131528960.png)![](8_Abstract_Data_Type.assets/image-20240208131602221.png)![](8_Abstract_Data_Type.assets/image-20240208131808574.png)![](8_Abstract_Data_Type.assets/image-20240208131819063.png)![](8_Abstract_Data_Type.assets/image-20240208131830948.png)![](8_Abstract_Data_Type.assets/image-20240208132119319.png)![](8_Abstract_Data_Type.assets/image-20240208132133371.png)![](8_Abstract_Data_Type.assets/image-20240208132145700.png)










