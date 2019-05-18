# Move all zeros present in the array to the end
Given an array of integers, move all zeros present in the array to the end. The solution should maintain the relative order of items in the array.
For example,

**Input:**  { 6, 0, 8, 2, 3, 0, 4, 0, 1 }

**Output:** { 6, 8, 2, 3, 4, 1, 0, 0, 0 }

The idea is very simple. If the current element is non-zero, we can place the element at next available position in the array. After all elements in the array are processed, we fill all remaining indices by 0.
This is demonstated below in C++

##### C++
```C++
#include <iostream>
using namespace std;
// Function to move all zeros present in the array to the end
int reorder(int A[], int n)
{
    // k stores index of next available position
    int k = 0;
    // do for each element
    for (int i = 0; i < n; i++)
    {
        // if current element is non-zero, put the element at
        // next free position in the array
        if (A[i] != 0)
            A[k++] = A[i];
    }
    // move all 0's to the end of the array (remaining indices)
    for (int i = k; i < n; i++)
        A[i] = 0;
}
// Move all zeros present in the array to the end
int main()
{
    int A[] = { 6, 0, 8, 2, 3, 0, 4, 0, 1 };
    int n = sizeof(A) / sizeof(A[0]);
    reorder(A, n);
    for (int i = 0; i < n; i++)
        cout << A[i] << " ";
    return 0;
}
```

**Output:**
6 8 2 3 4 1 0 0 0

The time complexity of above solution is O(n) and auxiliary space used by the program is O(1).
### Using partitioning logic of quicksort
We can also solve this problem in one scan of array by modifying partitioning logic of quicksort. The idea is to use 0 as a pivot element and make one pass of partition process. The partitioning logic will read all elements and each time we encounter a non-pivot element, that element is swapped with the first occurrence of pivot.

##### C++
```C++
#include <iostream>
using namespace std;
// Function to move all zeros present in the array to the end
int Partition(int A[], int n)
{
    int j = 0;
    // each time we encounter a non-zero, j is incremented and
    // the element is placed before the pivot
    for (int i = 0; i < n; i++)
    {
        if (A[i] != 0)   // pivot is 0
        {
            swap(A[i], A[j]);
            j++;
        }
    }
}
// Move all zeros present in the array to the end
int main()
{
    int A[] = { 6, 0, 8, 2, 3, 0, 4, 0, 1 };
    int n = sizeof(A) / sizeof(A[0]);
    Partition(A, n);
    for (int i = 0; i < n; i++)
        cout << A[i] << " ";
    return 0;
}
```

**Output:**
6 8 2 3 4 1 0 0 0

The time complexity of above solution is O(n) and auxiliary space used by the program is O(1).