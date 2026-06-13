[Link](https://leetcode.com/problems/number-of-equivalent-domino-pairs/description/)

```java
class Solution {
    public int numEquivDominoPairs(int[][] dominoes) {
        int hash[] = new int[100];
        int temp;
        for(int i=0;i<dominoes.length;i++){
            int a = dominoes[i][0],b=dominoes[i][1];
            if(a<b)temp = a*10+b;
            else temp = b*10+a;
            hash[temp]++;
        }
        int ans=0;
        for(int i=0;i<100;i++){
            int t = hash[i];
            if(t>1)ans+=t*(t-1)/2;
        }
        return ans;
    }
}
```