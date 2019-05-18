# Find a duplicate element in a limited range array
Given a limited range array of size **n** where array contains elements between 1 to n-1 with one element repeating, find the duplicate number in it.
For example,
**Input:** { 1, 2, 3, 4, 4 }
**Output:** The duplicate element is 4

**Input:** { 1, 2, 3, 4, 2 }
**Output:** The duplicate element is 2
### Approach 1: (Hashing)
The idea is to use hashing to solve this problem. We can use a visited boolean array to mark if an element is seen before or not. If the element is already encountered before, the visited array will return true.
##### C++
```C++
#include <iostream>
using namespace std;
// Function to find a duplicate element in a limited range array
int findDuplicate(int arr[], int n)
{
    // create an visited array of size n+1
    // we can also use map instead of visited array
    bool visited[n];
    fill(visited, visited + n, 0); // sets every value in the array to 0
    // for each element of the array mark it as visited and
    // return the element if it is seen before
    for (int i = 0; i < n; i++)
    {
        // if element is seen before
        if (visited[arr[i]])
            return arr[i];
        // mark element as visited
        visited[arr[i]] = true;
    }
    // no duplicate found
    return -1;
}
// main function
int main()
{
    // input array contains n numbers between [1 to n - 1]
    // with one duplicate
    int arr[] = { 1, 2, 3, 4, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Duplicate element is " << findDuplicate(arr, n);
    return 0;
}
```

##### Java
```Java
class FindDuplicate
{
    // Function to find a duplicate element in a limited range array
    public static int findDuplicate(int[] A)
    {
        // create an visited array of size n+1
        // we can also use map instead of visited array
        boolean visited[] = new boolean[A.length + 1];
        // for each element of the array mark it as visited and
        // return the element if it is seen before
        for (int i = 0; i < A.length; i++)
        {
            // if element is seen before
            if (visited[A[i]]) {
                return A[i];
            }
            // mark element as visited
            visited[A[i]] = true;
        }
        // no duplicate found
        return -1;
    }
    // main function
    public static void main (String[] args)
    {
        // input array contains n numbers between [1 to n - 1]
        // with one duplicate, where n = A.length
        int[] A = { 1, 2, 3, 4, 4 };
        System.out.println("Duplicate element is " + findDuplicate(A));
    }
}
```
**Output:**
Duplicate element is 4
The time complexity of above solution is O(n) and auxiliary space used by the program is O(n).
### Approach 2:
We can solve this problem in constant space. Since the array contains all distinct elements except one and all elements lies in range 1 to n-1, we can check for duplicate element by marking array elements as negative by using array index as a key. For each array element ```arr[i]```, we get absolute value of the element ```abs(arr[i])``` and invert the sign of element present at index ```abs(arr[i])-1```. Finally, we traverse array once again and if a positive number is found at index i, then the duplicate element is i+1.
Above approach takes two traversals of the array. We can achieve the same in only one traversal. For each array element ```arr[i]```, we get absolute value of the element ```abs(arr[i])``` and invert the sign of element present at index ```abs(arr[i])-1``` if it is positive else if element is already negative, then it is a duplicate.
##### C++
```C++
#include <iostream>
using namespace std;
// Function to find a duplicate element in a limited range array
int findDuplicate(int arr[], int n)
{
    int duplicate = -1;
    // do for each element in the array
    for (int i = 0; i < n; i++)
    {
        // get absolute value of current element
        int absVal = (arr[i] < 0) ? -arr[i] : arr[i];
        // make element at index abs(arr[i])-1 negative if it is positive
        if (arr[absVal - 1] >= 0) {
            arr[absVal - 1] = -arr[absVal - 1];
        }
        else
        {
            // if element is already negative, it is repeated
            duplicate = absVal;
            break;
        }
    }
    // restore original array before returning
    for (int i = 0; i < n; i++)
    {
        // make negative elements positive
        if (arr[i] < 0)
            arr[i] = -arr[i];
    }
    // return duplicate element
    return duplicate;
}
// main function
int main()
{
    // input array contains n numbers between [1 to n - 1]
    // with one duplicate
    int arr[] = { 1, 2, 3, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Duplicate element is " << findDuplicate(arr, n);
    return 0;
}
```

##### Java
```Java
class FindDuplicate
{
    // Function to find a duplicate element in a limited range array
    public static int findDuplicate(int[] A)
    {
        int duplicate = -1;
        // do for each element in the array
        for (int i = 0; i < A.length; i++)
        {
            // get absolute value of current element
            int absVal = (A[i] < 0) ? -A[i] : A[i];
            // make element at index abs(arr[i]) - 1 negative
            // if it is positive
            if (A[absVal - 1] >= 0) {
                A[absVal - 1] = -A[absVal - 1];
            }
            else
            {
                // if element is already negative, it is repeated
                duplicate = absVal;
                break;
            }
        }
        // restore original array before returning
        for (int i = 0; i < A.length; i++) {
            // make negative elements positive
            if (A[i] < 0) {
                A[i] = -A[i];
            }
        }
        // return duplicate element
        return duplicate;
    }
    // main function
    public static void main (String[] args)
    {
        // input array contains n numbers between [1 to n - 1]
        // with one duplicate, where n = A.length
        int[] A = { 1, 2, 3, 4, 4 };
        System.out.println("Duplicate element is " + findDuplicate(A));
    }
}
```
**Output:**
Duplicate element is 2
The time complexity of above solution is O(n) and auxiliary space used by the program is O(1).
### Approach 3: (using xor)
We can also solve this problem by taking xor of all array elements with numbers from 1 to n-1. Since same elements will cancel out each other as a^a = 0, 0^0 = 0 and a^0 = a, we will be left with the duplicate element.
##### C
```C
#include <stdio.h>
// Function to find a duplicate element in a limited range array
int findDuplicate(int A[], int n)
{
    int xor = 0;
    // take xor of all array elements
    for (int i = 0; i < n; i++) {
        xor ^= A[i];
    }
    // take xor of numbers from 1 to n-1
    for (int i = 1; i <= n-1; i++) {
        xor ^= i;
    }
    // same elements will cancel out each other as a ^ a = 0,
    // 0 ^ 0 = 0 and a ^ 0 = a
    // xor will contain the missing number
    return xor;
}
// main function
int main()
{
    // input array contains n numbers between [1 to n - 1]
    // with one duplicate
    int arr[] = { 1, 2, 3, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printf("Duplicate element is %d", findDuplicate(arr, n));
    return 0;
}
```

##### Java
```Java
class FindDuplicate
{
    // Function to find a duplicate element in a limited range array
    public static int findDuplicate(int[] A)
    {
        int xor = 0;
        // take xor of all array elements
        for (int i = 0; i < A.length; i++) {
            xor ^= A[i];
        }
        // take xor of numbers from 1 to n-1
        for (int i = 1; i <= A.length - 1; i++) {
            xor ^= i;
        }
        // same elements will cancel out each other as a ^ a = 0,
        // 0 ^ 0 = 0 and a ^ 0 = a
        // xor will contain the missing number
        return xor;
    }
    // main function
    public static void main(String[] args)
    {
        // input array contains n numbers between [1 to n - 1]
        // with one duplicate, where n = A.length
        int[] A = { 1, 2, 3, 4, 4 };
        System.out.println("Duplicate element is " + findDuplicate(A));
    }
}
```
**Output:**
Duplicate element is 2
The time complexity of above solution is O(n) and auxiliary space used by the program is O(1).
### Approach 4:
Finally, the post is incomplete without this textbook solution: find sum of all element and find difference between it and all elements which are supposed to be there.
##### C++
```C++
#include <numeric>
#include <iostream>
#include <array>
template <typename It>
int find_duplicate(It start, It finish)
{
    auto size = std::distance(start, finish);
    int actual_sum = std::accumulate(start, finish, 0);
    int expected_sum = size * (size - 1) / 2;
    return actual_sum - expected_sum;
}
int main()
{
    std::array<int, 5> arr = {{ 1, 2, 3, 4, 4 }};
    std::cout << "The duplicate element is " <<
                find_duplicate(arr.begin(), arr.end());
    return 0;
}
```

##### Java
```Java
import java.util.stream.IntStream;
class FindDuplicate
{
    public static int findDuplicate(int[] A)
    {
        int actual_sum = IntStream.of(A).sum();
        int expected_sum = A.length * (A.length - 1) / 2;
        return actual_sum - expected_sum;
    }
    public static void main(String[] args)
    {
        int[] A = { 1, 2, 3, 4, 4 };
        System.out.println("The duplicate element is " + findDuplicate(A));
    }
}
```

**Output:**
The duplicate element is 4
The duplicate element is 2
The time complexity of above solution is O(n) and auxiliary space used by the program is O(1).