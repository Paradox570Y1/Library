## Problem statement

Ninja has to implement a data structure ”TRIE” from scratch. Ninja has to complete some functions.

```
1) Trie(): Ninja has to initialize the object of this “TRIE” data structure.

2) insert(“WORD”): Ninja has to insert the string “WORD”  into this “TRIE” data structure.

3) countWordsEqualTo(“WORD”): Ninja has to return how many times this “WORD” is present in this “TRIE”.

4) countWordsStartingWith(“PREFIX”): Ninjas have to return how many words are there in this “TRIE” that have the string “PREFIX” as a prefix.

5) erase(“WORD”): Ninja has to delete one occurrence of the string “WORD” from the “TRIE”.
```

Note:

```
1. If erase(“WORD”) function is called then it is guaranteed that the “WORD” is present in the “TRIE”.

2. If you are going to use variables with dynamic memory allocation then you need to release the memory associated with them at the end of your solution.
```

Can you help Ninja implement the "TRIE" data structure?

Detailed explanation ( Input/output format, Notes, Images )

**Constraints:**

```
1 <= “T” <= 50
1 <= “N” <= 10000
 “WORD” = {a to z}
1 <= | “WORD” | <= 1000

Where “T” is the number of test cases, “N” denotes how many times the functions(as discussed above) we call, “WORD” denotes the string on which we have to perform all the operations as we discussed above, and | “WORD” | denotes the length of the string “WORD”.

Time limit: 1 sec.
```

##### Sample Input 1:

```
1
5
insert coding
insert ninja
countWordsEqualTo coding
countWordsStartingWith nin
erase coding
```

##### Sample Output 1:

```
1
1   
```

##### Explanation of sample input 1:

```
After insertion of “coding” in “TRIE”:
```

```
After insertion of “ninja” in “TRIE”:
```

```
Count words equal to “coding” :
```

```
Count words those prefix is “nin”:
```

```
After deletion of the word “coding”, “TRIE” is:
```

##### Sample Input 2:

```
1
6
insert samsung
insert samsung
insert vivo
erase vivo
countWordsEqualTo samsung
countWordsStartingWith vi
```


# Insert method to count words
- It has two counters
	- ew - ends with (number of words that ends with the given word)
	- cp - count prefix (number of words that starts with the given word)

![[Pasted image 20251002172453.png]]



```java
import java.util.* ;
import java.io.*; 
public class Trie {
    class Node{
        private Node links[];
        private int ew, cp;
        Node() {
            links = new Node[26];
            ew = cp = 0;
        }
        public boolean contains(char ch) {
            return links[ch - 'a'] != null;
        }
        public Node get(char ch) {
            return links[ch - 'a'];
        }
        public void put(char ch, Node node) {
            links[ch - 'a'] = node;
        }
        public void setEnd() {
            ew = ew + 1;
        }
    }
    Node root;
    public Trie() {
        // Write your code here.
        root = new Node();
    }

    public void insert(String word) {
        // Write your code here.
        Node trav = root;
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            if (!trav.contains(ch)) {
                trav.put(ch, new Node());
            }
            Node next = trav.get(ch);
            next.cp++;
            trav = next;
        }
        trav.setEnd();
    }

    public int countWordsEqualTo(String word) {
        // Write your code here.
        Node trav = root;
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            if (!trav.contains(ch)) return 0;
            trav = trav.get(ch);
        }
        return trav.ew;
    }

    public int countWordsStartingWith(String word) {
        // Write your code here.
        Node trav = root;
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            if (!trav.contains(ch)) return 0;
            trav = trav.get(ch);
        }
        return trav.cp;
    }

    public void erase(String word) {
        // Write your code here.
        Node trav = root;
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            Node next = trav.get(ch);
            next.cp--;
            trav = next;
        }
        trav.ew--;
    }

}
```


OR

All methods inbuild int Node class
```java
import java.util.* ;
import java.io.*; 
public class Trie {
    class Node{
        private Node links[];
        private int ew, cp;
        Node() {
            links = new Node[26];
            ew = cp = 0;
        }
        public boolean contains(char ch) {
            return links[ch - 'a'] != null;
        }
        public Node get(char ch) {
            return links[ch - 'a'];
        }
        public void put(char ch, Node node) {
            links[ch - 'a'] = node;
        }
        public void incPrefix() {
            cp = cp + 1;
        }
        public void incEnd() {
            ew = ew + 1;
        }
        public void decPrefix() {
            cp--;
        }
        public void decEnd() {
            ew--;
        }
        public int getPrefix() {
            return cp;
        }
        public int getStartsWith() {
            return ew;
        }
    }
    Node root;
    public Trie() {
        // Write your code here.
        root = new Node();
    }

    public void insert(String word) {
        // Write your code here.
        Node trav = root;
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            if (!trav.contains(ch)) {
                trav.put(ch, new Node());
            }
            trav = trav.get(ch);
            trav.incPrefix();
        }
        trav.incEnd();
    }

    public int countWordsEqualTo(String word) {
        // Write your code here.
        Node trav = root;
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            if (trav.contains(ch)) {
                trav = trav.get(ch);
            } else return 0;
        }
        return trav.getStartsWith();
    }

    public int countWordsStartingWith(String word) {
        // Write your code here.
        Node trav = root;
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            if (trav.contains(ch)) {
                trav = trav.get(ch);
            } else return 0;
        }
        return trav.getPrefix();
    }

    public void erase(String word) {
        // Write your code here.
        Node trav = root;
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            trav = trav.get(ch);
            trav.decPrefix();
        }
        trav.decEnd();
    }

}
```

OR

```java
import java.util.* ;
import java.io.*; 
public class Trie {
    class TrieNode{
        private TrieNode[] links;
        private int endCount;
        private int passCount;
        TrieNode() {
            links = new TrieNode[26];
            endCount = 0;
            passCount = 0;
        }

        public boolean containsKey(char ch) {
            return links[ch-'a'] != null;
        }

        public TrieNode put(char ch) {
            if (!this.containsKey(ch)) {
                links[ch-'a'] = new TrieNode();
            }
            links[ch-'a'].passCount++;
            return this.get(ch);
        }

        public TrieNode get(char ch) {
            return links[ch-'a'];
        }

        public void setEnd() {
            endCount++;
        }

        public int getEndCount() {
            return endCount;
        }

        public int getPassCount() {
            return passCount;
        }

        public void reducePassCount() {
            passCount--;
        }

        public void reduceEndCount() {
            endCount--;
        }
    }
    TrieNode root;
    public Trie() {
        // Write your code here.
        root = new TrieNode();
    }

    public void insert(String word) {
        // Write your code here.
        TrieNode trav = root;
        for (char ch : word.toCharArray()) {
            trav = trav.put(ch);
        }
        trav.setEnd();
    }
    public int countWordsEqualTo(String word) {
        // Write your code here.
        TrieNode trav = root;
        for (char ch : word.toCharArray()) {
            if (!trav.containsKey(ch)) return 0;
            trav = trav.get(ch);
        }
        return trav.getEndCount();
    }

    public int countWordsStartingWith(String word) {
        // Write your code here.
        TrieNode trav = root;
        for (char ch : word.toCharArray()) {
            if (!trav.containsKey(ch)) return 0;
            trav = trav.get(ch);
        }
        return trav.getPassCount();
    }

    public void erase(String word) {
        // Write your code here.
        TrieNode trav = root;
        for (char ch : word.toCharArray()) {
            trav = trav.get(ch);
            trav.reducePassCount();
        }
        trav.reduceEndCount();
    }

}

```