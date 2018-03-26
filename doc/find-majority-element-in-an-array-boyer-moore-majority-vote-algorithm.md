# Find majority element in an array (Boyer–Moore majority vote algorithm)
Given an array of integers containing duplicates, return the majority element in an array if present. A majority element appears more than n/2 times where n is the size of the array.
For example, the majority element is 2 in the array `{2, 8, 7, 2, 2, 5, 2, 3, 1, 2, 2}`
Naive solution would be to count frequency of each element present in the first half of the array to check if it is majority element or not. Below is the naive implementation

```
int majorityElementNaive(int A[], int n)
{
    // check if A[i] is majority element or not
    for (int i = 0; i <= n/2; i++)
    {
        int count = 1;
        for (int j = i + 1; j < n; j++) {
            if (A[j] == A[i]) {
                count++;
            }
        }
        if (count > n/2) {
            return A[i];
        }
    }
    return -1;
}
```
The time complexity of above solution is O(n^2^).
We can improve worst case time complexity to O(nlogn) by sorting the array and then perform binary search for first and last occurrence of each element. If difference between first and last occurrence is more than n/2, we have found majority element.

### O(n) solution
We can use hashing to solve this problem in linear time. The idea is to store each element’s frequency in a map and return the element if its frequency becomes more than n/2. If no such element is present, then majority element does not exists in the array and we return -1. The time complexity of above solution is O(n) and auxiliary space used by the program is O(n).
##### C++
```C++
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;
// Function to find majority element is present in an array (vector)
int majorityElement(vector<int> A)
{
    // create an empty map
    unordered_map<int, int> map;
    // get input size
    int n = A.size();
    // 1. store each element's frequency in a map
    for (int i = 0; i < n; i++) {
        map[A[i]]++;
    }
    // 2. return the element if its count is more than n/2
    for (auto pair: map) {
        if (pair.second > n/2) {
            return pair.first;
        }
    }
    // Note that step 2 and step 3 can be merged into one
    /* for (int i = 0; i < n; i++)
    {
        if (++map[A[i]] > n/2)
            return A[i];
    } */
    // return -1 if no majority element is present
    return -1;
}
// main function
int main()
{
    vector<int> vec = { 2, 8, 7, 2, 2, 5, 2, 3, 1, 2, 2 };
    int res = majorityElement(vec);
    if (res != -1)
        cout << "Majority element is " << res;
    else
        cout << "Majority element doesn't exists";
    return 0;
}
```

**Output:**
Majority element is 2
##### Java
```Java
import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;
class MajorityElement
{
    // Function to return majority element present in given array
    public static int majorityElement(int[] A)
    {
        // create an empty Hash Map
        Map<Integer, Integer> map = new HashMap<>();
        // store each element's frequency in a map
        for (int i = 0; i < A.length; i++)
        {
            if (map.get(A[i]) == null) {
                map.put(A[i], 0);
            }
            map.put(A[i], map.get(A[i]) + 1);
        }
        // return the element if its count is more than n/2
        Iterator<Map.Entry<Integer,Integer>> it = map.entrySet().iterator();
        while (it.hasNext())
        {
            Map.Entry<Integer, Integer> pair = it.next();
            if (pair.getValue() > A.length/2)
                return pair.getKey();
            it.remove(); // avoids ConcurrentModification Exception
        }
        // no majority element is present
        return -1;
    }
    public static void main (String[] args)
    {
        // Assumption - valid input (majority element is present)
        int arr[] = { 1, 8, 7, 4, 1, 2, 2, 2, 2, 2, 2 };
        int res = majorityElement(arr);
        if (res != -1) {
            System.out.println("Majority element is " + res);
        } else {
            System.out.println("Majority element does not exist");
        }
    }
}
```

**Output:**
Majority element is 2

### Boyer–Moore majority vote algorithm
We can find the majority element using linear time and constant space using Boyer–Moore majority vote algorithm. The algorithm can be expressed in pseudocode as the following steps:
```
Initialize an element m and a counter i = 0
for each element x of the input sequence:
    if i = 0, then
        assign m = x and i = 1
    else
        if m = x, then assign i = i + 1
    else
        assign i = i – 1
return m
```
The algorithm processes the each element of the sequence, one at a time. When processing an element x,
1. If the counter is 0, we set the current candidate to x and we set the counter to 1.
2. If the counter is not 0, we increment or decrement the counter according to whether x is the current candidate.

At the end of this process, if the sequence has a majority, it will be the element stored by the algorithm. If there is no majority element, the algorithm will not detect that fact, and will still output one of the elements. We can modify the algorithm to verify that the element found is really is a majority element or not.
##### C
```C
#include <stdio.h>
// Function to return majority element present in given array
int majorityElement(int A[], int n)
{
    // m stores majority element (if present)
    int m;
    // initalize counter i with 0
    int i = 0;
    // do for each element A[j] of the array
    for (int j = 0; j < n; j++)
    {
        // If the counter i becomes 0, we set the current candidate
        // to A[j] and reset the counter to 1
        if (i == 0)
            m = A[j], i = 1;
        // If the counter is not 0, we increment or decrement the counter
        // according to whether A[j] is the current candidate
        else (m == A[j]) ? i++ : i--;
    }
    return m;
}
// main function
int main(void)
{
    // Assumtion - valid input (majority element is present)
    int arr[] = { 1, 8, 7, 4, 1, 2, 2, 2, 2, 2, 2 };
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("Majority element is %d", majorityElement(arr, n));
    return 0;
}
```

**Output:**
Majority element is 2

##### Java
```Java
class MajorityElement
{
    // Function to return majority element present in given array
    public static int majorityElement(int[] A)
    {
        // m stores majority element if present
        int m = -1;
        // initialize counter i with 0
        int i = 0;
        // do for each element A[j] of the array
        for (int j = 0; j < A.length; j++)
        {
            // if the counter i becomes 0
            if (i == 0)
            {
                // set the current candidate to A[j]
                m = A[j];
                // reset the counter to 1
                i = 1;
            }
            // else increment the counter if A[j] is current candidate
            else if (m == A[j]) {
                i++;
            }
            // else decrement the counter if A[j] is not current candidate
            else {
                i--;
            }
        }
        return m;
    }
    // main function
    public static void main (String[] args)
    {
        // Assumption - valid input (majority element is present)
        int[] arr = { 1, 8, 7, 4, 1, 2, 2, 2, 2, 2, 2 };
        System.out.println("Majority element is " + majorityElement(arr));
    }
}
```

**Output:**
Majority element is 2