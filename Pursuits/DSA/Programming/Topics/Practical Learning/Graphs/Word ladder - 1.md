[127. Word Ladder](https://leetcode.com/problems/word-ladder/)

A **transformation sequence** from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words `beginWord -> s1 -> s2 -> ... -> sk` such that:

- Every adjacent pair of words differs by a single letter.
- Every `si` for `1 <= i <= k` is in `wordList`. Note that `beginWord` does not need to be in `wordList`.
- `sk == endWord`

Given two words, `beginWord` and `endWord`, and a dictionary `wordList`, return _the **number of words** in the **shortest transformation sequence** from_ `beginWord` _to_ `endWord`_, or_ `0` _if no such sequence exists._

**Example 1:**

**Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
**Output:** 5
**Explanation:** One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.

**Example 2:**

**Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
**Output:** 0
**Explanation:** The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.

**Constraints:**

- `1 <= beginWord.length <= 10`
- `endWord.length == beginWord.length`
- `1 <= wordList.length <= 5000`
- `wordList[i].length == beginWord.length`
- `beginWord`, `endWord`, and `wordList[i]` consist of lowercase English letters.
- `beginWord != endWord`
- All the words in `wordList` are **unique**.


# Using BFS
Brute 1 (TLE)
```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        HashMap<String, ArrayList<String>> adjMap = new HashMap<>();
        HashSet<String> vis = new HashSet<>();
        adjMap.put(beginWord, new ArrayList<>());
        for(String s: wordList) {
            if(s.length() == beginWord.length()) {
                adjMap.put(s, new ArrayList<>());
            }
        }
        
        for (String s: adjMap.keySet()) {
            if (hammingDistance(beginWord, s) == 1) {
                adjMap.get(s).add(beginWord);
            }
            vis.add(beginWord);
        }

        for (String word: wordList) {
            if (vis.contains(word)) continue;
            for (String node: adjMap.keySet()) {
                if (hammingDistance(word, node) == 1) {
                    adjMap.get(node).add(word);
                }
            }
            vis.add(word);
        }
        vis = new HashSet<>();
        Queue<String> queue = new LinkedList<>();
        queue.offer(beginWord);
        vis.add(beginWord);

        int res = 0;
        while(!queue.isEmpty()) {
            res++;
            int size = queue.size();
            while (size-- > 0) {
                String cur = queue.poll();
                if (cur.equals(endWord)) {
                    return res;
                }
                for (String node: adjMap.get(cur)) {
                    if (!vis.contains(node)) {
                        vis.add(node);
                        queue.offer(node);
                    }
                }
            }
        }
        return 0;
    }
    private int hammingDistance(String s1, String s2) {
        int distinctCnt = 0;
        for (int i = 0; i < s1.length(); i++) {
            if (s1.charAt(i) != s2.charAt(i)) {
                distinctCnt++;
            }
        }
        return distinctCnt;
    }
}
```



```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        HashSet<String> vis = new HashSet<>();
        for (String word:wordList) {
            vis.add(word);
        }
        Queue<String> queue = new LinkedList<>();
        queue.offer(beginWord);
        vis.add(beginWord);

        int res = 0;
        while(!queue.isEmpty()) {
            res++;
            int size = queue.size();
            while (size-- > 0) {
                String cur = queue.poll();
                if (cur.equals(endWord)) {
                    return res;
                }
                for (int k = 0; k < beginWord.length(); k++) {
                    for (char c = 'a'; c <= 'z'; c++) {
                        String newWord = cur.substring(0, k) + c + cur.substring(k+1);
                        if(vis.contains(newWord)) {
                            vis.remove(newWord);
                            queue.offer(newWord);
                        }
                    }
                }
            }
        }
        return 0;
    }
}
```


## ⚖️ Comparison Table

| Approach                         | Time Complexity | Space Complexity | Notes                                                 |
| -------------------------------- | --------------- | ---------------- | ----------------------------------------------------- |
| **Brute 1** (Adjacency List)     | **O(N² · L)**   | **O(N²)**        | Heavy preprocessing; wastes time building dense graph |
| **Brute 2** (Generate Neighbors) | **O(N · L)**    | **O(N)**         | Much more efficient; avoids storing edges explicitly  |

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        HashSet<String> vis = new HashSet<>();
        for (String word:wordList) {
            vis.add(word);
        }
        Queue<String> queue = new LinkedList<>();
        queue.offer(beginWord);
        vis.add(beginWord);

        int res = 0;
        while(!queue.isEmpty()) {
            res++;
            int size = queue.size();
            while (size-- > 0) {
                String cur = queue.poll();
                if (cur.equals(endWord)) {
                    return res;
                }
                for (int k = 0; k < beginWord.length(); k++) {
                    for (char c = 'a'; c <= 'z'; c++) {
                        String newWord = cur.substring(0, k) + c + cur.substring(k+1);
                        if(vis.contains(newWord)) {
                            vis.remove(newWord);
                            queue.offer(newWord);
                        }
                    }
                }
            }
        }
        return 0;
    }
}
```


Optimization using StringBuilder
```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        HashSet<String> vis = new HashSet<>();
        for (String word:wordList) {
            vis.add(word);
        }
        Queue<String> queue = new LinkedList<>();
        queue.offer(beginWord);
        vis.add(beginWord);

        int res = 0;
        while(!queue.isEmpty()) {
            res++;
            int size = queue.size();
            while (size-- > 0) {
                String cur = queue.poll();
                if (cur.equals(endWord)) {
                    return res;
                }
                for (int k = 0; k < beginWord.length(); k++) {
                    StringBuilder word = new StringBuilder(cur);
                    for (char c = 'a'; c <= 'z'; c++) {
                        word.setCharAt(k, c);
                        if(vis.contains(word.toString())) {
                            vis.remove(word.toString());
                            queue.offer(word.toString());
                        }
                    }
                }
            }
        }
        return 0;
    }
}
```

Conculsion

Approach 1

```java
class Solution {
    private int transform(List<String> wordList, String beginWord, String endWord) {
        Queue<String> q = new LinkedList<>();
        boolean vis[] = new boolean[wordList.size()];
        q.offer(beginWord);
        int count = 1;
        while (!q.isEmpty()) {
            int size = q.size();
            while (size-->0) {
                String initialWord = q.poll();
                if (endWord.equals(initialWord)) return count;
                for (int i = 0; i < wordList.size(); i++) {
                    String finalWord = wordList.get(i);
                    if (!vis[i] && canTransform(initialWord, finalWord)) {
                        vis[i] = true;
                        q.offer(finalWord);
                    }
                }
            }
            count++;
        }
        return 0;
    }
    private boolean canTransform(String a, String b) {
        int diff = 0;
        for (int i = 0; i < a.length(); i++) {
            if (a.charAt(i) != b.charAt(i)) diff++;
            if (diff > 1) return false;
        }
        return (diff == 1);
    }
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        if (!wordList.contains(endWord)) return 0;
        int res = transform(wordList, beginWord, endWord);
        if (res >= (int) 1e9) return 0;
        return res;
    }
}
```

OR
Approach 2
```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> wordSet = new HashSet<>();
        for (String word : wordList) {
            wordSet.add(word);
        }

        Queue<String> queue = new LinkedList<>();
        queue.offer(beginWord);
        int count = 1;
        while (!queue.isEmpty()) {
            int size = queue.size();
            while (size-- > 0) {
                StringBuilder word = new StringBuilder(queue.poll());
                if (word.toString().equals(endWord)) return count;
                //transforms this word
                for (int i = 0; i < word.length(); i++) {
                    char letter = word.charAt(i);
                    for (char ch = 'a'; ch <= 'z'; ch++) {
                        word.setCharAt(i, ch);
                        String transformedWord = word.toString();
                        if (wordSet.contains(transformedWord)) {
                            queue.offer(transformedWord);
                            wordSet.remove(transformedWord);
                        }
                    }
                    word.setCharAt(i, letter);
                }
            }
            count++;
        }
        return 0;
    }
}
```

# Using Bi-Directional BFS  (Optimal)

- Create Two Sets which initially contain begin Word and end Word respectively.
- Now try changing 1 letter in all ways possible in smaller set of the two in all containing strings. 
- While performing above steps check if new word formed is present in other set if it is then return count of steps till now + 1 as end Word is also included in total steps. Otherwise add keep adding it into buffer set if that word exist in wordlist and not visited earlier.
- Now point the set that you chose in second step to the buffer set and increase the step count by 1.


```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> beginSet = new HashSet<>();
        Set<String> endSet = new HashSet<>();
        Set<String> wordSet = new HashSet<>(wordList);
        beginSet.add(beginWord);
        endSet.add(endWord);
        wordSet.remove(beginWord);
        if(wordSet.contains(endWord))wordSet.remove(endWord);
        else return 0;

        int steps = 1;
        
        while (!beginSet.isEmpty()  && !endSet.isEmpty()) {
            if (beginSet.size() > endSet.size()) {
                Set<String> temp = beginSet;
                beginSet = endSet;
                endSet = temp;
            }
            Set<String> bufferSet = new HashSet<>();
            for (String s : beginSet) {
                char[] word = s.toCharArray();
                for (int i = 0; i < word.length; i++) {
                    for (char c = 'a'; c <= 'z'; c++) {
                        if (word[i] == c) continue;
                        String transformation = transformWord(word, i, c);
                        if (endSet.contains(transformation)) return steps + 1;
                        if (wordSet.contains(transformation)) {
                            wordSet.remove(transformation);
                            bufferSet.add(transformation);
                        }
                    }
                }
            }
            beginSet = bufferSet;
            steps++;
        }
        return 0;
    }
    private String transformWord(char[] word, int pos, char ch) {
        char temp = word[pos];
        word[pos] = ch;
        String res = new String(word);
        word[pos] = temp;
        return res;
    }
}
```

OR

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> beginSet = new HashSet<>();
        Set<String> endSet = new HashSet<>();
        Set<String> wordSet = new HashSet<>(wordList);
        if (!wordSet.contains(endWord)) return 0;
        beginSet.add(beginWord);
        endSet.add(endWord);
        if(wordSet.contains(beginWord)) wordSet.remove(beginWord);
        wordSet.remove(endWord);
        int count = 1;
        while (!beginSet.isEmpty() && !endSet.isEmpty()) {
            if (beginSet.size() > endSet.size()) {
                Set<String> temp = beginSet;
                beginSet = endSet;
                endSet = temp;
            }
            Set<String> buffer = new HashSet<>();
            for (String word : beginSet) {
                StringBuilder sb = new StringBuilder(word);
                for (int i = 0; i < word.length(); i++) {
                    char letter = sb.charAt(i);
                    for (char ch = 'a'; ch <= 'z'; ch++) {
                        sb.setCharAt(i, ch);
                        String transformedWord = sb.toString();
                        if (endSet.contains(transformedWord)) return count + 1;
                        if (wordSet.contains(transformedWord)) {
                            buffer.add(transformedWord);
                            wordSet.remove(transformedWord);
                        }
                    }
                    sb.setCharAt(i, letter);
                }
            }
            beginSet = buffer;
            count++;
        }
        return 0;
    }
}
```