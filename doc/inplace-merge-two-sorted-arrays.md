# Inplace merge two sorted arrays
Given two sorted arrays ```X[]``` and ```Y[]``` of size ```m``` and ```n``` each, merge elements of ```X[]``` with elements of array ```Y[]``` by maintaining the sorted order. i.e. fill X[] with first m smallest elements and fill Y[] with remaining elements.
The conversion should be done in-place and without using any other data structure.
For example,
**Input:**
X[] = { 1, 4, 7, 8, 10 }
Y[] = { 2, 3, 9 }
**Output:**
X[] = { 1, 2, 3, 4, 7 }
Y[] = { 8, 9, 10 }
The idea is very simple. We consider each element of array X[] and ignore the element if it is already in correct order (i.e. the element smallest among all remaining elements) else we swap it with smallest element which happens to be first element of Y. After swapping, we move the element (now present at Y[0]) to its correct position in Y[] to maintain the sorted order. The merge process is almost similar to merge routine of mergesort algorithm. The only difference is that we are not using an auxiliary array for merging.

##### C++
```C++
#include <iostream>
#include <algorithm>
using namespace std;
// Utility function to print contents of an array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << '\n';
}
// in-place merge two sorted arrays X[] and Y[]
// invariant: X[] and Y[] are sorted at any point
void merge(int X[], int Y[], int m, int n)
{
    // consider each element X[i] of array X and ignore the element
    // if it is already in correct order else swap it with next smaller
    // element which happens to be first element of Y
    for (int i = 0; i < m;  i++)
    {
        // compare current element of X[] with first element of Y[]
        if (X[i] > Y[0])
        {
            swap(X[i], Y[0]);
            int first = Y[0];
            // move Y[0] to its correct position to maintain sorted
            // order of Y[]. Note: Y[1..n-1] is already sorted
            int k;
            for (k = 1; k < n && Y[k] < first; k++) {
                Y[k - 1] = Y[k];
            }
            Y[k - 1] = first;
        }
    }
}
// main function
int main()
{
    int X[] = { 1, 4, 7, 8, 10 };
    int Y[] = { 2, 3, 9 };
    int m = sizeof(X) / sizeof(X[0]);
    int n = sizeof(Y) / sizeof(Y[0]);
    merge(X, Y, m, n);
    cout << "X: "; printArray(X, m);
    cout << "Y: "; printArray(Y, n);
    return 0;
}
```

##### Java
```Java
import java.util.Arrays;
class Merge
{
    // in-place merge two sorted arrays X[] and Y[]
    // invariant: X[] and Y[] are sorted at any point
    public static void merge(int[] X, int[] Y)
    {
        int m = X.length;
        int n = Y.length;
        // consider each element X[i] of array X and ignore the element
        // if it is already in correct order else swap it with next smaller
        // element which happens to be first element of Y
        for (int i = 0; i < m; i++)
        {
            // compare current element of X[] with first element of Y[]
            if (X[i] > Y[0])
            {
                // swap (X[i], Y[0])
                int temp = X[i];
                X[i] = Y[0];
                Y[0] = temp;
                int first = Y[0];
                // move Y[0] to its correct position to maintain sorted
                // order of Y[]. Note: Y[1..n-1] is already sorted
                int k;
                for (k = 1; k < n && Y[k] < first; k++) {
                    Y[k - 1] = Y[k];
                }
                Y[k - 1] = first;
            }
        }
    }
    // main function
    public static void main (String[] args)
    {
        int[] X = { 1, 4, 7, 8, 10 };
        int[] Y = { 2, 3, 9 };
        merge(X, Y);
        System.out.println("X: " + Arrays.toString(X));
        System.out.println("Y: " + Arrays.toString(Y));
    }
}
```
**Output:**
X: 1 2 3 4 7
Y: 8 9 10

The time complexity of above solution is O(mn) and auxiliary space used by the program is O(1). The problem can in fact be solved in linear time and constant space.