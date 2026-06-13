> [Resources](https://www.geeksforgeeks.org/manachers-algorithm-linear-time-longest-palindromic-substring-part-1/)

- Used to calculate LPS(Longest Palindrome Substring).
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

OR

```java
class Solution {
    private int maxPal(String s,int i){
        int n = s.length();
        int j = i;
        int cnt=1;
        i--;j++;
        while(i>=0 && j<n && s.charAt(i) == s.charAt(j)){cnt+=2;i--;j++;}
        return cnt;
    }
    public String longestPalindrome(String s) {
        int st = 1;
        int end = 1;
        String q = "#" + s.replaceAll("","#") + "#";
        int n = q.length();
        int length[] = new int[n];
        int maxLen=0;
        int center = 0;
        int right = 0;
        for(int i=0;i<n;i++){
            if(i<right){
                length[i] = Math.min(length[2*center-i],right-i);
            }
            while(i-length[i]-1>=0 && i+length[i]+1<n && q.charAt(i-length[i]-1) == q.charAt(i+length[i]+1))length[i]++;
            if(i+length[i] > right){
                center = i;
                right = i+length[i];
            }
            if(length[i] > maxLen){
                st = i-length[i];
                end = i+length[i];
                maxLen = length[i];
            }
        }
        return q.substring(st,end+1).replaceAll("#","");
    }
}
```

OR

Expand Around center (light version of manacher's algorithm)
```java
class Solution {
    private String expand(String s, int i, int j) {
        while (i >= 0 && j < s.length() && s.charAt(i) == s.charAt(j)) {
            i--;
            j++;
        }
        return s.substring(i+1, j);
    }
    public String longestPalindrome(String s) {
        int n = s.length();
        String res = s.substring(0, 1);
        for (int i = 0; i < n; i++) {
            String a = expand(s, i, i);
            String b = expand(s, i, i+1);
            if (a.length() > res.length()) {
                res = a;
            }
            if (b.length() > res.length()) {
                res = b;
            }
        }
        return res;
    }
}
```