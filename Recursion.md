# Recursion
### 1. Merge Sort
```C++
void MergeSort(an array) {
	if (sizeOfArray ==1)
		return;
	MergeSort(first half of array);
	MergeSort(second half of array);
	Merge(the two array halves);
}
```

* Rule 1: Every recursive function must have a **Stopping condition!** aka Base Case. Must be able to solve the most basic problem without using recursion.

* Rule 2. Every recursive function must have a **simplifying step**. Must
pass in a smaller sub-problem that ensures the algorithm will evetually reach its stopping condition.

```C++
void eatCandy(int layer)
{
	if (layer == 0) { // <- Stopping condition
		cout << "Eat Center!":
		return;
	}
	cout << "Lick layer "<< layer;
	eatCandy(layer -1); // <- Simplifying step
}
```

* Rule 2.5: Recursive function should **never use** `GLOBAL, STATIC, MEMBER variables`

### 6 steps:
1. Write the function header
2. Define your magic function
3. Add the base case code
4. Solve the function with the magic function
5. Remove the magic
6. Validate the function

```C++
int fact(int n) {
	if (n == 0)
		return 1;
	return n * fact(n-1);
}

int sumArr(int arr[], int n) { // we can write *arr, it's same
	if (n == 0)
		return;
	if (n == 1)
		return arr[0];
	return (arr[n-1]+ sumArr(arr, n-1));
}

int main() {
	const int n = 5;
	int arrn[n] = {10, 100, 42, 72, 16}, s;
	s = sumArr(arr, n-1);   // first n-1
	s = sumArr(arr+1, n-1); // last n-1
	s = sumArr(arr, n/2);   // Sum 1st half
	s = sumArr(arr+n/2, n - n/2);   // Sum 2st half
}
```

```C++
int biggest(Node* cur) {
	if (cur->next == nullptr)
		return cur->val;
	int x = biggest(cut->next);
	if (cur->val >= x)
		return cur->val;
	else
		return x;
}
```
### CRITICAL HINT
* Recursive function should **only access the current** node/array cell passed into it. 

```C++
int recursiveBad(Node *p) {
	...
	if (p->next->value == someValue) {} // really bad
	if (p->next->next == nullptr) {}    // really bad

}
```
