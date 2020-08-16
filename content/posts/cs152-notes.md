---
date: "2020-03-14"
tags:
- uchicago
- notes
title: CS 152 Notes 
---

These are notes for the final exam in CS 152, taught by Diana Franklin. The code for the class can be found <a href = "https://github.com/deblnia/CS152" target = "_blank">here</a>. 

#### Data Representation

**To convert to unsigned binary:**

  1. Number of places is number of bits, fill all with zeroes by default (every place has value of 2 to the power of the place -- from the right, zero based indexing)
  2. Find highest power of two that goes into decimal number 
  3. Go to that power's place, and change to one
  4. Keep adding powers of two until you get to number 
  
**To convert to hex:**

  1. Divide the decimal number by 16 (treat division as integer division)
  2. Write down the remainder in hexadecimal (becomes alphabet starting with 'A' at 10)
  3. Divide the result again by 16 (still integer division)
  4. Repeat step 2 and 3 until result is 0 
  5. The hex value is the digit sequence of remainders from last to first 
  
**Bitwise Operations:**

- `&` is bitwise AND 
- `|` is bitwise OR 
- `^` is bitwise XOR (exclusive OR)
- `-` is bitwise complement 
- `<<` is bitwise shift left 
- `>>` is bitwise shift right 

<a href = "https://www.learn-c.org/en/Bitmasks" target = "_blank">Always used with binary.</a>

#### Data Structures: 

**Array:** 

- An array is a data structure consisting of several elements, each identified by a key. 
- In C, arrays are not mutable. 

**Tree:**

- In it's simplest form, a tree is made up of nodes that each have a _data pointer_, a _left pointer_ and a _right pointer_
- It's used for parsing and fast sorted, indexing 
- There are several methods of traversing a tree: inorder (L-Root-R), preorder (Root-L-R), and postorder (L-R-Root)
- With N-ary trees, the N stands for the numbr of children each node has 
  - Usually implemented with binary trees 

**Stack:**

- Useful for implementing recursive or multi-threaded algorithms 
- LIFO (last in, first out), so it grows by adding to the tail (also called push), and then removes from the tail (also called pop)
- A variation on a queue 
- When implemented as an array, can have either top-down or bottom up stacks: 
  - the beginning of a topdown stack is given as the first address following the last element of the array; 
  - the beginning of a bottom-up stack is given as the address of the first element of the array. 

**Queue:** 

- FIFO (first in, first out), things are added to the end and removed from the beginning 
- Priority queues (like the stack) organzie data according to an arbitrary designation of importance 


**Graph:** 

- Graphs are like n-ary trees but can have cycles (point back to themselves)
- Also searched bredth-first / depth-first 
- Can be directed / undirected 

**Hash Table:**

- Stores data as key value pairs 
- Hash is a function that converts one value to another 
- Key is a piece of information used to retrieve some data 
- Collision-resolution techniques are used to deal with collisions in the table (permits find, insert and delete operations that work correctly)
  - linear probing: does a linear search for an empty slot when there is a collision 
    - advantages: 
      - easy to implement
      - always finds a location if there is one
      - very good average-case performance when the table is not very full
    - disadvantages: 
      - “clusters” or "clumps" of keys form in adjacent slots in the table
when these clusters fill most of the array
      - performance deteriorates badly as the probe sequence performs what is essentially an exhaustive search of most of the array
  - double hashing: make the offset to the next position probed depend on the key value, so it can be different for different keys
      - advantages: 
        - It drastically reduces clustering.
        - It requires fewer comparisons.
        - Smaller hash tables can be used.
      - disadvantages: 
        - Performance degrades as table fills up 
  - linked-list collision resolution: inserts creates a linked list to the slot for which collision occurs, the new key is then inserted in the linked list, and then these linked lists to the slots appear like chains
      - advantages: 
        - Simple to implement.
        - Hash table never fills up, we can always add more elements to the chain
        - Less sensitive to the hash function or load factors.
        - It is mostly used when it is unknown how many and how frequently keys may be inserted or deleted.
      - disadvantages: 
        - Cache performance of chaining is not good as keys are stored using a linked list. Open addressing provides better cache performance as everything is stored in the same table.
        - Wastage of Space (Some Parts of hash table are never used)
        - If the chain becomes long, then search time can become O(n) in the worst case.
        - Uses extra space for links.

- Clustering is when many consecutive elements form groups and it starts taking time to find a free slot or to search an element. (It's a problem in linear probing.)
- A hash algorithm is a mathematical function that maps data of arbitrary size to a hash of a fixed size. It's designed to be a one-way function, infeasible to invert.
- Universal hashing is the idea that we select the hash function randomly from a group of hash functions. This means an adversary cannot choose keys that he knows will give worst case performance anymore, since the adversary doesn’t even know what hash function will be chosen for the table. If we form the group of hash
functions carefully, we can assure that the expected time for each operations is O(1), even if there is an adversary who is trying to achieve worst case performance.

**Linked List:**

- A list of nodes that each have a _data pointer_, and a _node pointer_ 
- First element in the list is called the head, the other is called the tail 

**Heaps:** 
 
- Heaps are a data structure with an order property, and a structure property. 
    - order property: all heaps are ordered in a way where there is a clear relationship (min/max, commonly) between every group of parent and children nodes 
    - structure property: all heaps are complete trees (or almost complete), which is to say that insertion is done left to right on the leaf nodes 
- Binary heaps are usually implemented as BSTs, but are also a maximally efficient implementation of the priorty queue abstract data type. 
  - A binary heap is <a href = "https://www.geeksforgeeks.org/array-representation-of-binary-heap/" target = "_blank">implemented in an array </a> using the following formulas: 
    - `Arr[0]` is the root node 
    For any other node, `Arr[i]`: 
      - `Arr[(i-1)/2]` returns the parent node 
      - `Arr[(2*i)+1]` returns the left child node 
      - `Arr[(2*i)+2]` returns the right child node 
  - Traversal using the array implementation is in order level, as in below 

<center> 

![](https://media.geeksforgeeks.org/wp-content/uploads/HeapRepresentation-1.png)

</center> 

#### Algorithmic Complexity 

  - Rules of thumb: 
    1. Every for loop multiplies $O(n)$ complexity because the compiler must iterate through every item in the structure. 
    2. Every recursive call adds $O(2^n)$ complexity, provided there's only one base case. 
    3. If every additional call halves the set, the complexity is $O(log_2 n)$


#### Sorting 

**Merge Sort:** 

- A divide and conquer algorithm (divides array into two halves, calls itself for the two halves and then merges the two sorted halves)
- Does not sort in place 
- Time Complexity is $O(nlogn)$ because splits in half and then takes linear time to merge halves 

1. Find the middle point to divide the array into two halves: middle `m = (l+r)/2`
2. Call mergeSort for first half: Call `mergeSort(arr, l, m)`
3. Call mergeSort for second half: Call `mergeSort(arr, m+1, r)`
4. Merge the two halves sorted in step 2 and 3: Call `merge(arr, l, m, r)`

Or the C implementation: 

```
// Merges two subarrays of arr[]. 
// First subarray is arr[l..m] 
// Second subarray is arr[m+1..r] 
void merge(int arr[], int l, int m, int r) 
{ 
    int i, j, k; 
    int n1 = m - l + 1; 
    int n2 =  r - m; 
  
    /* create temp arrays */
    int L[n1], R[n2]; 
  
    /* Copy data to temp arrays L[] and R[] */
    for (i = 0; i < n1; i++) 
        L[i] = arr[l + i]; 
    for (j = 0; j < n2; j++) 
        R[j] = arr[m + 1+ j]; 
  
    /* Merge the temp arrays back into arr[l..r]*/
    i = 0; // Initial index of first subarray 
    j = 0; // Initial index of second subarray 
    k = l; // Initial index of merged subarray 
    while (i < n1 && j < n2) 
    { 
        if (L[i] <= R[j]) 
        { 
            arr[k] = L[i]; 
            i++; 
        } 
        else
        { 
            arr[k] = R[j]; 
            j++; 
        } 
        k++; 
    } 
  
    /* Copy the remaining elements of L[], if there 
       are any */
    while (i < n1) 
    { 
        arr[k] = L[i]; 
        i++; 
        k++; 
    } 
  
    /* Copy the remaining elements of R[], if there 
       are any */
    while (j < n2) 
    { 
        arr[k] = R[j]; 
        j++; 
        k++; 
    } 
} 
  
/* l is for left index and r is right index of the 
   sub-array of arr to be sorted */
void mergeSort(int arr[], int l, int r) 
{ 
    if (l < r) 
    { 
        // Same as (l+r)/2, but avoids overflow for 
        // large l and h 
        int m = l+(r-l)/2; 
  
        // Sort first and second halves 
        mergeSort(arr, l, m); 
        mergeSort(arr, m+1, r); 
  
        merge(arr, l, m, r); 
    } 
} 

``` 

<center> 

![](https://gifimage.net/wp-content/uploads/2017/10/merge-sort-gif-7.gif)

</center> 

**Bubble Sort:** 

- The simplest sorting algorithm (repeatedly swaps adjacent elements if they are in the wrong order)
- Sorts in place 
- Time complexity is $O(n)$ best case, or $O(n^2)$ worst case 

C implementation: 

```
void swap(int *xp, int *yp) 
{ 
    int temp = *xp; 
    *xp = *yp; 
    *yp = temp; 
} 
  
// A function to implement bubble sort 
void bubbleSort(int arr[], int n) 
{ 
   int i, j; 
   for (i = 0; i < n-1; i++)       
  
       // Last i elements are already in place    
       for (j = 0; j < n-i-1; j++)  
           if (arr[j] > arr[j+1]) 
              swap(&arr[j], &arr[j+1]); 
} 
```

<center> 

![](https://miro.medium.com/max/3840/1*p_wD00rbc6RkA8w6lqqCkg.gif)

</center> 


**Quick Sort:** 

- A divide and conquer algorithm (like merge sort)
- It is implemented recursively, so does technically modify the array in place (extra space used to store function calls, not manipulate the input)
- Time complexity is $O(n^2)$ in the worst case and $O(nlogn)$ in the best and average cases. 
- The algorithm picks an element as a pivot (usually first, last, random, or median) and partitions the given array around the picked pivot


The C implementation: 

```
void swap(int* a, int* b) 
{ 
    int t = *a; 
    *a = *b; 
    *b = t; 
} 
  
/* This function takes last element as pivot, places 
   the pivot element at its correct position in sorted 
    array, and places all smaller (smaller than pivot) 
   to left of pivot and all greater elements to right 
   of pivot */
int partition (int arr[], int low, int high) 
{ 
    int pivot = arr[high];    // pivot 
    int i = (low - 1);  // Index of smaller element 
  
    for (int j = low; j <= high- 1; j++) 
    { 
        // If current element is smaller than the pivot 
        if (arr[j] < pivot) 
        { 
            i++;    // increment index of smaller element 
            swap(&arr[i], &arr[j]); 
        } 
    } 
    swap(&arr[i + 1], &arr[high]); 
    return (i + 1); 
} 
  
/* The main function that implements QuickSort 
 arr[] --> Array to be sorted, 
  low  --> Starting index, 
  high  --> Ending index */
void quickSort(int arr[], int low, int high) 
{ 
    if (low < high) 
    { 
        /* pi is partitioning index, arr[p] is now 
           at right place */
        int pi = partition(arr, low, high); 
  
        // Separately sort elements before 
        // partition and after partition 
        quickSort(arr, low, pi - 1); 
        quickSort(arr, pi + 1, high); 
    } 
} 
```

<center> 

![](https://miro.medium.com/max/1056/1*KYMf-QvVTynOKK4HSxG0oA.gif)

</center>



**Insertion Sort** 

- Simple sorting algorithm that sorts incrementally 
- Sorts in place 
- Time complexity is $O(n^2)$


C implementation: 

```

/* Function to sort an array using insertion sort*/
void insertionSort(int arr[], int n) 
{ 
    int i, key, j; 
    for (i = 1; i < n; i++) { 
        key = arr[i]; 
        j = i - 1; 
  
        /* Move elements of arr[0..i-1], that are 
          greater than key, to one position ahead 
          of their current position */
        while (j >= 0 && arr[j] > key) { 
            arr[j + 1] = arr[j]; 
            j = j - 1; 
        } 
        arr[j + 1] = key; 
    } 
} 

```

#### Advanced Types in C 

**Pointers:** a type that contains an address to another location in memory (when dereferenced with the `*`, follows that address)


**Function Pointers:** a pointer to a function 
- they allow functions to be used in different cases (i.e. flexibility)

``` 
[return type](*function_name)(function input, another input)
``` 

**Void Pointers:** a pointer that can point to objects of any data type 

- use the keyword `void` when declaring the pointers type 
- cannot be dereferenced directly! Must be cast to another pointer type before dereferencing 
- useful in pointing to structs 

**ENUM:** a user defined data type in C 
- assigns names to integer constants (can also specify integer constants, and multiple and be the same)
- must be unique (name, number) in their scope

**Unions:** like a structure, but only has space for one possible attribute 
- allocates space for biggest possible, but can't have two! 


