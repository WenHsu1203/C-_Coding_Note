# Hash Table

* ID #s -> f(x) -> slot #s, such function f(x) is called hash function.

```C++
class HashTables
{
public:
	void addItem(int n)
	{
		int bucket = hashFunc(n);
		m_array[bucket] = true;
	}
private:
	int hashFunc (int idNum)
	{
		const int ARRAY_SIZE = 100000;
		int bucket = idNum % ARRAY_SIZE;
		return bucket;
	}
	bool m_array[100000];
};
int main()
{
	HashTables x;
	x.addItem(400683948);
	x.addItem(111105224);
	x.addItem(222205224); // <- collision happens
}
```

* Coliision: where two or more values both "hash" to the 
			   same bucket in the array.
* Solution: **Close** or **Open Hash Table**

### Closed Hash Table

* Linear Probing Insertation: putting each value as close as possible
	* If the target bucket is empty, we can store our value there. Instead of storing true in the bucket, we store our full ORIGINAL value. If the bucket is occupied, scan dow from that bucket until we hit the first open bucket.
	* Sometimes, we  need to insert an item near the end of the table. Then we need to wrap back. 

```C++
struct BUCKET
{
	int idNum;
	string name;
	float GPA;
	bool used;
};
#define NUM_BUCK = 10;
class HashTable {
public:
	void insert (int idNum, string &name; float GPA) {
		int bucket = hasFunc(idNum);
		for (int tries=0; tries<NUM_BUCK;tries++) {
			if (m_buckets[Bucket].used = false) {
				m_buckets[bucket].idNum = idNum;
				m_buckets[bucket].name = name;
				m_buckets[bucket].GPA = GPA;
				m_buckets[Bucket].used = true;
				return;
			}
			bucket = (bucket + 1) % NUM_BUCK;
		}
	}
	bool search(int idNum, string &name, float &GPA) {
		int bucket = hashFunc(idNum);
		for (int tries = 0; tries < NUM_BUCK; tries++) {
			if (m_buckets[bucket].used == false)
				return false;
			if (m_buckets[bucket].idNum == idNum) {
				name = m_buckets[bucket].name;
				GPA = m_buckets[bucket].GPA;
				return true;
			}
			bucket = (bucket+1) % NUM_BUCK;
		}
		return false;
	}
private:
	int hashFunc(int idNum) const 
		{ return idNum % NUM_BUCK; }
	BUCKET m_buckets[NUM_BUCK];
}
```

* Problem with closed hash table + linear probing:
	* Difficult to delete items
	* It has a cap on the number of items it can hold 

### Open Hash Table : 
Instead of storing our values directly in the array, each array bucket points to a linked list of values.

1. Insert
	1. As before, compute a bucket # with the hash function
	2. Add the new value to the LinkedList at array[bucket]
	3. DONE
2. Search
	1. As before, compute a bucket # with the hash function
	2. Search the linked list at array[bucket] for your item
	3. If we reach the end of the list without finding-> not found
3. delete
	* Just like delete a node as what we do before

---
* Hash Table Efficiency:
	*  The type of has table
	*  How full the hash table is
	*  How many collisions we have in the hash table
* The Load Factor(L) : Max # of values to insert / Total buckets in the array
	* Close: Average # of tries = 0,5(1+1/(1-L))
	* Open:  Average # of tries = 1+ L/2

* Tradeoff: fast or small waste of memory
	* Always try to choose a prime number of buckets.

* Hash Function for strings:

```C++
int hashFunc(string& name)
{
	int i, total = 0;
	for (i = 0; i < name.length(); i++)
		total = total + (i+1)*name[i]; // <-now TAB and BAT are different
	total = total % HASH_TABLE_SIZE;
	return total;
}
```
### Hash Functions for string: 

```C++
#include <functional>
unsigned int yourHashFunction(const std::string &hashMe)
{
	std::hash<std::string> str_hash;
	unsigned int hashValue = str_hash(hashMe);
	unsigned int bucketNum = hashValue % NUM_BUCKETS;
	return bucketNum;
}
```

* Tips for choosing a Hash Function:
	1. Must always give us the same bucket # for a given input
	2. Should disperse items throughout the hash array as randomly as possible
	3. When coming up with a new hash function, always measure how well it disperse item.

	
# The unordered_map:
```C++
#include <unordered_map>
#include <iostream>
#include <stirng>
using namespace std;
int main()
{
	unordered_map<string,int> hm;
	unordered_map<string,int> :: iterator iter; 
	hm["Carey"] = 10;
	hm["David"] = 20;
	iter = hm.find("Carey");
	if (it == hm.end())
		cout << "Carey was not found!";
	else
	{
		cout << "When we look up" << iter->first;
		cout << "We find "<<iter->second;
	}
}
```
* Hash Table vs. Binary Search Trees

|               | HashTable      | BST      |
| ------------- |:--------------:|:--------:|
| Speed         | O(1)           | O(log2N) |
| Simplicity    | Easy           | More Complex|
| Max Size      | Open: unlimited| unlimited|
| Space Efficiency| More Wasteful| Use as much as needed|
| Ordering      | No             | Ordered   |        



# Tables:
* A group of related data is called "record"
* Each record has a bunch of "fields" which can be filled in with values.
* A field that has unique values across all records is called **key field**

* Implementing Tables:

```C++
struct Student
{
	string name;
	int IDNum;
	flaot GPA;
	string phone;
	...
};
class TableOfStudents
{
public:
	TableOfStudents();
	~TableOfStudents();
	void addStudent(Student & stud);// push_back(record)
	Student getStudent(int s);      // Retriveve Students from slot s
	int SearchByName(string& name); // iterate the vecotr to search
	int SearchByPhone(int phone);
private:
	vector<Student> m_students;
	map<string,int> m_nameToSlot; //->these secondary data structures are called indexes
	map<int,int> m_idToSlot; //->these secondary data structures are called indexes
}
void TableOfStudents::addStudent(Student &stud)
{
	m_students.push_back(stud);
	// But now every time adding a record, we need to add the ID to slot
	int slot = m_students.size()-1;
	m_nameToSlot[stud.name] = slot;
	m_idToSlot[stud.name] = slot;
}
```



























