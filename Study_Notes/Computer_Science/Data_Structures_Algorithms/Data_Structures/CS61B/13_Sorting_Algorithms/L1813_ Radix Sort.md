[Lab 13_ Radix Sorts _ CS 61B Spring 2018.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1682213798613-0cd71c4d-54cb-499e-8c07-4a90dfc3d264.pdf)
[lab13.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/12393765/1682213806891-37fca8b8-bc83-41c7-b602-e654677efe22.zip)


# Counting Sort
## Naive Implementation - Nonnegative Arrays
> 本算法只包含正数。

```java
public static int[] naiveCountingSort(int[] arr) {
    // find max
    int max = Integer.MIN_VALUE;
    for (int i : arr) {
        max = max > i ? max : i;
    }

    System.out.println(max);
    // gather all the counts for each value
    int[] counts = new int[max + 1];
    for (int i : arr) {
        counts[i]++;
    }

    // when we're dealing with ints, we can just put each value
    // count number of times into the new array
    int[] sorted = new int[arr.length];
    int k = 0;
    for (int i = 0; i < counts.length; i += 1) {
        for (int j = 0; j < counts[i]; j += 1, k += 1) {
            sorted[k] = i;
        }
    }

    // however, below is a more proper, generalized implementation of
    // counting sort that uses start position calculation
    int[] starts = new int[max + 1];
    int pos = 0;
    for (int i = 0; i < starts.length; i += 1) {
        starts[i] = pos;
        pos += counts[i];
    }

    int[] sorted2 = new int[arr.length];
    for (int i = 0; i < arr.length; i += 1) {
        int item = arr[i];
        int place = starts[item];
        sorted2[place] = item;
        starts[item] += 1;
    }

    // return the sorted array
    return sorted;
}
```



## Better Solution - Negative Arrays
> **思路是：**
> 1. 将`min(array)`作为`dictionary`中最小的一项
> 2. 然后依次更新`array[i-min]`即可(`for i in array`)即可。

```java
public static int[] betterCountingSort(int[] arr) {
    // Make counting sort work with arrays containing negative numbers.
    int min = Integer.MAX_VALUE;
    int max = Integer.MIN_VALUE;
    for (int value : arr) {
        if (min > value) {
            min = value;
        }
        if (max < value) {
            max = value;
        }
    }
    int[] counts = new int[max - min + 1];
    for (int i : arr) {
        counts[i - min] += 1;
    }

    int[] starts = new int[max - min + 1];
    int pos = 0;
    for (int i = 0; i < starts.length; i += 1) {
        starts[i] = pos;
        pos += counts[i];
    }

    int[] sorted = new int[arr.length];
    for (int i = 0; i < arr.length; i += 1) {
        int item = arr[i];
        int place = starts[item - min];
        sorted[place] = item;
        starts[item - min] += 1;
    }

    return sorted;
}
```


# Radix Sort
## LSD Implementation(Easy)
> **思路是:**
> 1. 首先`Right padding string with \0`, 因为`\0`在`ASCII`中式最小的$0$。
> 2. 然后从最右侧开始依次向左调用`countingsort(str[index])`

```java
private static void LSDSort(String[] asciis) {
    // Padding
    int maxLength = Integer.MIN_VALUE;
    for (String s: asciis) {
        maxLength = maxLength > s.length() ? maxLength : s.length();
    }

    // Right append 0 to the string
    String[] asciiCopy = asciis.clone();
    for (int i = 0; i < asciiCopy.length; i++) {
        StringBuilder sb = new StringBuilder(asciiCopy[i]);
        for (int j = 0; j < maxLength - asciiCopy[i].length(); j++) {
            sb.append("\0");
        }
        asciiCopy[i] = sb.toString();
    }

    // Start Sorting from right to left
    for (int d = maxLength - 1; d >= 0; d--) {
        sortHelperLSD(asciiCopy, d);
    }

    for (int i = 0; i < asciis.length; i++) {
        asciis[i] = asciiCopy[i];
    }
}


/**
 * LSD helper method that performs a destructive counting sort the array of
 * Strings based off characters at a specific index.
 * @param asciis Input array of Strings
 * @param index The position to sort the Strings on.
 */
private static void sortHelperLSD(String[] asciis, int index) {
    // Optional LSD helper method for required LSD radix sort
    String[] sorted = new String[asciis.length]; //  Sorted result of ascii based on asciis[i][index]

    // Frequency map
    int[] freqMap = new int[RADIX]; // Dictionary for frequency

    for (String ascii: asciis) {
        freqMap[ascii.charAt(index)]++;
    }

    // Position map
    int[] startingPosition = new int[RADIX]; // Dictionary for position

    // Calculating positions
    for (int i = 0; i < freqMap.length; i++) {
        int pos = 0;
        for (int j = 0; j < i; j++) {
            pos += freqMap[j];
        }
        startingPosition[i] = pos;
    }

    // Sorting according to the position map
    for (String ascii: asciis) {
        sorted[startingPosition[ascii.charAt(index)]] = ascii;
        startingPosition[ascii.charAt(index)]++;
    }

    for (int i = 0; i < asciis.length; i++) {
        asciis[i] = sorted[i];
    }
}
```

## MSD Implementaion(Medium)
> **思路是:**
> 1. 首先`Right padding string with \0`, 因为`\0`在`ASCII`中式最小的$0$。
> 2. 然后从最左侧开始依次向右分组调用`countingsort(str[index])`(采用递归)

```java
private static void MSDSort(String[] asciis) {
    // Padding
    int maxLength = Integer.MIN_VALUE;
    for (String s: asciis) {
        maxLength = maxLength > s.length() ? maxLength : s.length();
    }

    MAX_LENGTH = maxLength;

    // Right append 0 to the string
    String[] asciiCopy = asciis.clone();
    for (int i = 0; i < asciiCopy.length; i++) {
        StringBuilder sb = new StringBuilder(asciiCopy[i]);
        for (int j = 0; j < maxLength - asciiCopy[i].length(); j++) {
            sb.append("\0");
        }
        asciiCopy[i] = sb.toString();
    }

    sortHelperMSD(asciiCopy, 0, asciis.length, 0);

    for (int i = 0; i < asciiCopy.length; i++) {
        asciis[i] = asciiCopy[i];
    }
}

/**
 * MSD radix sort helper function that recursively calls itself to achieve the sorted array.
 * Destructive method that changes the passed in array, asciis.
 *
 * @param asciis String[] to be sorted
 * @param start int for where to start sorting in this method (includes String at start)
 * @param end int for where to end sorting in this method (does not include String at end)
 * @param index the index of the character the method is currently sorting on
 *
 **/
private static void sortHelperMSD(String[] asciis, int start, int end, int index) {
    // Optional MSD helper method for optional MSD radix sort
    if (index == MAX_LENGTH - 1 || start == end) {
        return;
    }

    // Create a freqMap in [start, end)
    int[] freqMap = new int[RADIX];

    for (int i = start; i < end; i++) {
        freqMap[asciis[i].charAt(index)]++;
    }

    // Create a positionMap in [start, end)
    int[] positionMap = new int[RADIX];

    int newPos = start;
    for (int i = 0; i < positionMap.length; i++) {
        positionMap[i] = newPos;
        newPos += freqMap[i];
    }

    int[] positionMapCopy = Arrays.copyOfRange(positionMap, 0, positionMap.length);

    String[] sorted = Arrays.copyOfRange(asciis, 0, asciis.length);

    for (int i = start; i < end; i++) {
        sorted[positionMap[asciis[i].charAt(index)]] = asciis[i];
        positionMap[asciis[i].charAt(index)]++;
    }

    // Modify the original list,changing the reference
    for (int i = 0; i < asciis.length; i++) {
        asciis[i] = sorted[i];
    }

    // Break into subproblems
    int startPos = start;
    int endPos;
    int pos = start;
    for (int i = 0; i < positionMapCopy.length; i++) {
        if (positionMapCopy[i] > 0 && positionMapCopy[i] != pos) {
            endPos = positionMapCopy[i];
            sortHelperMSD(asciis, startPos, endPos, index + 1);
            startPos = endPos;
            pos = endPos;
        }
    }
}
```



# Submission
> ![image.png](L1813_%20Radix%20Sort.assets/4ef26eee7475eddf86720f27928c9f6e_MD5.png)

