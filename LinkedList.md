# LinkedList

### Reverse
```C++
void reverse(Node* head) {
	Node* cur = head;
	Node* prev = nullptr;
	Node* next = nullptr;
	while(cur != nullptr) {
		next = cur->next;
		cur->next = prev;
		prev = cur;
		cur = next;
	}
	head = prev;
}
```
### Slow-Fast
```C++
// to find the middle of the list
slow = head;
fast = head;
while (fast && fast->next) {
	slow = losw->next;
	fast = fast->next->next;
}

```
### Structure
```C++
struct Node {
	int val;
	Node* next;
	Node (int val):val(val){}
};
• Delete doesnt kill the pointer, it kills what pointer points to
class LinkedList {
public: 
	LinkedList();
	void addToFront(int);
	void addToRear(int);
	void addItem(int);
	void deleteItem(int);
	bool findItem(int);
	void printItem();
	~LinkedList();
private: 
	Node* head;
}
```
### Constructor
```C++
LinkedList::LinkedList() {
	head = nullptr;
}
```
### Iterate LinkedList
```C++
LinkedList::printItem() {
	Node* p = head;
	while(p != nullptr) {
		cout << p->val;
		p = p->next;
	}
}
```
### Add Node
```C++
LinkedList::addToFront(int v) {
	Node* p = new Node;
	p -> val = v;
	p -> next = head;
	head = p;
}
LinkedList::addToRear(int v) {
	if (head == nullptr)
		addToFront(v);
	Node* p = head;
	while(p->next != nullptr)
		p = p->next;
	Node* newNode = new Node;
	newNode -> val = v;
	p ->next = newNode;
	newNode->next = nullptr;
}
void LinkedList::addItem(int v) {
	if (head == nullptr)
		addToFront(v);
	else if (v < head->val)
		addToFront(v);
	else {
		Node* p = head;
		while(p->next!=nullptr) {
			if (p->next->val >= v && p->val <= v)
				break;
			p = p->next;
		}
		Node* latest = new Node;
		latest-> val = v;
		latest->next = p->next;
		p->next = latest;
	}
}
```
### Delete Node
```C++
void LinkedList::deleteItem(int v)
{
	if (head == nullptr)
		return;
	if (head->val == v) {
		Node *killMe = head;
		head = killMe ->next;
		delete killMe;
		return;
	}
	Node* p = head;
	while(p != nullptr) {
		if (p->next != nullptr && p->next->val == v)
			break;
		p = p->next;
	}
	if (p != nullptr) {
		Node* killMe = p->next;
		p->next = killMe->next;
		delete killMe;
	}
}
```
### Find Node
```C++
bool LinkedList::findItem(int v){
	if (head->val == v)
		return true;
	Node* p = head;
	while(p != nullptr) {
		if (p->val == v)
			return true;
		p = p->next;
	}
	return false;
}
```
### Destructor
```C++
LinkedList::~LinkedList() {
	Node* p = head;
	while(p != nullptr) {
		Node* n = p->next;
		delete p;
		p = n;
	}
}
```