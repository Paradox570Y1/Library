[13. Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

**Symbol**       **Value**
I             1
V             5
X             10
L             50
C             100
D             500
M             1000

For example, `2` is written as `II` in Roman numeral, just two ones added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer.

**Example 1:**

**Input:** s = "III"
**Output:** 3
**Explanation:** III = 3.

**Example 2:**

**Input:** s = "LVIII"
**Output:** 58
**Explanation:** L = 50, V= 5, III = 3.

**Example 3:**

**Input:** s = "MCMXCIV"
**Output:** 1994
**Explanation:** M = 1000, CM = 900, XC = 90 and IV = 4.

**Constraints:**

- `1 <= s.length <= 15`
- `s` contains only the characters `('I', 'V', 'X', 'L', 'C', 'D', 'M')`.
- It is **guaranteed** that `s` is a valid roman numeral in the range `[1, 3999]`.


# Basic Hashing
```java
class Solution {
    public int romanToInt(String s) {
        HashMap<Character,Integer> mp = new HashMap<>();
        mp.put('I',1);
        mp.put('V',5);
        mp.put('X',10);
        mp.put('L',50);
        mp.put('C',100);
        mp.put('D',500);
        mp.put('M',1000);
        int ans=0;
        for(int i=0;i<s.length();i++){
            int c = mp.get(s.charAt(i));
            if(i+1==s.length() || c >= mp.get(s.charAt(i+1))){
                ans+=c;
            }
            else{
                ans += mp.get(s.charAt(i+1)) - c;
                i++;
            }
        }
        return ans;
    }
}
```

# Optimal way without extra space

```java
class Solution {
    public int romanToInt(String s) {
        int ans = 0;
        int n = s.length();
        int i=0;
        while(i<n){
            char ch = s.charAt(i);
            if(ch == 'I'){
                if(i+1<n && s.charAt(i+1) == 'V'){ans +=4;i++;}
                else if(i+1<n && s.charAt(i+1) == 'X'){ans+=9;i++;}
                else ans++;
            }
            else if(ch == 'X'){
                if(i+1<n && s.charAt(i+1) == 'L'){ans +=40;i++;}
                else if(i+1<n && s.charAt(i+1) == 'C'){ans+=90;i++;}
                else ans+=10;
            }
            else if(ch == 'C'){
                if(i+1<n && s.charAt(i+1) == 'D'){ans +=400;i++;}
                else if(i+1<n && s.charAt(i+1) == 'M'){ans+=900;i++;}
                else ans+=100;
            }
            else if(ch == 'V'){
                ans+=5;
            }
            else if(ch == 'L'){
                ans+=50;
            }
            else if(ch == 'D'){
                ans += 500;
            }
            else if(ch == 'M'){
                ans += 1000;
            }
            i++;
        }
        return ans;
    }
}
```


OR

```java
class Solution {
    int findVal(char i){
        switch(i){
            case 'I': return 1;
            case 'V':return 5;
            case 'X':return 10;
            case 'L':return 50;
            case 'C':return 100;
            case 'D':return 500;
            case 'M':return 1000;
        }
        return -1;
    }
    public int romanToInt(String s) {
        int ans=0;
        if(s.length()==0)return 0;
        for(int i=0;i<s.length();i++){
            int currIdx = findVal(s.charAt(i));
            if(i+1==s.length() || currIdx >= findVal(s.charAt(i+1))){
                ans+=currIdx;
            }
            else{
                ans += findVal(s.charAt(i+1)) - currIdx;
                i++;
            }
        }
        return ans;
    }
}
```


> NOTE
> To map countable values we can make a function using Switch case as well to reduce the overhead of map data structure but this will search linearly.