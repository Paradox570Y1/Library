![[Pasted image 20240927165311.png|400]]

# Inheritance
- Multilevel inheritance
```cpp
#include <iostream>
using namespace std;
class Animal {
	public:
	void eat() {
	cout <<"Eating.. \n";
}
};
class Dog: public Animal {
	public:
	void bark(){
	cout << "Barking..\n";
}
};
class Puppy : public Dog {
	public:
	void sleep(){
		cout << "Sleeping. ..\n";
	}
};
int main(){
	Puppy Puppy;
	Puppy.eat();
	Puppy.bark();
	Puppy.sleep();
	return 0;
}
```

- Multilevel Inhertiance

- Hybrid Inheritance
```cpp
#include <iostream>
using namespace std;

class Vehicle {
public:
    void start() {
        cout << "Vehicle Starting...\n";
    }
};

class Car : virtual public Vehicle {
public:
    void drive() {
        cout << "Car Driving...\n";
    }
};

class Truck : virtual public Vehicle {
public:
    void loadCargo() {
        cout << "Loading Cargo...\n";
    }
};

class Hybrid : public Car, public Truck {
public:
    void hybridDrive() {
        cout << "Hybrid Driving...\n";
    }
};

int main() {
    Hybrid myHybrid;
    myHybrid.start();
    myHybrid.drive();
    myHybrid.loadCargo();
    myHybrid.hybridDrive();
    return 0;
}
```

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    void eat() {
        cout << "Eating...\n";
    }
};

class Dog : public Animal {
public:
    void bark() {
        cout << "Barking...\n";
    }
};

class Cat : public Animal {
public:
    void meow() {
        cout << "Meowwwww...\n";
    }
};

int main() {
    Dog myDog;
    myDog.eat();
    myDog.bark();

    Cat myCat;
    myCat.eat();
    myCat.meow();

    return 0;
}

```

# Ambiguity in multiple and multipath inheritance(Diamond Problem)
The Diamond Problem is a common issue encountered in object-oriented programming, specifically when two classes inherit from the same base class, and a third class inherits from both of them.

###### The Problem:
In multiple inheritance, when a class inherits from more than one class, there can
be if the same member (IIT$function or variable) is inherited from more
than one base class. This often happens when both parent classes are derived from
the same grandparent class, creating a diamond-shaped inheritance structure.

# Binding
```cpp
// Online C++ compiler to run C++ program online
#include <iostream>
using namespace std;
class Base{
    public:
    virtual void show(){
        cout << "Base class show function" << endl;
    }
    void print(){
        cout << "Base class print function" << endl;
    }
};
class Derived : public Base {
    public:
    void show(){
        cout << "Derived class show function" << endl;
    }
    void print(){
        cout << "Derived class print function" << endl;
    }
};
int main() {
    // Write C++ code here
    Base * basePtr;
    Derived derivedObj;
    basePtr = &derivedObj;
    basePtr->show();
    basePtr->print();

    return 0;
}
```


```cpp
// Online C++ compiler to run C++ program online
#include <iostream>
using namespace std;
class Base{
    public:
    Base(){
        cout << "Base Constructor" << endl;
    }
    virtual ~Base (){
        cout << "Base destructor" << endl;
    }
};

class Derived : public Base {
    public:
    Derived(){
        cout << "Derived Constructor"<< endl;
    }
    ~Derived(){
        cout << "Derived Desturctor"<< endl;
    }
};
int main() {
    // Write C++ code here
    Base* obj = new Derived();
    delete obj;

    return 0;
}
```

```cpp
// Online C++ compiler to run C++ program online
#include <iostream>
using namespace std;
class Math{
    public:
    int add(int a,int b){
        return a+b;
    }
    float add(float a,float b){
        return a+b;
    }
};
int main() {
    // Write C++ code here
    Math math;
    cout << math.add(3,5) << endl;
    cout << math.add(3.2f,5.4f)<< endl;
    return 0;
}
```

```cpp
// Online C++ compiler to run C++ program online
#include <iostream>
using namespace std;

class Vehicle{
    public:
    virtual void startEngine(){
        cout << "Starting vehicle Engine..."<< endl;
    }
};
class Car : public Vehicle{
    public:
    void startEngine(){
        cout << "Starting car engine..." << endl;
    }
};
class Bike: public Vehicle{
    public:
    void startEngine() override{
        cout << "Starting bike engine " << endl;
    }
};

int main() {
    // Write C++ code here
    Vehicle* vehiclePtr;
    Car myCar;
    Bike myBike;
    vehiclePtr = &myCar;
    vehiclePtr->startEngine();
    vehiclePtr = &myBike;
    vehiclePtr->startEngine();
    return 0;
}
```