# Find maximum length sub-array having equal number of 0’s and 1’s
Given an binary array containing 0 and 1, find maximum length sub-array having equal number of 0’s and 1’s.
For example,
**Input:** { 0, 0, 1, 0, 1, 0, 0 }
**Output:** Largest subarray is { 0, 1, 0, 1 } or { 1, 0, 1, 0}

Naive solution would be to consider all sub-arrays and for each sub-array, we count total number of 0’s and 1’s present. If sub-array contains equal number of 0’s and 1’s, we update maximum length sub-array if required. The time complexity of naive solution is O(n<sup>3</sup>) as there are n<sup>2</sup> sub-arrays and it takes O(n) time to find count 0’s and 1’s. The method can be optimized to run in O(n<sup>2</sup>) time by calculating count of 0’s and 1’s in constant time.
We can use map to solve this problem in linear time. The idea is to replace 0 with -1 and find out the largest subarray with 0 sum. To find largest subarray with 0 sum, we create an empty map which stores the ending index of first sub-array having given sum. We traverse the given array, and maintain sum of elements seen so far.
+ If sum is seen for first time, insert the sum with its index into the map.
+ If sum is seen before, there exists a sub-array with 0 sum which ends at current index and we update maximum length sub-array if current sub-array has more length.

##### C++
```C++
#include <iostream>
#include <unordered_map>
using namespace std;
// Function to find maximum length sub-array having equal number
// of 0's and 1's
void max_len_subarray(int arr[], int n)
{
    // create an empty map to store ending index of first sub-array
    // having some sum
    unordered_map<int, int> map;
    // insert (0, -1) pair into the set to handle the case when
    // sub-array with sum 0 starts from index 0
    map[0] = -1;
    // len stores the maximum length of sub-array with sum 0
    int len = 0;
    // stores ending index of maximum length sub-array having sum 0
    int ending_index = -1;
    int sum = 0;
    // Traverse through the given array
    for (int i = 0; i < n; i++)
    {
        // sum of elements so far (replace 0 with -1)
        sum += (arr[i] == 0)? -1 : 1;
        // if sum is seen before
        if (map.find(sum) != map.end())
        {
            // update length and ending index of maximum length
            // sub-array having sum 0
            if (len < i - map[sum])
            {
                len = i - map[sum];
                ending_index = i;
            }
        }
        // if sum is seen for first time, insert sum with its
        // index into the map
        else {
            map[sum] = i;
        }
    }
    // print the sub-array if present
    if (ending_index != -1) {
        cout << "[" << ending_index - len + 1 << ", " << ending_index << "]";
    } else {
        cout << "No sub-array exists";
    }
}
// main function
int main()
{
    int arr[] = { 0, 0, 1, 0, 1, 0, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    max_len_subarray(arr, n);
    return 0;
}
```

##### Java
```Java
import java.util.Map;
import java.util.HashMap;
class MaxLengthSubArray
{
    // Function to find maximum length sub-array having equal number
    // of 0's and 1's
    public static void maxLenSubarray(int[] A)
    {
        // create an empty Hash Map to store ending index of first
        // sub-array having some sum
        Map<Integer, Integer> map = new HashMap<>();
        // insert (0, -1) pair into the set to handle the case when
        // sub-array with sum 0 starts from index 0
        map.put(0, -1);
        // len stores the maximum length of sub-array with sum 0
        int len = 0;
        // stores ending index of maximum length sub-array having sum 0
        int ending_index = -1;
        int sum = 0;
        // Traverse through the given array
        for (int i = 0; i < A.length; i++)
        {
            // sum of elements so far (replace 0 with -1)
            sum += (A[i] == 0)? -1: 1;
            // if sum is seen before
            if (map.containsKey(sum))
            {
                // update length and ending index of maximum length
                // sub-array having sum 0
                if (len < i - map.get(sum))
                {
                    len = i - map.get(sum);
                    ending_index = i;
                }
            }
            // if sum is seen for first time, insert sum with its
            // index into the map
            else {
                map.put(sum, i);
            }
        }
        // print the sub-array if present
        if (ending_index != -1) {
            System.out.println("[" + (ending_index - len + 1) + ", " +
                                       ending_index + "]");
        }
        else {
            System.out.println("No sub-array exists");
        }
    }
    // main function
    public static void main (String[] args)
    {
        int[] A = { 0, 0, 1, 0, 1, 0, 0 };
        maxLenSubarray(A);
    }
}
```
**Output:**
[1, 4]
The time complexity of above solution is O(n) and auxiliary space used by the program is O(n).