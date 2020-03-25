## What is data structure?

Data structure availability may vary by programming languages. Commonly available data structures are: list, arrays, stack, queues, graph, tree etc.

## What is a graph?

A graph is a pictorial representation of a set of objects where some pairs of objects are connected by links. The interconnected objects are represented by points termed as vertices, and the links that connect the vertices are called edges.

## What is linear searching?

Linear search or sequential search is a method for finding a target value within a list. It sequentially checks each element of the list for the target value until a match is found or until all the elements have been searched. Linear search runs in at worst linear time and makes at most n comparisons, where n is the length of the list.

- Worst-case performance: O(n)
- Best-case performance: O(1)
- Average performance: O(n)
- Worst-case space complexity: O(1) iterative

In theory other search algorithms may be faster than linear search (for instance binary search), in practice even on medium-sized arrays (around 100 items or less) it might be infeasible to use anything else.

## What is algorithm?

Algorithm is a step by step procedure, which defines a set of instructions to be executed in certain order to get the desired output.

## What is linear data structure and what are common operations to perform on it?

A linear data-structure has sequentially arranged data items. The next item can be located in the next memory address. It is stored and accessed in a sequential manner. `Array` and `List` are example of linear data structure.

The following operations are commonly performed on any data structure:

- Insertion: adding a data item
- Deletion: removing a data item
- Traversal: accessing and/or printing all data items
- Searching: finding a particular data item
- Sorting: arranging data items in a pre-defined sequence

## What is an average case complexity of Bubble Sort?

Bubble sort, sometimes referred to as sinking sort, is a simple sorting algorithm that repeatedly steps through the list to be sorted, compares each pair of adjacent items and swaps them if they are in the wrong order. The pass through the list is repeated until no swaps are needed, which indicates that the list is sorted.

Bubble sort has a worst-case and average complexity of О(n2), where n is the number of items being sorted. Most practical sorting algorithms have substantially better worst-case or average complexity, often O(n log n). Therefore, bubble sort is not a practical sorting algorithm.

## Why do we use stacks?

In data-structure, stack is an Abstract Data Type (ADT) used to store and retrieve values in Last In First Out (LIFO) method.

Stacks follows LIFO method and addition and retrieval of a data item takes only Ο(n) time. Stacks are used where we need to access data in the reverse order or their arrival. Stacks are used commonly in recursive function calls, expression parsing, depth first traversal of graphs etc.

The below operations can be performed on a stack:

- push() − adds an item to stack
- pop() − removes the top stack item
- peek() − gives value of top item without removing it
- isempty() − checks if stack is empty
- isfull() − checks if stack is full

## Why do we use queues?

Queue is an abstract data structure (ADS), somewhat similar to stack. In contrast to stack, queue is opened at both end. One end is always used to insert data (enqueue) and the other is used to remove data (dequeue). Queue follows First-In-First-Out (FIFO) methodology, i.e., the data item stored first will be accessed first.

As queues follows FIFO method, they are used when we need to work on data-items in exact sequence of their arrival. Every operating system maintains queues of various processes. Priority queues and breadth first traversal of graphs are some examples of queues.

The below operations can be performed on a queue:

- enqueue() − adds an item to rear of the queue
- dequeue() − removes the item from front of the queue
- peek() − gives value of front item without removing it
- isempty() − checks if stack is empty
- isfull() − checks if stack is full

## What is Selection Sort?

Selection sort is in-place sorting technique. It divides the data set into two sub-lists: sorted and unsorted. Then it selects the minimum element from unsorted sub-list and places it into the sorted list. This iterates unless all the elements from unsorted sub-list are consumed into sorted sub-list.

## Why we need to do algorithm analysis?

A problem can be solved in more than one ways. So, many solution algorithms can be derived for a given problem. We analyze available algorithms to find and implement the best suitable algorithm.

An algorithm are generally analyzed on two factors − time and space. That is, how much execution time and how much extra space required by the algorithm.

## What is the difference between Linear Search and Binary Search?

A linear search looks down a list, one item at a time, without jumping. In complexity terms this is an O(n) search - the time taken to search the list gets bigger at the same rate as the list does.

A binary search is when you start with the middle of a sorted list, and see whether that's greater than or less than the value you're looking for, which determines whether the value is in the first or second half of the list. Jump to the half way through the sublist, and compare again etc. In complexity terms this is an O(log n) search - the number of search operations grows more slowly than the list does, because you're halving the "search space" with each operation.

Comparing the two:

- Binary search requires the input data to be sorted; linear search doesn't
- Binary search requires an ordering comparison; linear search only requires equality comparisons
- Binary search has complexity O(log n); linear search has complexity O(n)
- Binary search requires random access to the data; linear search only requires sequential access (this can be very important - it means a linear search can stream data of arbitrary size)

## Name some approaches to develop algorithms

There are three commonly used approaches to develop algorithms:

- Greedy Approach: finding solution by choosing next best option
- Divide and Conquer: diving the problem to a minimum possible sub-problem and solving them independently
- Dynamic Programming: diving the problem to a minimum possible sub-problem and solving them combinedly

## What examples of greedy algorithms do you know?

- Travelling Salesman Problem
- Prim's Minimal Spanning Tree Algorithm
- Kruskal's Minimal Spanning Tree Algorithm
- Dijkstra's Minimal Spanning Tree Algorithm
- Graph - Map Coloring
- Graph - Vertex Cover
- Knapsack Problem
- Job Scheduling Problem

## What are some examples of divide and conquer algorithms?

- Merge Sort
- Quick Sort
- Binary Search
- Strassen's Matrix Multiplication
- Closest pair (points)

## What are some examples of dynamic programming algorithms?

- Fibonacci number series
- Knapsack problem
- Tower of Hanoi
- All pair shortest path by Floyd-Warshall
- Shortest path by Dijkstra
- Project scheduling

## Why is Insertion sort better than Quick sort for small list of elements?

Insertion Sort is faster for small n because Quick Sort has extra overhead from the recursive function calls. Insertion sort is also more stable than Quick sort and requires less memory.

## Tell me something about Insertion sort?

Insertion sort divides the list into two sub-list, sorted and unsorted. It takes one element at time and finds it appropriate location in sorted sub-list and insert there. The output after insertion is a sorted sub-list. It iteratively works on all the elements of unsorted sub-list and inserts them to sorted sub-list in order.

Consider:

```
5, 9, 13, 4, 1, 6 // the only sorted part is the first item
5, 9, 13, 4, 1, 6 // 9 > 5 so we don't move it
5, 9, 13, 4, 1, 6 // 13 > 9 we don't move it
4, 5, 9, 13, 1, 6 // compare all to 4, until we reach the head
1, 4, 5, 9, 13, 6 // compare all to 1, until we reach the head
1, 4, 5, 6, 9, 13 // first smaller item is 5, place 6 before it
```

And code:

```js
function insertionSort(items) {
  for (var i = 0; i < items.length; i++) {
    let value = items[i];
    // store the current item value so it can be placed right
    for (var j = i - 1; j > -1 && items[j] > value; j--) {
      // loop through the items in the sorted array (the items from the current to the beginning)
      // copy each item to the next one
      items[j + 1] = items[j];
    }
    // the last item we've reached should now hold the value of the currently sorted item
    items[j + 1] = value;
  }

  return list;
}

const list = [54, 26, 93, 17, 77, 31, 44, 55, 20];
console.log(insertionSort(list)); // [ 17, 20, 26, 31, 44, 54, 55, 77, 93 ]
```
