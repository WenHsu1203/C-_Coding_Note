# Sorting
* Rule 1: Do not choose a sorting algorithm until you understand the requirement of your problem.
* Rule 2: Always choose the simplest sorting algorithm possible that meets your requirement.

### 1. Selection Sort O(n^2): 
* Always swap the smallest number to the smallest position.
* O(n^2)
* Even mostly sorted, still take as many steps as before

```C++
void selectionSort(int A[], int n) {
	for (int i = 0 ; i < n; i++) {
		int minIndex = i;
		for (int j = i+1 ; j < n; j++) {
			if (A[j] < A[minIndex])
				minIndex = i;
		}
		swap(A[i], A[minIndex]);
	}
}
```

### 2. Insertion Sort O(n^2):

* O(n^2)
* But if it is already sorted, then do not need to do anything! (perfectly mis-ordered set will be the worst)

```C++
void insertionSort(int A[], n) {
	for (int s = 2; s<=n; s++) {
		int sortMe = A[s-1];
		int i = s-2;
		while (i >= 0 && sortMe < A[i]) {
			A[i+1] = A[i];
			i--;
		}
		A[i+1] = sortMe;
	}
}
```
### 3. Bubble Sort O(n^2):
* O(n^2)
* But if it is already sorted, then do not need to do anything!

```C++
void bubbleSort(int A[], int n) {
	bool atLeastOneSwap;
	do {
		atLeastOneSwap = false;
		for (int j = 0 ; j < n-1 ; j++) {
			if (A[j] > A[j+1]) {
				swap(A[j], A[j+1]);
				atLeastOneSwap = true;
			}
		}
	} while (atLeastOneSwap == true);
}

```

## Advanced Sort:
1. Divide the elements to be sorted into two groups of roughly equal size.
2. Sort each of these smaller groups of elements.
3. Combine the two sorted groups into one large sorted list.

### 1. Quicksort O(nlog(n)):
* Algorithm:

```C++
	1. If the arrary contains only 0 or 1, return.
	2. Select an arbitrary element P from the array(typically first element)
	3. Move less than or equal to p to the left, greater to the right(called partitioning)
Recursively repeat this process on the left and then the right sub-array
```

* O(nlog2(n))
* If it is already sorted, then this wil be very slow(reverse order as well)
* Can be parallelized across multiple cores

```C++
int Partition(int A[], int low, int high) {
	// Use the first item as the pivot
	int pi = low;
	int pivot = A[pi];
	do {
		while (low <= high && A[low] <= pivot)
			low++;
		while( A[high] > pivot)
			high--
		if (low < high)
			swap(A[low], A[high]);
	} while (low < high);
	swap (A[pi], A[high]);
	// return the pivot's index
	pi = high;
	return pi;
}

void quickSort(int A[], int First, int Last) {
	if (Last - First >=1) {
		int PivotIndex;
		PivotIndex = Partition(A, First, Last);
		quickSort(A, First, PivotIndex-1);
		quickSort(A, PivotIndex+1, Last);
	}
}
```
### 2. Mergesort O(nlog(n)):
* Algorithm: 

```C++
1. If array has one element, then return.
2. Split the array in two equal sections.
3. Call Mergesort on the left half.
4. Call Mergesort on the right half.
5. Merge the two halves back together.
```

* O(nlog(n))
* Mergesort works equally regardless of the ordering of the data.
* But since it need secondary arrays to merge -> slow down a little bit

```C++
void merge(int A[], int n1, int n2) {
	int i=0, j=0, k=0;
	int *temp = new int[n1+n2];
	int *sechalf = A + n1;
	while (i < n1 || j < n2) {
		if (i == n1)
			temp[k++] = sechalf[j++];
		else if (j == n2) 
			temp[k++] = A[i++];
	else if (A[i] < sechalf[j]) 
		temp[k++] = A[i++];
	else
		temp[k++] = sechalf[j++];
	}
	for (i = 0 ; i < n1+n2; i++)
		A[i] = temp[i];
	delete [] temp;
}
```



















 
























