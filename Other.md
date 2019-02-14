# Corner Case
#### BFS

``` C++ 
while (!queue.empty()) {}
```

#### DFS/BT/BST
```C++
if (root == nullptr) { return nullptr; }
if (treeNode != nullptr) { continue; }
```

#### Linked List
```C++
if (head == nullptr) { return nullptr; }
if (head->next == nullptr) { return nullptr; }
```

# Math
```C++
#include <math.h> 

cout << INT_MIN;  // -2^31 = -2147483648
cout << INT_MAX;  // 2^31-1 = 2147483647
cout << 5/2;      // 2
cout << abs(-5);  // 5
float x = 4.9;
cout << int(x);   // 4
cout << round(x); // 5 
cout << ceil(x); // 5 
cout << floor(x); // 4
 
cout << pow(2,3); // 8
int y = 4;
cout << float(y); // 4

```
# Random Number
```C++
#include <stdio.h>    // printf()
#include <stdlib.h>   // rand()
#include<time.h>      // time()

srand(time(0));
printf(" %d ", rand());

```

# Pair
* pair (data_type1, data_type2) Pair_name (val1, val2);

```C++
include<utility>
include<vector>
using namespace std;
int main() {
	vector<pair<int,int>> vec;
	pair <int, int> p1 (3,4);
  	pair <int, int> p2 (5,6);  	
  	pair <int, int> p3 (p1); // copy
  	pair <int, int> p4;
  	p4 = make_pair(10,12);
  	cout << p2.first; // 5
	cout << p2.second; // 6
  	vec.push_back(p1);
  	vec.push_back(p2);
  	vec.push_back({11,12}); // valid!
  	auto it = find(vec.begin(), vec.end(), p3);
  	if it != vec.end()) {
	   cout << "found!" << endl; // found
	   cout << it->first;  // 3
	   cout << it->second;	// 4
   }
}
```

# Binary Search
```C++
int bsearch(int arr[], target) {
	int start = 0;
	int end = arr.size()-1;
	while (start <= end) {
		int mid = start + (end-start)/2;
		if (arr[mid] == target)
			return mid;
		if (arr[mid] < target)
			start = mid + 1;
		else
			end = mid - 1;
	}
	return -1;
}
```

# BFS
#### Tree
```C++
#include <iostream>
#include <queue>
using namesapce std;

void bfs(TreeNode* root) {
	queue<TreeNode*> q;
	q.push(root);
	while(!q.empty()) {
		TreeNode* temp = q.front();
		q.pop();
		cout << temp->val;
		if (q->left)
			q.push(q->left);
		if (q->right)
			q.push(q->right);
	}
}
```
#### Grid / Matrix
```C++
#include <iostream>
#include <utility>
#include <queue>
using namespace std;

// TODO
```

# Dynamic Programming

* Solve **MATH** problem first 
	* Step 1: (LHS) State Definition, from last state
	* Step 2: (RHS) Transition Function
	* Step 3: (IF)  Edge Case, initial
	* Step 4: (FOR) Compute Order
* Be careful about dp table and original list













