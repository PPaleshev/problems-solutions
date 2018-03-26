# Sort an array containing 0’s, 1’s and 2’s (Dutch national flag problem)
Given an array containing only 0’s, 1’s and 2’s, sort the array in linear time and using constant space.
For example,

**Input:**{ 0, 1, 2, 2, 1, 0, 0, 2, 0, 1, 1, 0 }
**Output:**{ 0, 0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2 }

Simple solution would be to perform count sort. We count the number of 0’s, 1’s and 2’s and then put them in the array in their correct order. The time complexity of above solution is O(n) but it requires two traversal of the array. 
We can rearrange the array in single traversal using an alternative **linear-time partition routine** can be used that separates the values into three groups:
+ values less than the pivot
+ values equal to the pivot and
+ values greater than the pivot.

To solve this particular problem, we consider 1 as a pivot. Below linear-time partition routine is similar to three-way Partitioning for Dutch national flag problem.

##### C
```C
#include <stdio.h>
// Utility function to swap two elements A[i] and A[j] in the array
void swap(int A[], int i, int j) {
    int temp = A[i];
    A[i] = A[j];
    A[j] = temp;
}
// Linear-time partition routine to sort an array containing 0, 1 and 2
// It similar to three-way Partitioning for Dutch national flag problem
int threeWayPartition(int A[], int end)
{
    int start = 0, mid = 0;
    int pivot = 1;
    while (mid <= end)
    {
        if (A[mid] < pivot)         // current element is 0
        {
            swap(A, start, mid);
            ++start, ++mid;
        }
        else if (A[mid] > pivot)    // current element is 2
        {
            swap(A, mid, end);
            --end;
        }
        else                         // current element is 1
        {
            ++mid;
        }
    }
}
// Sort an array containing 0’s, 1’s and 2’s
int main()
{
    int A[] = { 0, 1, 2, 2, 1, 0, 0, 2, 0, 1, 1, 0 };
    int n = sizeof(A)/sizeof(A[0]);
    threeWayPartition(A, n - 1);
    for (int i = 0 ; i < n; i++) {
        printf("%d ", A[i]);
    }
    return 0;
}
```

##### Java
```Java

import java.util.Arrays;
class ThreeWayPartition
{
    // Linear-time partition routine to sort an array containing 0, 1 and 2
    // It similar to three-way Partitioning for Dutch national flag problem
    public static void threeWayPartition(int[] A, int end)
    {
        int start = 0, mid = 0;
        int pivot = 1;
        while (mid <= end)
        {
            if (A[mid] < pivot)         // current element is 0
            {
                swap(A, start, mid);
                ++start;
                ++mid;
            }
            else if (A[mid] > pivot)    // current element is 2
            {
                swap(A, mid, end);
                --end;
            }
            else                        // current element is 1
                ++mid;
        }
    }
    // Utility function to swap two elements A[i] and A[j] in the array
    private static void swap(int[] A, int i, int j) {
        int temp = A[i];
        A[i] = A[j];
        A[j] = temp;
    }
    // Sort an array containing 0’s, 1’s and 2’s
    public static void main (String[] args)
    {
        int A[] = { 0, 1, 2, 2, 1, 0, 0, 2, 0, 1, 1, 0 };
        threeWayPartition(A, A.length - 1);
        System.out.println(Arrays.toString(A));
    }
}
```
**Output:**
0 0 0 0 0 1 1 1 1 2 2 2

The time complexity of above solution is O(n) and auxiliary space used by the program is O(1).