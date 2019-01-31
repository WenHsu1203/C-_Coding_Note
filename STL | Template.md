# Generic Programming

### 1. Custom Comparison Operators:

* **CASE: Outside of the class**
	* Must retrun `bool` value
	* Only accept `const` **reference**
	* Not necessarily be `const` function, but **only** use `public` method
	* Since input are all `const`, we can only call `const` function
	 
```C++
bool operator>= (const Dog &a, const Dog &b) {
	// getWeight() must be const
	if (a.getweight() >= b.getweight())
		return true;
	return false;
}
```

* **CASE: Inside of the class**

```C++
class Dog {
public:
	bool operator< (const Dog &other) const {
		if (m_weight < other.m_weight)
			return true;
		return false;
	}
private:
	int m_weight;
};
```


### 2. Template feature:
* **ALWAYS** place your **ENTIRE** templated fuctions in **HEADER FILE.** Then include .h and use the function.
* Define at least ONE formal parameter using template data
* C++ always choose the specialized version of a function,
not template one

```C++
template <typename Item> || template <class Item> 
void swap(Item &a, Item &b) {
	Item temp;
	temp = a;
	a = b;
	b = temp;
}
```

* If the template function uses a **comparison operator**, we must define a comparison operator if the default one does not work!
* We can have multiple typename:

```C++
template<typename Type1, typename Type2>
void foo(Type1 a, Type2 b) {
	Type1 temp;
	Type2 array[20];
	temp = a;
	array[3] = b;
	...
}
```

### 3. Generic Classes:

```C++
template <typename Item>
class HoldOneValue {
public:
	void setValue(Item a){ m_a = a; }
	void printTenTimes() {
	   // but not every int should be replaced by Item!!
		for (int i = 0; i < 10; i ++)
			cout << m_a;
	}
private:
	Item m_a;
};
```

* Now we can use the template fumction to hold any type of data

```C++
int main() {
	HoldOneValue<int> v1;
	HoldOneValue<string> v2;
}
```

* Externally-defined member function will be very ugly...
	1. Add prefix before class and function def outside the class
	2. Update the data type 
	3. place <XXX> between class name and ::

```C++
template <typename Item>
class Foo {
public:
	void setVal(Item a);
	void printVal();
private:
	Item m_a;
};

template <typename Item>
void Foo <Item>:: setVal(Item a) {
	m_a = a;
}

template <typename Item>
void Foo<Item>::printVal() {
	cout << m_a <<"\n";
}
```

### 4. Standard Template Library

#### 1. `Vector` (Dynamically Allocate Array)

```C++
#include <vector>
using namespace std;  <- or std::vector
int main() {
	// create 444 444
	vector<double> nums(2, 444);
	vector<Robot> robots;

	vector<int> geeks(3);
	geeks.push_back(1);
	geeks.push_back(2);
		 Now nums have 0 0 0 1 2
	geeks[0] = 42;
		 Now nums have 42 0 0 1 2
	cout << geeks[7]  <- CRASH
	cout << geeks.front();
	cout << geeks.back();
	geeks.popback();  remove from the back
	cout << geeks.size();  Only for vector, not array!
	assert(!geeks.empty());
	return 0;
}
```
#### 2. `list`
* Like vector, list has `push_back`, `pop_back`, `front`, `back`, `size`, `empty`
* EXTRA: `push_front`, `pop_front` 
* **BUT CANNOT access using BRACKET!**

```C++
#include <list>
using namespace std;

int main() {
	list<float> lf;
	lf.push_back(1.1);
	lf.push_front(2.2);
	lf.pop_front(2.2);
}
```
* **Only `vector` can access element through []. Other STL need iterator variable!** (only for STL ALSO)

```C++
int main() {
	vector<int > nums;
	nums.push_back(1234);
	nums.push_back(5);
	nums.push_back(7);
	// use this syntax to declare a iterator
	vector<int>:: iterator it;
	// to point the first item, use begin()
	it = nums.begin(); // it's just a pointer
	cout << (*it);
	it ++; it --;  // now we can access any element
	// to point the last item, use end()
	// BUT!!! It points JUST PAST the last item
	it = nums.end();
	it--; cout << (*it);
	// WHY????? Cause it's easy to loop
	it = nums.begin();
	while (it!= nums.end) 	
		cout << (*it); it++;
}
```

* Actually, it's just like ptr, so we can use `it->functionName()` or `(*it).functionName()`
* But it's **not a pointer**

* If Passing a container as a `const` reference parameter, **regular iterator** **does not work!!** => Using `const iterator` to fix it!

```C++
void tickleNerds(const list<string> & nerds) {
	list<string>::const_iterator it;  // IMPORTANT
	for (it = nerds.begin(); it!= nerds.end() ; it++)
		cout << *it << "say fuck!!!!\n";
}
```
#### 3. `map`
```C++
#include <map>
#include <string>
using namespace std;

int main() {
	map<string, int> name2phone;
	name2phone["Joe"] = 12353;
	name2phone["Wen"] = 12354;
	// Modify
	name2phone["Wen"] = 11111;
	// Iterator
	map<string, int>::iterator it;
	// using "find" to get the element by the key
	// if nothing found, then it points to the end()
	it = name2phone.find("Wen");
	cout << it->first; // print the key
	cout << it->second; // print the second element
	map<string, int>::iterator it;
	for (it = name2phone.begin(); it != name2phone.end(); it++)
		cout << it->first; cout << it->second;
	   // the map ALWAYS maintains items in alphabetically order!
}
```

* `map` is capable of containing structs and classes, but, first we must define `opertaor <` to make sure we can sort it

```C++
struct stud {
	string name;
	int idNum;
};
```

* We must define this since map<class,...>

```C++
bool operator<(const stud& a, const stud& a) {
	return(a.name < b.name);
}
int main() {
	map<stud,float> stud2GPA;
	stud d;
	d.name = "David Smallberg";
	d.idNum = 9128;
	stud2GPA[d] = 1.3;
}
```

* If the case: `map<float, stud>`, then we don't need to define `operator <` first.


#### 4. `set`

```C++
#include <set>
using namespace std;
struct Course {
	string name;
	int unit;
};
```
* Must define `operator<`

```C++
bool operator<(const Course &a, const Course &b) {
	return (a.name < b.name);
}

int main() {
	set<int> a;
	a.insert(2);
	a.insert(3);
	a.insert(4);
	a.insert(2);  // This will be ignored since set has it already

	cout << a.size();
	a.erase(2);

	set<Course> myClasses; // BUT MUST define operator < first!
	Course lec1;
	lec1.name = "CS32";
	lec1.unit = 16;
	myClasses.insert(lec1); 
	it = a.find(2); // Like map, or using iterate, and aphalbatically order
}
```

* Most STL containers have earse()
* After adding or erasing, all old iterators that were assigned before
* are **invalidated!**, but this problem does not occur with `set`, `list`, `map` (unless delete what it points to...)

#### 5. Sort Function:
Works on `array` and `vector` and it sorts in ascending order.

```C++
#include <vector>
#include <algorithm>

int main() {
	vector<int> nums;
	nums.push_back(1234);
	nums.push_back(5);
	nums.push_back(7);
	// pass in two iterators
	// WARNING!!
	// end() will give the next element of the last one
	// but the below will sort from begin() to end()-1
	sort(nums.begin(), nums.end());
	// case ARRAY
	int arr[4] = {2,5,1,-7};
	sort(&arr[0], &arr[4]);
}
```

#### 6. Inline:
* All the functions in the class are `inline` by default but **externally-defined method** must add `inline` before function return type.
	 
``` C++
template <typename Item>
inline // <- HERE
void Foo<Item>::setVal(Item a) {
	m_a = a;
}
```

* Inline speed up the program, but increase the size of exe. file

#### 7. find function:
* STL provides a `find` function for the `vector`/`list` make sure `#include <algorithm>`
* It works for the `array` too!

```C++
#include <list>
#include <algorithm>

int main() {
	list<string> names;
	list<string>::iterator a,b,itr;
	a = names.begin();
	b = names.end();
	// second element point JUST AFTER where you want to search
	itr = find(a, b, "Wen");
	if (itr == b)
		cout << "fail";
}
```

#### 8. find_if function:
* Process until predict function return true or run out of the elements
* Predict function must return a `boolean`
* Predict function must accept value type of container/array

```C++
find_if(&a[0], &a[4], is_even); // <- is_even is predict function
```
