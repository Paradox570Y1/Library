[451. Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/)

Given a string `s`, sort it in **decreasing order** based on the **frequency** of the characters. The **frequency** of a character is the number of times it appears in the string.

Return _the sorted string_. If there are multiple answers, return _any of them_.

**Example 1:**

**Input:** s = "tree"
**Output:** "eert"
**Explanation:** 'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.

**Example 2:**

**Input:** s = "cccaaa"
**Output:** "aaaccc"
**Explanation:** Both 'c' and 'a' appear three times, so both "cccaaa" and "aaaccc" are valid answers.
Note that "cacaca" is incorrect, as the same characters must be together.

**Example 3:**

**Input:** s = "Aabb"
**Output:** "bbAa"
**Explanation:** "bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.

**Constraints:**

- `1 <= s.length <= 5 * 105`
- `s` consists of uppercase and lowercase English letters and digits.


# using basic Hashing

```d
Collections.sort(list, comparator) → Older approach (before Java 8).

list.sort(comparator) → Modern, direct, and preferred approach since
                        Java 8.
```

```java
class Solution {
    public String frequencySort(String s) {
        HashMap<Character,Integer> mp = new HashMap<>();
        for(char c:s.toCharArray()){
            mp.put(c,mp.getOrDefault(c,0)+1);
        }
        List<Map.Entry<Character,Integer>> list = new ArrayList<>(mp.entrySet());
        list.sort((entry1,entry2)->entry2.getValue().compareTo(entry1.getValue()));
        StringBuilder sb = new StringBuilder();
        for(Map.Entry<Character,Integer> e:list){
            int n = e.getValue();
            for(int i=0;i<n;i++){
                sb.append(e.getKey());
            }
        }
        return sb.toString();
    }
}
```

**Max Heap Implementation**

```java
class Solution {
    public String frequencySort(String s) {
        HashMap<Character,Integer> hm = new HashMap<>();
        for(char ch:s.toCharArray()){
            hm.put(ch,hm.getOrDefault(ch,0)+1);
        }
        PriorityQueue<Map.Entry<Character,Integer>> maxHeap = new PriorityQueue<>((a,b)->b.getValue()-a.getValue());
        maxHeap.addAll(hm.entrySet());
        StringBuilder sb = new StringBuilder();
        while(!maxHeap.isEmpty()){
            Map.Entry<Character,Integer> entry = maxHeap.poll();
            char ch = entry.getKey();
            int freq = entry.getValue();
            while(freq-->0){
                sb.append(ch);
            }
        }
        return sb.toString();
    }
}
```
# Optimal

```java
class Solution {
    public String frequencySort(String s) {
        int hash[] = new int[128];
        char ans[] = new char[s.length()];
        for(char c:s.toCharArray()){
            hash[(int)c]++;
        }
        int i=0;
        while(i<s.length()){
            int ch = '.';
            for(int j=0;j<128;j++){
                if(hash[j]>hash[ch]) ch = j;
            }
            while(hash[ch]-->0){
                ans[i++] = (char)ch;
            }
        }
        return new String(ans);
    }
}
```