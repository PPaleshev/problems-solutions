# Print all sub-arrays with 0 sum
Given an array of integers, print all sub-arrays with 0 sum.
For example,

**Input:**  `{ 4, 2, -3, -1, 0, 4 }`

Sub-arrays with 0 sum are
+ `{ -3, -1, 0, 4 }`
+ `{ 0 }`

**Input:**  `{ 3, 4, -7, 3, 1, 3, 1, -4, -2, -2 }`

Sub-arrays with 0 sum are
+ `{ 3, 4, -7 }`
+ `{ 4, -7, 3 }`
+ `{ -7, 3, 1, 3 }`
+ `{ 3, 1, -4 }`
+ `{ 3, 1, 3, 1, -4, -2, -2 }`
+ `{ 3, 4, -7, 3, 1, 3, 1, -4, -2, -2 }`

### Approach 1: Naive solution
Naive solution would be to consider all sub-arrays and find its sum. If sub-array sum is equal to 0, we print it. The time complexity of naive solution is O(n<sup>3</sup>) as there are n<sup>2</sup> sub-arrays and it takes O(n) time to find sum of its elements. The method can be optimized to run in O(n<sup>2</sup>) time by calculating sub-array sum in constant time.

##### C++
```C++
#include <iostream>
#include <unordered_map>
using namespace std;
// Function to print all sub-arrays with 0 sum present
// in the given array
void printallSubarrays(int arr[], int n)
{
    // consider all sub-arrays starting from i
    for (int i = 0; i < n; i++)
    {
        int sum = 0;
        // consider all sub-arrays ending at j
        for (int j = i; j < n; j++)
        {
            // sum of elements so far
            sum += arr[j];
            // if sum is seen before, we have found a sub-array
            // with 0 sum
            if (sum == 0) {
                cout << "Subarray [" << i << ".." << j << "]\n";
            }
        }
    }
}
// main function
int main()
{
    int arr[] = { 3, 4, -7, 3, 1, 3, 1, -4, -2, -2 };
    int n = sizeof(arr)/sizeof(arr[0]);
    printallSubarrays(arr, n);
    return 0;
}
```

##### Java
```Java
class PrintallSubarrays
{
    // Function to print all sub-arrays with 0 sum present
    // in the given array
    public static void printallSubarrays(int[] A)
    {
        // consider all sub-arrays starting from i
        for (int i = 0; i < A.length; i++)
        {
            int sum = 0;
            // consider all sub-arrays ending at j
            for (int j = i; j < A.length; j++)
            {
                // sum of elements so far
                sum += A[j];
                // if sum is seen before, we have found a subarray with 0 sum
                if (sum == 0) {
                    System.out.println("Subarray [" + i + ".." + j + "]");
                }
            }
        }
    }
    // main function
    public static void main (String[] args)
    {
        int[] A = { 3, 4, -7, 3, 1, 3, 1, -4, -2, -2 };
        printallSubarrays(A);
    }
}
```
**Output:**
+ Subarray [0..2]
+ Subarray [0..9]
+ Subarray [1..3]
+ Subarray [2..5]
+ Subarray [3..9]
+ Subarray [5..7]

### Approach 2: Using multimap to print all subarrays
We can use MultiMap to print all sub-arrays with 0 sum present in the given array. The idea is to create an empty multimap to store ending index of all sub-arrays having given sum. We traverse the given array, and maintain sum of elements seen so far. If sum is seen before, there exists at-least one sub-array with 0 sum which ends at current index and we print all such sub-arrays.

##### C++
```C++
#include <iostream>
#include <unordered_map>
using namespace std;
// Function to print all sub-arrays with 0 sum present
// in the given array
void printallSubarrays(int arr[], int n)
{
    // create an empty multi-map to store ending index of all
    // sub-arrays having same sum
    unordered_multimap<int, int> map;
    // insert (0, -1) pair into the map to handle the case when
    // sub-array with 0 sum starts from index 0
    map.insert(pair<int, int>(0, -1));
    int sum = 0;
    // traverse the given array
    for (int i = 0; i < n; i++)
    {
        // sum of elements so far
        sum += arr[i];
        // if sum is seen before, there exists at-least one
        // sub-array with 0 sum
        if (map.find(sum) != map.end())
        {
            auto it = map.find(sum);
            // find all sub-arrays with same sum
            while (it != map.end() && it->first == sum)
            {
                cout << "Subarray [" << it->second + 1 << ".." << i << "]\n";
                it++;
            }
        }
        // insert (sum so far, current index) pair into multi-map
        map.insert(pair<int, int>(sum, i));
    }
}
// main function
int main()
{
    int arr[] = { 3, 4, -7, 3, 1, 3, 1, -4, -2, -2 };
    int n = sizeof(arr)/sizeof(arr[0]);
    printallSubarrays(arr, n);
    return 0;
}
```

##### Java
```Java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
class PrintallSubarrays
{
    // Utility function to insert <key, value> into the Multimap
    private static<K,V> void insert(Map<K, List<V>> hashMap, K key, V value)
    {
        // if the key is seen for the first time, initialize the list
        if (!hashMap.containsKey(key)) {
            hashMap.put(key, new ArrayList<>());
        }
        hashMap.get(key).add(value);
    }
    // Function to print all sub-arrays with 0 sum present
    // in the given array
    public static void printallSubarrays(int[] A)
    {
        // create an empty Multi-map to store ending index of all
        // sub-arrays having same sum
        Map<Integer, List<Integer>> hashMap = new HashMap<>();
        // insert (0, -1) pair into the map to handle the case when
        // sub-array with 0 sum starts from index 0
        insert(hashMap, 0, -1);
        int sum = 0;
        // traverse the given array
        for (int i = 0; i < A.length; i++)
        {
            // sum of elements so far
            sum += A[i];
            // if sum is seen before, there exists at-least one
            // sub-array with 0 sum
            if (hashMap.containsKey(sum))
            {
                List<Integer> list = hashMap.get(sum);
                // find all sub-arrays with same sum
                for (Integer value: list) {
                    System.out.println("Subarray [" + (value + 1) + ".." +
                                               i + "]");
                }
            }
            // insert (sum so far, current index) pair into the Multi-map
            insert(hashMap, sum, i);
        }
    }
    // main function
    public static void main (String[] args)
    {
        int[] A = { 3, 4, -7, 3, 1, 3, 1, -4, -2, -2 };
        printallSubarrays(A);
    }
}
```
**Output:**
+ Subarray [0..2]
+ Subarray [1..3]
+ Subarray [2..5]
+ Subarray [5..7]
+ Subarray [3..9]
+ Subarray [0..9]