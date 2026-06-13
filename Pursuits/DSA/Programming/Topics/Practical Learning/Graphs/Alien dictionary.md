[Link](https://www.naukri.com/code360/problems/alien-dictionary_630423)
[Link2](https://neetcode.io/problems/foreign-dictionary/question?list=neetcode150)
## Problem statement

You have been given a sorted (lexical order) dictionary of an alien language.

Write a function that returns the order of characters as a string in the alien language. This dictionary will be given to you as an array of strings called _**'dictionary'**_, of size _**'N'**_.


**Example :**

```
If the dictionary consists of the following words:-
["caa", "aaa", "aab"], and 'K' is 3.

Then, the order of the alphabet is -
['c', 'a', 'b']
```

**Note:**

```
If the language consists of four letters, the four letters should be the starting four letters of the English language. 

However, their order might differ in the alien language.
```

Detailed explanation ( Input/output format, Notes, Images )

**Sample Input 1 :**

```
3 1
a aa aaa
```

**Sample Output 1 :**

```
true
```

**Explanation For Sample Output 1 :**

```
The words are 'a', 'aa', and 'aaa'. Since the unique character here is 'a', the array to be returned will just be ['a']. 

The 'true' being printed signifies that the output returned by the function is valid.
```

**Sample Input 2 :**

```
3 3
caa aaa aab
```

**Sample Output 2 :**

```
true
```

**Constraints :**

```
1 ≤ N ≤ 300
1 ≤ K ≤ 26
1 ≤ Length of words ≤ 50

Time Limit: 1 sec
```


- All the characters present in strings is first k characters from ascending alphabets.


# Using BFS

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Queue;
import java.util.LinkedList;
public class Solution {
    public static String getAlienLanguage(String [] dict, int K) {
        List<int[]> list = new ArrayList<>();
        for (int i = 0; i < dict.length - 1; i++) {
            String s1 = dict[i];
            String s2 = dict[i+1];
            int n = Math.min(s1.length(), s2.length());
            for (int j = 0; j < n; j++) {
                if (s1.charAt(j) != s2.charAt(j)) {
                    list.add(new int[]{s1.charAt(j) - 'a', s2.charAt(j) - 'a'});
                    break;
                }
            }
        }
        List<List<Integer>> adjList = new ArrayList<>();
        int[] indegree = new int[K];
        for (int i = 0; i < K; i++) {
            adjList.add(new ArrayList<>());
        }
        for (int[] edge : list) {
            int u = edge[0];
            int v = edge[1];
            adjList.get(u).add(v);
            indegree[v]++;
        }

        Queue<Integer> q = new LinkedList<>();

        for (int i = 0; i < K; i++) {
            if (indegree[i] == 0) {
                q.offer(i);
            }
        }
        StringBuilder res = new StringBuilder();
        while (!q.isEmpty()) {
            int node = q.poll();
            res.append((char)('a' + node));
            for (int next : adjList.get(node)) {
                indegree[next]--;
                if (indegree[next] == 0) q.offer(next);
            }
        }
        if (res.length() < K) return "";
        return res.toString();
    }
}
```

OR

```java
import java.util.*;
public class Solution {
    public static String getAlienLanguage(String []dictionary, int k) {
        // Write your code here.
        ArrayList<Integer>[] graph = new ArrayList[k];
        for (int i = 0; i < k; i++) {
            graph[i] = new ArrayList<>();
        }
        int n = dictionary.length;
        int inDegree[] = new int[k];
        for (int i = 1; i < n; i++) {
            String w1 = dictionary[i-1], w2 = dictionary[i];
            if (w1.length() > w2.length() && w1.startsWith(w2)) return "";
            int len = Math.min(w1.length(), w2.length());
            for (int j = 0; j < len; j++) {
                char a = w1.charAt(j), b = w2.charAt(j);
                if (a != b) {
                    graph[a-'a'].add(b-'a');
                    inDegree[b-'a']++;
                    break;
                }
            }
        }
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < k ; i++) {
            if (inDegree[i] == 0) queue.offer(i);
        }
        StringBuilder res = new StringBuilder();
        while (!queue.isEmpty()) {
            int u = queue.poll();
            res.append((char)('a' + u));
            for (int v : graph[u]) {
                inDegree[v]--;
                if (inDegree[v] == 0) queue.offer(v);
            }
        }
        return res.toString();
    }

}
```

# Using DFS

```java
import java.util.List;
import java.util.ArrayList;
public class Solution {
    private static boolean[] vis;
    private static boolean[] visPath;
    private static StringBuilder res;
    public static String getAlienLanguage(String [] dict, int K) {
        List<int[]> list = new ArrayList<>();
        for (int i = 0; i < dict.length - 1; i++) {
            String s1 = dict[i];
            String s2 = dict[i+1];
            int n = Math.min(s1.length(), s2.length());
            for (int j = 0; j < n; j++) {
                if (s1.charAt(j) != s2.charAt(j)) {
                    list.add(new int[]{s1.charAt(j) - 'a', s2.charAt(j) - 'a'});
                    break;
                }
            }
        }
        List<List<Integer>> adjList = new ArrayList<>();
        vis = new boolean[K];
        visPath = new boolean[K];
        res = new StringBuilder();
        for (int i = 0; i < K; i++) {
            adjList.add(new ArrayList<>());
        }
        for (int[] edge : list) {
            int u = edge[0];
            int v = edge[1];
            adjList.get(u).add(v);
        }
        
        for (int node = 0; node < K; node++) {
            if (!vis[node]) {
                if (isCyclic(adjList, node)) return "";
            }
        }
        return res.reverse().toString();
    }
    private static boolean isCyclic(List<List<Integer>> adjList, int node) {
        vis[node] = true;
        visPath[node] = true;
        for (int next : adjList.get(node)) {
            if (!vis[next] && isCyclic(adjList, next)) return true;
            else if(visPath[next]) return true;
        }
        res.append((char)(node + 'a'));
        visPath[node] = false;
        return false;
    }
}
```

- For cyclic dependency Topological order is not possible and hence above algo works.
![[Pasted image 20250906201439.png|300]]


```java
import java.util.*;
public class Solution {
    public static String getAlienLanguage(String []dictionary, int k) {
        // Write your code here.
        Map<Character, List<Character>> graph = new HashMap<>();
        for (String s : dictionary) {
            for (char ch : s.toCharArray()) {
                graph.putIfAbsent(ch, new ArrayList<>());
            }
        }
        int n = dictionary.length;
        for (int i = 1; i < n; i++) {
            String w1 = dictionary[i-1], w2 = dictionary[i];
            if (w1.length() > w2.length() && w1.startsWith(w2)) return "";
            int len = Math.min(w1.length(), w2.length());
            for (int j = 0; j < len; j++) {
                char a = w1.charAt(j), b = w2.charAt(j);
                if (a != b) {
                    graph.get(a).add(b);
                    break;
                }
            }
        }

        StringBuilder res = new StringBuilder();
        boolean[] vis = new boolean[26];
        boolean[] visPath = new boolean[26];
        for (char V : graph.keySet()) {
            if (!vis[V-'a']) {
                if(dfs(graph, V, vis, visPath, res)) return "";
            }
        }
        return res.reverse().toString();
    }

    private static boolean dfs(Map<Character, List<Character>> graph, char v, boolean[] vis, boolean[] visPath, StringBuilder res) {
        vis[v-'a'] = visPath[v-'a'] = true;
        for (char u : graph.get(v)) {
            if (!vis[u-'a']) {
                if (dfs(graph, u, vis, visPath, res)) return true;
            } else if (visPath[u-'a']) return true;
        }
        visPath[v-'a'] = false;
        res.append(v);
        return false;
    }
}
```

OR

```java
import java.util.*;
public class Solution {
    public static String getAlienLanguage(String []dictionary, int k) {
        // Write your code here.
        Map<Character, List<Character>> graph = new HashMap<>();
        for (int i = 0; i < k; i++) {  // k is number of letter used in words from a
            graph.put((char)('a'+i), new ArrayList<>());
        }
        int n = dictionary.length;
        for (int i = 1; i < n; i++) {
            String w1 = dictionary[i-1], w2 = dictionary[i];
            //remove below line in case of no need to verify
            if (w1.length() > w2.length() && w1.startsWith(w2)) return "";
            int len = Math.min(w1.length(), w2.length());
            for (int j = 0; j < len; j++) {
                char a = w1.charAt(j), b = w2.charAt(j);
                if (a != b) {
                    graph.get(a).add(b);
                    break;
                }
            }
        }

        StringBuilder res = new StringBuilder();
        boolean[] vis = new boolean[26];
        boolean[] visPath = new boolean[26];
        for (char V : graph.keySet()) {
            if (!vis[V-'a']) {
                if(dfs(graph, V, vis, visPath, res)) return "";
            }
        }
        return res.reverse().toString();
    }

    private static boolean dfs(Map<Character, List<Character>> graph, char v, boolean[] vis, boolean[] visPath, StringBuilder res) {
        vis[v-'a'] = visPath[v-'a'] = true;
        for (char u : graph.get(v)) {
            if (!vis[u-'a']) {
                if (dfs(graph, u, vis, visPath, res)) return true;
            } else if (visPath[u-'a']) return true;
        }
        visPath[v-'a'] = false;
        res.append(v);
        return false;
    }
}
```

OR

```java
import java.util.*;
public class Solution {
    public static String getAlienLanguage(String []dictionary, int k) {
        // Write your code here.
        ArrayList<Integer>[] graph = new ArrayList[k];
        for (int i = 0; i < k; i++) {
            graph[i] = new ArrayList<>();
        }
        int n = dictionary.length;
        for (int i = 1; i < n; i++) {
            String w1 = dictionary[i-1], w2 = dictionary[i];
            int len = Math.min(w1.length(), w2.length());
            for (int j = 0; j < len; j++) {
                char a = w1.charAt(j), b = w2.charAt(j);
                if (a != b) {
                    graph[a-'a'].add(b-'a');
                    break;
                }
            }
        }

        StringBuilder res = new StringBuilder();
        boolean[] vis = new boolean[26];
        boolean[] visPath = new boolean[26];
        for (int V = 0; V < k; V++) {
            if (!vis[V]) {
                if(dfs(graph, V, vis, visPath, res)) return "";
            }
        }
        return res.reverse().toString();
    }

    private static boolean dfs(ArrayList<Integer>[] graph, int v, boolean[] vis, boolean[] visPath, StringBuilder res) {
        vis[v] = visPath[v] = true;
        for (int u : graph[v]) {
            if (!vis[u]) {
                if (dfs(graph, u, vis, visPath, res)) return true;
            } else if (visPath[u]) return true;
        }
        visPath[v] = false;
        res.append((char)('a' + v));
        return false;
    }
}
```

OR
Even normal DFS works here as no need to verify

```java
import java.util.*;
public class Solution {
    public static String getAlienLanguage(String []dictionary, int k) {
        // Write your code here.
        ArrayList<Integer>[] graph = new ArrayList[k];
        for (int i = 0; i < k; i++) {
            graph[i] = new ArrayList<>();
        }
        int n = dictionary.length;
        for (int i = 1; i < n; i++) {
            String w1 = dictionary[i-1], w2 = dictionary[i];
            int len = Math.min(w1.length(), w2.length());
            for (int j = 0; j < len; j++) {
                char a = w1.charAt(j), b = w2.charAt(j);
                if (a != b) {
                    graph[a-'a'].add(b-'a');
                    break;
                }
            }
        }

        StringBuilder res = new StringBuilder();
        boolean[] vis = new boolean[26];
        for (int V = 0; V < k; V++) {
            if (!vis[V]) {
                dfs(graph, V, vis, res);
            }
        }
        return res.reverse().toString();
    }

    private static void dfs(ArrayList<Integer>[] graph, int v, boolean[] vis, StringBuilder res) {
        vis[v] = true;
        for (int u : graph[v]) {
            if (!vis[u]) {
                dfs(graph, u, vis, res);
            }
        }
        res.append((char)('a' + v));
    }
}
```