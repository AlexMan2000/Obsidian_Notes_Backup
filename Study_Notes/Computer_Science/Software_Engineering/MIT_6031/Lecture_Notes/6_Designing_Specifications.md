# Deterministic vs Underdetermined Specs
> [!def]
> - Deterministic Spec is the one that once the precondition is satisfied, the outcome is completely determined.
> - Underdetermined Spec is the one that even if the precondition of the spec is satisfied, the outcome is still not fixed.
> - Nondeterministic Program(there is no saying as nondeterministic Spec) is the program that sometimes behave one way and somtimes another even if the input is the same. This may be because of random number or concurrent process.
> - Underdetermined Spec doesn't have to be non-deterministic implementation, it can be totally determinisitic.
> - Underdetermined Spec leaves enough freedom for the implementer to implement the method.
> - **An underdetermined spec is typically implemented by a fully-deterministic implementation.**

> [!example] Distinguished 
> ![](6_Designing_Specifications.assets/image-20240119103403973.png)![](6_Designing_Specifications.assets/image-20240119103420630.png)

> [!example] Over/under
> ![](6_Designing_Specifications.assets/image-20240119103530488.png)![](6_Designing_Specifications.assets/image-20240119103536918.png)



# Declarative vs Operational Specs
> [!def]
> - ==_Operational_== specifications give a series of steps that the method performs; pseudocode descriptions are operational. 
> - ==_Declarative_== specifications don’t give details of intermediate steps. Instead, they just give properties of the final outcome, and how it’s related to the initial state.
> - **Declarative specifications are preferable. ** They’re usually shorter, easier to understand, and most importantly, they don’t inadvertently expose implementation details that a client may rely on (and then find no longer hold when the implementation is changed).
> - **One reason programmers sometimes lapse into operational specifications is because they’re using the spec comment to explain the implementation for a maintainer. Don’t do that. When it’s necessary, use comments within the body of the method, not in the spec comment.**

> [!example] Joint Declaration
> ![](6_Designing_Specifications.assets/image-20240119104638987.png)


# Stronger vs Weaker Specs
> [!def]
> A specification S2 is ==_stronger_== than a specification S1 if the set of implementations that satisfy S2 is a strict subset of those that match S1.
> 
> A precondition is a predicate over the state of the input, so making a precondition stronger means shrinking the set of legal inputs. Similarly, a postcondition is a predicate over the state of the output, so a stronger postcondition shrinks the set of allowed outputs and effects.


> [!thm]
> A specification S2 is stronger than or equal to a specification S1 if and only if:
> - S2’s **precondition is weaker** than or equal to S1’s
> - S2’s **postcondition is stronger** than or equal to S1’s, for the states that satisfy S1’s precondition.

> [!example]
> ![](6_Designing_Specifications.assets/image-20240119110035821.png)![](6_Designing_Specifications.assets/image-20240119110113200.png)



# Diagramming Specifications
> [!def]
> You can imagine the specification as a circle in the space. The stronger the spec is, the larger the area it covers.
> 
> Each implementaion of the specification should be a point in the same space. If the implementation satisfy the spec, then this point goes into the spec circle.
> ![](6_Designing_Specifications.assets/image-20240119110746290.png)![](6_Designing_Specifications.assets/image-20240119110751597.png)
> As we see, strengthening the specification would limit of number of possible implementations, making the area of the circle smaller.

> [!example] Bulking up
> ![](6_Designing_Specifications.assets/image-20240119111038746.png)

> [!example] Strenghth is truth
> ![](6_Designing_Specifications.assets/image-20240119111149053.png)

> [!example] Finding findExactlyOne
> ![](6_Designing_Specifications.assets/image-20240119111412571.png)![](6_Designing_Specifications.assets/image-20240119111419270.png)

> [!example] Finding findCanBeMissing
> ![](6_Designing_Specifications.assets/image-20240119111452458.png)![](6_Designing_Specifications.assets/image-20240119111547649.png)

> [!example] Found
> ![](6_Designing_Specifications.assets/image-20240119111726561.png)![](6_Designing_Specifications.assets/image-20240119111743406.png)![](6_Designing_Specifications.assets/image-20240119111748870.png)


# Designing good specifications
## Coherent
> [!def]
> A coherent spec makes sense to its clients as a single, complete unit. The spec shouldn’t have lots of different cases. Long argument lists, boolean flags that enable or disable behavior, and intricate logic, are all signs of trouble.
> ![](6_Designing_Specifications.assets/image-20240119113021442.png)


## Infomative Results
> [!def]
> ![](6_Designing_Specifications.assets/image-20240119113039000.png)


## Strong Enough
> [!def]
> ![](6_Designing_Specifications.assets/image-20240119113127612.png)



## Weak Enough
> [!def]
> ![](6_Designing_Specifications.assets/image-20240119113134602.png)



## Use Abstract Types
> [!def]
> ![](6_Designing_Specifications.assets/image-20240119113157093.png)



# Precondition or Postcondition?
> [!important]
> In fact, the most common use of preconditions is to demand a property precisely because it would be hard or expensive for the method to check it.
> 
> Sometimes, it’s not feasible to check a condition without making a method unacceptably slow, and a precondition is often necessary in this case. If we wanted to implement the `find` method using binary search, we would have to require as a precondition that the array be sorted. Forcing the method to actually _check_ that the array is sorted would defeat the entire purpose of the binary search: to obtain a result in logarithmic and not linear time.




