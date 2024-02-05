# Implementing Stack
> [!code]
> Note that once we use template class definition, we should keep all the implementations of the member functions inside the header file, instead of doing it separately in cpp file, which is different from non-template class definition. 
> 
> Thus, the implementation goes as follows:
```c++
#include <algorithm>

#include <iostream>

  

using namespace std;

  

template <typename T>

class OurStack {

    public:

        OurStack() {

            elems = new int[INITIAL_SIZE];

            logicalSize = 0;

            allocatedSize = INITIAL_SIZE;

        }

  

        /*

            Q: What is the ~OurStack() function? Why is each line in that function necessary? Why isn’t there any code in there involving the logicalSize or allocatedSize data members?

            A: This is the destructor. Its job is to deallocate any extra memory or resources that were allocated by the OurStack class and not otherwise automatically reclaimed. Here, we deallocate the memory we allocated earlier by using delete[]. We don’t need to do anything to logicalSize or allocatedSize because there were no dynamic allocations performed to get space for them. Generally speaking, you only need to explicitly clean up resources that you explicitly allocated.

        */

        ~OurStack() {

            delete[] elems;

            elems = nullptr;

        }

        void push(T elem) {

            if (isFull()) {

                grow();

            }

  

            elems[logicalSize] = elem;

            logicalSize++;

        }

        int pop() {

            if (isEmpty()) {

                cerr << "The stack is empty, cannot perform pop operation" << endl;

            }

  

            int res = elems[logicalSize];

            // elems[logicalSize] = nullptr;

            logicalSize;

            if (logicalSize < allocatedSize / 4) {

                setCapacity(allocatedSize / 2);

            }

            return res;

        }

        int peek() const {

            if (isEmpty()) {

                cerr << "The stack is empty, cannot perform peek operation" << endl;

            }

  

            return elems[logicalSize - 1];

        }

  

        int size() const {

            return logicalSize;

        }

  

        bool isEmpty() const {

            if (logicalSize == 0) {

                return true;

            }

  

            return false;

        }

  

        friend std::ostream& operator<<(std::ostream& out, const OurStack<T>& stack) {

            out << "From bottom to Top ";

            for (int i = 0; i < stack.logicalSize; i++) {

                out << stack.elems[i] << " ";

            }

            out << endl;

  

            return out;

        }

  

    private:

        T* elems;

        int logicalSize;

        int allocatedSize;

  

        static int const INITIAL_SIZE = 10;

  

        /* Q: In the OurStack::grow() function, one of the lines is delete[] elems,

              and in the next line we immediately write elems = newArr;.

              Why is it safe to do this? Doesn’t deleting elems make it unusable?

           A: The statement delete[] elems; means “destroy the memory pointed at by elems”

              rather than “destroy the elems variable.” As a result, after the first line executes

              , elems is still a perfectly safe variable to reassign.

        */

        void grow() {

            int* newElems = new int[allocatedSize * 2];

            for (int i = 0; i < logicalSize; i++)  {

                newElems[i] = elems[i];

            }

  

            delete[] elems;

            elems = newElems;

            allocatedSize *= 2;

        }

  
  

        /*

            Q: Explain why it would not be a good idea to cut the array size in half whenever fewer than half the elements are in use.

            A: Imagine we have a stack with logical size n – 1 and allocated size n.

               If we perform two pushes, we’ll double our stack’s allocated size to 2 n, which takes time O(n), and increase the logical size to n+1.

               If we now do two pops, we’ll drop the logical size down to n-1, which is less than half the allocated size.

               If we now shrink the allocated size by half down to n, we’ll have to do O(n) work transferring elements over, ending with a stack with logical size n – 1 and allocated size n.

               Overall, we’ve done two pushes and two pops, we’re right back where we’ve started, and we’ve done O(n) work. That’s a lot of work for very little payoff!

        */

        void setCapacity(int newSize) {

            int* newElems = new int[newSize];

            for (int i = 0; i < logicalSize; i++)  {

                newElems[i] = elems[i];

            }

  

            delete[] elems;

            elems = newElems;

            allocatedSize = newSize;

        }

  

        bool isFull() const {

            if (logicalSize == allocatedSize) {

                return true;

            }

  

            return false;

        }

}
```




# Hash Functions