# Pointer
### 1. Pointer
* The address of a variable is defined to be the lowest address in memory where the variable is stored
* We can get the address using the & operator

```C++
int foo() {
	short chickens = 5;
	short* ptr = &chickens;

	cout << chickens; // prints 5
	cout << ptr; 	  // prints 1001
	cout << &chickens;// prints 1001
	cout << &ptr;	  // prints 1004

	cout << *ptr;     // prints 5
	*ptr = 10;        // *1001 = 10
}

void set(int* pa) {
	*pa = 5;
}
int main() {
	int x = 1;
	set(&x);
	cout << x; // prints 5
}
```

* Pass by references. In fact, a ref is just a simpler notation for passing by a pointer

```C++
void set(int &val) {
	val = 5;
}

int main()
{
	int x = 1;
	set(x);
	cout << x; // print 5
}
```

* Must set the value of a pointer variable **before** using * operator

### 2. Arrays, Address and Pointers
```C++
int main() {
	int nums[3] = {10, 20, 30};
	cout << &nums;   // prints 9242
	cout << nums;    // also prints 9242	

	int *ptr = nums;
	cout << ptr[2];  // prints 30
	cout << *ptr;    // prints 10
	cout << *(ptr+2) // prints 30
}
```

* `ptr[j] == *(prt+j)`: Actually, this means skip down j bytes

### 3. Pointer Arithmetic and Arrays
* Whenever passing an array to a function, we are actually passing the **address** to the start of the array

```C++
void printData(int array[]) {
	cout << array[0];
	cout << array[1];
}

int main() {
	int nums[3] = {10, 20, 30};

	printData(nums);     // prints 10 20
	printData(&nums[1]); // prints 20 30
	printData(nums+1);   // prints 20 30
}
```
### 4. Classes and Pointers

```C++
class Circ {
public:
	Circ(float x, float y, float rad)
	: m_x(x), m_y(y), m_rad)(rad) {}
	float getArea(void)
	{ return (3.14*m_rad*m_rad); }
private:
	float m_x, m_y, m_rad;
}

void printInfo(Circ *ptr) {
	cout << "The area is: ";
	cout << ptr->getArea();
	cout << (*ptr).getArea();
}
int main() {
	Circ foo(3,4,10);
	printInfo(&foo);
}
```