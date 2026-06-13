## Class
- User defined Data type.
- If we had made a class and had not created its object then no space will be consumed in memory.
- If we have an empty class(nothing inside) and then creates its object then that object will consume 1 byte(not 0) which stores the existence of the object.
- We use semicolon because it means that we can't declare object before the semi colon but we can declare it after weather before class or in class.
  ![[Pasted image 20240708195723.png|200]]
- By default class is private so you can't access it.
  ![[Pasted image 20240708200021.png|300]]
- You can make it public , using public access specifier
  ![[Pasted image 20240708200559.png|300]]
  ![[Pasted image 20240708200616.png|200]]
- How to use function inside class
```cpp
  #include <bits/stdc++.h>
using namespace std;
class Student{
    public:
    int roll;
    int check(int n){
        return n;
    }
};
int main() {
    Student s1;
    s1.roll = 45;
    cout << s1.check(10);
    return 0;
}
```

![[Pasted image 20240708201000.png| 100]]

- Default parameter
```cpp
#include<bits/stdc++.h>
using namespace std;
int check(int a,int b,int c=5){
    return a+b+c;
}
int main(){
    cout << check(2,3);
}
```
![[Pasted image 20240709192539.png|100]]

- Inline function
	- When we call the function ,in case of inline function it will be replaced directly with the value to be returned.
```cpp
#include<bits/stdc++.h>
using namespace std;
inline int check(int a,int b){
    return a+b;
}
int main(){
    cout << check(2,3);
}
```
here check() is directly replaced with a+b.

- Constructor
	- Special kind of function whose name is same as name of class
	- It doesn't have any return type not even void.
	- When we create object constructor gets called.
	- Two types:
		- Default constructor
		- Parameterized constructor
```cpp
#include<bits/stdc++.h>
using namespace std;
class student{
    public:
    int a,b;
    student(int x,int y){
        cout << x << " " << y << endl;
        a=x;
        b=y;
    }
};
int main(){
    student s1(10,20);
    student s2(30,40);
    cout << endl;
    cout << s2.a << " " << s2.b << endl;
    s2 = s1;
    cout << s2.a << " " << s2.b << endl;
    return 0;
}

```

- Destructor
	- No return type
	- name of destructor same as class.
	- It is called when object is about to destroy.


- [[#Introduction to Basic Concepts of Object-Oriented Programming:|Introduction to Basic Concepts of Object-Oriented Programming:]]
- [[#Comparison Between Procedural and Object-Oriented Programming Paradigms:|Comparison Between Procedural and Object-Oriented Programming Paradigms:]]
- [[#Problem Solving Strategies:|Problem Solving Strategies:]]
- [[#1. Inline Functions:|1. Inline Functions:]]
		- [[#Purpose:|Purpose:]]
		- [[#When to Use:|When to Use:]]
		- [[#Syntax and Example:|Syntax and Example:]]
		- [[#Explanation:|Explanation:]]
- [[#2. Default Arguments:|2. Default Arguments:]]
- [[#3. Function Prototyping:|3. Function Prototyping:]]
- [[#4. Function Overloading:|4. Function Overloading:]]
- [[#5. Call by Reference:|5. Call by Reference:]]
- [[#6. Call by Value:|6. Call by Value:]]
- [[#7. Call by Pointer:|7. Call by Pointer:]]
- [[#8. Return by Reference:|8. Return by Reference:]]
- [[#9. Introduction to Namespace:|9. Introduction to Namespace:]]
- [[#10.Specifying a Class:|10.Specifying a Class:]]
- [[#11. Creating Class Objects:|11. Creating Class Objects:]]
- [[#12. Accessing Class Members:|12. Accessing Class Members:]]
- [[#13. Access Specifiers – Public, Private, and Protected (With Inheritance):|13. Access Specifiers – Public, Private, and Protected (With Inheritance):]]
- [[#14. Objects and Memory:|14. Objects and Memory:]]
- [[#15. Static Members:|15. Static Members:]]
	- [[#15. Static Members:#Static Vs Non-Static Members|Static Vs Non-Static Members]]
		- [[#Static Vs Non-Static Members#Static Members:|Static Members:]]
		- [[#Static Vs Non-Static Members#Non-Static Members:|Non-Static Members:]]
- [[#16. Static Objects:|16. Static Objects:]]
- [[#17. Constant Member Function:|17. Constant Member Function:]]
- [[#18. Constant Objects:|18. Constant Objects:]]
- [[#19. Friend Functions:|19. Friend Functions:]]
- [[#20. Friend Class:|20. Friend Class:]]
- [[#21. Passing Object as an Argument:|21. Passing Object as an Argument:]]
- [[#22. Returning Object from a Function:|22. Returning Object from a Function:]]
- [[#23. **Need for Constructors and Destructors**|23. **Need for Constructors and Destructors**]]
- [[#24. **Copy Constructor**|24. **Copy Constructor**]]
- [[#25. **Deep Copy**|25. **Deep Copy**]]
- [[#26. **Dynamic Constructors**|26. **Dynamic Constructors**]]
- [[#27. **Destructors**|27. **Destructors**]]
- [[#28. **Constructors and Destructors with Static Members**|28. **Constructors and Destructors with Static Members**]]
- [[#29. **Defining Operator Overloading**|29. **Defining Operator Overloading**]]
			- [[#Non-Static Members:#Why use an initializer list?|Why use an initializer list?]]
- [[#30. **Rules for Overloading Operators**|30. **Rules for Overloading Operators**]]
- [[#31. **Overloading of Unary Operators**|31. **Overloading of Unary Operators**]]
- [[#32. _Binary Operators (+, -, /, *)_|32. _Binary Operators (+, -, /, *)_]]
- [[#33. **Binary Operators Using Friend Functions**|33. **Binary Operators Using Friend Functions**]]
- [[#34. **Manipulation of Strings Using Overloaded Operators (>, <,=\=)**|34. **Manipulation of Strings Using Overloaded Operators (>, <,=\=)**]]
- [[#35. Type Conversion:|35. Type Conversion:]]
	- [[#35. Type Conversion:#Basic type to class type|Basic type to class type]]
	- [[#35. Type Conversion:#Class type to Basic type|Class type to Basic type]]
	- [[#35. Type Conversion:#Class to class Type Conversion:|Class to class Type Conversion:]]
- [[#36.Pointers|36.Pointers]]
	- [[#36.Pointers#1. Accessing the Address of a Variable:|1. Accessing the Address of a Variable:]]
	- [[#36.Pointers#2. Declaring and Initializing Pointers:|2. Declaring and Initializing Pointers:]]
	- [[#36.Pointers#3. Accessing a Variable Through Its Pointer:|3. Accessing a Variable Through Its Pointer:]]
	- [[#36.Pointers#4.Pointer Arithmetic:|4.Pointer Arithmetic:]]
	- [[#36.Pointers#5.Pointer to a Pointer:|5.Pointer to a Pointer:]]
	- [[#36.Pointers#6.Pointer to a Function:|6.Pointer to a Function:]]
- [[#37.Dynamic memory management|37.Dynamic memory management]]
	- [[#37.Dynamic memory management#new and delete Operators|new and delete Operators]]
	- [[#37.Dynamic memory management#Pointers and Classes:|Pointers and Classes:]]
	- [[#37.Dynamic memory management#Pointer to an Object:|Pointer to an Object:]]
	- [[#37.Dynamic memory management#Pointer to a Member:|Pointer to a Member:]]
	- [[#37.Dynamic memory management#this Pointer|this Pointer]]
	- [[#37.Dynamic memory management#Dangling Pointer|Dangling Pointer]]
	- [[#37.Dynamic memory management#Wild Pointer|Wild Pointer]]
	- [[#37.Dynamic memory management#Null Pointer Assignment|Null Pointer Assignment]]
	- [[#37.Dynamic memory management#Memory Leak|Memory Leak]]
	- [[#37.Dynamic memory management#Allocation Failure|Allocation Failure]]
- [[#38.Inheritance|38.Inheritance]]
	- [[#38.Inheritance#Introduction: Concept of Reuse in Object-Oriented Programming (OOP)|Introduction: Concept of Reuse in Object-Oriented Programming (OOP)]]
	- [[#38.Inheritance#Defining Derived Classes|Defining Derived Classes]]
	- [[#38.Inheritance#Forms of inheritance (single, multilevel, multiple, hybrid & hierarchical)|Forms of inheritance (single, multilevel, multiple, hybrid & hierarchical)]]
	- [[#38.Inheritance#Single Inheritance|Single Inheritance]]
	- [[#38.Inheritance#Multilevel Inheritance|Multilevel Inheritance]]
	- [[#38.Inheritance#Multiple Inheritance|Multiple Inheritance]]
	- [[#38.Inheritance#Hybrid Inheritance|Hybrid Inheritance]]
	- [[#38.Inheritance#Hierarchical Inheritance|Hierarchical Inheritance]]
	- [[#38.Inheritance#Diamond Problem|Diamond Problem]]
	- [[#38.Inheritance#The Problem:|The Problem:]]
	- [[#38.Inheritance#Solving the Diamond Problem with Virtual Inheritance:|Solving the Diamond Problem with Virtual Inheritance:]]
	- [[#38.Inheritance#Inheritance with constructor|Inheritance with constructor]]
- [[#39.Function Overriding|39.Function Overriding]]
- [[#40.Function Overloading|40.Function Overloading]]
- [[#41.Binding|41.Binding]]
	- [[#41.Binding#Static Binding (Early Binding)|Static Binding (Early Binding)]]
	- [[#41.Binding#Dynamic Binding (Late Binding)|Dynamic Binding (Late Binding)]]
- [[#42.Virtual Function vs Pure Virtual functions|42.Virtual Function vs Pure Virtual functions]]
- [[#43.**Abstract Classes**|43.**Abstract Classes**]]
- [[#44.**Virtual Destructors and Polymorphism**|44.**Virtual Destructors and Polymorphism**]]
- [[#45.**Order of Execution of Virtual Functions**|45.**Order of Execution of Virtual Functions**]]
- [[#46.**Overriding Member Functions**|46.**Overriding Member Functions**]]
- [[#47.**Accessing Base Class Functions**|47.**Accessing Base Class Functions**]]
- [[#48.**Order of Execution of Constructors and Destructors**|48.**Order of Execution of Constructors and Destructors**]]
- [[#49.**Review of Traditional Error Handling**|49.**Review of Traditional Error Handling**]]
- [[#50.**Basics of Exception Handling**|50.**Basics of Exception Handling**]]
- [[#51.**Exception Handling Mechanism**|51.**Exception Handling Mechanism**]]
	- [[#51.**Exception Handling Mechanism**#**Throwing Mechanism**|**Throwing Mechanism**]]
	- [[#51.**Exception Handling Mechanism**#**Catching Mechanism**|**Catching Mechanism**]]
	- [[#51.**Exception Handling Mechanism**#**Re-Throwing an Exception**|**Re-Throwing an Exception**]]
	- [[#51.**Exception Handling Mechanism**#**Specifying Exceptions**|**Specifying Exceptions**]]
- [[#52**Problems on Recursion**|52**Problems on Recursion**]]
	- [[#52**Problems on Recursion**#Problem: Calculate Factorial Using Recursion|Problem: Calculate Factorial Using Recursion]]
	- [[#52**Problems on Recursion**#Problem: Fibonacci Series Using Recursion|Problem: Fibonacci Series Using Recursion]]
- [[#53.**Concept of Streams**|53.**Concept of Streams**]]
	- [[#53.**Concept of Streams**#**Example: Overloading `>>` and `<<`**|**Example: Overloading `>>` and `<<`**]]
- [[#54.**File Streams**|54.**File Streams**]]
- [[#54.**Error Handling During File Operations**|54.**Error Handling During File Operations**]]
	- [[#54.**Error Handling During File Operations**#**Key Functions for Error Handling**:|**Key Functions for Error Handling**:]]
	- [[#54.**Error Handling During File Operations**#**Example: Error Handling in File Operations**|**Example: Error Handling in File Operations**]]
- [[#**55.Reading/Writing Files and Accessing Records Randomly**|**55.Reading/Writing Files and Accessing Records Randomly**]]
	- [[#**55.Reading/Writing Files and Accessing Records Randomly**#**Key Methods**:|**Key Methods**:]]
	- [[#**55.Reading/Writing Files and Accessing Records Randomly**#**Example: Writing and Reading Records Randomly**|**Example: Writing and Reading Records Randomly**]]


## History of Programming Language - Complexity and Security:

Programming languages have evolved to meet increasing complexity and security needs over time. Early languages like Assembly were low-level and lacked features to manage complexity. As systems became more intricate, high-level languages (e.g., C++, Java) emerged with better abstractions to handle complexity. Security concerns have been addressed by developing features like memory management, type safety, and secure execution environments.


### Introduction to Basic Concepts of Object-Oriented Programming:

1. **Data Hiding**: Restricts access to certain parts of an object to prevent unintended or malicious modification.
2. **Abstraction**: Simplifies complex systems by focusing on essential details and hiding the unnecessary ones.
3. **Encapsulation**: Combines data and the methods that operate on it within a single unit (class), safeguarding data from external interference.
4. **Inheritance**: Enables a new class to acquire properties and behavior of an existing class, promoting code reusability.
5. **Polymorphism**: Allows objects to be treated as instances of their parent class, enabling methods to behave differently based on the object calling them.

### Comparison Between Procedural and Object-Oriented Programming Paradigms:

- **Procedural Programming**: Focuses on a step-by-step sequence of instructions (e.g., C), where functions operate on data. It lacks the modularity and flexibility of OOP.
- **Object-Oriented Programming**: Focuses on objects that encapsulate data and behavior, leading to more modular and maintainable code. It promotes reusability through inheritance and flexibility through polymorphism.

### Problem Solving Strategies:

1. **Top-Down**: Breaks down a problem into smaller sub-problems, solving each individually.
2. **Bottom-Up**: Starts by solving small, manageable parts of the problem and integrates them into a larger solution.
3. **Problems on Array**: Arrays are often used to practice these strategies, involving tasks like searching, sorting, and manipulating array elements to find solutions efficiently.


### 1. Inline Functions:

An **inline function** is a function definition, usually placed at the point of call, allowing the compiler to insert the code directly in the calling function rather than using a traditional function call. This reduces overhead, especially for small functions, improving execution speed. However, inline functions are only a suggestion to the compiler and are not always guaranteed to be inlined, especially if the function is complex.
##### Purpose:
The main advantage of using inline functions is to eliminate the overhead associated with function calls, especially for very small functions that are called frequently. This can make your program faster, as the function call and return sequence is avoided.

##### When to Use:
- For small, frequently used functions like getter methods.
- For functions that don’t contain complex logic (loops, recursion).

##### Syntax and Example:
To define an inline function, you use the `inline` keyword before the function definition.

```cpp
using namespace std;
inline int square(int x) {     
   return x * x; 
}  
int main() {     
   int a = 5;     
   cout << "Square of " << a << " is " << square(a) << endl;     
   return 0; 
}

```

##### Explanation:
- In this example, the `square()` function is marked as `inline`.
- When `square(a)` is called in the `main` function, instead of performing a traditional function call, the compiler replaces the call with the actual function code like this:

```cpp
cout << "Square of " << a << " is " << (a * a) << endl;
```

### 2. Default Arguments:
**Default arguments** are values provided in the function declaration, allowing the function to be called with fewer arguments than specified. If the user does not provide values for all parameters during the function call, the compiler uses the default values. This feature simplifies function calls and improves code readability. For example:

```cpp
void display(int x, int y = 10) {     
	cout << x << " " << y; 
}
```

Here, `y` has a default value of `10`, so `display(5)` would output `5 10`.


### 3. Function Prototyping:

**Function prototyping** is the declaration of a function before its actual definition, specifying the function’s name, return type, and parameters. This allows the compiler to check function calls against their prototypes for correct arguments and return types, ensuring type safety. It also allows for functions to be defined after their use in a program. For example:


```cpp
int add(int, int);  // Prototype 
int add(int a, int b) { return a + b; }  // Definition
```

These topics are key in C++ for reducing errors and improving efficiency in program execution.




### 4. Function Overloading:

**Function overloading** is the ability to define multiple functions with the same name but different parameter types or numbers of parameters. The correct function is chosen by the compiler based on the argument types or the number of arguments passed during the function call. Example:


```cpp
int add(int a, int b) { return a + b; } 
double add(double a, double b) { return a + b; }
```

Here, `add` is overloaded with different parameter types (int and double).

### 5. Call by Reference:

In **call by reference**, the function receives the address of the actual parameters, allowing it to modify the actual variables in the calling function. This is useful when you need to modify the arguments or pass large data structures without copying. Example:

```cpp
void swap(int &x, int &y) {     
	int temp = x;     
	x = y;     
	y = temp; 
}
```

Here, the variables `x` and `y` are passed by reference, allowing the `swap` function to modify the original variables.

### 6. Call by Value:

In **call by value**, a copy of the actual parameters is passed to the function. Changes made to the parameters inside the function do not affect the actual arguments. Example:

```cpp
void add(int a, int b) {     
 a = a + b;  // Only changes within the function, not affecting original variables 
}
```

Here, `a` and `b` are passed by value, and changes to them inside the function will not affect the original variables.

### 7. Call by Pointer:

In **call by pointer**, the function is passed the memory address (pointer) of the actual argument, allowing direct modification of the original data. Example:

```cpp
void increment(int *a) {     
	(*a)++; 
}
```

The function `increment` takes a pointer to an integer, allowing it to modify the original variable passed to it.

### 8. Return by Reference:

In **return by reference**, the function returns a reference to an existing variable rather than a copy, allowing the caller to modify the returned value directly. Example:

```cpp
int& largest(int &x, int &y) {     
	return (x > y) ? x : y; 
}
```

In this example, the function `largest` returns a reference to either `x` or `y`, allowing the calling function to modify the returned value.

These concepts are essential for understanding how functions interact with variables in different ways in C++.


### 9. Introduction to Namespace:
A **namespace** in C++ is a declarative region that provides scope to identifiers like variables, functions, and classes to avoid name conflicts. Namespaces help manage large codebases by grouping logically related entities together. The standard C++ library uses the `std` namespace, so `std::cout` refers to `cout` within the `std` namespace. You can define your own namespaces to prevent clashes between variable names in different parts of the program.

Example:

```cpp
	namespace myNamespace {   int value = 10; }
```

### 10.Specifying a Class:

**Specifying a class** in C++ means defining a blueprint for objects. A class contains data members (variables) and member functions (methods) that operate on the data. Classes use access specifiers (`public`, `private`, `protected`) to control how the members can be accessed.

```cpp
class Rectangle { private:     
					 int width, height;  
				 public:     
					 void setValues(int w, int h) {         
						 width = w;         
						 height = h;     
					 }      
					 int area() {         
					 return width * height;     
					 }
				};
```

### 11. Creating Class Objects:

**Creating objects** means instantiating a class, which allocates memory for its data members and provides access to its methods. Objects are instances of a class.

Example:


```cpp
Rectangle rect;  // Creating an object of class Rectangle 
rect.setValues(5, 10);  // Accessing member function 
cout << rect.area();  // Calling another member function
```

In this example, `rect` is an object of class `Rectangle`, and its member functions are accessed using the dot operator.

### 12. Accessing Class Members:

Class members (variables and functions) are accessed using the **dot operator (`.`)** for regular objects and **arrow operator (`->`)** for pointers. Depending on the access specifiers (public, private, protected), access to these members varies.

Example:


```cpp
class MyClass { 
    public:     
	int x;     
	void print() {         
		 cout << x;     
	} 
};  
int main() {     
	MyClass obj;     
	obj.x = 10;  // Accessing public member     
	obj.print(); // Accessing public method }
```

### 13. Access Specifiers – Public, Private, and Protected (With Inheritance):

1. **Public**: Members declared as public can be accessed by any function outside the class.
2. **Private**: Members declared as private can only be accessed by member functions of the class.
3. **Protected**: These members can only be accessed by the class itself and its derived classes, but not by other classes or functions outside the class.

**Inheritance** plays a key role in how these access specifiers work:

- **Public inheritance**: Public members of the base class remain public, and protected members remain protected in the derived class.
- **Protected inheritance**: Public and protected members of the base class become protected in the derived class.
- **Private inheritance**: Public and protected members of the base class become private in the derived class.

Example:


```cpp
class Base { protected:     
				int protectedVar; public:     
				int publicVar; 
			};  
			class Derived : public Base { 
				public:     
					void display() {         
						cout << protectedVar; // Accessible due to protected inheritance     } };
```

### 14. Objects and Memory:

When an object is created, **memory** is allocated for its data members (variables) based on their types. Each object has its own memory space for non-static members, ensuring that modifying one object's members does not affect another. **Static members**, however, share the same memory across all objects of a class, and **member functions** do not occupy memory separately for each object (they are shared).

In terms of object lifetime, dynamic objects (created using `new`) are stored on the **heap**, while automatic objects (created without `new`) are stored on the **stack**. The `delete` operator is used to free heap memory for dynamic objects.


```cpp
Rectangle *rect = new Rectangle();  // Memory is allocated on the heap 
delete rect;  // Frees memory
```

### 15. Static Members:

**Static members** are class-level variables or functions that are shared by all objects of the class. A static variable is initialized only once, and its value is shared across all instances of the class. Static functions, similarly, are not tied to any specific object and can be called using the class name without creating an instance.

Example:


```cpp
class MyClass { 
public:     
	static int count;  // Static variable     
	static void showCount() {  // Static function         
		cout << "Count: " << count;     
	} 
}; 
int MyClass::count = 0;  // Defining and initializing static variable
```

#### Static Vs Non-Static Members
##### Static Members:

1. **Shared across all instances**:
    
    - A static member (either a variable or a function) belongs to the class itself, not to any specific object. It is shared among all objects of that class.
    - Changes to a static variable affect all objects of the class.
2. **Memory allocation**:
    
    - Static variables are allocated memory only once, regardless of how many objects are created.
    - Static variables exist for the lifetime of the program.
3. **Access**:
    
    - Static members can be accessed without creating an instance of the class.
    - They can be accessed using the class name (e.g., `ClassName::staticMember`).
4. **Initialization**:
    
    - Static variables must be defined outside the class definition, and they are initialized once.
5. **Functions**:
    
    - Static member functions can only access other static members (variables or functions).
    - They do not have access to `this` pointer, since they do not operate on any particular object.
6. **Use case**:
    
    - Static members are useful when you want to share common data or functionality across all instances of a class.

##### Non-Static Members:

1. **Specific to each object**:
    
    - A non-static member is tied to a specific instance of the class. Each object has its own copy of the non-static variables.
2. **Memory allocation**:
    
    - Non-static variables are allocated memory separately for each object when the object is created.
    - They exist for the lifetime of the object.
3. **Access**:
    
    - Non-static members can only be accessed by an object (e.g., `objectName.nonStaticMember`).
4. **Functions**:
    
    - Non-static member functions can access both static and non-static members of the class.
    - They have access to the `this` pointer, which refers to the calling object.
5. **Use case**:
    
    - Non-static members are used when you want each object of the class to maintain its own state or behavior.

### 16. Static Objects:

**Static objects** are objects that persist for the lifetime of the program, unlike automatic objects, which are destroyed once they go out of scope. A static object retains its value between function calls and is only destroyed when the program terminates.

Example:


```cpp
void createObject() {     
	static MyClass obj;  // Static object 
}
```

This object will be created only once and persist across multiple function calls.

### 17. Constant Member Function:

A **constant member function** is a function that does not modify any member variables of the class. It is declared with the `const` keyword after the function signature to indicate that it won’t alter the object’s state.

Example:

```cpp
class MyClass { 
public:     
    int value;     
	int getValue() const {  // Constant member function         
		return value;     
	} 
};
```

Here, `getValue` cannot modify any member variables and ensures that the function maintains the const correctness of the object.

### 18. Constant Objects:

A **constant object** is an object whose state (member variables) cannot be modified after initialization. This is enforced by using the `const` keyword during object creation. Only constant member functions can be called on constant objects.

Example:


```cpp
const MyClass obj;  // Constant object 
obj.getValue();  // Allowed because getValue is a constant member function
```

Here, `obj` is a constant object, so any attempt to modify its data members or call non-const member functions would result in a compilation error.

These concepts are important for ensuring proper memory management, enforcing immutability where necessary, and providing shared resources efficiently in object-oriented programs.

### 19. Friend Functions:

A **friend function** is a function that is not a member of a class but is allowed access to its private and protected members. It’s declared with the keyword `friend` inside the class definition. This is useful when external functions need access to a class’s internal details.

Example:
```cpp
class MyClass {
private:
    int data;
public:
    MyClass(int value) : data(value) {}
    friend void displayData(MyClass obj);  // Friend function declaration
};

void displayData(MyClass obj) {
    cout << "Data: " << obj.data;  // Accessing private member
}

```
### 20. Friend Class:

A **friend class** is a class that is given access to the private and protected members of another class. This allows for close cooperation between classes, where one class needs to manipulate the private data of another.

Example:
```cpp
class A {
private:
    int data;
public:
    A(int value) : data(value) {}
    friend class B;  // Class B is a friend
};

class B {
public:
    void showData(A obj) {
        cout << "Data: " << obj.data;  // Accessing private member of class A
    }
};
```

### 21. Passing Object as an Argument:

1. **By Value**: A copy of the object is passed to the function. Changes made to the object inside the function don’t affect the original object.
```cpp
void display(MyClass obj) {  // Passed by value
    cout << obj.getData();
}
```

2. **By Reference**: The actual object is passed to the function, allowing changes to the object’s state.
```cpp
void modify(MyClass &obj) {  // Passed by reference
    obj.setData(10);
}
```

3. **By Address**: A pointer to the object is passed, allowing the function to access and modify the object’s members using the arrow operator (`->`).
```cpp
void modify(MyClass *obj) {  // Passed by address
    obj->setData(10);
}
```


### 22. Returning Object from a Function:

A function can return an object, either by value or reference. When returned by value, a new copy of the object is created, whereas returning by reference allows the function to return a reference to an existing object.

Example:
```cpp
MyClass createObject() {  // Returning by value
    MyClass obj;
    return obj;
}

MyClass& returnReference(MyClass &obj) {  // Returning by reference
    return obj;
}
```
Returning objects is a powerful way to create new instances or modify existing ones via function calls.

### 23. **Need for Constructors and Destructors**

- **Constructor**: A constructor initializes an object when it is created. Without it, you would need to manually set initial values, which can lead to errors. Constructors ensure that the object starts in a well-defined state.
Example:
```cpp
class Example {
    int x;
public:
    Example() { // Constructor
        x = 0; // Initializes x to 0
    }
    void display() {
        cout << "x = " << x << endl;
    }
};

int main() {
    Example obj; // Constructor is called
    obj.display(); // x = 0
}
```
- When the object `obj` is created, the constructor initializes `x` to 0 automatically.

- **Destructor**: A destructor is used to free resources, like memory or file handles, when an object is destroyed. It is called automatically when the object goes out of scope.
Example:
```cpp
class Example {
public:
    Example() {
        cout << "Constructor called" << endl;
    }
    ~Example() { // Destructor
        cout << "Destructor called" << endl;
    }
};

int main() {
    Example obj; // Constructor called
    // When main ends, destructor is called automatically
}
```
- The destructor frees any resources if necessary (e.g., dynamically allocated memory).

### 24. **Copy Constructor**

A **copy constructor** is used to create a new object by copying an existing object. By default, C++ provides a copy constructor that performs a **shallow copy**.

- **Shallow Copy**: Just copies the memory addresses, leading to issues like multiple pointers pointing to the same resource.
    
- **Deep Copy**: Copies the actual data, ensuring each object has its own copy of dynamically allocated memory.
Example:
```cpp
class Example {
    int* x;
public:
    Example(int val) { // Constructor
        x = new int(val);
    }
    Example(const Example& obj) { // Copy constructor
        x = new int(*(obj.x)); // Deep copy
    }
    void display() {
        cout << "x = " << *x << endl;
    }
    ~Example() {
        delete x; // Destructor frees memory
    }
};

int main() {
    Example obj1(10); // Constructor
    Example obj2 = obj1; // Copy constructor (deep copy)
    obj1.display(); // x = 10
    obj2.display(); // x = 10
}
```

- The **copy constructor** makes a deep copy, ensuring that `obj1` and `obj2` have separate memory locations for `x`.
### 25. **Deep Copy**

A **deep copy** ensures that dynamically allocated resources are duplicated properly. When dealing with raw pointers or dynamic memory allocation, shallow copies (the default copy behavior) can lead to issues where two objects point to the same memory. This is solved by implementing a deep copy.

```csharp
class Example {
    int* data;
public:
    Example(int value) {
        data = new int(value); // Dynamic allocation
    }
    Example(const Example& obj) {
        data = new int(*(obj.data)); // Deep copy
    }
    void display() {
        cout << "Data: " << *data << endl;
    }
    ~Example() {
        delete data; // Clean up memory
    }
};

int main() {
    Example obj1(5);
    Example obj2 = obj1; // Deep copy
    obj1.display(); // Data: 5
    obj2.display(); // Data: 5
}
```
- Here, `obj1` and `obj2` point to different memory locations, so modifying one will not affect the other.
### 26. **Dynamic Constructors**
A **dynamic constructor** uses dynamic memory allocation to create objects. This is useful when you don’t know the size of the required memory at compile time.

Example:
```cpp
class Example {
    int* arr;
    int size;
public:
    Example(int n) { // Constructor dynamically allocates memory
        size = n;
        arr = new int[size];
        for (int i = 0; i < size; ++i) {
            arr[i] = i + 1;
        }
    }
    void display() {
        for (int i = 0; i < size; ++i) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }
    ~Example() {
        delete[] arr; // Destructor frees memory
    }
};

int main() {
    Example obj(5); // Creates an array of 5 integers
    obj.display(); // Output: 1 2 3 4 5
}
```
- The constructor dynamically allocates an array of integers and initializes it. The destructor cleans up the memory when the object is destroyed.

### 27. **Destructors**

A **destructor** is a special member function that is automatically called when an object goes out of scope or is explicitly deleted. It is primarily used to release resources like memory, files, or network connections that were allocated by the constructor or other member functions. In C++, destructors have the following characteristics:

- They have the same name as the class but are preceded by a tilde (`~`).
- They do not take any arguments and do not return any value.
- Destructors are called in reverse order of the object's creation.

**Example**:
```cpp
class Example {
    int* data;
public:
    Example() { 
        data = new int[5];  // Allocate dynamic memory
        cout << "Constructor: Memory allocated" << endl;
    }
    ~Example() { 
        delete[] data;  // Free dynamic memory
        cout << "Destructor: Memory deallocated" << endl;
    }
};

int main() {
    Example obj;  // Constructor is called here
    // Destructor is called automatically when the object goes out of scope
    return 0;
}
```

### 28. **Constructors and Destructors with Static Members**

Static members in a class are shared among all objects of the class and are not tied to any specific instance. They are initialized only once, and they remain in memory throughout the program's lifetime. Since static members are shared, their initialization happens outside of the constructor, and destructors do not handle them.

However, constructors can still initialize them indirectly if needed, and static members can be manipulated through any object or even directly via the class name.

- **Key points**:
    - **Static data members**: Declared with the keyword `static` and are shared across all instances of a class.
    - **Static member functions**: These functions can access only static members of a class, and they can be called without creating an object.
    - Static members are **not destroyed** when an object is destructed since they belong to the class itself, not the instance.

**Example**:
```cpp
class Example {
    static int count;  // Static data member
public:
    Example() {
        count++;
        cout << "Constructor: Object count = " << count << endl;
    }
    ~Example() {
        count--;
        cout << "Destructor: Object count = " << count << endl;
    }
    static void displayCount() {  // Static member function
        cout << "Current object count: " << count << endl;
    }
};

int Example::count = 0;  // Definition of static member outside the class

int main() {
    Example obj1;  // Constructor increments count
    Example obj2;  // Another object increments count
    Example::displayCount();  // Static function call without object

    // Destructor called for obj2 and obj1 when they go out of scope
    return 0;
}
```
In this example:

- The static member `count` is shared across all objects, and it tracks how many instances of `Example` exist.
- When the constructor is called, `count` is incremented, and when the destructor is called, it is decremented.
- The static function `displayCount()` can be called without creating any objects and can access the static member `count`.

### 29. **Defining Operator Overloading**

Operator overloading in C++ allows you to redefine the way operators work for user-defined types (such as classes). By overloading an operator, you can give it a custom behavior when used with class objects, similar to how operators like `+` and `*` work with basic types like `int` and `float`.

**Example**: Overloading the `+` operator for a `Complex` number class:
```cpp
class Complex {
    int real, imag;
public:
    Complex(int r = 0, int i = 0) : real(r), imag(i) {}

    // Overloading the + operator
    Complex operator + (const Complex& obj) {
        Complex result;
        result.real = real + obj.real;
        result.imag = imag + obj.imag;
        return result;
    }

    void display() {
        cout << real << " + " << imag << "i" << endl;
    }
};

int main() {
    Complex c1(3, 4), c2(1, 2);
    Complex c3 = c1 + c2;  // Calls the overloaded + operator
    c3.display();  // Output: 4 + 6i
}
```
In this example, the `+` operator is overloaded to add two `Complex` objects.

**`: real(r), imag(i)`**:

- This is called the **initializer list**.
- It directly initializes the members `real` and `imag` with the values of `r` and `i`, respectively.
- `real(r)` initializes the member variable `real` with the value `r`, and `imag(i)` initializes `imag` with the value `i`.
###### Why use an initializer list?
- **Efficiency**: Initializer lists initialize members directly when the object is created, rather than first default constructing them and then assigning values in the constructor body.
- **Mandatory for const or reference members**: If `real` or `imag` were `const` or references, they would need to be initialized in an initializer list, as you cannot assign values to them in the constructor body.
### 30. **Rules for Overloading Operators**
When overloading operators, there are several rules and restrictions:

- **Cannot create new operators**: You can only overload existing operators; new ones cannot be defined.
- **At least one operand must be user-defined**: This prevents you from changing the behavior of operators for built-in types (like making `int + int` do something different).
- **Preserve the operator's original meaning**: It's a good practice to ensure that the overloaded operator behaves logically according to the standard meaning (e.g., use `+` for addition-like behavior).
- **Function syntax**: Overloaded operators can be member functions or friend functions. For example:
    - Member function: `ClassName operator +(const ClassName& obj);`
    - Friend function: `friend ClassName operator +(const ClassName& obj1, const ClassName& obj2);`
- **Certain operators cannot be overloaded**: Some operators like `::`, `.*`, `.`, and `?:` cannot be overloaded.

### 31. **Overloading of Unary Operators**

Unary operators are operators that operate on a single operand, like `++`, `--`, `-`, and `!`. Overloading unary operators allows you to define their behavior for user-defined types.

**Example**: Overloading the `++` operator (prefix and postfix) for a class:
```cpp
class Counter {
    int count;
public:
    Counter() : count(0) {}

    // Overloading the prefix ++ operator
    Counter& operator++() {
        ++count;
        return *this;
    }

    // Overloading the postfix ++ operator
    Counter operator++(int) {
        Counter temp = *this;
        count++;
        return temp;
    }

    void display() {
        cout << "Count: " << count << endl;
    }
};

int main() {
    Counter c;
    ++c;  // Calls prefix ++
    c.display();  // Count: 1

    c++;  // Calls postfix ++
    c.display();  // Count: 2
}
```
- **Prefix `++`** increments the value and returns the updated object.
- **Postfix `++`** returns the current object and then increments the value.

This example demonstrates overloading for both forms of the `++` operator.

```cpp
#include <iostream>
using namespace std;
class Counter{
    private:
    static int count;
    int cnt;
    public:
    Counter operator ++ (int){
        Counter temp = *this;
        count++;
        cnt=count;
        return temp;
    }
    void display(){
        cout << cnt << endl;
    }
};
int Counter::count =0;
int main() {
    // Write C++ code here
    Counter obj;
    obj.display();       // output: 0
    (obj++).display();   // output: 0
    obj.display();       // output: 1
    return 0;
}
```

### 32. _Binary Operators (+, -, /, *)_

Binary operators operate on two operands and can be overloaded to work with user-defined types like classes. Operators such as `+`, `-`, `/`, and `*` can be overloaded to perform arithmetic on objects.

**Example**: Overloading the `+` operator for a `Vector` class:
```cpp
class Vector {
    int x, y;
public:
    Vector(int x1 = 0, int y1 = 0) : x(x1), y(y1) {}

    // Overloading the + operator
    Vector operator + (const Vector& obj) {
        return Vector(x + obj.x, y + obj.y);
    }

    void display() {
        cout << "Vector: (" << x << ", " << y << ")" << endl;
    }
};

int main() {
    Vector v1(1, 2), v2(3, 4);
    Vector v3 = v1 + v2;  // Overloaded + operator
    v3.display();  // Output: Vector: (4, 6)
}
```
In this example, the `+` operator is overloaded to add the components of two vectors.

### 33. **Binary Operators Using Friend Functions**

A **friend function** can be used to overload binary operators when the left-hand operand isn't necessarily an object of the class (for instance, if you want to allow expressions like `5 + obj`). Friend functions are not members of the class but can access private members.

**Example**: Overloading the `-` operator using a friend function:
```cpp
class Complex {
    int real, imag;
public:
    Complex(int r = 0, int i = 0) : real(r), imag(i) {}

    // Friend function to overload the - operator
    friend Complex operator - (const Complex& c1, const Complex& c2);

    void display() {
        cout << real << " + " << imag << "i" << endl;
    }
};

// Friend function definition
Complex operator - (const Complex& c1, const Complex& c2) {
    return Complex(c1.real - c2.real, c1.imag - c2.imag);
}

int main() {
    Complex c1(5, 4), c2(2, 3);
    Complex c3 = c1 - c2;  // Calls friend function to overload -
    c3.display();  // Output: 3 + 1i
}
```
Here, the `-` operator is overloaded using a friend function to subtract two `Complex` objects.

### 34. **Manipulation of Strings Using Overloaded Operators (>, <,=\=)**
- Operators like >,<,== can be overloaded to compare two strings or user-defined objects.

**Example**: Overloading comparison operators for a `String` class:
```cpp
#include <cstring>
class String {
    char* str;
public:
    String(const char* s = "") {
        str = new char[strlen(s) + 1];
        strcpy(str, s);
    }

    // Overloading the == operator
    bool operator == (const String& s) const {
        return strcmp(str, s.str) == 0;
    }

    // Overloading the < operator
    bool operator < (const String& s) const {
        return strcmp(str, s.str) < 0;
    }

    // Overloading the > operator
    bool operator > (const String& s) const {
        return strcmp(str, s.str) > 0;
    }

    void display() {
        cout << str << endl;
    }

    ~String() {
        delete[] str;  // Free allocated memory
    }
};

int main() {
    String s1("Hello"), s2("World");

    if (s1 == s2) {
        cout << "Strings are equal" << endl;
    } else if (s1 > s2) {
        cout << "First string is greater" << endl;
    } else {
        cout << "Second string is greater" << endl;
    }

    return 0;
}
```


### 35. Type Conversion: 
#### Basic type to class type 
In C++, converting a basic data type (like int , float , etc.) to a class type is achieved by writing a constructor in the class that takes a basic data type as an argument. This way, when you assign a basic type to an object of the class, the constructor automatically converts the basic type to the class type.

```cpp
#include <iostream> 
using namespace std; 
class Distance { 
	private: 
	int meters; 
	public: 
	// Constructor that converts an int to a Distance object 
	Distance(int m) { 
		meters = m; 
	} 
	// A function to display the distance 
	void display() { 
		cout << "Distance: " << meters << " meters" << endl; 
	} 
}; 
int main() { 
	int distanceInMeters = 10; 
	// This calls the constructor and converts int to Distance 
	Distance d = distanceInMeters; 
	d.display();  // Output: Distance: 10 meters 
	return 0; 
}
```

#### Class type to Basic type 
In C++, converting a class type to a basic type (like int , float , etc.) is done by defining a type conversion function in the class. This function tells the compiler how to convert an object of the class to a basic data type.

```cpp
#include <iostream>
using namespace std;
class Distance
{
private:
    int meters;

public:
    // Constructor to initialize the distance
    Distance(int m)
    {
        meters = m;
    }
    // Conversion operator to convert Distance to int
    operator int()
    {
        return meters; // Returns the value of meters as an int
    }
    // A function to display the distance
    void display()
    {
        cout << "Distance: " << meters << " meters" << endl;
    }
};
int main()
{
    Distance d(15); // Creating a Distance object with 15 meters
    // Converting class type (Distance) to basic type (int)
    int distanceInMeters = d;                                   // Calls the conversion operator
    cout << "Distance in meters: " << distanceInMeters << endl; // Output:
    15 return 0;
}
```

#### Class to class Type Conversion: 
In C++, converting from one class type to another is done using constructors or conversion operators. This process allows an object of one class to be converted into an object of another class.

```cpp
#include <iostream> 
using namespace std; 
class DistanceInMeters { 
	private: 
	int meters; 
	public: 
	// Constructor to initialize meters 
	DistanceInMeters(int m) { 
		meters = m; 
	} 
	// A function to get the value of meters 
	int getMeters() const { 
		return meters; 
	} 
}; 
class DistanceInKilometers { 
	private: 
	float kilometers; 
	public: 
	// Constructor to initialize kilometers from a DistanceInMeters object 
	DistanceInKilometers(const DistanceInMeters& dm) { 
		kilometers = dm.getMeters() / 1000.0;  // Convert meters to kilometers 
	} 
	// A function to display the distance in kilometers 
	void display() { 
		cout << "Distance: " << kilometers << " kilometers" << endl; 
	} 
}; 
int main() { 
	DistanceInMeters distanceInMeters(1500);  // 1500 meters 
	// Convert DistanceInMeters object to DistanceInKilometers object 
	DistanceInKilometers distanceInKilometers = distanceInMeters; 
	distanceInKilometers.display();  // Output: Distance: 1.5 kilometers 
	return 0; 
}
```

### 36.Pointers
#### 1. Accessing the Address of a Variable: 
Every variable in C++ is stored at a specific memory location. You can access the memory address of a variable using the address-of operator ( & ).

#### 2. Declaring and Initializing Pointers: 
To declare a pointer in C++, you use the * symbol just like in C.

#### 3. Accessing a Variable Through Its Pointer: 
You can access the value of the variable that pointer points to using the dereference operator (\*) .

```cpp
#include <iostream> 
using namespace std; 
	int main() { 
	int a = 10;   // Declare an integer variable 
	int *p = &a;  // Declare and initialize a pointer to 'a' 
	// Access and print the address of 'a' 
	cout << "Address of a: " << &a << endl; 
	// Print the address stored in pointer 'p' 
	cout << "Address stored in pointer p: " << p << endl; 
	// Access and print the value of 'a' through pointer 'p' 
	cout << "Value of a (through pointer p): " << *p << endl; 
	// Modify the value of 'a' using the pointer 
	*p = 100; 
	// Print the modified value of 'a' 
	cout << "Modified value of a: " << a << endl; 
	return 0; 
} 
```

#### 4.Pointer Arithmetic: 
Pointer arithmetic is the process of modifying the memory address that a pointer holds. You can increment or decrement pointers, or perform addition and subtraction, but the operations depend on the size of the data type the pointer is pointing to. When you increment a pointer, it moves by the size of the data type it points to (e.g., if the pointer points to an integer, incrementing it moves the address by `sizeof(int)` bytes).

```cpp
#include <iostream> 
using namespace std; 
int main() { 
	int arr[] = {10, 20, 30, 40, 50}; 
	int *p = arr;  // Pointer pointing to the first element of 
	the array 
	// Access elements of the array using pointer 
	arithmetic 
	cout << "Value at p (arr[0]): " << *p << endl; 
	p++;  // Increment pointer (moves to the next element) 
	cout << "Value at p (arr[1]): " << *p << endl; 
	p += 2;  // Increment by 2 (moves to the third element) 
	cout << "Value at p (arr[3]): " << *p << endl; 
	return 0; 
} 
```

#### 5.Pointer to a Pointer: 
A pointer to a pointer (or double pointer) is a pointer that stores the address of another pointer. It allows you to indirectly access and modify variables through multiple levels of indirection.

```cpp
#include <iostream> 
using namespace std; 
int main() { 
	int a = 10; 
	int *p = &a;   // Pointer to an integer 
	int **pp = &p; // Pointer to a pointer 
	// Accessing the value of 'a' using pointer to pointer 
	cout << "Value of a: " << a << endl; 
	cout << "Value of a (using *p): " << *p << endl; 
	cout << "Value of a (using **pp): " << **pp << endl; 
	// Modifying the value of 'a' using pointer to pointer 
	**pp = 20; 
	cout << "Modified value of a: " << a << endl; 
	return 0; 
} 
```

####  6.Pointer to a Function:
A pointer to a function is a pointer that stores the address of a function. Function pointers can be used to call functions dynamically or to pass functions as arguments to other functions.

```cpp
#include <iostream> 
using namespace std; 
// Function to add two numbers 
int add(int a, int b) { 
	return a + b; 
} 
// Function to subtract two numbers 
int subtract(int a, int b) { 
	return a - b; 
} 
// Function that takes a pointer to a function as a parameter 
void calculate(int (*func_ptr)(int, int), int x, int y) { 
	cout << "Result: " << func_ptr(x, y) << endl; 
} 
int main() { 
// Declare a pointer to a function that takes two integers and returns an integer 
	int (*func_ptr)(int, int); 
	// Point the function pointer to the 'add' function 
	func_ptr = add; 
	cout << "Calling add via function pointer: " << 
	func_ptr(10, 20) << endl; 
	// Point the function pointer to the 'subtract' function 
	func_ptr = subtract; 
	cout << "Calling subtract via function pointer: " << 
	func_ptr(30, 10) << endl; 
	// Pass function pointers as arguments 
	calculate(add, 50, 20); 
	calculate(subtract, 50, 20); 
	return 0; 
}
```

- `int (*func_ptr)(int, int)` declares a pointer to a function that takes two int parameters and returns an int . 
- `func_ptr = add` assigns the address of the add function to the pointer. 
- `func_ptr(x, y)` calls the function via the pointer. 
- The calculate function takes a function pointer as an argument and calls the function dynamically.

### 37.Dynamic memory management
In C++, dynamic memory management is crucial for managing memory during runtime. The new and delete operators, pointers with classes, pointers to objects, and pointers to members are all important concepts for managing and accessing memory efficiently

#### new and delete Operators
- `new operator`: Allocates memory on the heap. 
- `delete operator`: Deallocates memory that was dynamically allocated using new.

```cpp
#include <iostream>
using namespace std;
int main()
{
    // Dynamic allocation of an integer
    int *p = new int; // Allocates memory for an integer on the heap
    *p = 10; // Assigns a value to the allocated memory
    cout<< "Value of p: " << *p << endl; // Accessing the value through the pointer
        // Deallocating the memory
    delete p;
    // Dynamic allocation of an array
    int *arr = new int[5]; // Allocates memory for an array of 5 integers 
    for (int i = 0; i < 5; i++)
    {
        arr[i] = i + 1; // Assigning values to the array
    }
    cout << "Array values: ";
    for (int i = 0; i < 5; i++)
    {
        cout << arr[i] << " ";
    }
    cout << endl;
    // Deallocating the array
    delete[] arr;
    return 0;
}
```

#### Pointers and Classes:
Pointers can also be used with classes to dynamically allocate objects and access their members.

```cpp
#include <iostream> 
using namespace std; 
class Student { 
	public: 
	string name; 
	int age; 
	// Constructor 
	Student(string n, int a) : name(n), age(a) {} 
	// Method to display student details 
	void display() { 
	cout << "Name: " << name << ", Age: " << age << endl; 
} 
}; 
int main() { 
	// Dynamically creating a Student object 
	Student *s = new Student("John", 20); 
	// Accessing class members using the pointer 
	s->display(); 
	// Deallocating memory 
	delete s; 
	return 0; 
}
```

#### Pointer to an Object: 
A pointer to an object is used to dynamically allocate memory for an object and access its members using the arrow operator ( -> ).

```cpp
#include <iostream>
using namespace std;
class Car
{
public:
    string model;
    int year;
    // Constructor
    Car(string m, int y) : model(m), year(y) {}
    // Method to display car details
    void showDetails()
    {
        cout << "Model: " << model << ", Year: " << year << endl;
    }
};
int main()
{
    // Dynamically creating an object of Car class
    Car *carPtr = new Car("Tesla", 2023);
    // Accessing object members using pointer
    carPtr->showDetails();
    // Deallocating memory
    delete carPtr;
    return 0;
}
```

#### Pointer to a Member:
A pointer to a member is used to point to a specific member (data member or function) of a class. This allows indirect access to class members through pointers.

```cpp
#include <iostream>
using namespace std;
class Employee
{
public:
    string name;
    int salary;
    // Constructor
    Employee(string n, int s) : name(n), salary(s) {}
    // Method to display employee details
    void display()
    {
        cout << "Name: " << name << ", Salary: " << salary << endl;
    }
};
int main()
{
    // Creating an object of Employee class
    Employee emp("Alice", 50000);
    // Pointer to a data member
    int Employee::*ptrSalary = &Employee::salary;
    // Accessing the data member through pointer to member
    cout << "Employee salary (using pointer to member): " << emp.*ptrSalary << endl;
    // Pointer to a member function
    void (Employee::*ptrDisplay)() = &Employee::display;
    // Calling the member function through pointer to member function
    (emp.*ptrDisplay)();
    return 0;
}
```

`int Employee::*ptrSalary = &Employee::salary` is a pointer to the salary member of the Employee class. 
`void (Employee::*ptrDisplay)()= &Employee::display` is a pointer to the display method. 
`emp.*ptrSalary` accesses the salary member using the pointer to member. 
`(emp.*ptrDisplay)()` calls the display method using the pointer to the member function.

#### this Pointer
In C++, the this pointer is used in member functions to refer to the object for which the member function is called. It allows access to the invoking object’s members.

```cpp
#include <iostream>
using namespace std;
class Example
{
    int x;

public:
    Example(int x)
    {
        this->x = x; // 'this' points to the current object
    }
    void display()
    {
        cout << "Value of x: " << this->x << endl;
    }
};
int main()
{
    Example obj(10);
    obj.display(); // Output: Value of x: 10
    return 0;
}
```

In this example, the this pointer is used to distinguish between the parameter x and the class member variable x .
#### Dangling Pointer
Dangling pointers are variables which stores memory addresses that points to garbage after being deleted.

```cpp
#include <iostream>
using namespace std;
int main()
{
    int *ptr = new int(10);// dynamically allocate memory and assign value 10 
    cout << "Value: " << *ptr << endl; // Output: 10
    delete ptr; // deallocate memory
// Now, 'ptr' is a dangling pointer because the memory it was pointing to is freed
    cout << "Dangling Pointer Value: " << *ptr << endl; //Undefined behavior !
    return 0;
}
```

#### Wild Pointer
A wild pointer is a pointer that has not been initialized to anything, i.e., it contains some random address. Dereferencing such pointers leads to a crash or undefined behavior.

```cpp
#include <iostream> 
using namespace std; 
int main() { 
	int* ptr;  // Wild pointer (uninitialized) 
	cout << *ptr << endl;  // Undefined behavior 
	return 0; 
} 
```

#### Null Pointer Assignment
A null pointer is a pointer that points to nothing. It’s often initialized with `nullptr` to avoid wild pointers. Dereferencing a null pointer causes a runtime error (segmentation fault).

```cpp
#include <iostream> 
using namespace std; 
int main() { 
	int* ptr = nullptr;  // Null pointer 
	if (ptr == nullptr) { 
		cout << "Pointer is null, can't dereference!" << endl; 
	} else { 
		cout << *ptr << endl;  // Runtime error if dereferenced 
	} 
	return 0; 
}
```
In this example, the pointer ptr is assigned nullptr , and we check before dereferencing to avoid a crash.

#### Memory Leak
A memory leak occurs when dynamically allocated memory is not properly freed, leading to wasted memory resources.

```cpp
#include <iostream> 
using namespace std; 
void memoryLeak() { 
	int* ptr = new int(10);  // Dynamically allocated memory 
// Forgetting to free the memory (delete ptr) leads to a memory leak 
} 
int main() { 
	memoryLeak(); 
	return 0; 
}
```

In this case, the allocated memory using new is not freed with delete , resulting in a memory leak.

#### Allocation Failure
Memory allocation failure happens when the system runs out of memory, and new fails to allocate memory. In C++, new throws an exception when it fails to allocate memory.

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "Before allocation" << endl;
    try
    {
        int *ptr = new int[100000000000]; // Large allocation request
        cout << "Allocation succeeded" << endl;
    }
    catch (bad_alloc &e)
    {
        cout << "Memory allocation failed: " << e.what() << endl;
    }
    cout << "After allocation" << endl;
    return 0;
}
```




```cpp
// To add a number with itself
#include <iostream>
using namespace std;

class prac{

  public:
  int  t;
  prac(int a){
      t = a;
  }
  operator int(){
      return t;
  }
  void display(){
      cout << t << endl;
  }
};
int main() {
    // Write C++ code here
    int ans;
    prac *obj = nullptr;
    obj = new prac(12);
    int prac::*ptr = &prac::t;
    obj->*ptr += (*obj).*ptr;
    ans = *obj;
    cout << ans;
    return 0;
}
```

### 38.Inheritance
#### Introduction: Concept of Reuse in Object-Oriented Programming (OOP) 
In Object-Oriented Programming (OOP), one of the key concepts is reuse . Reuse refers to the ability to utilize existing code or classes to reduce redundancy, minimize errors, and enhance productivity. Reuse is accomplished through inheritance, where a new class (called a derived class) inherits properties and behaviors from an existing class (called a base class or superclass). This way, programmers can avoid writing similar code multiple times by reusing the code from already created classes.

#### Defining Derived Classes 
Defining derived classes in C++ is the process of creating a new class that inherits properties and behaviors from an existing class (called the base class). The derived class can either use or modify the base class's attributes and methods, and it can also add new ones specific to its purpose.

Syntax:
```cpp
class DerivedClassName : accessSpecifier BaseClassName { 
// Body of the derived class 
}; 
```

#### Forms of inheritance (single, multilevel, multiple, hybrid & hierarchical)
In object-oriented programming (OOP), inheritance is a key concept that allows one class to inherit the properties (fields) and behaviors (methods) of another class. It promotes code reuse, making systems more modular and easier to maintain. There are several types of inheritance based on how classes are related to one another. Below are the detailed explanations of each form of inheritance:
#### Single Inheritance 
In single inheritance, a class (child class or subclass) inherits from only one parent class (superclass). This is the most straightforward form of inheritance.

```cpp
#include <iostream>
using namespace std;
class Animal
{
public:
    void eat()
    {
        cout << "Eating...\n";
    }
};
class Dog : public Animal
{
public:
    void bark()
    {
        cout << "Barking...\n";
    }
};
int main()
{
    Dog myDog;
    myDog.eat();  // Inherited from Animal
    myDog.bark(); // Specific to Dog
    return 0;
}
```

Key Points: 
- Simple structure.
- Easy to implement and understand.
- Limits flexibility because a subclass can only inherit from one superclass

#### Multilevel Inheritance 
In multilevel inheritance , a class derives from a child class, forming a chain of inheritance across multiple levels.

```cpp
#include <iostream>
using namespace std;
class Animal
{
public:
    void eat()
    {
        cout << "Eating...\n";
    }
};
class Dog : public Animal
{
public:
    void bark()
    {
        cout << "Barking...\n";
    }
};
class Puppy : public Dog
{
public:
    void weep()
    {
        cout << "Weeping...\n";
    }
};
int main()
{
    Puppy myPuppy;  // Creating an object of Puppy class
    myPuppy.eat();  // Inherited from Animal class
    myPuppy.bark(); // Inherited from Dog class
    myPuppy.weep(); // Specific to Puppy class
    return 0;
}
```

Key Points: 
- Inherits across multiple levels of the hierarchy. 
- Allows a subclass to inherit features from its parent and grandparent classes. 
- Can sometimes make debugging harder if there are multiple levels of inheritance.

#### Multiple Inheritance 
In multiple inheritance , a class can inherit from more than one base class. This allows a class to combine the functionality of multiple classes.

```cpp
#include <iostream>
using namespace std;
class Engine
{
public:
    void engineStart()
    {
        cout << "Engine Starting...\n";
    }
};
class Wheel
{
public:
    void rotate()
    {
        cout << "Wheels Rotating...\n";
    }
};
class Car : public Engine, public Wheel
{
public:
    void drive()
    {
        cout << "Car Driving...\n";
    }
};
int main()
{
    Car myCar;           // Create an object of Car class
    myCar.engineStart(); // Call method from Engine class
    myCar.rotate();      // Call method from Wheel class
    myCar.drive();       // Call method from Car class
    return 0;
}
```

Key Points: 
- Increases flexibility by allowing a class to use features from multiple classes.
- It can lead to a problem known as the diamond problem , where the ambiguity arises if the same method is inherited from multiple parent classes (often handled using virtual inheritance in C++).

#### Hybrid Inheritance 
Hybrid inheritance is a combination of more than one type of inheritance. It can be a mix of single, multiple, and multilevel inheritance.

```cpp
#include <iostream>
using namespace std;
class Vehicle
{
public:
    void start()
    {
        cout << "Vehicle Starting...\n";
    }
};
// Use virtual inheritance to avoid multiple instances of
Vehicle class Car : virtual public Vehicle
{
public:
    void drive()
    {
        cout << "Car Driving...\n";
    }
};
class Truck : virtual public Vehicle
{
public:
    void loadCargo()
    {
        cout << "Loading Cargo...\n";
    }
};
class Hybrid : public Car, public Truck
{
public:
    void hybridDrive()
    {
        cout << "Hybrid Driving...\n";
    }
};
int main()
{
    Hybrid myHybrid; // Create an object of the Hybrid
    class
        myHybrid.start(); // Call the start() method from
    Vehicle class
        myHybrid.drive(); // Call the drive() method from Car
    class
        myHybrid.loadCargo(); // Call the loadCargo() method from
    Truck class
        myHybrid.hybridDrive(); // Call the hybridDrive() method
    from Hybrid class
        return 0;
}
```
Here,  Hybrid  inherits from both  Car  and  Truck , which  themselves inherit from 
Vehicle . This creates a combination of single, multilevel,  and multiple inheritance.

Key Points: 
- Offers the most flexibility by combining different inheritance types. 
- Careful design is required to avoid complexity and ambiguity, especially with diamond problems.

#### Hierarchical Inheritance
In hierarchical inheritance , multiple child classes inherit from a single parent class.

```cpp
#include <iostream>
using namespace std;
class Animal
{
public:
    void eat()
    {
        cout << "Eating...\n";
    }
};
class Dog : public Animal
{
public:
    void bark()
    {
        cout << "Barking...\n";
    }
};
class Cat : public Animal
{
public:
    void meow()
    {
        cout << "Meowing...\n";
    }
};
int main()
{
    Dog myDog;    // Creating an object of Dog class
    Cat myCat;    // Creating an object of Cat class
    myDog.eat();  // Inherited from Animal
    myDog.bark(); // Specific to Dog
    myCat.eat();  // Inherited from Animal
    myCat.meow(); // Specific to Cat
    return 0;
}
```


Key Points: 
- Useful when multiple classes share common functionality from a single base class. 
- Allows easy scalability since new subclasses can inherit from the parent class. 
- If the base class is changed, all derived classes are affected.


#### Diamond Problem
`Ambiguity in multiple and multipath inheritance`

The Diamond Problem is a common issue encountered in multiple inheritance in object-oriented programming, specifically when two classes inherit from the same base class, and a third class inherits from both of them. 
#### The Problem: 
In multiple inheritance , when a class inherits from more than one class, there can be ambiguity if the same member (like a function or variable) is inherited from more than one base class. This often happens when both parent classes are derived from the same grandparent class, creating a diamond-shaped inheritance structure.

```cpp
#include <iostream>
using namespace std;
class A
{
public:
    void show()
    {
        std::cout << "Class A\n";
    }
};
class B : public A
{
    // Class B inherits from A
};
class C : public A
{
    // Class C inherits from A
};
class D : public B, public C
{
    // Class D inherits from both B and C
};
int main()
{
    D obj;
    obj.show(); // ERROR: Ambiguity!
    return 0;
}
```
Now, if we try to call the show() method from an object of Class D , the compiler gets confused because D has two copies of the show() method — one from B (which comes from A ), and one from C (which also comes from A ).


#### Solving the Diamond Problem with Virtual Inheritance:
We can use virtual inheritance to solve this problem. By marking the inheritance of A as virtual in both B and C , we tell the compiler to share a single instance of A between B and C , and thus D will only inherit one copy of A .

```cpp
#include <iostream>
using namespace std;
class A
{
public:
    void show()
    {
        std::cout << "Class A\n";
    }
};
class B : public virtual A
{
    // Class B virtually inherits from A
};
class C : public virtual A
{
    // Class C virtually inherits from A
};
class D : public B, public C
{
    // Class D inherits from both B and C
};
int main()
{
    D obj;
    obj.show(); // Works fine, no ambiguity
    return 0;
}
```

Explanation of the Solution:
- By using virtual before A in both B and C , we ensure that only one instance of A is inherited by D . 
- When D calls the show() method, it knows exactly which show() function to call, because there is only one copy of A .


#### Inheritance with constructor
In C++, inheritance allows a class (child class) to inherit properties and behavior from another class (parent class). When inheritance involves constructors, the constructor of the parent class is called automatically when an object of the child class is created. If we want to control how the parent constructor is called, we can use an initializer list in the child class constructor.

```cpp
#include <iostream>
using namespace std;
class Parent
{
public:
    int x;
    // Constructor of the parent class
    Parent(int a)
    {
        x = a;
        cout << "Parent constructor called. x = " << x << endl;
    }
};
class Child : public Parent
{
public:
    int y;
    // Constructor of the child class
    Child(int a, int b) : Parent(a)
    {
        // Calling Parent constructor explicitly
        y = b;
        cout << "Child constructor called. y = " << y << endl;
    }
};
int main()
{
    Child obj(10, 20); // This will call both Parent and Child
    constructors return 0;
}
```

Explanation: 
- The Parent constructor is called with the value 10 before the Child constructor is executed. 
- The initializer list : Parent(a) calls the parent constructor explicitly when creating a Child object.

### 39.Function Overriding
Function overriding occurs when a function in a child class has the same name and parameters as a function in the parent class, but it redefines the behavior. The overridden function in the child class is called instead of the parent’s version.

```cpp
#include <iostream>
using namespace std;
class Parent
{
public:
    void show()
    {
        cout << "This is the Parent class function." << endl;
    }
};
class Child : public Parent
{
public:
    void show()
    { // Overriding the Parent's function
        cout << "This is the Child class function." << endl;
    }
};
int main()
{
    Parent p;
    p.show(); // Calls Parent's function
    Child c;
    c.show(); // Calls Child's overridden function
    return 0;
}
```

Explanation: 
- The show() function in Child class overrides the show() function in Parent . When you call `c.show()` , the child class function is executed.

### 40.Function Overloading
Function overloading is a feature in C++ where two or more functions can have the same name but differ in the number or types of parameters. Overloaded functions must differ in their signatures.

```cpp
#include <iostream>
using namespace std;
class Example
{
public:
    // Overloaded functions with different signatures
    void show(int a)
    {
        cout << "Integer: " << a << endl;
    }
    void show(double b)
    {
        cout << "Double: " << b << endl;
    }
    void show(string c)
    {
        cout << "String: " << c << endl;
    }
};
int main()
{
    Example obj;
    obj.show(10);      // Calls show(int)
    obj.show(5.7);     // Calls show(double)
    obj.show("Hello"); // Calls show(string)
    return 0;
}
```

### 41.Binding
Binding refers to the process of converting identifiers (such as variable and performance names) into addresses. Binding is done for each variable and function. For functions, it means matching the call with the right function definition by the compiler. It takes place either at compile time or at runtime.

#### Static Binding (Early Binding)
Static binding occurs at compile-time, meaning the function to be called or the value of the variable is determined before the program is executed. The compiler knows exactly which function to call based on the function signature, so no runtime decision-making is required. This is also referred to as early binding.

```cpp
#include <iostream>
using namespace std;
class A
{
public:
    void show()
    {
        cout << "Class A";
    }
};
class B : public A // inherting class A on B
{
	public:
	void show()
	{
	    cout << "Class B";
	}
};


int main()
{
    A *bptr; // pointer of A class
    A aa;    // object of A(base) class
    //  B aa; // object of B(derived) class
    bptr = &aa; // refering aa object to the bptr pointer
    bptr->show();
    return 0;
}
```


#### Dynamic Binding (Late Binding)
Dynamic binding occurs at runtime, meaning the exact function to be called is determined during the execution of the program. This usually happens in the context of polymorphism with virtual functions. Dynamic binding is also called late binding or runtime binding. 

Dynamic binding uses virtual functions and pointers or references to the base class to achieve runtime decision-making.

```cpp
#include <iostream>
using namespace std;
class A
{
public:
    void virtual show()
    {
        cout << "Class A";
    }
};
class B : public A // inherting class A on B
{
public:
    void show()
    {
        cout << "Class B";
    }
};
int main()
{
    A *bptr; // pointer of A class
    A aa;    // object of A(base) class
    // B aa; // object of B(derived) class
    bptr = &aa; // refering aa object to the bptr pointer
    bptr->show();
    return 0;
}
```

### 42.Virtual Function vs Pure Virtual functions
The virtual keyword in C++ is used to define virtual functions, which enable runtime polymorphism. Virtual functions allow derived classes to override functions in a base class and provide their own implementations. When a function is marked as virtual , the decision of which function to call is made at runtime based on the type of the object being pointed to, rather than at compile time. This concept is at the heart of dynamic binding or late binding , where the actual method invoked depends on the type of the object rather than the type of the reference or pointer.
![[Pasted image 20241017092514.png]]


### 43.**Abstract Classes**
An abstract class is a class that cannot be instantiated and serves as a blueprint for derived classes. It contains at least one pure virtual function.

```cpp
#include <iostream>
using namespace std;

// Abstract class
class Shape {
public:
    virtual void draw() = 0; // Pure virtual function
    virtual ~Shape() {} // Virtual destructor
};

// Derived class
class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing Circle" << endl;
    }
};

// Derived class
class Square : public Shape {
public:
    void draw() override {
        cout << "Drawing Square" << endl;
    }
};

int main() {
    Shape* shape1 = new Circle();
    Shape* shape2 = new Square();

    shape1->draw(); // Drawing Circle
    shape2->draw(); // Drawing Square

    delete shape1;
    delete shape2;
    return 0;
}
```

### 44.**Virtual Destructors and Polymorphism**

Virtual destructors ensure that when deleting an object through a base class pointer, the derived class's destructor is also called, avoiding resource leaks.

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual ~Base() {
        cout << "Base Destructor" << endl;
    }
};

class Derived : public Base {
public:
    ~Derived() {
        cout << "Derived Destructor" << endl;
    }
};

int main() {
    Base* obj = new Derived();
    delete obj; // Derived Destructor followed by Base Destructor
    return 0;
}
```

OUTPUT:
![[Pasted image 20241120184845.png|150]]

### 45.**Order of Execution of Virtual Functions**
Virtual function calls are resolved at runtime based on the actual type of the object, not the type of the pointer/reference.

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void show() {
        cout << "Base class show" << endl;
    }
    virtual ~Base() {}
};

class Derived : public Base {
public:
    void show() override {
        cout << "Derived class show" << endl;
    }
};

int main() {
    Base* obj = new Derived();
    obj->show(); // Derived class show
    delete obj;
    return 0;
}
```


### 46.**Overriding Member Functions**
Function overriding occurs when a derived class provides a specific implementation for a virtual function of the base class.

**Without `virtual` Keyword:**

- If you define a function with the same name and signature in a derived class without declaring the base class function as `virtual`, it will **hide** the base class function, not override it.
- This means that function calls are resolved at **compile-time** based on the type of the object reference, not the actual type of the object.

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void display() {
        cout << "Base class display" << endl;
    }
};

class Derived : public Base {
public:
    void display() override { // Overriding the base class function
        cout << "Derived class display" << endl;
    }
};

int main() {
    Base* obj = new Derived();
    obj->display(); // Derived class display
    delete obj;
    return 0;
}
```

### 47.**Accessing Base Class Functions**
When a derived class overrides a base class function, the base class version can still be accessed explicitly using the `scope resolution operator (::)`.

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    void display() {
        cout << "Base class display" << endl;
    }
};

class Derived : public Base {
public:
    void display() {
        cout << "Derived class display" << endl;
    }

    void showBaseDisplay() {
        Base::display(); // Accessing base class function
    }
};

int main() {
    Derived obj;
    obj.display();       // Derived class display
    obj.showBaseDisplay(); // Base class display
    return 0;
}
```

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void display() {
        cout << "Base class display" << endl;
    }
    virtual void showBaseDisplay() = 0;
};

class Derived : public Base {
public:
    void display() override {
        cout << "Derived class display" << endl;
    }

    void showBaseDisplay() {
        Base::display(); // Accessing base class function
    }
};

int main() {
    Base *obj;
    obj = new Derived;
    obj->display();
    obj->showBaseDisplay();
    return 0;
}
```


### 48.**Order of Execution of Constructors and Destructors**
Constructors are called in the order of inheritance (base class first, then derived class), while destructors are called in the reverse order.

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    Base() {
        cout << "Base Constructor" << endl;
    }
    ~Base() {
        cout << "Base Destructor" << endl;
    }
};

class Derived : public Base {
public:
    Derived() {
        cout << "Derived Constructor" << endl;
    }
    ~Derived() {
        cout << "Derived Destructor" << endl;
    }
};

int main() {
    Derived obj;
    // Output:
    // Base Constructor
    // Derived Constructor
    // Derived Destructor
    // Base Destructor
    return 0;
}
```


### 49.**Review of Traditional Error Handling**
Before exception handling, errors were managed using return codes or flags, making error management cumbersome and less intuitive.

```cpp
#include <iostream>
using namespace std;

int divide(int a, int b) {
    if (b == 0) {
        return -1; // Error code
    }
    return a / b;
}

int main() {
    int result = divide(10, 0);
    if (result == -1) {
        cout << "Division by zero error" << endl;
    } else {
        cout << "Result: " << result << endl;
    }
    return 0;
}
```


### 50.**Basics of Exception Handling**
Exception handling uses `try`, `catch`, and `throw` keywords for managing runtime errors in a structured way.

```cpp
#include <iostream>
using namespace std;

int main() {
    try {
        int a = 10, b = 0;
        if (b == 0)
            throw runtime_error("Division by zero error");
        cout << "Result: " << a / b << endl;
    } catch (const exception& e) {
        cout << "Exception: " << e.what() << endl;
    }
    return 0;
}
```


### 51.**Exception Handling Mechanism**

The **exception handling mechanism** involves three key parts:

1. **Throwing an exception:** The `throw` keyword is used to signal an error.
2. **Catching an exception:** The `catch` block handles the thrown exception.
3. **Termination of the `try` block:** Once an exception is thrown, the `try` block terminates.

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

void divide(int a, int b) {
    if (b == 0) 
        throw runtime_error("Cannot divide by zero.");
    cout << "Result: " << a / b << endl;
}

int main() {
    try {
        divide(10, 0);
    } catch (const runtime_error& e) {
        cout << "Caught exception: " << e.what() << endl;
    }
    return 0;
}                                                                       
```

#### **Throwing Mechanism**
The `throw` keyword is used to signal that an error has occurred. It can throw built-in or user-defined exceptions.

```cpp
#include <iostream>
using namespace std;

void checkAge(int age) {
    if (age < 18) 
        throw "Age must be 18 or older!";
}

int main() {
    try {
        checkAge(16);
    } catch (const char* msg) {
        cout << "Error: " << msg << endl;
    }
    return 0;
}
```

#### **Catching Mechanism**
The `catch` block handles exceptions. It can be specific (for certain exception types) or generic (`catch(...)`).

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    try {
        throw string("A string exception");
    } catch (const string& e) {
        cout << "Caught: " << e << endl;
    } catch (...) {
        cout << "Caught an unknown exception" << endl;
    }
    return 0;
}
```


#### **Re-Throwing an Exception**
You can re-throw an exception using the `throw` keyword inside a `catch` block if you want to propagate the exception for further handling.

```cpp
#include <iostream>
using namespace std;

void func() {
    try {
        throw runtime_error("Error in func");
    } catch (...) {
        cout << "Handling in func, re-throwing..." << endl;
        throw; // Re-throwing exception
    }
}

int main() {
    try {
        func();
    } catch (const runtime_error& e) {
        cout << "Caught in main: " << e.what() << endl;
    }
    return 0;
}
```

#### **Specifying Exceptions**
In older C++ versions, you could specify the type of exceptions a function could throw using the `throw()` specifier. In modern C++ (from C++11), this is replaced with `noexcept`.
1. **Declaration of `safeFunc`**:
    
    - The function is marked with `noexcept`, meaning the compiler knows it will not throw exceptions. This helps during optimization and allows calling code to safely handle it without exception-handling overhead.
2. **Usage in `main`**:
    
    - `safeFunc` is called like any other function. The `noexcept` specifier does not affect how the function is used but rather ensures its internal behavior.

```cpp
#include <iostream>
using namespace std;

void safeFunc() noexcept {
    cout << "This function won't throw exceptions." << endl;
}

int main() {
    safeFunc();
    return 0;
}
```

### 52**Problems on Recursion**

#### Problem: Calculate Factorial Using Recursion
```cpp
#include <iostream>
using namespace std;

int factorial(int n) {
    if (n <= 1) 
        return 1;
    return n * factorial(n - 1);
}

int main() {
    int num = 5;
    cout << "Factorial of " << num << " is " << factorial(num) << endl; // Output: 120
    return 0;
}
```

#### Problem: Fibonacci Series Using Recursion
```cpp
#include <iostream>
using namespace std;

int fibonacci(int n) {
    if (n <= 1) 
        return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int terms = 5;
    for (int i = 0; i < terms; i++) {
        cout << fibonacci(i) << " ";
    }
    return 0; // Output: 0 1 1 2 3
}
```


### 53.**Concept of Streams**

Streams are used for input and output in C++. `cin` and `cout` are the most common examples. Overloading `>>` and `<<` operators allows custom classes to work with these streams.

#### **Example: Overloading `>>` and `<<`**
```cpp
#include <iostream>
using namespace std;

class Point {
    int x, y;
public:
    friend ostream& operator<<(ostream& out, const Point& p);
    friend istream& operator>>(istream& in, Point& p);
};

ostream& operator<<(ostream& out, const Point& p) {
    out << "(" << p.x << ", " << p.y << ")";
    return out;
}

istream& operator>>(istream& in, Point& p) {
    in >> p.x >> p.y;
    return in;
}

int main() {
    Point p;
    cout << "Enter coordinates (x y): ";
    cin >> p;
    cout << "You entered: " << p << endl;
    return 0;
}
```

### 54.**File Streams**
File streams (`ifstream` and `ofstream`) allow file input and output. The hierarchy of file stream classes includes `ios`, `istream`, and `ostream`.
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    ofstream outFile("example.txt");
    if (outFile.is_open()) {
        outFile << "Hello, file!" << endl;
        outFile.close();
    }

    ifstream inFile("example.txt");
    if (inFile.is_open()) {
        string line;
        while (getline(inFile, line)) {
            cout << line << endl; // Output: Hello, file!
        }
        inFile.close();
    }
    return 0;
}
```


### 54.**Error Handling During File Operations**

When performing file operations, it’s crucial to check for errors such as a file not opening, reading from an empty file, or writing to a file without the proper permissions. C++ file streams provide member functions like `fail()`, `bad()`, and `eof()` to handle such scenarios.

#### **Key Functions for Error Handling**:

1. **`fail()`**: Checks if a file operation failed.
2. **`bad()`**: Checks if a non-recoverable error occurred.
3. **`eof()`**: Checks if the end of the file has been reached.
4. **`good()`**: Returns `true` if no errors occurred.

#### **Example: Error Handling in File Operations**
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    ifstream file("nonexistent.txt");

    // Check if the file opened successfully
    if (!file) {
        cout << "Error: File could not be opened!" << endl;
        return 1;
    }

    string content;
    while (file >> content) {
        cout << content << " ";
    }

    // Check if the file operation encountered an error
    if (file.eof()) {
        cout << "\nEnd of file reached." << endl;
    } else if (file.fail()) {
        cout << "\nError: File read operation failed!" << endl;
    }

    file.close();
    return 0;
}
```

### **55.Reading/Writing Files and Accessing Records Randomly**

Random file access allows you to directly move to a specific position in a file to read or write data. This is done using `seekg()` (seek get pointer for reading) and `seekp()` (seek put pointer for writing).
#### **Key Methods**:

1. **`seekg(offset, direction)`**: Moves the file reading pointer.
2. **`seekp(offset, direction)`**: Moves the file writing pointer.
3. **`tellg()`**: Returns the current position of the get pointer.
4. **`tellp()`**: Returns the current position of the put pointer.
#### **Example: Writing and Reading Records Randomly**
```cpp
#include <iostream>
#include <fstream>
using namespace std;

struct Record {
    int id;
    char name[20];
    float salary;
};

int main() {
    fstream file("records.dat", ios::in | ios::out | ios::binary | ios::trunc);

    // Writing records to the file
    Record r1 = {1, "Alice", 5000}, r2 = {2, "Bob", 6000};
    file.write(reinterpret_cast<char*>(&r1), sizeof(r1));
    file.write(reinterpret_cast<char*>(&r2), sizeof(r2));

    // Accessing the second record directly
    file.seekg(sizeof(Record), ios::beg); // Move to the second record
    Record r;
    file.read(reinterpret_cast<char*>(&r), sizeof(r));
    cout << "ID: " << r.id << ", Name: " << r.name << ", Salary: " << r.salary << endl;

    // Modifying the salary of the second record
    r.salary = 7000;
    file.seekp(sizeof(Record), ios::beg); // Move to the second record
    file.write(reinterpret_cast<char*>(&r), sizeof(r));

    // Verifying the update
    file.seekg(sizeof(Record), ios::beg);
    file.read(reinterpret_cast<char*>(&r), sizeof(r));
    cout << "Updated Record -> ID: " << r.id << ", Name: " << r.name << ", Salary: " << r.salary << endl;

    file.close();
    return 0;
}
//output
//ID: 2, Name: Bob, Salary: 6000
//Updated Record -> ID: 2, Name: Bob, Salary: 7000

```

