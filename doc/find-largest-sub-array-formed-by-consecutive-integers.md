# Find largest sub-array formed by consecutive integers
Given an array of integers, find largest sub-array formed by consecutive integers. The sub-array should contain all distinct values.
For example,
**Input:** { 2, 0, 2, 1, 4, 3, 1, 0 }
**Output:** The largest sub-array is { 0, 2, 1, 4, 3 }

The idea is to consider every sub-array and keep track of largest subarray found so far which is formed by consecutive integers. In order for an sub-array to contain consecutive integers,
+ The difference between maximum and minimum element in it should be exactly equal to length of the subarray minus one.
+ All elements in the array should be distinct (we can check this by inserting the elements in set or using a visited array).


##### C++
```C++
#include <iostream>
#include <vector>
using namespace std;
// Function to check if sub-array A[i..j] is formed by consecutive
// integers. Here min and max denotes the minimum and maximum element
// in the sub-array respectively
bool isConsecutive(int A[], int i, int j, int min, int max)
{
    // in order for an array to contain consecutive integers, the diff
    // between maximum and element element in it should be exactly j-i
    if (max - min != j - i)
        return false;
    // create a visited array (we can also use a set)
    vector<bool> visited(j - i + 1);
    // traverse the sub-array and checks if each element appears only once
    for (int k = i; k <= j; k++)
    {
        // if element is seen before, return false
        if (visited[A[k] - min])
            return false;
        // mark element as seen
        visited[A[k] - min] = true;
    }
    // we reach here when all elements in array are distinct
    return true;
}
// Find largest sub-array formed by consecutive integers
void findMaxSubArray(int A[], int n)
{
    int len = 1;
    int start = 0, end = 0;
    // consider each sub-array formed by A[i..j]
    // i denotes the beginning of sub-array
    for (int i = 0; i < n - 1; i++)
    {
        // stores minimum and maximum element in an sub-array A[i..j]
        int min_val = A[i], max_val = A[i];
        // j denotes the end of sub-array
        for (int j = i + 1; j < n; j++)
        {
            // update minimum and maximum element of the sub-array
            min_val = min(min_val, A[j]);
            max_val = max(max_val, A[j]);
            // check if subarray A[i..j] is formed by consecutive integers
            if (isConsecutive(A, i, j, min_val, max_val))
            {
                if (len < max_val - min_val + 1) {
                    len = max_val - min_val + 1,
                    start = i, end = j;
                }
            }
        }
    }
    // print maximum length sub-array
    cout << "The largest sub-array is [" << start << ", " << end << "]";
}
// main function
int main()
{
    int A[] = { 2, 0, 2, 1, 4, 3, 1, 0 };
    int n = sizeof(A) / sizeof(A[0]);
    findMaxSubArray(A, n);
    return 0;
}
```

##### Java
```Java
import java.lang.Math;
class MaxSubArray
{
    // Function to check if sub-array A[i..j] is formed by consecutive
    // integers. Here min and max denotes the minimum and maximum element
    // in the sub-array respectively
    static boolean isConsecutive(int A[], int i, int j, int min, int max)
    {
        // in order for an array to contain consecutive integers, the diff
        // between maximum and element element in it should be exactly j-i
        if (max - min != j - i) {
            return false;
        }
        // create a visited array (we can also use a set)
        boolean visited[] = new boolean[j - i + 1];
        // traverse the sub-array and checks if each element appears
        // only once
        for (int k = i; k <= j; k++)
        {
            // if element is seen before, return false
            if (visited[A[k] - min]) {
                return false;
            }
            // mark element as seen
            visited[A[k] - min] = true;
        }
        // we reach here when all elements in array are distinct
        return true;
    }
    // Find largest sub-array formed by consecutive integers
    public static void findMaxSubArray(int[] A)
    {
        int len = 1;
        int start = 0, end = 0;
        // consider each sub-array formed by A[i..j]
        // i denotes the beginning of sub-array
        for (int i = 0; i < A.length - 1; i++)
        {
            // stores minimum and maximum element in an sub-array A[i..j]
            int min_val = A[i], max_val = A[i];
            // j denotes the end of sub-array
            for (int j = i + 1; j < A.length; j++)
            {
                // update minimum and maximum element of the sub-array
                min_val = Math.min(min_val, A[j]);
                max_val = Math.max(max_val, A[j]);
                // check if A[i..j] is formed by consecutive integers
                if (isConsecutive(A, i, j, min_val, max_val))
                {
                    if (len < max_val - min_val + 1)
                    {
                        len = max_val - min_val + 1;
                        start = i;
                        end = j;
                    }
                }
            }
        }
        // print maximum length sub-array
        System.out.println("The largest sub-array is [" + start + ", "
                            + end + "]");
    }
    // main function
    public static void main (String[] args)
    {
        int[] A = { 2, 0, 2, 1, 4, 3, 1, 0 };
        findMaxSubArray(A);
    }
}
```
**Output:**
The largest sub-array is [1, 5]
The time complexity of above solution is O(n<sup>3</sup>) and auxiliary space used by the program is ```O(n)```.