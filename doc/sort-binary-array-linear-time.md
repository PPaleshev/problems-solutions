# Sort Binary Array in Linear Time
Given an binary array, sort it in linear time and constant space. Output should print contain all zeroes followed by all ones.
For example,
**Input:** { 1, 0, 1, 0, 1, 0, 0, 1 }
**Output:** { 0, 0, 0, 0, 1, 1, 1, 1 }
Simple solution would be to count number of 0’s present in the array (say k) and fill first k indices in the array by 0 and all remaining indices by 1.
Alternatively, we can also count number of 1’s present in the array (say k) and fill last k indices in the array by 1 and all remaining indices by 0.

##### C
```C

#include <stdio.h>
// Function to sort binary array in linear time
int sort(int A[], int n)
{
    // count number of 0's
    int zeros = 0;
    for (int i = 0; i < n; i++) {
        if (A[i] == 0) {
            zeros++;
        }
    }
    // put 0's in the beginning
    int k = 0;
    while (zeros--) {
        A[k++] = 0;
    }
    // fill all remaining elements by 1
    while (k < n) {
        A[k++] = 1;
    }
}
// Sort binary array in linear time
int main(void)
{
    int A[] = { 0, 0, 1, 0, 1, 1, 0, 1, 0, 0 };
    int n = sizeof(A)/sizeof(A[0]);
    sort(A, n);
    // print the rearranged array
    for (int i = 0 ; i < n; i++) {
        printf("%d ", A[i]);
    }
    return 0;
}
```

##### Java
```Java

import java.util.Arrays;
class SortBinaryArray
{
    // Function to sort binary array in linear time
    public static void sort(int[] A)
    {
        // count number of 0's
        int zeros = 0;
        for (int i = 0; i < A.length; i++) {
            if (A[i] == 0) {
                zeros++;
            }
        }
        // put 0's in the beginning
        int k = 0;
        while (zeros-- != 0) {
            A[k++] = 0;
        }
        // fill all remaining elements by 1
        while (k < A.length) {
            A[k++] = 1;
        }
    }
    // Sort binary array in linear time
    public static void main (String[] args)
    {
        int A[] = { 0, 0, 1, 0, 1, 1, 0, 1, 0, 0 };
        sort(A);
        // print the rearranged array
        System.out.println(Arrays.toString(A));
    }
}
```
**Output:**
0 0 0 0 0 0 1 1 1 1

The time complexity of above solution is O(n) and auxiliary space used by the program is O(1).
Instead of counting number of zeroes, if the current element is 0, we can place 0 at next available position in the array. After all elements in the array are processed, we fill all remaining indices by 1.
##### C
```C

#include <stdio.h>
// Function to sort binary array in linear time
int sort(int A[], int n)
{
    // k stores index of next available position
    int k = 0;
    // do for each element
    for (int i = 0; i < n; i++)
    {
        // if current element is zero, put 0 at next free
        // position in the array
        if (A[i] == 0) {
            A[k++] = 0;
        }
    }
    // fill all remaining indices by 1
    for (int i = k; i < n; i++) {
        A[k++] = 1;
    }
}
// Sort binary array in linear time
int main(void)
{
    int A[] = { 0, 0, 1, 0, 1, 1, 0, 1, 0, 0 };
    int n = sizeof(A)/sizeof(A[0]);
    sort(A, n);
    // print the rearranged array
    for (int i = 0 ; i < n; i++) {
        printf("%d ", A[i]);
    }
    return 0;
}
```

##### Java
```Java

import java.util.Arrays;
class SortBinaryArray
{
    // Function to sort binary array in linear time
    public static void sort(int[] A)
    {
        // k stores index of next available position
        int k = 0;
        // do for each element
        for (int i = 0; i < A.length; i++)
        {
            // if current element is zero, put 0 at next free
            // position in the array
            if (A[i] == 0) {
                A[k++] = 0;
            }
        }
        // fill all remaining indices by 1
        for (int i = k; i < A.length; i++) {
            A[k++] = 1;
        }
    }
    // Sort binary array in linear time
    public static void main (String[] args)
    {
        int A[] = { 0, 0, 1, 0, 1, 1, 0, 1, 0, 0 };
        sort(A);
        // print the rearranged array
        System.out.println(Arrays.toString(A));
    }
}
```
**Output:**
0 0 0 0 0 0 1 1 1 1

The time complexity of above solution is O(n) and auxiliary space used by the program is O(1).
We can also solve this problem in linear time by using partitioning logic of quicksort. The idea is to use 1 as pivot element and make one pass of partition process. The resultant array will be sorted.
##### C
```C
#include <stdio.h>
// Utility function to swap two elements A[i] and A[j] in the array
void swap(int A[], int i, int j) {
    int temp = A[i];
    A[i] = A[j];
    A[j] = temp;
}
// Function to sort binary array in linear time
int partition(int A[], int n)
{
    int pivot = 1;
    int j = 0;
    // each time we encounter a 0, j is incremented and
    // 0 is placed before the pivot
    for (int i = 0; i < n; i++)
    {
        if (A[i] < pivot)
        {
            swap(A, i, j);
            j++;
        }
    }
}
// Sort binary array in linear time
int main(void)
{
    int A[] = { 1, 0, 0, 0, 1, 0, 1, 1 };
    int n = sizeof(A)/sizeof(A[0]);
    partition(A, n);
    // print the rearranged array
    for (int i = 0 ; i < n; i++) {
        printf("%d ", A[i]);
    }
    return 0;
}
```

##### Java
```Java

import java.util.Arrays;
class SortBinaryArray
{
    // Function to sort binary array in linear time
    public static void sort(int[] A)
    {
        int pivot = 1;
        int j = 0;
        // each time we encounter a 0, j is incremented and
        // 0 is placed before the pivot
        for (int i = 0; i < A.length; i++)
        {
            if (A[i] < pivot)
            {
                swap(A, i, j);
                j++;
            }
        }
    }
    // Utility function to swap elements at two indices in the given array
    private static void swap(int[] A, int i, int j) {
        int temp = A[i];
        A[i] = A[j];
        A[j] = temp;
    }
    // Sort binary array in linear time
    public static void main (String[] args)
    {
        int A[] = { 0, 0, 1, 0, 1, 1, 0, 1, 0, 0 };
        sort(A);
        // print the rearranged array
        System.out.println(Arrays.toString(A));
    }
}
```
**Output:**
0 0 0 0 1 1 1 1

The time complexity of above solution is O(n) and auxiliary space used by the program is O(1).