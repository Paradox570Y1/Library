[30. Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)
You are given a string `s` and an array of strings `words`. All the strings of `words` are of **the same length**.

A **concatenated string** is a string that exactly contains all the strings of any permutation of `words` concatenated.

- For example, if `words = ["ab","cd","ef"]`, then `"abcdef"`, `"abefcd"`, `"cdabef"`, `"cdefab"`, `"efabcd"`, and `"efcdab"` are all concatenated strings. `"acdbef"` is not a concatenated string because it is not the concatenation of any permutation of `words`.

Return an array of _the starting indices_ of all the concatenated substrings in `s`. You can return the answer in **any order**.

**Example 1:**

**Input:** s = "barfoothefoobarman", words = ["foo","bar"]

**Output:** [0,9]

**Explanation:**

The substring starting at 0 is `"barfoo"`. It is the concatenation of `["bar","foo"]` which is a permutation of `words`.  
The substring starting at 9 is `"foobar"`. It is the concatenation of `["foo","bar"]` which is a permutation of `words`.

**Example 2:**

**Input:** s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]

**Output:** []

**Explanation:**

There is no concatenated substring.

**Example 3:**

**Input:** s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]

**Output:** [6,9,12]

**Explanation:**

The substring starting at 6 is `"foobarthe"`. It is the concatenation of `["foo","bar","the"]`.  
The substring starting at 9 is `"barthefoo"`. It is the concatenation of `["bar","the","foo"]`.  
The substring starting at 12 is `"thefoobar"`. It is the concatenation of `["the","foo","bar"]`.

**Constraints:**

- `1 <= s.length <= 104`
- `1 <= words.length <= 5000`
- `1 <= words[i].length <= 30`
- `s` and `words[i]` consist of lowercase English letters.
# Brute

TLE
```java
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        int n = s.length();
        int subWinSize = words[0].length();
        int winCnt = words.length;
        int winSize = subWinSize*winCnt;
        int j=0;
        List<Integer> li = new ArrayList<>();
        HashMap<String,Integer> mp = new HashMap<>();
        for(int i=0;i<winCnt;i++){
            mp.put(words[i],mp.getOrDefault(words[i],0)+1);
        }
        int cnt=0;
        for(int i=0;i<n;i++){
            if(i<winSize-1)continue;
            for(int st=j;st<=i;st+=subWinSize){
                String word = s.substring(st,st+subWinSize);
                mp.put(word,mp.getOrDefault(word,0)-1);
                if(mp.get(word)>=0)cnt++;
            }
            if(cnt<winCnt){
                for(int st=j;st<=i;st+=subWinSize){
                    String word = s.substring(st,st+subWinSize);
                    mp.put(word,mp.getOrDefault(word,0)+1);
                }
                cnt=0;
            }
            int temp =j;
            if(cnt==winCnt){
                li.add(j);
                while(cnt!=0 && j<=i){
                    String word = s.substring(j,j+subWinSize);
                    mp.put(word,mp.get(word)+1);
                    if(mp.get(word)>0)cnt--;
                    j+=subWinSize;
                }
                j=temp;
            }
            
            j++;
        }
        return li;
    }
}
```


```java
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        HashMap<String,Integer> mp = new HashMap<>();
        int n = words.length;
        List<Integer> li= new ArrayList<>();
        for(int i=0;i<n;i++){
            String word = words[i];
            mp.put(word,mp.getOrDefault(word,0)+1);
        }
        int subWinLen = words[0].length();
        int winCnt = words.length;
        int winLen = subWinLen * winCnt;
        int j=0;
        HashMap<String,Integer> smp = new HashMap<>();
        for(int i=0;i<s.length();i++){
            if(i-j+1 < winLen)continue;
            smp.clear();
            for(int st=j;st<=i;st+=subWinLen){
                String subDiv = s.substring(st,st+subWinLen);
                smp.put(subDiv,smp.getOrDefault(subDiv,0)+1);
            }
            if(mp.equals(smp))li.add(j);
            j++;
        }
        return li;
    }
}
```



# Optimal

```java
import java.util.*;

class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> result = new ArrayList<>();
        int wordLength = words[0].length();
        int totalWords = words.length;
        int totalLength = wordLength * totalWords;
        int sLength = s.length();
        
        if (sLength < totalLength) {
            return result;
        }
        
        Map<String, Integer> wordCount = new HashMap<>();
        for (String word : words) {
            wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
        }
        
        for (int i = 0; i < wordLength; i++) {
            int left = i;
            int right = i;
            Map<String, Integer> currentCount = new HashMap<>();
            int wordsFound = 0;
            
            while (right + wordLength <= sLength) {
                String currentWord = s.substring(right, right + wordLength);
                right += wordLength;
                
                if (!wordCount.containsKey(currentWord)) {
                    currentCount.clear();
                    wordsFound = 0;
                    left = right;
                } else {
                    currentCount.put(currentWord, currentCount.getOrDefault(currentWord, 0) + 1);
                    wordsFound++;
                    
                    while (currentCount.get(currentWord) > wordCount.get(currentWord)) {
                        String leftWord = s.substring(left, left + wordLength);
                        currentCount.put(leftWord, currentCount.get(leftWord) - 1);
                        wordsFound--;
                        left += wordLength;
                    }
                    
                    if (wordsFound == totalWords) {
                        result.add(left);
                    }
                }
            }
        }
        
        return result;
    }
}
```