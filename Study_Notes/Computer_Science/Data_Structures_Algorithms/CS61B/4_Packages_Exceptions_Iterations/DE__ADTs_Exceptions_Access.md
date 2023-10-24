# 1 Discussion
## ADTs - sp18
[disc05.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674528982641-0006e57d-4f00-48db-a35e-9aba47b346ed.pdf)
[disc05sol.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674528982709-2fbbff83-071e-4b34-9883-22933eb7a35d.pdf)
[Discussion 5 Slides.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674529453730-04eba71f-9e1c-4ec0-a6cb-6c7f06c11ae6.pdf)

### ADT APIs
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944278997.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944272514.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944289993.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944287961.png)
:::


### Q1 Problems with ADTs⭐⭐
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944283391.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944288199.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944283720.png)
考察知识点：ADT&APIs
:::
**Solution**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944289172.png)


### Q2 BidDividerMap⭐⭐
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944296675.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944299864.png)
考察知识点: ADT&APIs
:::
**Solution (a)**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944295347.png)
**Solution (b)**⭐⭐⭐![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944298076.png)
小于`Median`的`PQL`的`Priority`是越大的数优先级越高
大于`Median`的`PQR`的`Priority`是越小的数优先级越高
每次加入一个数就重新计算一下`Median`, 然后调整两个`PQs`中的元素，只需要移动`PQL`中的一个到`PQR`或者移动`PQR`中的一个到`PQL`。


### Q3 Queue from Stacks⭐⭐⭐⭐⭐
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944291979.png)
:::
```java
import java.util.ArrayList;
import java.util.List;

/**
 * Created by AlexMan
 */
public class UserQueue<T> {

    private int size;
    private UserStack<T> s1;

    public UserQueue() {
        s1 = new UserStack<>();
        size = 0;
    }


    public void push(T item) {
        s1.push(item);
        size++;
    }

    public T pop() {
        if (s1.isEmpty()) {
            return null;
        }
        UserStack<T> auxStack = new UserStack<>();
        while (!s1.isEmpty()) {
            auxStack.push(s1.pop());
        }
        T elem = auxStack.pop();
        while (!auxStack.isEmpty()) {
            s1.push(auxStack.pop());
        }
        size--;
        return elem;
    }

    public T get(int index) {
        if (index < 0 || index >= size) {
            return null;
        }
        UserStack<T> temp = new UserStack<>();
        int popNum = size - index;
        while (popNum > 1) {
            temp.push(s1.pop());
            popNum--;
        }
        T res = s1.pop();
        // Restore the data structure
        s1.push(res);
        while (!temp.isEmpty()) {
            s1.push(temp.pop());
        }
        return res;
    }

    /**
     * Used for test
     * @return
     */
    public List<T> getArray() {
        UserStack<T> us = new UserStack<>();
        List<T> list = new ArrayList<>();
        while (!s1.isEmpty()) {
            us.push(s1.pop());
        }
        while (!us.isEmpty()) {
            list.add(us.pop());
        }
        return list;
    }



    @Override
    public boolean equals(Object o) {
        if (this == o) {
            return true;
        }
        if (this == null || o == null) {
            return false;
        }
        if (this.getClass() != o.getClass()) {
            return false;
        }
        UserQueue<T> casted = (UserQueue) o;
        List<T> castedArray = casted.getArray();
        List<T> thisArray = this.getArray();
        return castedArray.equals(thisArray);
    }


    @Override
    public String toString() {
        List<T> thisArray = this.getArray();
        StringBuilder sb = new StringBuilder();
        sb.append("[");
        for (int i = 0; i < thisArray.size() - 1; i++) {
            sb.append(thisArray.get(i) + ", ");
        }
        sb.append(thisArray.get(thisArray.size() - 1));
        sb.append("]");
        return sb.toString();
    }
}
```
```java
/**
 * Created by AlexMan
 */
public class UserQueueOneStack<T> extends UserQueue<T>{

    private UserStack<T> s1;
    private int size;

    public UserQueueOneStack() {
        s1 = new UserStack<>();
        size = 0;
    }

    @Override
    public void push(T item) {
        s1.push(item);
    }

    @Override
    public T pop() {
        if (s1.isEmpty()) {
            return null;
        }
        return pop(s1.pop());
    }


    /**
     * Recursive Implementation of pop, helper function
     * @param previous, used as the recursion state
     * @return the bottom element in the stack
     */
    public T pop(T previous) {
        if (s1.isEmpty()) {
            return previous;
        }
        T current = s1.pop();
        T res = pop(current);
        // Revoke
        push(previous);
        return res;
    }
}
```
```java
import edu.princeton.cs.algs4.Stack;

/**
 * Created by AlexMan
 */
public class UserStack<T> extends Stack<T> {
}

```
```java
import org.junit.Test;
import static org.junit.Assert.*;

/**
 * Created by AlexMan
 */
public class TestingUserQueue {

    @Test
    public void randomizeTestPushPop() {
        UserQueue<Integer> s1 = new UserQueue<>();
        UserQueueOneStack<Integer> s2 = new UserQueueOneStack<>();
        RightQueue<Integer> exp = new RightQueue<>();
        StringBuilder sb = new StringBuilder();
        int N = 1000;
        for (int i = 0; i < N; i++) {
            double rand = StdRandom.uniform();
            int randInt = StdRandom.uniform(10);
            if (rand > 0.5) {
                s1.push(randInt);
                s2.push(randInt);
                exp.push(randInt);
                sb.append("push(");
                sb.append(randInt + ")\n");
            } else {
                Integer popped1 = s1.pop();
                Integer popped2 = s2.pop();
                Integer poppedExp = exp.pop();
                assertEquals("s1 pop()", popped1, poppedExp);
                assertEquals("s2 pop()", popped2, poppedExp);
            }
        }

    }

    @Test
    public void testGet() {
        UserQueue<Integer> s1 = new UserQueue<>();
        for (int i = 0; i < 5; i++) {
            s1.push(i);
        }
        for (int i = 0; i < 5; i++) {
            assertEquals(s1.get(i), (Integer) i);
        }
    }
}

```


## Access Control&ADT&Packages - sp18
[disc06.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674529463888-2092c409-8933-4ccd-a3e7-70f3413dce16.pdf)
[disc06sol.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674529463895-12887629-b73d-4fec-8240-f4f3bd3c7bcb.pdf)
[Discussion 6_Slides.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674529464110-2f4992b1-32ae-4af4-b8dd-83c1c8de8b38.pdf)


### Q1 Access Control
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944305580.png)
:::
**Solutions**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944301899.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944306217.png)


### Q2 Stack ADT - Exception⭐⭐⭐
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944307063.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944306868.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944309027.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944304694.png)
:::
```java
/**
 * Created by AlexMan
 */
public class BadIntegerStack {

    public class Node {
        public Integer value;
        public Node prev;

        public Node(Integer v, Node n) {
            this.value = v;
            this.prev = n;
        }
    }

    // The pointer to the top of the stack
    public Node top;

    public boolean isEmpty() {
        return top == null;
    }
    
    
    public void push(Integer num) {
        top = new Node(num, top);
    }

    public Integer pop() {
        Integer ans = top.value;
        top = top.prev;
        return ans;
    }

    public Integer peek() {
        return top.value;
    }

    public static void main(String[] args) {
        
    }
}
```
```java
/**
 * Created by AlexMan
 */
public class BadIntegerStack {

    public class Node {
        public Integer value;
        public Node prev;

        public Node(Integer v, Node n) {
            this.value = v;
            this.prev = n;
        }
    }

    // The pointer to the top of the stack
    public Node top;

    public boolean isEmpty() {
        return top == null;
    }


    public void push(Integer num) {
        top = new Node(num, top);
    }

    public Integer pop() {
        Integer ans = top.value;
        top = top.prev;
        return ans;
    }

    public Integer peek() {
        return top.value;
    }

    public static void main(String[] args) {
        BadIntegerStack temp = new BadIntegerStack();
        try {
            Integer ans = temp.pop();
        } catch (NullPointerException e) {
            System.out.println("Success");
        }
        
        
        // Due to the public keyword, we can freely modify the structure
        // of the stack outside of the class(from the client side)
        temp.push(1);
        temp.top.prev = temp.top;
        while (!temp.isEmpty()) {
            temp.pop();
        }
        System.out.println("This statement is unreachable");
    }
}
```
**Solutions**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944304198.png)


### Q3 Package Design
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944319688.png)
Detailed Implementation in `disc6/ParkingLot`（有点问题）, 要注意的是，我们在使用类继承的时候`Dynamic Method Selection`只在我们使用了`@Override`之后才会生效，否则执行的永远是父类的方法，更新的也永远是父类中的实例变量或者是类变量。
`extends`关键字不会继承`Constructor`构造器，每新增一个子类都会需要写一个子类专属的`Constructor`。
子类可以**继承(没有**`**Override**`**重写)**父类中**用于修改/获取父类实例变量/类变量的方法**，但是子类调用从父类继承而来的方法的时候，修改/获取的永远是父类中的变量。这点要注意。
:::
**Formal Solution**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944313856.png)

## Exceptions&PolyMorphism&Iterables - sp19/21
[disc05_19.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674529198495-eede20d9-5e02-41c8-b4a1-f2e59f27a4c7.pdf)
[disc05sol_19.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674529198545-23cd6c7c-7490-4240-884f-d075c7dc187d.pdf)
[Discussion 5 Slides_19.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674529198766-701c9da5-816e-4ae7-bc08-4c3fda5114cb.pdf)
[disc05_21.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674529087358-95b052a2-3495-4b76-8b86-16b5680fe96c.pdf)
[disc05sol_21.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674529087373-2b2a4c28-77db-4954-b890-900f3cf99863.pdf)


### Q1 Iterators Warmup
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944318560.png)
:::
**Solution**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944313879.png)


### Q2 Office Hour Queue⭐⭐⭐
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944315402.png)
:::


#### Q2a Create an iterator
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944312547.png)
:::
```java
import java.util.Iterator;

/**
 * Created by AlexMan
 */
public class OHIterator implements Iterator<OHRequest> {
    OHRequest curr;

    public OHIterator(OHRequest queue) {
        curr = queue;
    }

    public boolean isGood(String description) {
        return description != null && description.length() > 5;
    }

    @Override
    public boolean hasNext() {
        while (curr != null && !isGood(curr.description)) {
            curr = curr.next;
        }
        return curr != null;
    }

    @Override
    public OHRequest next() {
        if (hasNext()) {
            OHRequest or = curr;
            curr = curr.next;
            return or;
        } else {
            throw new RuntimeException("StopIteration");
        }
    }
}

```
**Solution**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944318866.png)

#### Q2b OfficeHourQueue
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944325382.png)
:::
```java
import java.util.Iterator;

/**
 * Created by AlexMan
 */
public class OfficeHoursQueue implements Iterable<OHRequest> {

    OHRequest start;

    public OfficeHoursQueue (OHRequest queue) {
        start = queue;
    }

    public static void main(String[] args) {
        OHRequest s1 = new OHRequest("Failing my test for get in arrayDeque, NPE", "Pam", null);
        OHRequest s2 = new OHRequest("conceptual: what is dynamic method selection", "Michael", s1);
        OHRequest s3 = new OHRequest("git: what does checkout do.", "Jim", s2);
        OHRequest s4 = new OHRequest("help", "Dwight", s3);
        OHRequest s5 = new OHRequest("debugging get(i)", "Creed", s4);
        for (OHRequest or: new OfficeHoursQueue(s5)) {
            System.out.println(or.description);
        }
    }

    @Override
    public Iterator<OHRequest> iterator() {
        return new OHIterator(start);
    }
}

```
**Solution**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944325069.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944323334.png)


#### Q2c Main Method
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944326237.png)
:::
```java
import java.util.Iterator;

/**
 * Created by AlexMan
 */
public class OfficeHoursQueue implements Iterable<OHRequest> {

    OHRequest start;

    public OfficeHoursQueue (OHRequest queue) {
        start = queue;
    }

    public static void main(String[] args) {
        OHRequest s1 = new OHRequest("Failing my test for get in arrayDeque, NPE", "Pam", null);
        OHRequest s2 = new OHRequest("conceptual: what is dynamic method selection", "Michael", s1);
        OHRequest s3 = new OHRequest("git: what does checkout do.", "Jim", s2);
        OHRequest s4 = new OHRequest("help", "Dwight", s3);
        OHRequest s5 = new OHRequest("debugging get(i)", "Creed", s4);
        for (OHRequest or: new OfficeHoursQueue(s5)) {
            System.out.println(or.description);
        }
    }

    @Override
    public Iterator<OHRequest> iterator() {
        return new OHIterator(start);
    }
}

```
**Solution**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944324113.png)


### Q3 Thank u, next - TYIterator⭐⭐⭐
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944326444.png)
:::
```java
/**
 * Created by AlexMan
 */
public class TYIterator extends OHIterator{

    public TYIterator(OHRequest queue) {
        super(queue);
    }

    
    @Override
    public OHRequest next() {
        OHRequest result = super.next();
        if (curr != null && curr.description.contains("thank u")) {
            curr = curr.next;
        }
        return result;
    }
}

```



# 2 Exam Prep
## Sp18 - Comparator&Data Structure
[examprep05.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674528971461-816ec093-6600-40cc-b86e-8ecc1da5eda5.pdf)
[examprep05sol.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674528971509-e75ee77d-9e71-4d44-84dd-35d24a38f018.pdf)
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944338009.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944337551.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944331181.png)
:::



### Q1 Use Assorted ADT!⭐⭐⭐
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944336468.png)
:::
**Solutions**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944335419.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944339294.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944347834.png)



### Q2 Mutant ADTs
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944349228.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944343219.png)
:::
**Solution (a)**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944345150.png)
**Solution (b)**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944347335.png)


## Sp19
[examprep05_19.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674529253051-ea309852-d460-42e6-bf92-11f8017f3ebf.pdf)
[examprep05sol_19.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674529253098-fb3ab36a-7962-4214-98c1-b0a3be1c6ef5.pdf)

### Q1 FilteredList - Predicate
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944346137.png)
:::
```java
import java.util.Iterator;
import java.util.List;

/**
 * Created by AlexMan
 */
public class FilteredList<T> implements Iterable<T> {
    private List<T> FL;

    public FilteredList (List<T> L, Predicate<T> filter) {
        for (T elem: L) {
            if (filter.test(elem)) {
                FL.add(elem);
            }
        }
    }

    @Override
    public Iterator<T> iterator() {
        return new NumberIterator();
    }


    public class NumberIterator implements Iterator<T> {

        private int index;

        @Override
        public boolean hasNext() {
            return index < FL.size();
        }

        @Override
        public T next() {
            if (!hasNext()) {
                throw new RuntimeException("StopIteration");
            }
            T res = FL.get(index);
            index++;
            return res;
        }
    }
}
```
```java
import java.util.Iterator;
import java.util.List;

/**
 * Created by AlexMan
 */
public class FilteredList<T> implements Iterable<T> {
    List<T> FL;
    Predicate<T> pred;

    public FilteredList (List<T> L, Predicate<T> filter) {
        FL = L;
        pred = filter;
    }

    @Override
    public Iterator<T> iterator() {
        return new NumberIterator(FL, pred);
    }


    public class NumberIterator implements Iterator<T> {
        List<T> FL;
        Predicate<T> pred;
        int index;

        public NumberIterator(List<T> L, Predicate<T> filter) {
            this.FL = L;
            this.pred = filter;
            index = 0;
        }

        @Override
        public boolean hasNext() {
            if (index < FL.size() && !pred.test(FL.get(index))) {
                index++;
            }
            return index < FL.size();
        }

        @Override
        public T next() {
            if (!hasNext()) {
                throw new RuntimeException("StopIteration");
            }
            T res = FL.get(index);
            index++;
            return res;
        }
    }
}

```


### Q2 Iterator of Iterators⭐⭐⭐⭐⭐
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944346547.png)
本质上我们希望不断地在整个`List`中进行循环，则我们可以使用`%`操作来实现，代码如下:
:::
**Solution**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944359772.png)
```java
import java.util.Iterator;
import java.util.LinkedList;
import java.util.List;
import java.util.NoSuchElementException;

/**
 * Created by AlexMan
 */
public class IteratorOfIterators implements Iterator<Integer>{
    LinkedList<Integer> ll ;

    public IteratorOfIterators(List<Iterator<Integer>> a) {
        ll = new LinkedList<>();

        // Used for circular index; 0,1,2,0,1,2,0,1,2 for example.
        int i = 0;
        
        while (!a.isEmpty()) {
            // Get the i-th iterator
            Iterator<Integer> curr = a.get(i);
            if (curr.hasNext()) {
                ll.add(curr.next());
            } else {
                a.remove(curr);
                i--; //Make sure that the index is working just right
            }
            // If a is empty after the removal process above, then break the while loop
            if (a.isEmpty()) {
                break;
            }
            // Circular index
            i = (i + 1) % a.size();
        }
    }

    @Override
    public boolean hasNext() {
        return !ll.isEmpty();
    }

    @Override
    public Integer next(){
        return ll.removeFirst();
    }
}

```


### Q3 Every K-th Item
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944353020.png)![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944358061.png)
:::
```java
import java.util.Iterator;
import java.util.NoSuchElementException;

/**
 * Created by AlexMan
 */
public class KthIntList implements Iterator<Integer> {
    public int k;
    private IntList curList;
    private boolean hasNext;

    public KthIntList(IntList I, int k) {
        this.k = k;
        this.curList = I;
        this.hasNext = true;
    }

    /**
     * Returns true iff there is a next Kth element. Do not modify.
     * @return
     */
    @Override
    public boolean hasNext() {
        return this.hasNext;
    }


    /**
     * Returns the next Kth element of the IntList given in the constructor.
     * Returns the 0th element first. Throws a NoSuchElementException if there
     * are no Integers available to return
     * @return
     */
    @Override
    public Integer next() {
        if (!hasNext()) {
            throw new NoSuchElementException();
        }
        Integer res = this.curList.first;
        int i = 0;
        while (i < k && this.curList != null) {
            this.curList = this.curList.rest;
            i++;
        }
        if (i < k){
            this.hasNext = false;
        }
        return res;
    }

}

```
**Alternative Solution**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944358092.png)


## Sp21
[examprep05_21.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674529302672-02d3d7ae-ce55-49b6-978f-5e42d434c2cf.pdf)
[examprep05sol_21.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674529302682-f17c2e44-81ea-40c7-aef0-8ce436aef843.pdf)


### Q1 DMSComparator⭐⭐⭐⭐⭐
:::info
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944353980.png)
:::
**Explanations**本题非常重要，我们来分析一下:

1. `compare(animal, dog) => negative`
   - `first`: 静态方法绑定的是`Animal.speak(Animal a) {return 2}`, 然后动态执行的也是这个方法，所以，`first = 2`
   - `second`: 静态方法绑定的是`Animal.speak(Animal a) {return 2}`, 然后动态执行的是`Dog.speak(Animal a) { return 3 }`, 所以`second = 3`
   - `third`: 静态方法绑定的是`Animal.speak(Dog a) {return 1}`, 然后动态执行的也是这个，所以`third = 1`
   - `fourth`: 静态方法绑定的是`Animal.speak(Dog a) {return 1}`, 然后动态执行的是也是这个，因为`Dog`类中没有对这个方法进行重写操作，所以`fourth = 1`
2. `compare(dog, animal) => positive`
   - `first`: 静态方法绑定的是`Animal.speak(Animal a) {return 2}`, 然后动态执行的是`Dog.speak(Animal a) {return 3}`，所以`first = 3`
   - `second`: 静态方法绑定的是`Animal.speak(Animal a) {return 2}`, 然后动态执行的也是这个, 所以`second = 2`
   - `third`: 静态方法绑定的是`Animal.speak(Dog a) {return 1}`, 然后动态执行的也是这个，因为`Dog`类中没有对这个方法进行重写操作，所以`third = 1`
   - `fourth`: 静态方法绑定的是`Animal.speak(Dog a) {return 1}`, 然后动态执行的是也是这个，所以`fourth = 1`
3. `compare(dog, dog) => zero`

因为`o1`和`o2`一样，所以`first == second`,`third == fourth`一定成立，所以这可以作为我们第一个`if`的条件。

4. `compare(poodle, dog) => positive` 
   - `first`: 静态方法绑定的是`Animal.speak(Animal a) {return 2}`, 然后动态执行的也是这个方法，所以，`first = 2`
   - `second`: 静态方法绑定的是`Animal.speak(Animal a) {return 2}`, 然后动态执行的是`Dog.speak(Animal a){ return 3 }`, 所以`second = 3`
   - `third`: 静态方法绑定的是`Animal.speak(Dog a) {return 1}`, 然后动态执行的是`Poodle.speak(Dog a) {return 4}`，所以`third = 4`
   - `fourth`: 静态方法绑定的是`Animal.speak(Dog a) {return 1}`, 然后动态执行的是也是这个，因为`Dog`类中没有对这个方法进行重写操作，所以`fourth = 1`
5. `compare(dog, poodle) => negative`

和之前的推算方法一致即可。
综上，我们知道，`positive`的情况有两种`third == 4`或者`first == 3 && second == 2`。
**Solution**![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944357920.png)
![image.png](DE__ADTs_Exceptions_Access.assets/20230302_0944358935.png)
