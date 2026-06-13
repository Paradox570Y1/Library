- [[#Map|Map]]
- [[#2D List in Java|2D List in Java]]
- [[#sizeof()|sizeof()]]
- [[#Swapping without temp|Swapping without temp]]
- [[#Binary Search|Binary Search]]
		- [[#if you are searching in decimal numbers then the structure of binary search changes.|if you are searching in decimal numbers then the structure of binary search changes.]]
- [[#Comparing string in java|Comparing string in java]]
- [[#To get the max element in java using libraries|To get the max element in java using libraries]]
- [[#To do ceil in an array|To do ceil in an array]]


## Map
- In C++, when using map , inserting element directly is different then using insert.
```cpp
map.insert({1,2}); // here, it insert element if it is already not present
map[1] = 2; // here, it always insert the element

// Equivalent to insert will be
if(map.find(1) == map.end()){ // if not found
	map[1] = 2;
}
```
- In Java
```java
map.put(1,2); // always insert element

//To insert only when element doesn't already exist.
if(map.containsKey(1) == false){ // Or (!map.containsKey(1))
	map.put(1,2);
}
//To insert 1 if element doesn't exist otherwise increasing the element count by 1
map.put(ele,map.getOrDefault(ele,0)+1);
```

> **Note:** 
> - In map if you try to access a value of key which is not inserted then it will insert that key with a default value of 0 in case of integer.
> - In Java, accessing a key that doesn't exist in a `HashMap` or `Map` using methods like `get` will not insert the key into the map. Instead, these methods will simply return `null` if the key is not found.


## 2D List in Java
```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> li = new ArrayList<>();
        // Adding the first row to the list of lists
        li.add(new ArrayList<>(List.of(1))); // Adds the first row [1]
    }
}
```

```java
// To add multiple elements in one go
List<Integer> li = new ArrayList<>(Arrays.asList(nums[i],nums[j],nums[k]));
```

> In Hashing use arrays in java instead of hashmap for better time complexity as it is easier to fetch value from array than from hashmap.


## sizeof()
- **For static arrays:** `sizeof(arr) / sizeof(arr[0])` works correctly.
- **For dynamic arrays (pointers):** You need to track the size manually, as `sizeof` won't give the actual number of elements.


## Swapping without temp
```cpp
if(mini!=i){
            arr[mini] ^= arr[i];
            arr[i] ^= arr[mini];
            arr[mini] ^= arr[i];
        }
```
The XOR-based swap method is a clever way to avoid using a temporary variable, but it's less readable and generally slower than a simple swap using a temporary variable because modern compilers optimize simple swaps more effectively.

---



## Binary Search
#### if you are searching in decimal numbers then the structure of binary search changes.

![[Pasted image 20240928010245.png|300]]

## Comparing string in java
To compare strings in Java, you can use the following libraries and methods, depending on the type of comparison you need:

1. **Built-in Java String methods**:
    
    - **`equals()`**: Compares two strings for exact equality.
    
    
    `String str1 = "hello"; String str2 = "hello"; boolean isEqual = str1.equals(str2); // true`
    
    - **`compareTo()`**: Compares two strings lexicographically.
    
    `String str1 = "apple"; String str2 = "banana"; int result = str1.compareTo(str2); // negative value because "apple" < "banana"`
    
    - **`equalsIgnoreCase()`**: Compares strings ignoring case differences.
    
    
    `String str1 = "Hello"; String str2 = "hello"; boolean isEqual = str1.equalsIgnore`

## To get the max element in java using libraries

```java
 int arr[] = {2, 5, 1 , 54 ,22, 123 ,32 ,13};
System.out.println(Arrays.stream(arr).max().getAsInt());
```

## To do ceil in an array

![[Pasted image 20241211163645.png|250]]

The selected line is same as `Math.ceil(ele/rate)`
remember inside ceil the calculations should be in double in java, c++