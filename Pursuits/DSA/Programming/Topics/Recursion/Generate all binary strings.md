[Link](https://www.geeksforgeeks.org/generate-binary-strings-without-consecutive-1s/?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=generate-binary-strings-without-consecutive-1s)



```java
class Solution {
    static void generate(int n,String s,List<String> ans){
        if(n==0){
            ans.add(s);
            return;
        }
        generate(n-1,s+'0',ans);
        if(s.length()<1 || s.charAt(s.length()-1) == '0')
        generate(n-1,s+'1',ans);
    }
  public static List<String> generateBinaryStrings(int n) {
    // code here
    List<String> ans = new ArrayList<>();
    generate(n,"",ans);
    return ans;
  }
}
```


```java
import java.util.Scanner;
public class p1{
    static void generate(int k,StringBuilder sb,int n){
        if(n==k){
            System.out.println(sb.toString());
            return;
        }
        if(sb.charAt(n-1)=='0'){
            sb.setCharAt(n,'0');
            generate(k,sb,n+1);
            sb.setCharAt(n,'1');
            generate(k,sb,n+1);
        }
        if(sb.charAt(n-1)=='1'){
            sb.setCharAt(n,'0');
            generate(k,sb,n+1);
        }
    }
    public static void main(String[] args){
        int n;
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        StringBuilder sb = new StringBuilder(n);
        sb.setLength(n);
        sb.setCharAt(0,'0');
        generate(n,sb,1);
        sb.setCharAt(0,'1');
        generate(n,sb,1);
    }
}
```

OR

```java
// Java program to Generate all binary 
// strings without consecutive 1's
import java.util.*;

class GfG {

    // Recursive helper function to generate binary strings
    static void stringRecur(int i, StringBuilder s, List<String> ans) {
        
        // Base case: If we've filled all positions,
        // add the string to results
        if (i >= s.length()) {
            ans.add(s.toString());
            return;
        }
        
        // Case 1: Keep the current position as 
        // '0' and move to next position
        stringRecur(i + 1, s, ans);
        
        // Case 2: Try placing '1' at current position. 
        // Skip the next position when we place a '1' 
        // to avoid consecutive 1's
        s.setCharAt(i, '1');
        
        // Skip next position to avoid consecutive 1's
        stringRecur(i + 2, s, ans);  
        
        // Backtrack: Restore the current position back to '0'
        s.setCharAt(i, '0');
    }

    static List<String> generateBinaryStrings(int n) {
        
        // Initialize a string of n zeros 
        // as our starting point
        StringBuilder s = new StringBuilder();
        for (int j = 0; j < n; j++) {
            s.append('0');
        }
        
        List<String> ans = new ArrayList<>();
        
        stringRecur(0, s, ans);
        
        return ans;
    }

    public static void main(String[] args) {
        int n = 4;
        List<String> res = generateBinaryStrings(n);
        for (String s : res) {
            System.out.println(s);
        }
    }
}
```