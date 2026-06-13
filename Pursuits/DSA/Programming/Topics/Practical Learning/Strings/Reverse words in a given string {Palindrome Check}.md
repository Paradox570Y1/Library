[151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/)

A **word** is defined as a sequence of non-space characters. The **words** in `s` will be separated by at least one space.

Return _a string of the words in reverse order concatenated by a single space._

**Note** that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

**Example 1:**

**Input:** s = "the sky is blue"
**Output:** "blue is sky the"

**Example 2:**

**Input:** s = "  hello world  "
**Output:** "world hello"
**Explanation:** Your reversed string should not contain leading or trailing spaces.

**Example 3:**

**Input:** s = "a good   example"
**Output:** "example good a"
**Explanation:** You need to reduce multiple spaces between two words to a single space in the reversed string.

**Constraints:**

- `1 <= s.length <= 104`
- `s` contains English letters (upper-case and lower-case), digits, and spaces `' '`.
- There is **at least one** word in `s`.



TC=> O(N)
```java
class Solution {

    public String reverseWords(String s) {
        StringBuilder sb=new StringBuilder();
        int pt=-1,i=0,limit=s.length()-1;
        while(s.charAt(limit)==' ')limit--;
        while(i<limit){
            char c = s.charAt(i);
            if(c==' '){
                int k=i-1;
                boolean flag=false;
                while(k>pt){
                    sb.append(s.charAt(k--));
                    flag=true;
                } 
                if(flag) sb.append(' ');
                pt=i;
                while(pt+1<s.length() && s.charAt(pt+1)==' ')pt++;
                i=pt;
            }
            i++;
        }
        while(limit>pt){
            sb.append(s.charAt(limit--));
        } 
        
        return sb.reverse().toString();
    }
}
```

```java
class Solution {
    public String reverseWords(String s) {
        StringBuilder temp = new StringBuilder();
        StringBuilder ans = new StringBuilder();
        for(int i=0;i<s.length();i++){
            //to handle trailing spaces
            if(s.charAt(i)==' ' && i+1<s.length() && s.charAt(i+1) == ' ')continue;

            if(s.charAt(i) == ' '){
                ans.append(temp.reverse().toString());
                if(i!=s.length()-1 && temp.length()>0)
                ans.append(' ');
                temp.setLength(0);
                continue;
            }
            temp.append(s.charAt(i));
        }
        ans.append(temp.reverse().toString());
        return ans.reverse().toString();
    }
}
```

![[Pasted image 20250129191629.png|400]]

```java
class Solution {
    public String reverseWords(String s) {
        String ans = "";
        String arr[] = s.trim().split("\\s+");
        for(int i=arr.length-1;i>0;i--){
            ans += arr[i] + " ";
        }
        return ans + arr[0];
    }
}
```

```java
public class Solution {
  
  public String reverseWords(String s) {
    if (s == null) return null;
    
    char[] a = s.toCharArray();
    int n = a.length;
    
    // step 1. reverse the whole string
    reverse(a, 0, n - 1);
    // step 2. reverse each word
    reverseWords(a, n);
    // step 3. clean up spaces
    return cleanSpaces(a, n);
  }
  
  void reverseWords(char[] a, int n) {
    int i = 0, j = 0;
      
    while (i < n) {
      while (i < j || i < n && a[i] == ' ') i++; // skip spaces
      while (j < i || j < n && a[j] != ' ') j++; // skip non spaces
      reverse(a, i, j - 1);                      // reverse the word
    }
  }
  
  // trim leading, trailing and multiple spaces
  String cleanSpaces(char[] a, int n) {
    int i = 0, j = 0;
      
    while (j < n) {
      while (j < n && a[j] == ' ') j++;             // skip spaces
      while (j < n && a[j] != ' ') a[i++] = a[j++]; // keep non spaces
      while (j < n && a[j] == ' ') j++;             // skip spaces
      if (j < n) a[i++] = ' ';                      // keep only one space
    }
    return new String(a).substring(0, i);
  }
  
  // reverse a[] from a[i] to a[j]
  private void reverse(char[] a, int i, int j) {
    while (i < j) {
      char t = a[i];
      a[i++] = a[j];
      a[j--] = t;
    }
  }
  
}
```


OR

```java
class Solution {
    public String reverseWords(String s) {
	    int n = s.length();
        int i = n-1;
        int j = n-1;
        StringBuilder sb = new StringBuilder();
        while(i>=0 && s.charAt(i)==' ')i--;
        j=i;
        while(i>=0) {
            while(i>=0 && s.charAt(i)!=' ')i--;
            if(i+1<n && j<n)sb.append(s.substring(i+1,j+1));
            while(i>=0 && s.charAt(i)==' ')i--;
            if(i!=-1)sb.append(" ");
            j=i;
        }
        return sb.toString();
    }

}
```