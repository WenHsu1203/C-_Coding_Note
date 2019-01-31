# Inheritance

1. Reuse

* Only **public members** in the base class are exposed/ reused in the derived class
* **Private members** in the base class are hidden from the derived class
* If you want the **derived class** to use the **private** member function => make them `protected`

```C++
class Robot {
public:
	Robot();
	int getX() const;
protected:
	void chargeBattery();
private:
	int m_x, m_y;
};
class ShieldRobot : public Robot
{
public: 
	ShieldRobot() {
		m_shield = 1;
		chargeBattery(); // WORK!
	}
	void set_shield();
private:
	int m_shield;
};
itn main() {
	ShieldRobot stan;
	stan.chargeBattery(); // <- FAIL!!!!
}
```
### 2. Extension
* Base class knows **nothing** about classes derived from it.

### 3. Specialization
```C++
class Student {
public:
	virtual void WhatDoISay();
};
void Student::WhatDoISay() { // Don't write virtual here
	cout << "Go Bruin";
}
class NerdyStudent : public Student {
public:
	virtual WhatDoISay();
};
void NerdyStudent::WhatDoISay() { // Don't write virtual here
	cout << "I love circuit!";
}
```
* Derived class will always use the **most derived version** of a specialized method by `default`

```C++
class Student {
public:
	virtual void cheer() { cout << "go bruins!"; }
	void goToBathroom()  { cout << "splat!"; }
};
class NerdyStudent: public Student {
public:
	virtual void cheer() {
	 cout << "go algorithm!"; 
	 // can also add Student::cheer(); here to reuse the function
	}
	void getExciteAboutCS() {
		cheer(); // this will print out "go algorithm!"
		Student::cheer(); // this will print out "go bruins!"
	}
}
int main() {
	NerdyStudent lily;
	lily.getExciteAboutCS();
	lily.Student::cheer(); // rare but valid
}
```

### 4. Inheritance & Construction
* C++ always constructs the base part first, then the derived part second

```C++
class Machine {
public:
	Machine() { #3 }
};
class Robot : public Machine {
	Robot()
		// Call Machine's constructor #2
		// Call m_bat's constructor #4
	{ m_x = m_y = 0; #5 }
private:
	int m_x, m_y;
	Battery m_bat;
};
class ShieldRobot : public Robot
{
public:
	ShieldRobot()
		// Call Robot's constructor #1
		// Call m_sg's constructor  #6
	{ m_shieldSrength = 1; #7  }
private:
	int m_shieldSrength;
	ShieldGenerator m_sg;
};
```

### 5. Inheritance & Destruction
* C++ **destructs the derived part first**, then the base part second

### 6. Inheritance & Initializer Lists
```C++
class Animal {
public: 
	Animal(int lbs) m_lbs(lbs){} // Since no default constructor
private:
	int m_lbs;
};
class Duck : public Animal {
public:
	Duck(): Animal(2), m_belly(1) // Must initialize here!
	{ m_feathers = 99; }
private:
	int m_feathers;
	Stomache m_belly;
};
```

### 7. Inheritance & Assignment Ops
* It works fine if the base and derived classes **do not have dynamically member variables**, or we must define assignment ops and copy constructor for both base and derived classes

# Polymorphism
### 1. Basic

Polymorphism
: Anytime we use a base pointer or a base ref to access a derived object, this is called polymorphism, we **must use a pointer or a ref**, or the "chopping" happens

```C++
class Shape {
public:
	virtual double getArea() = 0;
};
class Square: public Shape {
public:
	Square(int side) { m_side = side; }
	virtual double getArea() {
		return (m_side*m_side);
	}
private:
	int m_side;
};
class Circle: public Shape {
public:
	Circle(int rad) { m_rad = rad; }
	virtual double getArea() {
		return (3.14*m_rad*m_rad);
	}
private:
	int m_rad;
};

void printPrice(Shape& x) {
	cout << "Cost is: $";
	cout << x.getArea()*3.25;
}
int main() {
	Square s(5);
	Circle c(5);
	printPrice(s);
	printPrice(c);
	Shape sh();
	print(sh) <- ERROR, doesnt declare getArea()
}
```

* `printPrice()` actually has no idea what functions in Circle and Square, so **DO NOT call function from derived classes only**

* When do I use `virtual`?
	1. Redefine a function in a derived class
	2. for **EVERY destructor** (or polymorphism will cause trouble)
	3. **NOT for constructor, ALWAYS**

### 2. Polymorphism and Pointers
```C++
int main() {
	Square s(5);
	Shape *p;
	p = &s;
	cout << p->getArea(); // <- WORKS!!!
}
```

* Since Suqare is a type of Shape, we may point to a Square using a Sh
* ape pointer
* **BUT we may never point a subclass pointer at a super class variable**

### 3. Pure Virtual Functions
```C++
class Shape { // so called Abstract Base Class(ABC)
public:
	virtual float getArea() = 0;
	virtual float getCircum() = 0;
}
int main() {
	Shape s; // ERROR, cannot define if having pure virtual funcs.
	cout << s.getArea();   // ERROR
	cout << s.getCircum(); // ERROR
}
```

* If defining an ABC:
	* Derived classes **must** re-define all pure vitrual functions!!! Or the derived class **becomes ABC too**
