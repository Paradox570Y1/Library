### Basic Concepts

#### 1. What is a List?

`List` is an ordered collection (also known as a sequence) that allows duplicates. It is part of the Java Collections Framework and is defined in the `java.util` package. `List` maintains the insertion order of elements and provides positional access and insertion of elements.

#### 2. Importing List

Before using `List`, you need to import it from the `java.util` package:

java

Copy code

```java
import java.util.List;
```

#### 3. Creating a List

Since `List` is an interface, you cannot instantiate it directly. Instead, you can use one of its implementing classes, such as `ArrayList`:


```java
List<String> list = new ArrayList<>();
```

#### 4. Adding Elements

You can add elements using the `add()` method:


```java
list.add("Apple"); 
list.add("Banana"); 
list.add("Cherry");
// To add multiple elements in one go
List<Integer> li = new ArrayList<>(Arrays.asList(nums[i],nums[j],nums[k]));
```

#### 5. Accessing Elements

You can access elements using the `get()` method:

```java
String fruit = list.get(0); // "Apple"
```

#### 6. Removing Elements

You can remove elements using the `remove()` method:

```java
list.remove(1); // Removes "Banana"
```

#### 7. Iterating Over Elements

You can iterate over elements using a for loop or an enhanced for loop:

```java
for (int i = 0; i < list.size(); i++) {     
	System.out.println(list.get(i)); 
}  
for (String fruit : list) {     
	System.out.println(fruit); 
}
```

### Intermediate Concepts

#### 8. Other Useful Methods

- `size()`: Returns the number of elements in the list.
- `contains(Object o)`: Checks if the list contains the specified element.
- `isEmpty()`: Checks if the list is empty.
- `clear()`: Removes all elements from the list.
- `indexOf(Object o)`: Returns the index of the first occurrence of the specified element, or -1 if the list does not contain the element.
- `set(int index, E element)`: Replaces the element at the specified position with the specified element.


```java
int size = list.size(); 
boolean hasApple = list.contains("Apple"); 
boolean isEmpty = list.isEmpty(); 
list.clear(); 
int index = list.indexOf("Cherry"); 
list.set(0, "Orange");
```

#### 9. Working with Different Implementations

`List` has several implementations, each with different performance characteristics:

- `ArrayList`: Resizable array implementation. Provides fast random access and is efficient for adding/removing elements at the end.
- `LinkedList`: Doubly-linked list implementation. Efficient for adding/removing elements at both ends but slower for random access.
- `Vector`: Synchronized version of `ArrayList`. Rarely used in modern Java.

Example of using `LinkedList`:


```java
import java.util.LinkedList;  
List<String> linkedList = new LinkedList<>(); 
linkedList.add("Dog"); 
linkedList.add("Cat");
```

### Advanced Concepts

#### 10. Sorting a List

You can sort a list using `Collections.sort()`:

java

Copy code

```java
import java.util.Collections;  
List<String> list = new ArrayList<>(); 
list.add("Banana"); 
list.add("Apple"); 
list.add("Cherry");  
Collections.sort(list);  
for (String fruit : list) {     
	System.out.println(fruit); 
}
```

#### 11. List of Custom Objects

You can create a list of custom objects. For example:

java

Copy code

`class Person {     String name;     int age;      Person(String name, int age) {         this.name = name;         this.age = age;     }      @Override     public String toString() {         return name + " (" + age + ")";     } }  List<Person> people = new ArrayList<>(); people.add(new Person("Alice", 30)); people.add(new Person("Bob", 25));  for (Person person : people) {     System.out.println(person); }`

#### 12. Sorting a List of Custom Objects

You need to implement the `Comparable` interface or provide a `Comparator` to sort a list of custom objects:

Using `Comparable`:

java

Copy code

`class Person implements Comparable<Person> {     String name;     int age;      Person(String name, int age) {         this.name = name;         this.age = age;     }      @Override     public int compareTo(Person other) {         return this.age - other.age;     }      @Override     public String toString() {         return name + " (" + age + ")";     } }  List<Person> people = new ArrayList<>(); people.add(new Person("Alice", 30)); people.add(new Person("Bob", 25));  Collections.sort(people);  for (Person person : people) {     System.out.println(person); }`

Using `Comparator`:

java

Copy code

`import java.util.Comparator;  List<Person> people = new ArrayList<>(); people.add(new Person("Alice", 30)); people.add(new Person("Bob", 25));  Comparator<Person> nameComparator = new Comparator<Person>() {     @Override     public int compare(Person p1, Person p2) {         return p1.name.compareTo(p2.name);     } };  Collections.sort(people, nameComparator);  for (Person person : people) {     System.out.println(person); }`

#### 13. Synchronizing a List

To make a list thread-safe, you can use `Collections.synchronizedList()`:

java

Copy code

`List<String> synchronizedList = Collections.synchronizedList(new ArrayList<>());  synchronizedList.add("Apple"); synchronizedList.add("Banana");`

#### 14. Using Streams with Lists

Java 8 introduced the Stream API, which can be used with lists for various operations like filtering, mapping, and reducing:

java

Copy code

`import java.util.stream.Collectors;  List<String> list = new ArrayList<>(); list.add("Apple"); list.add("Banana"); list.add("Cherry");  // Filter elements that start with 'A' List<String> filteredList = list.stream()                                 .filter(s -> s.startsWith("A"))                                 .collect(Collectors.toList());  filteredList.forEach(System.out::println); // "Apple"`

### Summary

- `List` is an interface that provides ordered collections.
- Common methods: `add()`, `get()`, `remove()`, `size()`, `contains()`, `clear()`.
- Use different implementations (`ArrayList`, `LinkedList`, `Vector`) based on your needs.
- Sort lists using `Collections.sort()`.
- Work with custom objects by implementing `Comparable` or providing `Comparator`.
- Synchronize lists for thread safety using `Collections.synchronizedList()`.
- Utilize the Stream API for functional-style operations on lists.