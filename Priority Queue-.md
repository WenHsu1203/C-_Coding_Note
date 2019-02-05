# Priority Queue:
A queue allowing to keep a priortized list of items. Each item has a priority rating and always dequeue an item with  highest priority.

* Operation: `Insert`, `Dequeue`, `Remove`

* The `heap` structure is one of the most efficient to implement
a priority queue! (Using CBT not BST)

### Complete Binary Tree(CBT): 
1. The top N-1 levels of the tree are completely filled with nodes. 
2. All nodes on the bottom-most level must be as far left as possible.
   
* Two Type: `minheaps` and `maxheaps`
	1. The values contained by a node is always greater(smaller)
	   than or equal to the values of the node children
	2. Must be a CBT

* Operation on a MaxHeap:
##### 1. Extracting the biggest item:

```C++
1. If the tree is empty, return error
2. Otherwise, the top item in the tree is the biggest.
3. If the heap has only one child, delete it and return the saved value
4. Copy the value from the right-most node in the bottom-most row 
   to the root node.
5. Delete the right-most node in the bottom-most row
6. Switching down to get the CBT again 
```

##### 2. Adding a node to a MaxHeap:

```C++	
1. If the tree is empty, create a new root node and return.
2. Otherwise, insert the new node in the bottom-most, left-most position of the tree
3. Compare the new value with its parents value.
4. If the new value is greater, then swap.
5. Repeat 3-4 until the new value rises to its proper place.
```

* Implementing a heap: `array`
* Formula: 

```
leftChild  = 2 * parent + 1
rightChild = 2 * parent + 2
parent = (child-1) / 2
```

##### 1.Extracting from a Maxheap(array version);

```C++
1. if count == 0; return error
2. heap[0] holds the biggest value.
3. If the count == 1, set count = and return the saved value
4. heap[0] = heap[count-1]
5. count = count-1;
6. Start i = 0, compare and swap heap[i] with heap[2*i+1] and  heap[2*i+2]
7. return the saved value to the user.
```

##### 2.Adding a node to a MaxHeap:
1. heap[count] = value; count++;
2. Compare the new value heap[i] with its parent value
3. then swap if necessary.
4. repeat step2,3 until reach the top or CBT

* Time Complexity of the Heap:
	1. Inserting: O(logN)
	2. Extracting: O(logN)














