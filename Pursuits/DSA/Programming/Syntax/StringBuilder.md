### **1. `append(String s)`**

Adds the specified string to the end of the existing string.

**Syntax:**

```java
StringBuilder sb = new StringBuilder("Hello"); 
sb.append(" World"); 
System.out.println(sb); // Output: Hello World
```

---

### **2. `insert(int offset, String s)`**

Inserts the specified string at the given position.

**Syntax:**


```java
StringBuilder sb = new StringBuilder("Hello"); 
sb.insert(5, " World"); 
System.out.println(sb); // Output: Hello World
```

---

### **3. `replace(int start, int end, String s)`**

Replaces the characters in a substring of this sequence with the specified string.

**Syntax:**


```java
StringBuilder sb = new StringBuilder("Hello World"); 
sb.replace(6, 11, "Java"); 
System.out.println(sb); // Output: Hello Java
```

---

### **4. `delete(int start, int end)`**

Deletes the characters in a substring of this sequence.

**Syntax:**


```java
StringBuilder sb = new StringBuilder("Hello World"); 
sb.delete(5, 11); 
System.out.println(sb); // Output: Hello
```

---

### **5. `deleteCharAt(int index)`**

Deletes the character at the specified index.

**Syntax:**


```java
StringBuilder sb = new StringBuilder("Hello"); 
sb.deleteCharAt(4); 
System.out.println(sb); // Output: Hell
```

---

### **6. `reverse()`**

Reverses the characters in the `StringBuilder`.

**Syntax:**

```java
StringBuilder sb = new StringBuilder("Hello"); 
sb.reverse(); 
System.out.println(sb); // Output: olleH
```

---

### **7. `charAt(int index)`**

Returns the character at the specified index.

**Syntax:**

```java
StringBuilder sb = new StringBuilder("Hello"); 
char ch = sb.charAt(1); 
System.out.println(ch); // Output: e
```

---

### **8. `setCharAt(int index, char ch)`**

Sets the character at the specified index to a new value.

**Syntax:**

```java
StringBuilder sb = new StringBuilder("Hello"); 
sb.setCharAt(0, 'h'); 
System.out.println(sb); // Output: hello
```

---

### **9. `substring(int start)`**

Returns a new string that is a substring of the sequence starting from the specified index.

**Syntax:**


`StringBuilder sb = new StringBuilder("Hello World"); String sub = sb.substring(6); System.out.println(sub); // Output: World`

---

### **10. `substring(int start, int end)`**

Returns a substring of the sequence from `start` to `end`.

**Syntax:**

java

Copy code

`StringBuilder sb = new StringBuilder("Hello World"); String sub = sb.substring(0, 5); System.out.println(sub); // Output: Hello`

---

### **11. `length()`**

Returns the length of the string.

**Syntax:**


```java
StringBuilder sb = new StringBuilder("Hello"); System.out.println(sb.length()); // Output: 5
```

---

### **12. `capacity()`**

Returns the current capacity of the `StringBuilder`.

**Syntax:**

java

Copy code

`StringBuilder sb = new StringBuilder("Hello"); System.out.println(sb.capacity()); // Default: 16 + initial string length`

---

### **13. `setLength(int newLength)`**

Sets the length of the sequence. If `newLength` is less than the current length, the sequence is truncated. If greater, it is padded with null characters.

**Syntax:**


```java
StringBuilder sb = new StringBuilder("Hello"); sb.setLength(10); 
System.out.println(sb); // Output: Hello (with 5 null characters)
```

---

### **14. `ensureCapacity(int minimumCapacity)`**

Ensures that the capacity is at least equal to the specified value.

**Syntax:**

java

Copy code

`StringBuilder sb = new StringBuilder(); sb.ensureCapacity(50); System.out.println(sb.capacity()); // Output: 50 (if initial capacity was smaller)`

---

### **15. `indexOf(String str)`**

Returns the index of the first occurrence of the specified string.

**Syntax:**

java

Copy code

`StringBuilder sb = new StringBuilder("Hello World"); int index = sb.indexOf("World"); System.out.println(index); // Output: 6`

---

### **16. `lastIndexOf(String str)`**

Returns the index of the last occurrence of the specified string.

**Syntax:**

java

Copy code

`StringBuilder sb = new StringBuilder("Hello World World"); int index = sb.lastIndexOf("World"); System.out.println(index); // Output: 12`

---

### **17. `toString()`**

Converts the `StringBuilder` object to a `String`.

**Syntax:**

java

Copy code

`StringBuilder sb = new StringBuilder("Hello World"); String str = sb.toString(); System.out.println(str); // Output: Hello World`