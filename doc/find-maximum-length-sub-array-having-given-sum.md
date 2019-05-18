# Find maximum length sub-array having given sum
Given an array of integers, find maximum length sub-array having given sum.
For example, consider below array:
```A[] = { 5, 6, -5, 5, 3, 5, 3, -2, 0 }```
Sum = 8
Sub-arrays with sum 8 are
{ -5, 5, 3, 5 }
{ 3, 5 }
{ 5, 3 }
The longest subarray is { -5, 5, 3, 5 } having length 4
Naive solution would be to consider all sub-arrays and find their sum. If sub-array sum is equal to given sum, we update maximum length sub-array. The time complexity of naive solution is O(n<sup>3</sup>) as there are n<sup>2</sup> sub-arrays and it takes O(n) time to find sum of its elements. The method can be optimized to run in O(n<sup>2</sup>) time by calculating sub-array sum in constant time.

##### C
```C
#include <stdio.h>
// Naive function to find maximum length sub-array with sum S present
// in the given array
void maxLengthSubArray(int arr[], int n, int S)
{
    // len stores the maximum length of sub-array with sum S
    int len = 0;
    // stores ending index of maximum length sub-array having sum S
    int ending_index = -1;
    // consider all sub-arrays starting from i
    for (int i = 0; i < n; i++)
    {
        int sum = 0;
        // consider all sub-arrays ending at j
        for (int j = i; j < n; j++)
        {
            // sum of elements in current sub-array
            sum += arr[j];
            // if we have found a sub-array with sum S
            if (sum == S)
            {
                // update length and ending index of max length sub-array
                if (len < j - i + 1)
                {
                    len =  j - i + 1;
                    ending_index = j;
                }
            }
        }
    }
    // print the sub-array
    printf("[%d, %d]", ending_index - len + 1, ending_index);
}
// main function
int main(void)
{
    int arr[] = { 5, 6, -5, 5, 3, 5, 3, -2, 0 };
    int sum = 8;
    int n = sizeof(arr)/sizeof(arr[0]);
    maxLengthSubArray(arr, n, sum);
    return 0;
}
```

##### Java
```Java
class MaxLengthSubArray
{
    // Naive function to find maximum length sub-array with sum S present
    // in the given array
    public static void maxLengthSubArray(int[] A, int S)
    {
        // len stores the maximum length of sub-array with sum S
        int len = 0;
        // stores ending index of maximum length sub-array having sum S
        int ending_index = -1;
        // consider all sub-arrays starting from i
        for (int i = 0; i < A.length; i++)
        {
            int sum = 0;
            // consider all sub-arrays ending at j
            for (int j = i; j < A.length; j++)
            {
                // sum of elements in current sub-array
                sum += A[j];
                // if we have found a sub-array with sum S
                if (sum == S)
                {
                    // update length & ending index of max length subarray
                    if (len < j - i + 1)
                    {
                        len =  j - i + 1;
                        ending_index = j;
                    }
                }
            }
        }
        // print the sub-array
        System.out.println("[" + (ending_index - len + 1)
                            + ", " + ending_index + "]");
    }
    // main function
    public static void main (String[] args)
    {
        int[] A = { 5, 6, -5, 5, 3, 5, 3, -2, 0 };
        int sum = 8;
        maxLengthSubArray(A, sum);
    }
}
```
**Output:**
[2, 5]

We can use map to solve this problem in linear time. The idea is to create an empty map to store ending index of first sub-array having given sum. We traverse the given array, and maintain sum of elements seen so far.
+ If sum is seen for first time, insert the sum with its index into the map.
+ If (sum – S) is seen before, there exists a sub-array with given sum which ends at current index and we update maximum length sub-array having sum S if current sub-array has more length.

##### C++
```C++
#include <iostream>
#include <unordered_map>
using namespace std;
// Function to find maximum length sub-array with sum S present
// in the given array
void maxLengthSubArray(int arr[], int n, int S)
{
    // create an empty map to store ending index of first sub-array
    // having some sum
    unordered_map<int, int> map;
    // insert (0, -1) pair into the set to handle the case when
    // sub-array with sum S starts from index 0
    map[0] = -1;
    int sum = 0;
    // len stores the maximum length of sub-array with sum S
    int len = 0;
    // stores ending index of maximum length sub-array having sum S
    int ending_index = -1;
    // traverse the given array
    for (int i = 0; i < n; i++)
    {
        // sum of elements so far
        sum += arr[i];
        // if sum is seen for first time, insert sum with its index
        // into the map
        if (map.find(sum) == map.end()) {
            map[sum] = i;
        }
        // update length and ending index of maximum length sub-array
        // having sum S
        if (map.find(sum - S) != map.end() && len < i - map[sum - S])
        {
            len =  i - map[sum - S];
            ending_index = i;
        }
    }
    // print the sub-array
    cout << "[" << (ending_index - len + 1) << "," << ending_index << "]";
}
int main()
{
    int arr[] = { 5, 6, -5, 5, 3, 5, 3, -2, 0 };
    int sum = 8;
    int n = sizeof(arr) / sizeof(arr[0]);
    maxLengthSubArray(arr, n, sum);
    return 0;
}
```

##### Java
```Java
import java.util.Map;
import java.util.HashMap;
class MaxLengthSubArray
{
    // Find maximum length sub-array with sum S present in the given array
    public static void maxLengthSubArray(int[] A, int S)
    {
        // create an empty Hash Map to store ending index of first
        // sub-array having some sum
        Map<Integer, Integer> map = new HashMap<>();
        // insert (0, -1) pair into the set to handle the case when
        // sub-array with sum S starts from index 0
        map.put(0, -1);
        int sum = 0;
        // len stores the maximum length of sub-array with sum S
        int len = 0;
        // stores ending index of maximum length sub-array having sum S
        int ending_index = -1;
        // traverse the given array
        for (int i = 0; i < A.length; i++)
        {
            // sum of elements so far
            sum += A[i];
            // if sum is seen for first time, insert sum with its index
            // into the map
            if (!map.containsKey(sum))
                map.put(sum, i);
            // update length and ending index of maximum length sub-array
            // having sum S
            if (map.containsKey(sum - S) && len < i - map.get(sum - S))
            {
                len =  i - map.get(sum - S);
                ending_index = i;
            }
        }
        // print the sub-array
        System.out.println("[" + (ending_index - len + 1) + ", "
                                   + ending_index + "]");
    }
    // main function
    public static void main (String[] args)
    {
        int[] A = { 5, 6, -5, 5, 3, 5, 3, -2, 0 };
        int sum = 8;
        maxLengthSubArray(A, sum);
    }
}
```
**Output:**
[2, 5]
The time complexity of above solution is O(n) and auxiliary space used by the program is O(n).