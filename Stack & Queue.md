# Stack & Queue
### 1. Stack: 

• **LIFO** (Last In First Out)

```C++
const int SIZE = 100;
class Stack {
public:
	Stack() { m_top = 0; }
	void push(int val) {
		if (m_top >= SIZE) 
			return;
		m_stack[m_top] = val;
		// Always post-increment
		m_top ++; 
	}
	// this version of pop will erase the value also return it
	int pop() {
		if (m_top == 0)
			return -1;
		// Always pre decrement
		m_top --;
		return m_stack[m_top];
	}
private:
	int m_stack[SIZE];
	int m_top;
};

```
####• STL package syntax
```C++
#include <iostream>
#include <stack>
int main() {
	std::stack<int> istack;
	istack.push(10);
	istack.push(20);
	cout << istack.top();
	istack.pop(); // Just remove it, won't return any value
	if (stack.empty() == false)
		cout << istack.size();
}
```

### 2. Postfix Evaluation Algorithm

1. Start with the left most<br>
2. If token is a number:<br>
	a. Push it onto the stack<br>
3. Else if the token is an operator:<br>
	a. Pop the top value into v2, and pop the second-to-top value into v1<br>
	b. Apply operator to v1 and v2 (e.g., v1/v2)<br>
	c. Push the result on the stack<br>
4. If there are more tokens, advance to the next token and go back to #2
5. After all tokens have been processed, the top # will be the answer

### 3. Queue:
* **FIFO** (First In First Out)

```C++
#include <iostream>
#include <queue>
int main() {
	std::queue<int> iqueue;
	iqueue.push(10); 		// add item to the rear
	iqueue.push(20);
	cout << iqueue.front(); // view front item
	iqueue.pop(); 			// discard front item
	if(iqueue.empty() == false)
		cout << iqueue.size();
}
```
* If using an array and an integer to represent queue, inserting or dequeuing an item will be annoying. So, using **LinkedList** to represent the 
