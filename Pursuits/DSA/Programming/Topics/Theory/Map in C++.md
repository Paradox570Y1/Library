mp[sum]=i;
above state insert a new key, value pair if it doesn't exist already in map but if key already exist then it updates that key with new value.

mp.insert(sum,i);

**Insertion Behavior**:

- If the key does not exist in the map, `insert()` will insert the key-value pair.
- If the key already exists in the map, `insert()` does nothing and returns an iterator to the existing element (key-value pair).

### Step-by-Step Guide to Using "map" in C++
#### 1. Include the Map Header
First, include the map header at the top of your C++ program:
```cpp
#include <map>
```

#### 2. Declare a Map
```cpp
map<int,string> myMap; // map with int keys and string values
```

#### 3. Inserting Elements

Use the `insert` function or the `[]` operator to add elements:

```cpp
// Using insert function
myMap.insert(pair<int, string>(1, "Apple"));
myMap.insert(make_pair(2, "Banana"));

// Using [] operator
myMap[3] = "Orange";

```

#### 4. Accessing Elements

Access elements using the `[]` operator or the `at` method:

```cpp
cout << "Key 1: " << myMap[1] << endl; // Outputs "Apple"
cout << "Key 2: " << myMap.at(2) << endl; // Outputs "Banana"
```
#### 5. Checking for Keys

Check if a key exists using the `find` method:

```cpp
if (myMap.find(3) != myMap.end()) {
    std::cout << "Key 3 found." << std::endl;
} 
else {
    std::cout << "Key 3 not found." << std::endl;
}

```

#### 6. Removing Elements

Remove elements using the `erase` method:

```cpp
myMap.erase(2); // Removes the element with key 2
```

#### 7. Iterating Over Elements

Iterate over the elements using an iterator:

```cpp
for (auto it = myMap.begin(); it != myMap.end(); ++it) {
    std::cout << "Key: " << it->first << ", Value: " << it->second << std::endl;
}
```
#### 8. Size of the Map

Get the number of elements in the map using the `size` method:

```cpp
std::cout << "Size of map: " << myMap.size() << std::endl;
```

### Time Complexities

1. **Insertion**:
    
    - `insert` and `[]` operator: O(log n)
    - Insertion is efficient due to the underlying balanced tree structure (usually a Red-Black tree).
2. **Accessing Elements**:
    
    - `[]` operator and `at` method: O(log n)
    - Searching for elements also has a logarithmic time complexity.
3. **Removing Elements**:
    
    - `erase` method: O(log n)
    - Removing an element requires finding it first, which is logarithmic, and then adjusting the tree structure, also logarithmic.
4. **Finding Elements**:
    
    - `find` method: O(log n)
    - The `find` method has a logarithmic time complexity.
5. **Iterating**:
    - Iteration over all elements: O(n)
    - Iterating through the map is linear in the number of elements, O(n), since every element is visited once.

### Example Code

Here is a complete example demonstrating these operations in C++:

```cpp
#include <iostream>
#include <map>

int main() {
    // Declare a map
    std::map<int, std::string> myMap;

    // Insert elements
    myMap.insert(std::pair<int, std::string>(1, "Apple"));
    myMap.insert(std::make_pair(2, "Banana"));
    myMap[3] = "Orange";

    // Access elements
    std::cout << "Key 1: " << myMap[1] << std::endl;
    std::cout << "Key 2: " << myMap.at(2) << std::endl;

    // Check for keys
    if (myMap.find(3) != myMap.end()) {
        std::cout << "Key 3 found." << std::endl;
    } else {
        std::cout << "Key 3 not found." << std::endl;
    }

    // Remove an element
    myMap.erase(2);

    // Iterate over elements
    for (auto it = myMap.begin(); it != myMap.end(); ++it) {
        std::cout << "Key: " << it->first << ", Value: " << it->second << std::endl;
    }

    // Size of the map
    std::cout << "Size of map: " << myMap.size() << std::endl;

    return 0;
}

```

This example demonstrates basic usage of the `map` container in C++ and provides the time complexities for various operations.