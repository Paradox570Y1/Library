### **Java**

- **Using `equals()` Method**: Compares the actual content of the strings.
- **Using `==` Operator**: Checks if two string references point to the same memory location (not the content).

#### Example:
```java
public class StringEquality {     
	public static void main(String[] args) {         
		String str1 = "Hello";         
		String str2 = "Hello";         
		String str3 = new String("Hello");//Content comparison 
		System.out.println(str1.equals(str2)); // true    
		System.out.println(str1.equals(str3)); // true                 // Reference comparison         
		System.out.println(str1 == str2); 
		// true (both point to the same interned object)       
		System.out.println(str1 == str3); 
		// false (str3 is a new object)     
	} 
}
```

---

### **C++**

- **Using `==` Operator**: For `std::string`, this compares the content of the strings.
- **Using `strcmp()` Function**: For C-style strings (`char[]`), this compares the content lexicographically.

#### Example:

```cpp
#include <iostream>
#include <string>
#include <cstring>

int main() {
    // Using std::string
    std::string str1 = "Hello";
    std::string str2 = "Hello";
    std::string str3 = "World";

    // Content comparison
    std::cout << (str1 == str2) << std::endl; // 1 (true)
    std::cout << (str1 == str3) << std::endl; // 0 (false)

    // Using C-style strings
    const char* cstr1 = "Hello";
    const char* cstr2 = "Hello";
    const char* cstr3 = "World";

    // Reference comparison
    std::cout << (cstr1 == cstr2) << std::endl; // 1 (true, but not reliable for content)
    
    // Content comparison
    std::cout << (std::strcmp(cstr1, cstr2) == 0) << std::endl; // 1 (true)
    std::cout << (std::strcmp(cstr1, cstr3) == 0) << std::endl; // 0 (false)

    return 0;
}
```

---

### Key Differences:

|Aspect|Java|C++|
|---|---|---|
|**Default Comparison**|`equals()` for content, `==` for reference|`==` for content (`std::string`)|
|**String Type**|`String` (immutable)|`std::string` or `char[]`|
|**C-style Strings**|Not used|Use `strcmp()` for comparison|