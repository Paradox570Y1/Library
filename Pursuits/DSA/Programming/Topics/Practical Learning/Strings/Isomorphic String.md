[205. Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings/)

Given two strings `s` and `t`, _determine if they are isomorphic_.

Two strings `s` and `t` are isomorphic if the characters in `s` can be replaced to get `t`.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

**Example 1:**

**Input:** s = "egg", t = "a`dd"

**Output:** true

**Explanation:**

The strings `s` and `t` can be made identical by:

- Mapping `'e'` to `'a'`.
- Mapping `'g'` to `'d'`.

**Example 2:**

**Input:** s = "foo", t = "bar"

**Output:** false

**Explanation:**

The strings `s` and `t` can not be made identical as `'o'` needs to be mapped to both `'a'` and `'r'`.

**Example 3:**

**Input:** s = "paper", t = "title"

**Output:** true

**Constraints:**

- `1 <= s.length <= 5 * 104`
- `t.length == s.length`
- `s` and `t` consist of any valid ascii character.

Remember
![[Pasted image 20250630194556.png]]

# Better

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        int n = s.length();
        int m = t.length();
        HashMap<Character,Character> hm = new HashMap<>();
        HashSet<Character> hs = new HashSet<>();
        if(n!=m)return false;
        for(int i=0;i<n;i++){
            char s1 = s.charAt(i);
            char s2 = t.charAt(i);
            if(hm.containsKey(s1)){
                if(s2 != hm.get(s1))return false;
            }
            else{
                if(hs.contains(s2))return false;
                hm.put(s1,s2);
                hs.add(s2);
            }
        }
        return true;
    }
}
```


# Optimal

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        char[] arr = new char[256];
        for (int i = 0; i < s.length(); i++) {
            char curs = s.charAt(i);
            char curt = t.charAt(i);
            if (arr[curs] != '\u0000') {
                if (arr[curs] != curt) return false;
            } else {
                for (char a : arr) {
                    if(a == curt) return false;
                }
                arr[curs] = curt;
            }

        }
        return true;
    }
}
```

```js
var isIsomorphic = function(s, t) {
    var arr = new Array(256);
    for(var i=0;i<s.length;i++){
        var s1 = s.charAt(i);
        var s2 = t.charAt(i);
        if(arr[s1.charCodeAt(0)] != undefined){
            if(arr[s1.charCodeAt(0)] != s2)return false;
        }
        else{
            for(var k=0;k<256;k++){
                if(arr[k] == s2)return false;
            }
            arr[s1.charCodeAt(0)] = s2;
        }
    }
    return true;
};
```

From comments
```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if(s.length() != t.length())return false;
        HashMap<Character,Integer> mp1 = new HashMap<>();
        HashMap<Character,Integer> mp2 = new HashMap<>();
        for(int i=0;i<s.length();i++){
            if (!mp1.containsKey(s.charAt(i))) {
                mp1.put(s.charAt(i), i);
            }

            if (!mp2.containsKey(t.charAt(i))) {
                mp2.put(t.charAt(i), i);
            }

            if (!mp1.get(s.charAt(i)).equals(mp2.get(t.charAt(i)))) {
                return false;
            }
        }
        return true;
    }
}
```

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if(s.length() != t.length())return false;
        HashMap<Character,Integer> mp1 = new HashMap<>();
        HashMap<Character,Integer> mp2 = new HashMap<>();
        for(int i=0;i<s.length();i++){
            boolean a = mp1.containsKey(s.charAt(i));
            boolean b = mp2.containsKey(t.charAt(i));
            if(a != b) return false;
            else{
                if(a && !mp1.get(s.charAt(i)).equals(mp2.get(t.charAt(i)))) 
                return false;
                mp1.put(s.charAt(i),i);
                mp2.put(t.charAt(i),i);
            }
        }
        return true;
    }
}
```

#### Note:
Changed `if(mp1.get(s.charAt(i)) != mp2.get(t.charAt(i)))` to `if(!mp1.get(s.charAt(i)).equals(mp2.get(t.charAt(i))))`. This properly compares the values stored in the maps instead of comparing their object references.

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if(s.length() == 0 || s.length() != t.length())return false;
        HashMap<Character,Integer> str1 = new HashMap<>();
        HashMap<Character,Integer> str2 = new HashMap<>();
        int p1=0,p2=0;
        for(int i=0;i<s.length();i++){
            p1++;p2++;
            if(str1.containsKey(s.charAt(i))){
                p1 = str1.get(s.charAt(i));
            }
            else str1.put(s.charAt(i),p1);

            if(str2.containsKey(t.charAt(i))){
                p2 = str2.get(t.charAt(i));
            }
            else str2.put(t.charAt(i),p2);
            if(p1!=p2) return false;
        }
        return true;
    }
}
```

Without data structures
```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        int hash1[] = new int[150];
        int hash2[] = new int[150];
        for(int i=0;i<s.length();i++){
            if(hash1[s.charAt(i)] != hash2[t.charAt(i)]) return false;
            hash1[s.charAt(i)]=i+1;
            hash2[t.charAt(i)]=i+1;
        }
        return true;
    }
}
```

