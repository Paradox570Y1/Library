```java
  String cleanSpaces(char[] a, int n) {
    int i = 0, j = 0;
      
    while (j < n) {
      while (j < n && a[j] == ' ') j++;             // skip spaces
      while (j < n && a[j] != ' ') a[i++] = a[j++]; // keep non spaces
      while (j < n && a[j] == ' ') j++;             // skip spaces
      if (j < n) a[i++] = ' ';                      // keep only one space
    }
  
    return new String(a).substring(0, i);
    //To return substring from an character array
    //OR
    // return new String(arr,0,i);
  }
```

### **Purpose of the Method**

The method `cleanSpaces` takes a character array `a` and its size `n`. It removes extra spaces from the character array and ensures that:

1. Leading and trailing spaces are removed.
2. Consecutive spaces are replaced by a single space.

Finally, it returns a new `String` formed from the processed characters.

---

### **Parameters**

- `char[] a`: The input character array containing spaces and non-space characters.
- `int n`: The number of valid characters in the array.

---

### **Key Variables**

- `i`: Write pointer — used to overwrite the input array with cleaned characters.
- `j`: Read pointer — used to traverse the input array.

---

### **Steps in the Code**

#### **1. Initialize Pointers**


`int i = 0, j = 0;`

- `i` starts at the beginning of the array, where cleaned characters will be written.
- `j` starts at the beginning of the array, where characters will be read.

---

#### **2. Outer `while (j < n)`**

The outer loop iterates through the array until `j` reaches the end (`n`).

---

#### **3. Skip Leading Spaces**


`while (j < n && a[j] == ' ') j++;`

- This loop skips over leading spaces by moving the read pointer `j` forward whenever it encounters a space.
- After this, `j` points to the first non-space character (or the end of the array if all spaces).

---

#### **4. Copy Non-Space Characters**

`while (j < n && a[j] != ' ') a[i++] = a[j++];`

- This loop copies non-space characters from position `j` to position `i` and increments both pointers.
- `i` advances to the next position to overwrite, while `j` advances to the next character to read.

---

#### **5. Skip Consecutive Spaces**

`while (j < n && a[j] == ' ') j++;`

- After copying a block of non-space characters, this loop skips over any consecutive spaces.

---

#### **6. Add a Single Space Between Words**

`if (j < n) a[i++] = ' ';`

- If `j` hasn't reached the end of the array, this line adds a single space between words.
- This ensures that only one space separates words, even if there were multiple spaces originally.

---

#### **7. Create and Return the Cleaned String**


`return new String(a).substring(0, i);`

- After the loop, `i` points to the position after the last valid character.
- A new `String` is created using the modified portion of the array (`substring(0, i)`).

---

### **How the Method Works (Example)**

#### Input:


`char[] a = "   hello   world   ".toCharArray(); int n = a.length; // 19`

#### Execution:

1. **Skip leading spaces**: `j` moves to index `3` (points to `'h'`).
2. **Copy non-space characters**: Copy `'hello'` to `i=0` to `i=5`.
3. **Skip consecutive spaces**: `j` moves to index `10` (points to `'w'`).
4. **Add a single space**: Add `' '` at `i=5`.
5. **Copy `'world'`**: Copy `'world'` to `i=6` to `i=11`.
6. **Skip trailing spaces**: `j` moves to the end of the array.
7. **Create substring**: Result is `"hello world"`.

#### Output:


`"hello world"`

---

### **Time Complexity**

- **Skipping spaces**: O(n) — Each character is processed once.
- **Copying non-space characters**: O(n) — Each character is processed once.
- **Total**: O(n).

### **Space Complexity**

- The input is modified in place (`char[] a`), so no additional space is used other than for creating the final `String`. Hence, **O(1)** auxiliary space.