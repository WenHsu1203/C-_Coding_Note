# Dynamic Variables

### 1. Dynamically Allocated Array
```C++
int main()
{
	int *arr;
	int size;
	cin << size;
	arr = new int[size];
	arr[0] = 10;
	arr[2] = 75;
	delete [] arr;
}
```
The __NEW__ command requires two pieces of information:

1. What type of array you want ot allocate
2. How many slots you want in your memory

### 2. Copy Constructor
What for? To initialize a new variable from an existing variable

```C++
class Circ {
public:
	Circ(const Circ &other)
	:m_x(other.m_x),m_y(other.m_y),m_rad(other.m_rad){}
private:
	float m_x, m_y, m_rad;
}
```

* Every Circ variable is allowed to touch every other Circ private variable
* Must be ```const```, ```reference```, ```same type```
* Any time your class holds pointer member variable*, 
  **must** write your own copy constructor like below:
  
```C++
class PiNerd {
public:
	PiNerd(int n){...}
	~PiNerd(){ delete [] m_pi; }
	PiNerd(const PiNerd& other) {
		m_n = other.m_n;
		m_pi = new int[m_n];
		for (int i = 0; i < m_n; i ++)
			m_pi[i] = other.m_pi[i];
	}
private:
	int *m_pi, m_n;
}
int main()
{
	PiNerd ann(3);
	if (...)
		PiNerd ben = ann;
}
```
### 3. Assignment Operator

```C++
class PiNerd {
	PiNerd(){}
	~PiNerd(){ delete [] m_pi; }
	PiNerd &operator= (const Circ& other)
	{
			// Avoid alisain
		if (&other == this)
			return;
		delete [] m_pi;
		m_n = other.m_n;
		m_pi = new int[m_n];
		for (int i = 0; i < m_n; i ++)
			m_pi[i] = other.m_pi[i];
		return (*this);
	}
private:
	int *m_pi, m_n;
}
```
# Constructor / Destructor
### 1. Constructor
* The constructor is **not called** when you just define a pointer variable<br>
* Must always add initializer list to the actual constructor definition, when having outside definition, then put it outside

### 2. Destructor
* Local objects defined in a function are destructed when they go out of scope
* Local variables defined in a block are destructed when the block finishes
* Dynamically allocated variables are destructed when delete is called