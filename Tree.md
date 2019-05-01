# Tree
	
#### 1. Pre-order Traversal:

```C++
void PreOrder(Node* cur)
{
	if (cur == NULL)
		return;
	cout << cur->val;
	PreOrder(cur->left);
	PreOrder(cur->right);
}
```
#### 2. In-order Traversal

```C++
void InOrder(Node* cur)
{
	if (cur == NULL)
		return;
	InOrder(cur->left);
	cout << cur-> val;
	InOrder(cur->right);
}
```
#### 3. Post-order Traversal
```C++
void InOrder(Node* cur)
{
	if (cur == NULL)
		return;
	InOrder(cur->left);
	InOrder(cur->right);
	cout << cur-> val;
}
```
#### 4. Level Order Traversal

```C++
1. Use a temp pointer variable and a queue of node pointers
2. Insert the root node pointer into the queue
3. while the queue is not empty:
	A. Dequeue the top node pointer and put it in temp
	B. Process the node
	C. Add the nodes children to queue if they are not NULL
```
*  ALl the big-O for each of traversal is O(n)

Expression Evaluation:

	1. If the current node is a number, return its value
	2. Recursively evaluate the left subtree and get the result
	3. Recursively evaluate the right subtree and get the result
	4. Apply the operator in the current node to the left and right results;
	   return the result.
	   
### Binary Search Trees:
```C++
struct TreeNode {
	Node(const int &myVal)
	{
		val = myVal;
		left = right = NULL;
	}
	int val;
	Node *left, *right;
}
```
#### 1. Searching a BST: Output true or false
* Algorithm:

```C++
Start at the root of the tree;
Keep going until hitting he NULL ptr.
	if V == the current node value, return true
	if V is less than current node value, go left
	if V is greater than current node value, go right
if hitting a NULL, not found
```
* Code:

```C++
bool Search(int V, Node* ptr) {
	if (ptr == NULL)
		return false;
	else if (v == ptr->value)
		return true;
	else if(V< ptr->value)
		return(Search(V,ptr->left));
	else
		return(Search(V,ptr->right));
}	
```
#### 2. Inserting a new value into a BST

* Algorithm

```C++
If the tree is empty:
	Allcote a new node and put V into it
	Point the root pointer to our new node.DONE!
Start at the root of the tree.
While we are not DONE
	if V is equal to current node value, DONE
	if V is less than current node value
		if there is a left child, then go left
		else allocate a new node and put V into it
			set current node left pointer to new node DONE
	if V is greater than current node value
		if there is a right child, then go right
		else allocate a new node and put V into it
			set current node right pointer to new node, DONE
```

* Code:

``` C++
void insert(const int& val, TreeNode* root) {
	if (root == NULL)
		{ root = new TreeNode(val); return; }
	TreeNode* cur = root;
	while(true) {
		if (val == cur->val) return;
		if (val < cur->val)
		{
			if (cur->left != nullptr)
				cur = cur->left;
		}
		else {
			cur->left = new TreeNode(val);
			return;
		}
		else if(val > cur->val) {
			if (cur->right != nullptr)
				cur = cur->right;
			else {
				cur->right = new TreeNode(val);
				return;
			}
		}	
	}
}
```

* Big O of inserting: O(log2(n))

#### 3. `GetMin` and `GetMax`: 
```C++	
int GetMin(TreeNode* root) {
	if (root == NULL)
		return -1;
	while(root->left != NULL)
		root = root->left;
	return(root->value);
}
int GetMax(Treenode* root) {
	if(root == NULL)
		return -1;
	while (root->right != NULL)
		root = root->right;
	return(root->value);
}
```

#### 4. Printing a BST in alphabetically order

```C++
void InOrder(TreeNode* root) {
	if (root == NULL)
		return;
	InOrder(root->left);
	cout << root->value;
	InOrder(root->right);
}
```
* Big O of printing: O(n)

#### 5. Delete the whole tree:
```C++
void FreeTree(Node* root) {
	if (root == NULL)
		return;
	FreeTree(root->left);
	FreeTree(root->right);
	delete cur;
}
```
#### 6. Delete a Node from a BST
* Algorithm:

```C++
Given a value ot delete from the tree:
Step 1: Searching for V
	1. parent = NULL;
	2. cur = root;
	3. while(cur!=NULL)
			if (v == cur->value) DONE
			if (v < cur->value) 
				parent = cur;
				cur = cur->left
			else if(V>cur->value)
				parent = cur;
				cur = cur->right;
Step 2: 3 cases(leaf, one child || two children)
case 1: leaf
	if target node is not the root node
		1. Unlink the parent node from the target node 
		   by setting the parent approprate link to NULL
		2. delete the target(cur) node
	if target node is the root node
		1. set the root pointer to NULL
		2. delete the target(cur) node
case 2: one child
	if target node is not the root node
		1. Relink the parent node to the target node only
		   child.
		2. delete the target(cur) node
	if target node is the root node
		1. Relink the root pointer to the target node only
	       child.
	   2. delete the target(cur) node
case 3: two children
	TRICKY: Replaceing the target node with 
	1. left subtree largest value
	2. right subtree smallest value
```
























