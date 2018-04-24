# Check if subarray with 0 sum is exists or not
Given an array of integers, check if array contains a sub-array having 0 sum.
For example,

**Input:**  { 3, 4, -7, 3, 1, 3, 1, -4, -2, -2 }

**Output:** Subarray with 0 sum exists

The sub-arrays with 0 sum are:

+ `{ 3, 4, -7 }`
+ `{ 4, -7, 3 }`
+ `{ -7, 3, 1, 3 }`
+ `{ 3, 1, -4 }`
+ `{ 3, 1, 3, 1, -4, -2, -2 }`
+ `{ 3, 4, -7, 3, 1, 3, 1, -4, -2, -2 }`

We can easily solve this problem in linear time by using hashing. The idea is to use set to check if sub-array with zero sum is present in the given array or not. We traverse the given array, and maintain sum of elements seen so far. If sum is seen before (i.e. sum exists in set), we return true as there exists at-least one sub-array with zero sum which ends at current index else we insert the sum into the set.
The time complexity of proposed solution is O(n) and auxiliary space used by the program is O(n).

##### C++
```C++
#include <iostream>
#include <unordered_set>
using namespace std;
// Function to check if sub-array with 0 sum is present
// in the given array or not
bool zeroSumSubarray(int A[], int n)
{
    // create an empty set to store sum of elements of each
    // sub-array A[0..i] where 0 <= i < n
    unordered_set<int> set;
    // insert 0 into set to handle the case when sub-array with
    // 0 sum starts from index 0
    set.insert(0);
    int sum = 0;
    // traverse the given array
    for (int i = 0; i < n; i++)
    {
        // sum of elements so far
        sum += A[i];
        // if sum is seen before, we have found a sub-array with 0 sum
        if (set.find(sum) != set.end()) {
            return true;
        } else {
            // insert sum so far into set
            set.insert(sum);
        }
    }
    // we reach here when no sub-array with 0 sum exists
    return false;
}
// main function
int main()
{
    int A[] = { 4, 2, -3, -1, 0, 4 };
    int n = sizeof(A)/sizeof(A[0]);
    zeroSumSubarray(A, n) ?
            cout << "Subarray exists":
            cout << "Subarray do not exist";
    return 0;
}
```

**Output:**
Subarray exists

##### Java
```Java
import java.util.Set;
import java.util.HashSet;
class ZeroSumSubarray
{
    // Function to check if sub-array with 0 sum is present
    // in the given array or not
    public static Boolean zeroSumSubarray(int[] A)
    {
        // create an empty set to store sum of elements of each
        // sub-array A[0..i] where 0 <= i < arr.length
        Set<Integer> set = new HashSet<>();
        // insert 0 into set to handle the case when sub-array with
        // 0 sum starts from index 0
        set.add(0);
        int sum = 0;
        // traverse the given array
        for (int i = 0; i < A.length; i++)
        {
            // sum of elements so far
            sum += A[i];
            // if sum is seen before, we have found a sub-array with 0 sum
            if (set.contains(sum)) {
                return true;
            }
            // insert sum so far into set
            set.add(sum);
        }
        // we reach here when no sub-array with 0 sum exists
        return false;
    }
    // main function
    public static void main (String[] args)
    {
        int[] A = { 4, -6, 3, -1, 4, 2, 7 };
        if (zeroSumSubarray(A)) {
            System.out.println("Subarray exists");
        } else {
            System.out.println("Subarray do not exist");
        }
    }
}
```

**Output:**
Subarray exists