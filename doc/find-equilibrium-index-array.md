# Find Equilibrium Index of an Array
Given an array of integers, find equilibrium index in it.
For an array A consisting `n` elements, index `i` is an equilibrium index if sum of elements of sub-array `A[0..i-1]` is equal to the sum of elements of sub-array `A[i+1..n-1]` i.e.
`(A[0] + A[1] + ... + A[i-1]) = (A[i+1] + A[i+2] + ... + A[n-1])` where 0 < i < n-1

Similarly, 0 is an equilibrium index if `(A[1] + A[2] + ... + A[n-1]) = 0` and `n-1` is an equilibrium index if `(A[0] + A[1] + ... + A[n-2]) = 0`

For example, consider the array `{0, -3, 5, -4, -2, 3, 1, 0}`. The equilibrium index found at index 0, 3 and 7.
### 1. Naive solution
Naive approach is to calculate sum of elements to the left and sum of elements to the right for each element of the array. If left sub-array sum is same as right sub-array sum for an element, we print its index. The time complexity of above solution is O(n^2^).

### 2. Linear time solution
We can solve this problem in linear time by using extra space. The idea is to create an auxiliary array left[] where left[i] stores sum of elements of sub-array `A[0..i-1]`. After left[] is filled, we traverse the array from right to left and update right sub-array sum for each element encountered. Now if sum of elements of left sub-array `A[0..i-1]` is equal to the sum of elements of right sub-array A[i+1..n) for element A[i], we have found equilibrium index at i.
##### C
```C

#include <stdio.h>
// Function to find equilibrium index of an array
void equilibriumIndex(int A[], int n)
{
    // left[i] stores sum of elements of sub-array A[0..i-1]
    int left[n];
    left[0] = 0;
    // traverse array from left to right
    for (int i = 1; i < n; i++) {
        left[i] = left[i - 1] + A[i - 1];
    }
    // right stores sum of elements of sub-array A[i+1..n)
    int right = 0;
    // traverse array from right to left
    for (int i = n - 1; i >= 0; i--)
    {
        /* If sum of elements of sub-array A[0..i-1] is equal to
           the sum of elements of sub-array A[i+1..n) i.e.
           (A[0] + A[1] + .. + A[i-1]) = (A[i+1] + A[i+2] + .. + A[n-1])
        */
        if (left[i] == right) {
            printf("Equilibrium Index found at %d\n", i);
        }
        // new right = A[i] + (A[i+1] + A[i+2] + .. + A[n-1])
        right += A[i];
    }
}
// Program to find the equilibrium index of an array
int main(void)
{
    int A[] = { 0, -3, 5, -4, -2, 3, 1, 0 };
    int n = sizeof(A) / sizeof(A[0]);
    equilibriumIndex(A, n);
    return 0;
}
```

##### Java
```Java

class EquilibriumIndex
{
    // Function to find equilibrium index of an array
    public static void equilibriumIndex(int A[])
    {
        // left[i] stores sum of elements of sub-array A[0..i-1]
        int left[] = new int[A.length];
        left[0] = 0;
        // traverse array from left to right
        for (int i = 1; i < A.length; i++) {
            left[i] = left[i - 1] + A[i - 1];
        }
        // right stores sum of elements of sub-array A[i+1..n)
        int right = 0;
        // traverse array from right to left
        for (int i = A.length - 1; i >= 0; i--)
        {
            /* if sum of elements of sub-array A[0..i-1] is equal to
               the sum of elements of sub-array A[i+1..n) i.e.
               (A[0] + .. + A[i-1]) = (A[i+1] + A[i+2] + .. + A[n-1]) */
            if (left[i] == right) {
                System.out.println("Equilibrium Index found at " + i);
            }
            // new right = A[i] + (A[i+1] + A[i+2] + .. + A[n-1])
            right += A[i];
        }
    }
    // Program to find the equilibrium index of an array
    public static void main (String[] args)
    {
        int[] A = { 0, -3, 5, -4, -2, 3, 1, 0 };
        equilibriumIndex(A);
    }
}
```
**Output:**
Equilibrium Index found at 7, 3 and 0

The time complexity of above solution is O(n) and auxiliary space used by the program is O(n).

### 3. Optimized solution
We can avoid using extra space. The idea is to calculate the sum of all elements of the array. Then we start from the last element of the array and maintain right sub-array sum. We can calculate left sub-array sum in constant time by subtracting right sub-array sum and current element from total sum. i.e.
Sum of left subarray `A[0..i-1] = total - (A[i] + sum of right subarray A[i+1..n-1])`
##### C++
```C++

#include <iostream>
#include <numeric>
using namespace std;
// Optimized method to find equilibrium index of an array
void equilibriumIndex(int A[], int n)
{
    // total stores sum of all elements of the array
    int total = accumulate(A, A + n, 0);
    // right stores sum of elements of sub-array A[i+1..n)
    int right = 0;
    // traverse array from right to left
    for (int i = n - 1; i >= 0; i--)
    {
        /* i is equilibrium index if sum of elements of sub-array A[0..i-1]
           is equal to the sum of elements of sub-array A[i+1..n) i.e.
           (A[0] + A[1] + .. + A[i-1]) = (A[i+1] + A[i+2] + .. + A[n-1]) */
        // sum of elements of left sub-array A[0..i-1] is
        // (total - (A[i] + right))
        if (right == total - (A[i] + right)) {
            cout << "Equilibrium Index found " << i << '\n';
        }
        // new right = A[i] + (A[i+1] + A[i+2] + .. + A[n-1])
        right += A[i];
    }
}
// Program to find the equilibrium index of an array
int main()
{
    int A[] = { 0, -3, 5, -4, -2, 3, 1, 0 };
    int n = sizeof(A) / sizeof(A[0]);
    equilibriumIndex(A, n);
    return 0;
}
```

##### Java
```Java

import java.util.stream.IntStream;
class EquilibriumIndex
{
    // Optimized method to find equilibrium index of an array
    public static void equilibriumIndex(int[] A)
    {
        // total stores sum of all elements of the array
        int total = IntStream.of(A).sum();    // Java 8
        // right stores sum of elements of sub-array A[i+1..n)
        int right = 0;
        // traverse array from right to left
        for (int i = A.length - 1; i >= 0; i--)
        {
            /* i is equilibrium index if sum of elements of sub-array
               A[0..i-1] is equal to the sum of elements of sub-array
               A[i+1..n) i.e. (A[0] + A[1] + .. + A[i-1]) =
               (A[i+1] + A[i+2] + .. + A[n-1]) */
            // sum of elements of left sub-array A[0..i-1] is
            // (total - (A[i] + right))
            if (right == total - (A[i] + right)) {
                System.out.println("Equilibrium Index found at " + i);
            }
            // new right = A[i] + (A[i+1] + A[i+2] + .. + A[n-1])
            right += A[i];
        }
    }
    // Program to find the equilibrium index of an array
    public static void main (String[] args)
    {
        int[] A = { 0, -3, 5, -4, -2, 3, 1, 0 };
        equilibriumIndex(A);
    }
}
```

**Output:**
Equilibrium Index found at 7, 3 and 0

The time complexity of above solution is O(n) and auxiliary space used by the program is O(1).