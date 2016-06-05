# Interview-prep

Best source -> https://github.com/bsikander/getting-a-gig

# Array
- Data structure to hold any type of data.
- Size of array is fixed (precomputed) and must be provide at creation time.

  **Advantages**
  - Random access i.e. myArray[index]
  - Contiguous memory allocation.
    - Binary Search can be applied for searching if array is sorted.

  **Disadvantages**
  - Not dynamically expandable due to fixed size.
  - Insertion/Deletion is slow as other values have to be relocated i.e. O(n)
    - Example: Consider keeping an array sorted and add unsorted entries.

## Resizable Array
- Can be dynamically resized.
  - Typically resizes it self when full.
- The Resizing Factor determines the next size. i.e. new size = current size * resizing factor
  - Typical resizing factor is 2.
- Resizing takes O(n). i.e. making a new array with resizing factor, copy all objects from previous array to new.
- Resizing happens rarely so the Amortized runtime is still O(1).
- Total number of copied elements can be determined by backtracking K/2 in a backwards loop.
  - Total number of copied elements will always be less than N.

## Strings
- String is essentially an immutable (fixed size) array of characters.
- It can be read character by character.
- Typically, String concatenation is done by originalString += anotherString.
  - As String is immutable, this will create a new String (of size originalString+anotherString) and copy both strings into it.
  - The runtime of this process is O(n). Which becomes O(n<sup>2</sup>) if a collection of strings (e.g. words) is required to be concatenated into a single string (e.g. sentence).
- To avoid the overhead of creating a new string with every concatenation, StringBuilder (in Java, or similar in other languages) can be used.
```java
String []words = new String[]{"This", " is", " an", " example", " of", " string", " concatenation", " in", " Java."};
StringBuilder sentenceBuilder = new StringBuilder();
for(String word: words){
  sentenceBuilder.append(nextWord);
}
String sentence = sentenceBuilder.toString();
```

# Linked List:
- Data structure to hold data of any type and size.
- Types:
  - Linear (Singly linked-list, Single pointer that points to next element).
  - Circular (Last node pointer points to head in a singly linked-list).
  - Doubly linked-list (Each node has two pointers, one for next and previous node respectively).
  - Doubly circular (Last node points to Head).
- Provides sequential access to each element.
- No size limitation.

  **Advantages:**
  - Insertion in O(1) (at Head or Tail).
  > Insertion consists of two functions Find + insert. Insert is always O(1) but find always makes the difference. If we have the pointer then find is O(1) otherwise find will be O(n) which makes the overall time of insert to be O(n). <-- [Good implementations will  always keep the pointer to the last node](http://stackoverflow.com/questions/1933085/linked-list-insertion-running-time-confusion)
  - Access is O(n).
  - Better memory management as unwanted elements can be deleted and memory is reclaimed.

  **Disadvantages**
  - Memory waste for extra pointers.
  - The memory is not contiguous, so Binary search cannot be applied.

## The 'Runner' pointer
- An extra pointer used to traverse linked-list, normally moves faster, to solve different problems.
  - Find a mid point of the linked-list.
  - Determine, whether there is a loop in the linked-list.

## Java specific Implementation
- LinkedList<E>, doubly linked-list implemented with 'List' & 'Dequeue' interface.
- Not thread safe.
- Index based operations are traversed from Head or Tail pointers (Which ever is the closest).
- Can be made synchronized by creating the linked-list via 'Collection.synchronizeList(new LinkedList(...))'.
- Fail-fast
  - Fail-fast is the behavior of the iterator to throw an exception is a structural change has been made to the list.

# Concepts:
- **Constant Time**:
"Constant time" has the same meaning as "O(1)", which doesn't mean that an algorithm runs in a fixed amount of time,
it just means that it isn't proportional to the length/size/magnitude of the input. i.e., for any input, it can be computed
in the same amount of time (even if that amount of time is really long).

[Linear + Constant Time]([https://www.quora.com/Difference-between-linear-time-and-constant-time-in-Data-structure)


## HashTable/HashMap
- Hashing used for storing and retrieving information as fast as possible.
- Array can be used as hashtable if our set of possible options is limited. Direct addressing can be used to access elements.
- The process of mapping the keys to a location is called hashing
- One simple hash function can be (key % hash table size)
- Components of hashing are Hash Table, Hash Function, Collisions, Collision Resolution Techniques

##### Hash Table
- Hash table is generalization of array.
- Used when we have less locations and more possible keys. So, use hashtable when the keys stored is small relative to the number of possible keys.

##### Hash Function
- Minimize Collision
-
http://www.cs.rmit.edu.au/online/blackboard/chapter/05/documents/contribute/chapter/05/linear-probing.html

## Queue
- is based on the concept of FIFO (First in first out)
- Overflow: Adding an element to the full queue
- Underflow: Remove an element from empty queue
- Bounded queue: Queue with limited number of elements.

##### Functions
 - Enqueue (Adding element to the rear end)
 - Dequeue (Removing element from the start)
 - Peek (Get the 1st element without dequeuing)

##### Implementation
Implementation can be done with two data structures:
- Best choice: Doubly-linked list (It has O(1))
- Other choice: Singly-linked list (If we keep track of last pointer along with first one)
- In ruby, we use push (<< operator) & shift() functions with array. Shift function is used to dequeue an element from the start of array.

## Heap
Heap is good at basic ordering & keeping track of max and mins.
- It is tree based data structure
- Two types:
 - Max heap (Max element is the root. Parent nodes are greater than or equal to children)
 - Min heap (Min element is the root. Parent nodes are less than or equal to children)
- Partially ordered (Meaning root is greater than children but there is no relationship between chidrens)
- Binary heap: It is the heap with complete binary tree (i.e. max two children of a node). With N nodes, the height will be log N
- Heap is Useful when need to remove the object with heighest or lowest priority.

##### Functions
- find-max or find-min
- insert
- extract-max or extract-min
- delete-max or delete-min
- replace: pop-root and push new key
- Internal functions used to complete the above mentioned operations include:
 - delete node
 - Shift-up
 - Shift-down

The shift-up and shift-down operations are used to restore the heap condition after deletion or insertion.

##### Implementation
- Normally the heap is implemented with Array.
- In binary heap, the nth node will have children at 2n and 2n + 1 index for the array starting from index 1. The parent will be located at n/2.
- [Binary heap](https://www.cs.cmu.edu/~adamchik/15-121/lectures/Binary%20Heaps/heaps.html)
- Insertion function
 - New element is appended at the end of the array
 - Compare added element with parent and replace until the root or the heap condition of max or min is satisfied
 - Worst case run time complexity is O(log n)
- Deletion function
 - Since minimum element is at root, so delete it
 - Replace root with the last elemnt of array
 - Restore heap property of max or min
 - Worst case run time O(log n)
- Find function
 - Its complexity is O(1)

## Priority Queue
- It is implemented with heap
- Each element in the queue has a priority
- Element with high priority is served before the element with low priority or vice versa depending on the heap type
- Elements with same priority are returned according to their order in queue

##### Implementation
It can be implemented with following data structures:
- Unordered list
 - Insertion is in O(1) as the element is added at the end of the array
 - Pull or getElement has a worst case complexity of O(n) because the complete array need to be traversed to find the element
- Using heap
 - Insertion/deletion has a worst case complexity of O(log n)
