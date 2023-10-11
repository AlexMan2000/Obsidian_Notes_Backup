# Environment Setup
> [https://sp21.datastructur.es/materials/lab/lab1/lab1SnapsSetupWindows.html](https://sp21.datastructur.es/materials/lab/lab1/lab1SnapsSetupWindows.html)



# Collatz Sequence
> 也称为`Hailstone Sequence`, 我们在`CS61A`中见过。


## Javadoc
> ![image.png](./L2101__Environment_Setup_Collatz_Sequence.assets/20230302_0931331665.png)


## Fix the Bug
> ![image.png](./L2101__Environment_Setup_Collatz_Sequence.assets/20230302_0931334825.png)![image.png](./L2101__Environment_Setup_Collatz_Sequence.assets/20230302_0931336979.png)

```java
/** Class that prints the Collatz sequence starting from a given number.
 *  @author YOUR NAME HERE
 */
public class Collatz {

    /** Buggy implementation of nextNumber! */
    public static int nextNumber(int n) {
        if (n  == 128) {
            return 1;
        } else if (n == 5) {
            return 3 * n + 1;
        } else {
            return n * 2;
        }
    }

    public static void main(String[] args) {
        int n = 5;
        System.out.print(n + " ");
        while (n != 1) {
            n = nextNumber(n);
            System.out.print(n + " ");
        }
        System.out.println();
    }
}
```
```java
/** Class that prints the Collatz sequence starting from a given number.
 *  @author YOUR NAME HERE
 */
public class Collatz {

    /** Buggy implementation of nextNumber! */
    public static int nextNumber(int n) {
        if (n  == 128) {
            return 1;
        } else if (n % 2 == 1) {
            return 3 * n + 1;
        } else {
            return n / 2;
        }
    }

    public static void main(String[] args) {
        int n = 5;
        System.out.print(n + " ");
        while (n != 1) {
            n = nextNumber(n);
            System.out.print(n + " ");
        }
        System.out.println();
    }

}
```


## Fun Facts
> ![image.png](./L2101__Environment_Setup_Collatz_Sequence.assets/20230302_0931339551.png)



# Submission
> ![image.png](./L2101__Environment_Setup_Collatz_Sequence.assets/20230302_0931342090.png)

