# Data Structure & Algorithms

## Table Of Content
- [Introduction](#introduction)
- [Abstract Data Type](#abstract-data-type)
- [Analysis Of Algorithm](#analysis-of-algorithm)
- [Searching](#searching)

## [Introduction](#Introduction)

### Data Structure
- Data is efficiently stored
- Data is arranged
- Programs access efficiently


**Types**
- Linear
    - Stack, Queue, LinkedList
- Non Linear
    - Graph, Tree, Heap

### Algorithm
- Plan or Blueprint
- Set of Instruction
- Execute in finite amount of time

**Why Algorithm ?**
- Mechanishm to compare Algorithms
- Predict performance
- Time and amount of resource


## [Abstract Data Type](#AbstractDataType)
- Abstraction to data structure
- Mathematical model of Data Structures
- Abtract Data Type specifies: 
    - Type of data represented or stored
    - Operation Supported

### Data Type
- Representation of Data
- Operations
- Primitive Data Types:
    - Integer, Byte, Long, Float, Double
    - Boolean, Character

## [Analysis Of Algorithm](#AnalysisOfAlgorithm)

### Time Complexity
- Running time of algorithm is proportional
- Increases with the size of the input

Ways to Analyse time complexity:
- Theoratical Analysis 
    - Performed on description of Algorithm
    - Independent of hardware & software
    - All possible input
- Experimental Analysis
    - Runtime measured on various input
    - Programming lanaguages provides time functions
    - Lapse time is computed.
    - Its easier than theoratical analysis
    - Hardware & Software dependent
    - Operating System dependent
    - Limited input
    - Difficult to predict precise running time
### Space Complexity
- How much memory is consumed.

## Order of Growth
![Screenshot from 2024-11-16 22-35-04](https://github.com/user-attachments/assets/66ae797a-f41a-43f3-8410-41f5422b8fc9)

## Asymptotic Analysis

```
f(n) n = 1,2,3,4,5...10...20...1,000...1,000,000

f(n) = n² + 6n + 5      n -> 1000

Note: Asymptotic means approaching a value

f(n) is said to be asymptotically equivalent to n²
```

### Asymptotic Notation
- Big-oh O( ): Worst Case: Upper Bound
- Big-Omega Ω( ): Best Case: Lower Bound
- Big-Theta θ( ): Average Case

## [Searching](#Searching)
Searching Algorithms are designed to check for an element or retrieve an element from any data structure where it is stored.

Based on the type of search operation, these algorithms are generally classified into two categories:

- Sequential Search: In this, the list or array is traversed sequentially and every element is checked.
- Interval Search: These algorithms are specifically designed for searching in sorted data-structures. These type of searching algorithms are much more efficient than Linear Search as they repeatedly target the center of the search structure and divide the search space in half.

### Linear Search
Linear Search is defined as a sequential search algorithm that starts at one end and goes through each element of a list until the desired element is found, otherwise the search continues till the end of the data set.

```cs
public class LinearSearch
{
    public int Search<T>(IEnumerable<T> list, T element)
    {
        int index = 0;
        
        foreach (var item in list)
        {
            if (item.Equals(element)) return index;
            index++;
        }
        return -1;
    }
}
```


**Time Complexity:**
- Best Case: In the best case, the key might be present at the first index. So the best case complexity is O(1)
- Worst Case: In the worst case, the key might be present at the last index i.e., opposite to the end from which the search has started in the list. So the worst-case complexity is O(N) where N is the size of the list.
- Average Case: O(N)

**Advantages of Linear Search:**

- Linear search can be used irrespective of whether the array is sorted or not. It can be used on arrays of any data type.
- Does not require any additional memory.
-It is a well-suited algorithm for small datasets.

**Drawbacks of Linear Search:**

- Linear search has a time complexity of O(N), which in turn makes it slow for large datasets.
- Not suitable for large arrays.

**When to use Linear Search?**

- When we are dealing with a small dataset.
- When you are searching for a dataset stored in contiguous memory.


### Binary Search
Binary Search is defined as a searching algorithm used in a sorted array by repeatedly dividing the search interval in half. The idea of binary search is to use the information that the array is sorted and reduce the time complexity to O(log N).

```cs
public class BinarySearch
{
    public int Search<T>(T[] list, T element) where T : IComparable<T>
    {
        int start = 0, end = list.Length - 1;
        while (start <= end)
        {
            int middle = (end - start) / 2 + start;
            int status = element.CompareTo(list[middle]);
            if (status == 0) return middle;
            else if (status > 0) start = middle + 1;
            else end = middle - 1;
        }
        return -1;
    }

    //Recursive Search
    public int Search<T>(T[] list, T element, int start, int end) where T : IComparable<T>
    {
        if (start > end) return -1;

        int middle = (end - start) / 2 + start;
        int status = element.CompareTo(list[middle]);

        if (status == 0) return middle;
        else if (status > 0) return Search(list, element, middle + 1, end);
        else return Search(list, element, start, middle - 1);
    }
}
```

**Time Complexity:**

- Best Case: O(1)
- Average Case: O(log N)
- Worst Case: O(log N) </br>
Note: Auxiliary Space: O(1), If the recursive call stack is considered then the auxiliary space will be O(logN).

**Advantages of Binary Search:**

- Binary search is faster than linear search, especially for large arrays.
- More efficient than other searching algorithms with a similar time complexity, such as interpolation search or exponential search.
- Binary search is well-suited for searching large datasets that are stored in external memory, such as on a hard drive or in the cloud.

**Drawbacks of Binary Search:**

- The array should be sorted.
- Binary search requires that the data structure being searched be stored in contiguous memory locations. 
- Binary search requires that the elements of the array be comparable, meaning that they must be able to be ordered.

**Applications of Binary Search:**

- Binary search can be used as a building block for more complex algorithms used in machine learning, such as algorithms for training neural networks or finding the optimal hyperparameters for a model.
- It can be used for searching in computer graphics such as algorithms for ray tracing or texture mapping.
- It can be used for searching a database.

# Meta Binary Search | One-Sided Binary Search
Meta Binary Search, also known as One-Sided Binary Search, is a variation of the binary search algorithm that is used to search an ordered list or array of elements. This algorithm is designed to reduce the number of comparisons needed to search the list for a given element.

The basic idea behind Meta Binary Search is to start with an initial interval of size n that includes the entire array. The algorithm then computes a middle element, as in binary search, and compares it to the target element. If the target element is found, the search terminates. If the middle element is greater than the target element, the algorithm sets the new interval to the left half of the previous interval, and if the middle element is less than the target element, the new interval is set to the right half of the previous interval. However, unlike binary search, Meta Binary Search does not perform a comparison for each iteration of the loop.

```cs
public class MetaBinarySearch
{
    public int Search<T>(T[] list, T element) where T : IComparable<T>
    {
        int bitsNeededForMaxIndex = (int)Math.Ceiling(Math.Log2 (list.Length));
        int cutoff = 0;
        for (int i = bitsNeededForMaxIndex - 1; i >= 0; i--)
        {
            if (element.CompareTo(list[cutoff]) == 0) return cutoff;

            int cutoffCandidate = cutoff | (1 << i);

            if (cutoffCandidate < list.Length && element.CompareTo(list[cutoffCandidate]) >= 0)
            {
                cutoff = cutoffCandidate;
            }
        }
        if (element.CompareTo(list[cutoff]) == 0) return cutoff;
        return -1;
    }
}
```
