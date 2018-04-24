# Rearrange the array with alternate high and low elements
Given an array of integers, rearrange the array such that every second element of the array is greater than its left and right elements. Assume no duplicate elements are present in the array.
For example,

**Input:**  
`{1, 2, 3, 4, 5, 6, 7}`

**Output:** 
`{1, 3, 2, 5, 4, 7, 6}`

---
**Input:**  `{9, 6, 8, 3, 7}`

**Output:** `{6, 9, 3, 8, 7}`

---
**Input:**  `{6, 9, 2, 5, 1, 4}`

**Output:** `{6, 9, 2, 5, 1, 4}`

A simple solution would be to sort the array in ascending order first. Then we take another auxiliary array and fill it with elements starting from the two end-points of the sorted array in alternate order. Below is the complete algorithm –
**rearrangeArray (int arr[], int n)**
1. Sort the array in ascending order.

2. Take two index variables `i` and `j` to that points to two end-points of the array (i.e. `i = 0` and `j = n – 1`)

3. Create an auxiliary array `A[]` and initialize an index `k` with `0`
4. 
    `while (i < j)`  
    `A[k++] = arr[i++]`  
    `A[k++] = arr[j–]`

5. print `A[]`

The Time complexity of this solution would be O(nlogn).
An efficient solution doesn’t involve sorting the array or use of auxiliary space. We start from the second element of the array and increment index by 2 for each iteration of loop. If previous element is greater than the current element, we swap the elements. Similarly if next element is greater than the current element, we swap both elements. At the end of loop, we will get the desired array that satisfies given constraints.

##### C
```C
#include <stdio.h>
// Utility function to swap two elements arr[i] and arr[j] in the array
void swap(int arr[], int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
// Function to rearrange the array such that every second element
// of the array is greater than its left and right elements
void rearrangeArray(int arr[], int n)
{
    // start from second element and increment index
    // by 2 for each iteration of loop
    for (int i = 1; i < n; i += 2)
    {
        // If the prev element is greater than current element,
        // swap the elements
        if (arr[i - 1] > arr[i]) {
            swap(arr, i-1, i);
        }
        // if next element is greater than current element,
        // swap the elements
        if (i + 1 < n && arr[i + 1] > arr[i]) {
            swap(arr, i+1, i);
        }
    }
}
// main function
int main(void)
{
    int arr[] = { 9, 6, 8, 3, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    rearrangeArray(arr, n);
    // print output array
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

##### Java
```Java
import java.util.Arrays;
class Rearrange
{
    // Utility function to swap two elements A[i] and A[j] in the array
    private static void swap(int[] A, int i, int j) {
        int temp = A[i];
        A[i] = A[j];
        A[j] = temp;
    }
    // Function to rearrange the array such that every second element
    // of the array is greater than its left and right elements
    public static void rearrangeArray(int[] A)
    {
        // start from second element and increment index
        // by 2 for each iteration of loop
        for (int i = 1; i < A.length; i += 2)
        {
            // If the prev element is greater than current element,
            // swap the elements
            if (A[i - 1] > A[i]) {
                swap(A, i - 1, i);
            }
            // if next element is greater than current element,
            // swap the elements
            if (i + 1 < A.length && A[i + 1] > A[i]) {
                swap(A, i + 1, i);
            }
        }
    }
    // main function
    public static void main (String[] args)
    {
        int[] A = { 9, 6, 8, 3, 7 };
        rearrangeArray(A);
        // print output array
        System.out.println(Arrays.toString(A));
    }
}
```
**Output:**
6 9 3 8 7

The time complexity of above solution is O(n) and auxiliary space used by the program is O(1).