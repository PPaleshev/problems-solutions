# Shuffle a given array of elements (Fisher–Yates shuffle)
Given an array of integers, in-place shuffle it. The algorithm should produce an unbiased permutation i.e. every permutation is equally likely.
Fisher–Yates shuffle is used to generate random permutations. It takes time proportional to the number of items being shuffled and shuffles them in place. At each iteration, the algorithm swaps the element with one chosen at random amongst all remaining unvisited elements, including the element itself. Below is complete algorithm 
**To shuffle an array a of n elements :**
```
for i from n-1 downto 1 do
    j = random integer such that 0 <= j <= i
    exchange a[j] and a[i]
```

##### C
```C

#include <stdio.h>
// Utility function to swap two elements A[i] and A[j] in the array
void swap(int A[], int i, int j) {
    int temp = A[i];
    A[i] = A[j];
    A[j] = temp;
}
// Function to shuffle an array A[] of n elements
void shuffle(int A[], int n)
{
    // read array from highest index to lowest
    for (int i = n - 1; i >= 1; i--)
    {
        // generate a random number j such that 0 <= j <= i
        int j = rand() % (i + 1);
        // swap current element with randomly generated index
        swap(A, i, j);
    }
}
// main function
int main(void)
{
    int A[] = { 1, 2, 3, 4, 5, 6 };
    int n = sizeof(A) / sizeof(A[0]);
    // seed for random input
    srand(time(NULL));
    shuffle(A, n);
    // print the shuffled array
    for (int i = 0; i < n; i++) {
        printf("%d ", A[i]);
    }
    return 0;
}
```

##### Java
```Java

import java.util.Arrays;
import java.util.Random;
class Shuffle
{
    // Utility function to swap two elements A[i] and A[j] in the array
    private static void swap(int[] A, int i, int j) {
        int temp = A[i];
        A[i] = A[j];
        A[j] = temp;
    }
    // Function to shuffle an array A[]
    public static void shuffle(int A[])
    {
        // read array from highest index to lowest
        for (int i = A.length - 1; i >= 1; i--)
        {
            Random rand = new Random();
            // generate a random number j such that 0 <= j <= i
            int j = rand.nextInt(i + 1);
            // swap current element with randomly generated index
            swap(A, i, j);
        }
    }
    // main function
    public static void main (String[] args)
    {
        int[] A = { 1, 2, 3, 4, 5, 6 };
        shuffle(A);
        // print the shuffled array
        System.out.println(Arrays.toString(A));
    }
}
```
The time complexity of above solution is O(n) and auxiliary space used by the program is O(1).

An equivalent version which shuffles the array in the opposite direction (from lowest index to highest) is:
**To shuffle an array a of n elements :**
```
for i from 0 to n-2 do
    j = random integer such that i <= j < n
    exchange a[i] and a[j]
```
##### C
```C

#include <stdio.h>
// Utility function to swap two elements A[i] and A[j] in the array
void swap(int A[], int i, int j) {
    int temp = A[i];
    A[i] = A[j];
    A[j] = temp;
}
// Function to shuffle an array A of n elements
void shuffle(int A[], int n)
{
    // read array from lowest index to highest
    for (int i = 0; i <= n - 2; i++)
    {
        // generate a random number j such that i <= j < n
        int j = i + rand() % (n - i);
        // swap current element with randomly generated index
        swap(A, i, j);
    }
}
// main function
int main(void)
{
    int A[] = { 1, 2, 3, 4, 5, 6 };
    int n = sizeof(A) / sizeof(A[0]);
    // seed for random input
    srand(time(NULL));
    shuffle(A, n);
    // print the shuffled array
    for (int i = 0; i < n; i++) {
        printf("%d ", A[i]);
    }
    return 0;
}
```

##### Java
```Java

import java.util.Arrays;
import java.util.Random;
class Shuffle
{
    // Utility function to swap two elements A[i] and A[j] in the array
    private static void swap(int[] A, int i, int j) {
        int temp = A[i];
        A[i] = A[j];
        A[j] = temp;
    }
    // Function to shuffle an array A[]
    public static void shuffle(int A[])
    {
        // read array from lowest index to highest
        for (int i = 0; i <= A.length - 2; i++)
        {
            Random rand = new Random();
            // generate a random number j such that i <= j < n
            int j = i + rand.nextInt(A.length - i);
            // swap current element with randomly generated index
            swap(A, i, j);
        }
    }
    // main function
    public static void main (String[] args)
    {
        int[] A = { 1, 2, 3, 4, 5, 6 };
        shuffle(A);
        // print the shuffled array
        System.out.println(Arrays.toString(A));
    }
}
```

The time complexity of above solution is O(n) and auxiliary space used by the program is O(1).