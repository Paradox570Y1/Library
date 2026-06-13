[5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

Given a string `s`, return _the longest_  _palindromic_ _substring in `s`.

**Example 1:**

**Input:** s = "babad"
**Output:** "bab"
**Explanation:** "aba" is also a valid answer.

**Example 2:**

**Input:** s = "cbbd"
**Output:** "bb"

**Constraints:**

- `1 <= s.length <= 1000`
- `s` consist of only digits and English letters.

# Brute

- Time complexity : _**O(n^3)**_. Assume that n is the length of the input string, there are a total of C(n, 2) = n(n-1)/2 substrings (excluding the trivial solution where a character itself is a palindrome). Since verifying each substring takes O(n) time, the run time complexity is O(n^3).
    
- Space complexity : _**O(1)**_.

```java
public class Solution {
    public String longestPalindrome(String s) {
        if (s.length() <= 1) {
            return s;
        }

        int maxLen = 1;
        String maxStr = s.substring(0, 1);

        for (int i = 0; i < s.length(); i++) {
            for (int j = i + maxLen; j <= s.length(); j++) {
                if (j - i > maxLen && isPalindrome(s.substring(i, j))) {
                    maxLen = j - i;
                    maxStr = s.substring(i, j);
                }
            }
        }

        return maxStr;
    }

    private boolean isPalindrome(String str) {
        int left = 0;
        int right = str.length() - 1;

        while (left < right) {
            if (str.charAt(left) != str.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }

        return true;
    }
}
```

OR

Without updating string everytime

```java
class Solution {
    private boolean isPal(String s,int i,int j){
        while(i<j){
            if(s.charAt(i) != s.charAt(j))return false;
            i++;j--;
        }
        return true;
    }
    public String longestPalindrome(String s) {
        int n = s.length();
        int st = 0;
        int end = 0;
        int len = 1;
        for(int i=0;i<n;i++){
            for(int j=i+len;j<n;j++){
                if(isPal(s,i,j)){
                    len = j-i+1;
                    st = i;
                    end = j;
                }
            }
        }
        return s.substring(st,end+1);
    }
}
```
# Better then DP approach(3rd approach)
**Approach 2: Expand Around Center**

**To enumerate all palindromic substrings of a given string, we first expand a given string at each possible starting position of a palindrome and also at each possible ending position of a palindrome and keep track of the length of the longest palindrome we found so far.**

# Approach :

1. We observe that a palindrome mirrors around its center. Therefore, a palindrome can be expanded from its center, and there are only 2n - 1 such centers.
2. You might be asking why there are 2n - 1 but not n centers? The reason is the center of a palindrome can be in between two letters. Such palindromes have even number of letters (such as "abba") and its center are between the two 'b's.'
3. Since expanding a palindrome around its center could take O(n) time, the overall complexity is O(n^2).

- Time complexity : _**O(n^2)**_. Since expanding a palindrome around its center could take O(n) time, the overall complexity is O(n^2).
    
- Space complexity : _**O(1)**_.

```java
class Solution {
    public String longestPalindrome(String s) {
        if(s.length() == 0)return "";
        if(s.length() == 1)return s;
        int maxi=1;
        int start=0,end=0;
        for(int i=0;i<s.length();i++){
            int right= i+1;
            int left = i-(right-i);
            int temp=1;
            while(left>=0 && right<s.length() && s.charAt(right) == s.charAt(left)){
                temp+=2;
                if(temp>maxi){
                    maxi = temp;
                    start = left;
                    end = right;
                }
                left--;right++;
            }
            right = i+1;
            left = i;
            temp=0;
            while(right<s.length() && left>=0 && s.charAt(right) == s.charAt(left)){
                temp+=2;
                if(temp>maxi){
                    maxi = temp;
                    start = left;
                    end = right;
                }
                left--;right++;
            }
        }
        return s.substring(start,end+1);
    }
}
```

- Here i can remove the array and just
```java
class Solution {
    public String longestPalindrome(String s) {
        if(s.length()<=1)return s;
        int n = s.length();
        int N = 2*n + 1;
        int maxi = 1;
        int start = 0;
        int end = 0;
        for(int i=2;i<N;i++){
            int left = ((i-2)-1)/2;
            int right = ((i+2)-1)/2;
            if(i%2==0){
                left = ((i-1)-1)/2;
                right = ((i+1)-1)/2;
            }
            while(left>=0 && right<n && s.charAt(left) == s.charAt(right)){
                left--;right++;
            }
            int temp =1;
            if(right<left) temp = 0;
            else temp = (right-1)-(left+1)+1;
            if(temp>maxi){
                start = left+1;
                end = right-1;
                maxi = temp;
            }
        }
        return s.substring(start,end+1);
    }
}
```

```java
public class Solution {
    public String longestPalindrome(String s) {
        if (s.length() <= 1) {
            return s;
        }

        String maxStr = s.substring(0, 1);

        for (int i = 0; i < s.length() - 1; i++) {
            String odd = expandFromCenter(s, i, i);
            String even = expandFromCenter(s, i, i + 1);

            if (odd.length() > maxStr.length()) {
                maxStr = odd;
            }
            if (even.length() > maxStr.length()) {
                maxStr = even;
            }
        }

        return maxStr;
    }

    private String expandFromCenter(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return s.substring(left + 1, right);
    }
}
```

OR
My way
```java
class Solution {
    private int maxPal(String s,int i,int j){
        int n = s.length();
        int cnt=0;
        if(i==j){
            i--;
            j++;
            cnt++;
        }
        while(i>=0 && j<n && s.charAt(i) == s.charAt(j)){cnt+=2;i--;j++;}
        return cnt;
    }
    public String longestPalindrome(String s) {
        int n = s.length();
        int st=0;
        int end=0;
        int maxLen=1;
        for(int i=1;i<n;i++){
            int len = maxPal(s,i-1,i);
            if(len>maxLen){
                st = i-len/2;
                end = i+len/2-1;
                maxLen = len;
            }
            len = maxPal(s,i,i);
            if(len>maxLen){
                st = i-(len-1)/2;
                end = i+(len-1)/2;
                maxLen = len;
            }
        }
        return s.substring(st,end+1);
    }
}
```

# Another better approach using DP (not that good)

**To improve over the brute force solution, we first observe how we can avoid unnecessary re-computation while validating palindromes. Consider the case "ababa". If we already knew that "bab" is a palindrome, it is obvious that "ababa" must be a palindrome since the two left and right end letters are the same.**

# Complexity Analysis

- Time complexity : _**O(n^2)**_. This gives us a runtime complexity of O(n^2).
    
- Space complexity : _**O(n^2)**_. It uses O(n^2) space to store the table.

```java
class Solution {
    public String longestPalindrome(String s) {
        if(s.length()<=1)return s;
        int maxi=1;
        int left =0,right=0;
        boolean arr[][] = new boolean[s.length()][s.length()];
        for(int i=0;i<s.length();i++){
            for(int j=0;j<s.length();j++){
                if(s.charAt(i) == s.charAt(j) && (i-j <= 2 || arr[j+1][i-1])){
                    arr[j][i] = true;
                    if(maxi<i-j+1){
                        left = j;
                        right = i;
                        maxi = i-j+1;
                    }
                }
            }
        }
        return s.substring(left,right+1);
    }
}
```



# Manacher's Algorithm 
(Linear Time Longest Palindromic Substring)

TC => O(N)
SC => O(N)


```java
class Solution {
    public String longestPalindrome(String s) {
        if(s.length()<=1)return s;
        int maxLen = 1;
        String maxStr = s.substring(0,1);
        s = "#" + s.replaceAll("","#") + "#";
        int arr[] = new int[s.length()];
        int center = 0;
        int right =0;
        for(int i=0;i<s.length();i++){
            if(i<right){
                arr[i] = Math.min(right-i,arr[2*center-i]);
            }
            while(i-arr[i]-1>=0 && i+arr[i]+1<s.length() && s.charAt(i-arr[i]-1) == s.charAt(i+arr[i]+1)){
                arr[i]++;
            }
            if(i+arr[i]>right){
                center = i;
                right = i+arr[i];
            }
            if(arr[i]>maxLen){
                maxLen = arr[i];
                maxStr = s.substring(i-arr[i],i+arr[i]+1).replaceAll("#","");
            }
        }
        return maxStr;
    }
}
```

```java
//my algo not working
class Solution {
    public String longestPalindrome(String s) {
        if(s.length()<=1)return s;
        int n = s.length();
        int N = 2*n + 1;
        int arr[] = new int[N];
        arr[0] = 0;
        arr[1] = 1;
        int maxi = 1;
        int start = 0;
        int end = 0;
        int mirror_i;
        int left=-1,right=-1;
        for(int i=2;i<N;i++){
            mirror_i = i - (i - ((right*2)+1 + (left*2)+1)/2);
            if(left != -1 && right*2+1 -i >= arr[mirror_i]){
                arr[i] = arr[mirror_i];
                continue;
            }
            else if(left != -1 && (right*2)+1 -i == (arr[mirror_i]-1)/2){
                int r = right+1;
                int l = i - (r - i);
                while(l>=0 && r<n && s.charAt(l) == s.charAt(r)){
                    l--;r++;
                }
                l++;r--;
                arr[i] = (r)-(l)+1;
                continue;
            }
            else{
                left = ((i-2)-1)/2;
                right = ((i+2)-1)/2;
                if(i%2==0){
                    left = ((i-1)-1)/2;
                    right = ((i+1)-1)/2;
                }
                while(left>=0 && right<n && s.charAt(left) == s.charAt(right)){
                    left--;right++;
                }
                left++;right--;
            }
            if(right<=left) arr[i] = 1;
            else arr[i] = (right)-(left)+1;
            if(arr[i]>maxi){
                start = left;
                end = right;
                maxi = arr[i];
            }
        }
        return s.substring(start,end+1);
    }
}
```


```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        string ns="";
        for(char ch:s){
            ns+='#';
            ns+=ch;;
        }
        ns+='#';
        int c=0;
        int r=0;
        vector<int> v(ns.size(),0);
        string ans="";
        for(int i=0;i<ns.size();i++){
            if(i<r)v[i] = min(v[2*c-i],r-i);
            while(i-v[i]-1>=0 && i+v[i]+1<ns.size() && ns[i-v[i]-1] == ns[i+v[i]+1])v[i]++;
            if(i+v[i]>r){
                c=i;
                r=i+v[i];
            }
            if(ans.size()<2*v[i]+1){
                ans = ns.substr(i-v[i],2*v[i]+1);
            }
        }
        string result="";
        for(char ch:ans){
            if(ch!='#')result+=ch;
        }
        return result;
    }
};
```