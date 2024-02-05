



# Chained Hashing vs Linear Probing
## Chained Hashing
> [!important]
> Suppose we have an arbitrary object, we follows:
> 1. Compute the hash code of the object by calling `hash(obj)` to get the corresponding hash code `codeObj`.
> 2. Put the object into the linked list started at `bucket[codeObj]`。
> 
> To summarize:
> ![](Assign7_Hashing(Unfinished).assets/image-20240116155830138.png)![](Assign7_Hashing(Unfinished).assets/image-20240116155851022.png)



## Linear Probing - Open Addressing
### Insert an element
> [!important]
> ![](Assign7_Hashing(Unfinished).assets/image-20240116155951696.png)
> Here, the first step is the same as chained hashing where we compute the hashcode of the object. However the second step is very different. 
> When handling hash collision:
> 1. Chained hashing simply append the object at the end of the corresponding linked list.
> 2. Open Addressing find the next available slot to put the object in collision.The ways to find the next available slots can vary. Linear probing is one way to do so which simply linearly searches the table one by one until the slot is available.



### Look Up and Element
> [!important]
> ![](Assign7_Hashing(Unfinished).assets/image-20240116160323970.png)


### Delete an Element
> [!important]
> ![](Assign7_Hashing(Unfinished).assets/image-20240116160648523.png)
> Due to the way we look up the element. Since the looking up process ended when we encounter a blank slot or when all the occupied slots have been examined. So if we delete the element just by removing it without any post processing, we may not find certain elements even if they are there, as the following example shows:
> 
> ![](Assign7_Hashing(Unfinished).assets/image-20240116161028084.png)
> Here we want to find $r$ but the $w$ between $r$ and $x$ is deleted with a blank slot, which prevents us from moving forward to the $r$ at slot 9.
> 
> ![](Assign7_Hashing(Unfinished).assets/image-20240116161149601.png)![](Assign7_Hashing(Unfinished).assets/image-20240116161238649.png)


### Summary
> [!important]
> ![](Assign7_Hashing(Unfinished).assets/image-20240116161334699.png)





# Efficiency Comparison
## Chained Hashing
> [!important]
> ![](Assign7_Hashing(Unfinished).assets/image-20240116161602482.png)![](Assign7_Hashing(Unfinished).assets/image-20240116161614055.png)![](Assign7_Hashing(Unfinished).assets/image-20240116161638126.png)


## Linear Probing
> [!important]
> ![](Assign7_Hashing(Unfinished).assets/image-20240116161819194.png)




# Robin Hood Hashing
## Why we need it?
> [!important]
> ![](Assign7_Hashing(Unfinished).assets/image-20240116181547748.png)
> We want to lower the variance of the number of steps used to find an abitrary element. So we will utilize this algorithm to smooth out the steps.


## Inserting Elements
### Idea
> [!important]
> ![](Assign7_Hashing(Unfinished).assets/image-20240116162358326.png)

### Demo
> [!important]
> ![](Assign7_Hashing(Unfinished).assets/image-20240116162419572.png)![](Assign7_Hashing(Unfinished).assets/image-20240116162424674.png)![](Assign7_Hashing(Unfinished).assets/image-20240116162432883.png)![](Assign7_Hashing(Unfinished).assets/image-20240116162440057.png)![](Assign7_Hashing(Unfinished).assets/image-20240116162447063.png)![](Assign7_Hashing(Unfinished).assets/image-20240116162453930.png)![](Assign7_Hashing(Unfinished).assets/image-20240116162459243.png)![](Assign7_Hashing(Unfinished).assets/image-20240116162505615.png)![](Assign7_Hashing(Unfinished).assets/image-20240116162512774.png)![](Assign7_Hashing(Unfinished).assets/image-20240116162523008.png)![](Assign7_Hashing(Unfinished).assets/image-20240116162534737.png)![](Assign7_Hashing(Unfinished).assets/image-20240116162541151.png)



## Looking up Elements
> [!important]
> ![](Assign7_Hashing(Unfinished).assets/image-20240116162925082.png)


## Deleting Elements
> [!important]
> ![](Assign7_Hashing(Unfinished).assets/image-20240116163131515.png)![](Assign7_Hashing(Unfinished).assets/image-20240116163159552.png)![](Assign7_Hashing(Unfinished).assets/image-20240116163207530.png)![](Assign7_Hashing(Unfinished).assets/image-20240116163212319.png)![](Assign7_Hashing(Unfinished).assets/image-20240116163218362.png)![](Assign7_Hashing(Unfinished).assets/image-20240116163223891.png)![](Assign7_Hashing(Unfinished).assets/image-20240116163229083.png)



## Summary
> [!important]
> ![](Assign7_Hashing(Unfinished).assets/image-20240116163250568.png)





# Linear Probing Hashing Implementations
## Code(CS106B)
> [!code]
> **Remarks:**
> 1. Linear Probing uses `SlotType`(enumeration type) to indicate the state of a slot.
> 2. The fixed number of slots should be determined by calling `hashFn.numSlots()`, otherwise the wrap around test will always fail.
> 3. Don't forget to update the `logicalSize` (actual number of elements in the hashtable) upon insertion or removal.
> 4. Don't forget to recycle from the tombstones so that we can make use of the slots that underwent the deletion operations. Recycle operation happens in `insert()` operation.
> 5. Don't forget to initialize every slot to be empty.
```c++
#include "LinearProbingHashTable.h"
using namespace std;

LinearProbingHashTable::LinearProbingHashTable(HashFunction<string> hashFn) {
    this -> hashFn = hashFn;
    this -> logicalSize = 0;
    int numSlots = this -> hashFn.numSlots();
    this -> allocatedSize  = numSlots;
    this -> elems = new Slot[numSlots];
    for (int i = 0; i < numSlots; i++) {
        this -> elems[i].type = SlotType::EMPTY;
    }
}

LinearProbingHashTable::~LinearProbingHashTable() {
    delete[] elems;
    elems = nullptr;
    logicalSize = 0;
}

int LinearProbingHashTable::size() const {
    return logicalSize;
}

bool LinearProbingHashTable::isEmpty() const {
    return logicalSize == 0;
}

bool LinearProbingHashTable::isFull() const {
    return logicalSize == allocatedSize;
}


bool LinearProbingHashTable::insert(const string& elem) {
    if (isFull()) {
        return false;
    }


    // Test whether insertion would cause duplicates
    if (contains(elem)) {
        return false;
    }


    int hashCode = hashFn(elem);


    // Start searching through the hashtable
    int counter = 0;
    int start = hashCode;

    // Search through the hashtable to see if elem is already there
    // Meanwhile, actively looking for blank spot for elem to be placed.
    while (!(elems[start].type == SlotType::EMPTY) && counter < allocatedSize) {
        if (elems[start].value == elem && elems[start].type == SlotType::FILLED) {
            return false;
        }


        // Recycle the tombstones
        if (elems[start].type == SlotType::TOMBSTONE) {
            elems[start].value = elem;
            elems[start].type = SlotType::FILLED;
            logicalSize++;
            return true;
        }
        start++;
        start = start % allocatedSize;
        counter++;
    }

    // Find a blank spot
    if (counter != allocatedSize) {
        elems[start].value = elem;
        elems[start].type = SlotType::FILLED;
        logicalSize++;
        return true;
    }

    // We have traversed the whole hashTable
    return false;
}

bool LinearProbingHashTable::contains(const string& elem) const {
    if (isEmpty()) {
        return false;
    }


    int hashCode = hashFn(elem);


    // Starting searching through the hashtable
    int counter = 0;
    int start = hashCode;
    while (!(elems[start].type == SlotType::EMPTY) && counter < allocatedSize) {
        if (elems[start].value == elem && elems[start].type == SlotType::FILLED) {
            return true;
        }
        start++;
        start = start % allocatedSize;
        counter++;
    }


    return false;
}

bool LinearProbingHashTable::remove(const string& elem) {
    if (isEmpty()) {
        return false;
    }


    int hashCode = hashFn(elem);

    int counter = 0;
    int start = hashCode;

    // Search through the hashtable to see if elem is already there
    while (!(elems[start].type == SlotType::EMPTY) && counter < allocatedSize) {
        if (elems[start].value == elem && elems[start].type == SlotType::FILLED) {
            elems[start].value = "";
            elems[start].type = SlotType::TOMBSTONE;
            logicalSize--;
            return true;
        }
        start++;
        start = start % allocatedSize;
        counter++;
    }

    // The element is not in the hash table.
    return false;
}

```


## Testing
> [!test]
> ![](Assign7_Hashing(Unfinished).assets/image-20240116174132295.png)




# Robin Hood Hasing Implementations
## Code (CS106B) - Stress Test Pending
> [!code]
> **Remarks:**
> 1. `Robin Hood Hashing` uses a sufficiently large negative number -137 to indicate that the slot is empty(or blank), which is different from linear probing.
> 2. **You should mark slots empty by setting their distance value to the constant `EMPTY_SLOT`.** Any slot whose distance is not the value `EMPTY_SLOT` is assumed to be full and to be the indicated number of spots away from home.
```c++
#include "RobinHoodHashTable.h"
using namespace std;

RobinHoodHashTable::RobinHoodHashTable(HashFunction<string> hashFn) {
    this -> hashFn = hashFn;
    this -> logicalSize = 0;
    int numSlots = this -> hashFn.numSlots();
    this -> allocatedSize  = numSlots;
    this -> elems = new Slot[numSlots];
    for (int i = 0; i < allocatedSize; i++) {
        this -> elems[i].distance = EMPTY_SLOT;
    }
}

RobinHoodHashTable::~RobinHoodHashTable() {
    delete[] this -> elems;
    elems = nullptr;
    this -> logicalSize = 0;
}

int RobinHoodHashTable::size() const {
    return this -> logicalSize;
}

bool RobinHoodHashTable::isEmpty() const {
    return this -> logicalSize == 0;
}

bool RobinHoodHashTable::isFull() const {
    return this -> logicalSize == allocatedSize;
}


bool RobinHoodHashTable::insert(const Slot& elem, int start) {
    int distance = elem.distance;
    while (!(elems[start].distance == EMPTY_SLOT)) {
        if (distance > elems[start].distance) {
            Slot currentElement = elems[start];
            elems[start] = {elem.value, distance};
            return insert(currentElement, start);
        }
        start++;
        start = start % allocatedSize;
        distance++;
    }

    elems[start] = {elem.value, distance};
    logicalSize++;

    return true;
}

bool RobinHoodHashTable::insert(const string& elem) {
    // 1. If is full or alreay exists, return false
    if (isFull() || contains(elem)) {
        return false;
    }

    // 2. Start searching annd inserting
    int start = hashFn(elem);
    int distance = 0;
    while (!(elems[start].distance == EMPTY_SLOT)) {
        if (distance > elems[start].distance) {
            Slot currentElement = elems[start];
            elems[start] = {elem, distance};
            return insert(currentElement, start);
        }
        start++;
        start = start % allocatedSize;
        distance++;
    }


    elems[start] = {elem, distance};
    logicalSize++;


    return true;
}

bool RobinHoodHashTable::contains(const string& elem) const {
    int hashCode = hashFn(elem);

    int start = hashCode;
    int counter = 0; // Used to terminate when wwe have traversed all the elements in the hashtable
    int distance = 0; // Used to stop early

    while (!(elems[start].distance == EMPTY_SLOT) && counter < allocatedSize) {
        // Find the element before quitting the loop or early stop
        if (elems[start].value == elem) {
            return true;
        }

        // Early Stop
        if (distance > elems[start].distance) {
            return false;
        }
        start++;
        start = start % allocatedSize;
        counter++;
        distance++;
    }

    // Find a blank spot or searched through all the hashtable(actually impossible due to early stop)
    return false;
}

bool RobinHoodHashTable::remove(const string& elem) {
    if (isEmpty() || !contains(elem)) {
        return false;
    }

    int hashCode = hashFn(elem);
    int start = hashCode;


    while (!(elems[start].value == elem)) {
        start++;
        start = start % allocatedSize;
    }

    elems[start].distance = EMPTY_SLOT;
    logicalSize--;


    int next = start + 1;
    next = next % allocatedSize;
    while(!(elems[next].distance == 0) && elems[next].distance != EMPTY_SLOT) {
        elems[start] = elems[next];
        elems[start].distance -- ;
        elems[next].distance = EMPTY_SLOT;
        next++;
        next = next % allocatedSize;
        start++;
        start = start % allocatedSize;
    }

    return true;
}
```



## Testing -  Infinite Recursion
> [!test]



