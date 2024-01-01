# Sort Algorithm
> [!concept]
> `std::sort(IteratorStart, IteratorEnd, Comparator)`
> 

> [!example] Sorting the course ratings
> 
```C++
std::sort(courses.begin(), courses.end(), compareRatings);
std::copy(courses.begin(), courses.end(),
std::ostream_iterator<Course>(std::cout, "\n"));
```
> [!test] Output
> ![](STL_Algorithms.assets/image-20231231171102797.png)



# Stable-Partition
> [!concept]
> All the elements that causes the unary predicate to return true will appear at the front 
> 
> All the elements that causes the unary predicate to return false appear at the end.
> 
> The relative order of the elements won't change.
> ![](STL_Algorithms.assets/image-20231231120526365.png)![](STL_Algorithms.assets/image-20231231120531969.png)

> [!example] How to use
> ![](STL_Algorithms.assets/image-20231231120549773.png)

> [!test] Output
> ![](STL_Algorithms.assets/image-20231231171051675.png)




# Copy_If
> [!concept]
> Basically `std::copy_if` will copy the elements that satisfy the predicate to a new container(parametrized by an iterator). 
> ![](STL_Algorithms.assets/image-20231231121731714.png)
> Here in the code, `csCourses` is an iterator, but without the ability to expand the size(since iterator is not a member function of the container) of its container. Without such ability, once we copy too many elements so that we exceed the bound of the container, segment fault will happen as follows:
> 
> ![](STL_Algorithms.assets/image-20231231121937650.png)
> So we need a new kind of iterator that could change the size of its container, and `back_inserter(container)` did this by returning a smart iterator that could dynamically grow the size of its container.
> 
> ![](STL_Algorithms.assets/image-20231231122000566.png)![](STL_Algorithms.assets/image-20231231122051606.png)





# Remove_If
## How to use?
> [!concept]
> Basically `std::remove_if` will remove the elements that satisfy the predicate from the container.
> 
> The low-level implementation uses two pointers to iterate through the container.
> 
> First initialize a write-only iterator called `write`, and initialize a read-only iterator `iter`, when `*iter == val`, we delete this element and increment the `iter` to the next and write `*iter` to `*write`. Then we update the `write` iterator.
> 
> Repeat the above process until `iter == container.end()`
> The return value of `remove_if` is the final position of `write` iterator.
> 


## Demo Example
> [!code] 
> We see that if we use `remove_if` , there are garbage data at the end of the container, but if we use erase-remove idiom, we are guarantee to perform clean erasion.
> ![](STL_Algorithms.assets/image-20231231165705293.png)![](STL_Algorithms.assets/image-20231231165726969.png)![](STL_Algorithms.assets/image-20231231165759137.png)
```C++
std::vector<int> v = {1,2,3,1,4,5,1};
auto isEqualToOne = [target = 1](auto val) -> bool {
	return val == target;
};

std::vector<int>::iterator iter = std::remove_if(v.begin(), v.end(), isEqualToOne);
std::copy(v.begin(), v.end(),
			  std::ostream_iterator<int>(std::cout, "\n")); // 2 3 4 5 4 5 1


v.erase(iter, v.end());
std::copy(v.begin(), v.end(),
		  std::ostream_iterator<int>(std::cout, "\n"));  // 2 3 4 5

```


> [!example] Behind the Scene of remove_if
> 
> ![](STL_Algorithms.assets/image-20231231165518567.png)![](STL_Algorithms.assets/image-20231231165525194.png)![](STL_Algorithms.assets/image-20231231165530265.png)![](STL_Algorithms.assets/image-20231231165535592.png)![](STL_Algorithms.assets/image-20231231165540177.png)![](STL_Algorithms.assets/image-20231231165544770.png)![](STL_Algorithms.assets/image-20231231165550906.png)![](STL_Algorithms.assets/image-20231231165556532.png)![](STL_Algorithms.assets/image-20231231165602559.png)![](STL_Algorithms.assets/image-20231231165609175.png)![](STL_Algorithms.assets/image-20231231165615171.png)![](STL_Algorithms.assets/image-20231231165621049.png)![](STL_Algorithms.assets/image-20231231165627684.png)![](STL_Algorithms.assets/image-20231231165633902.png)![](STL_Algorithms.assets/image-20231231165641380.png)




# Transform
## Apply a function to a range fo elements
> [!code]
> In this example, `std::transform` is used to calculate the square root of each element in `vec` and store the results in `sqrtVec`.
```C++
#include <algorithm>
#include <vector>
#include <iostream>
#include <cmath>

int main() {
    std::vector<double> vec = {1.0, 4.0, 9.0, 16.0};
    std::vector<double> sqrtVec(vec.size());
    
    std::transform(vec.begin(), vec.end(), sqrtVec.begin(), [](double x) {
        return std::sqrt(x);
    });
    
    for (double num : sqrtVec) {
        std::cout << num << " ";  // 1 2 3 4
    }
    std::cout << std::endl;
    
    return 0;
}
```


## Combinng Two Ranges
> [!code]
> You can also use `std::transform` to combine two ranges and store the result in a third range. This is useful for element-wise operations on two sequences.
> 
> Note that when the number of elements in two ranges doesn't match as shown in the following cases, strange behaviors will happen.
> 
> Notes on `std::transform`
> - The function or operation to be applied is passed as a function pointer, functor, or lambda expression.
> - When combining two ranges, both ranges should have at least as many elements as the range specified by the first two iterators.
> - The destination range should be large enough to store the output of the transformation. If it's a vector, it should be pre-sized or used with an inserter (`std::back_inserter`)
> - `std::transform` doesn't change the size of the output container. If the container is empty or smaller than the input range, this can lead to undefined behavior. Pre-sizing the container or using back inserters is a common practice to avoid this.
```C++
// 2. Second use of transform, combining two ranges

void combineTwoRangesAndPrint(const std::vector<int>& src1,const std::vector<int>& src2 ,std::vector<int>& target) {
    // CASE 1 and CASE 2
    std::transform(src1.begin(), src1.end(), src2.begin(), target.begin(), std::plus<int>());            
    // CASE 3: back_inserter
    std::transform(src1.begin(), src1.end(), src2.begin(), std::back_inserter(target), std::plus<int>());            

    printContainer(target.begin(), target.end());

}
// CASE 1: Out of range
std::vector<int> vec1 = {1, 2, 3, 4};
std::vector<int> vec2 = {10, 20};
std::vector<int> sumVec(vec1.size());
combineTwoRangesAndPrint(vec1, vec2, sumVec); // 11 22 -2040463021 505 

// CASE 2: Destination range not large enough
std::vector<int> vec1 = {1, 2, 3, 4};
std::vector<int> vec2 = {10, 20};
std::vector<int> sumVec(vec2.size());
combineTwoRangesAndPrint(vec1, vec2, sumVec); // 11 22


// CASE 3: Use back_inserter to ensure enough destination placeholder
std::vector<int> vec1 = {1, 2, 3, 4};
std::vector<int> vec2 = {10, 20, 30, 40};
std::vector<int> sumVec(vec2.size()); // Initialize a length 4 vec with 0 elements
combineTwoRangesAndPrint(vec1, vec2, sumVec); // 0 0 0 0 11 22 33 44
```


# Search
> [!concept]
> **`std::search`**: This algorithm is used to find a subrange within a range. It searches for the first occurrence of the second sequence in the first sequence.

## Find occurrence of subsequences
> [!code]
> 
```C++
#include <algorithm>

#include <vector>

#include <iostream>

  

int main() {

    std::vector<int> vec = {1, 2, 3, 4, 5, 6, 7, 8, 9};

    std::vector<int> sub = {4, 5, 6};

  

    auto it = std::search(vec.begin(), vec.end(), sub.begin(), sub.end());

  

    if (it != vec.end()) {

        std::cout << "Subrange found at position: " << (it - vec.begin()) << std::endl;

    } else {

        std::cout << "Subrange not found" << std::endl;

    }

    return 0;

}
```


## Count frequency of a word in a string
> [!code]
```C++
/**

 * Count the frequency of a specific text in the fileString

*/

int countOccurrences(const string& fileString, const string& text) {

    auto curr = fileString.begin();

    auto end = fileString.end();

    int freq = 0;

    while (curr != end) {
		// return the position iter if found
        auto found = search(fileString.begin(), fileString.end(), text.begin(), text.end());
		// return end if not found
        if (found == end) {
            break;
        }

        freq ++;

        curr = found + 1;

    }

    return freq;

}
```

# Find
> [!concept]
> 



# Count
> [!concept]
> 




# Applications
## Document Distance
> [!code]

```C++
#include "../header/fileOperation.hh"
using namespace std;

/**

 * Read the content of a filestream as a string and return.

*/

string fileToString(ifstream& file) {

    string res = ""; // The buffer

  

    string line; // Buffer that contains a line

  

    while (getline(file, line)) {

        transform(line.begin(), line.end(), line.begin(), [](char c){return tolower(c);});

        res += line + " ";

    }

  

    return res;

}

  

/**

 * Count the frequency of a specific text in the fileString

*/

int countOccurrences(const string& fileString, const string& text) {

    auto curr = fileString.begin();

    auto end = fileString.end();

    int freq = 0;

  

    while (curr != end) {

        auto found = search(fileString.begin(), fileString.end(), text.begin(), text.end());

  

        if (found == end) {

            break;

        }

  

        freq ++;

        curr = found + 1;

    }

    return freq;

}

  

map<string, int> comstructFreqMap(const string& fileString) {

    stringstream ss(fileString);

    map<string, int> res;

    string word;

    while (ss >> word) {

        res[word]++;

    }

    return res;

}

  

double computeInnerProduct(map<string, int>& doc1, map<string, int>& doc2) {

    double res = 0.0;

    for (auto iter = doc1.begin(); iter != doc1.end(); ++iter) {

        if (doc2.find((*iter).first) != doc2.end()) {

            res += (*iter).second * doc2.at((*iter).first);

        }

    }

    return res;

}

  
  

double computeCosineSimilarity(map<string, int>& doc1, map<string, int>& doc2) {

    double res = 0.0;

    res += computeInnerProduct(doc1, doc2);

    res /= std::sqrt(computeInnerProduct(doc1, doc1) * computeInnerProduct(doc2, doc2));

    return res;

}

  
  

int main() {

  

    ifstream file1("./res/jj.txt");

    ifstream file2("./res/ladygaga.txt");

  

    if (!file1.is_open() || !file2.is_open()) {

        std::cerr << "File is not correctly opened" << std::endl;

    }

  

    string string1 = fileToString(file1);

    string string2 = fileToString(file2);

  

    auto freq1 = comstructFreqMap(string1);

    auto freq2 = comstructFreqMap(string2);

  

    cout << computeCosineSimilarity(freq1, freq2) << endl;

    return 0;

}
```


# Summary
> [!summary]
> ![](STL_Algorithms.assets/image-20231231171628422.png)


























