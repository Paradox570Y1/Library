[Link](https://www.geeksforgeeks.org/problems/fractional-knapsack-1587115620/1)

Difficulty: **Medium**Accuracy: **32.46%**Submissions: **318K+**Points: **4**Average Time: **20m**

Given two arrays, `**val[]**` and **`wt[]`**, representing the values and weights of items, and an integer **`capacity`** representing the maximum weight a knapsack can hold, determine the maximum total value that can be achieved by putting items in the knapsack. You are allowed to break items into fractions if necessary.  
Return the maximum value as a double, rounded to 6 decimal places.

**Examples :**

**Input:** val[] = [60, 100, 120], wt[] = [10, 20, 30], capacity = 50
**Output:** 240.000000
**Explanation:** Take the item with value 60 and weight 10, value 100 and weight 20 and split the third item with value 120 and weight 30, to fit it into weight 20. so it becomes (120/30)*20=80, so the total value becomes 60+100+80.0=240.0 Thus, total maximum value of item we can have is 240.00 from the given capacity of sack. 

**Input:** val[] = [60, 100], wt[] = [10, 20], capacity = 50
**Output:** 160.000000
**Explanation:** Take both the items completely, without breaking. Total maximum value of item we can have is 160.00 from the given capacity of sack.

**Input:** val[] = [10, 20, 30], wt[] = [5, 10, 15], capacity = 100
**Output:** 60.000000  
**Explanation:** In this case, the knapsack capacity exceeds the combined weight of all items (5 + 10 + 15 = 30). Therefore, we can take all items completely, yielding a total maximum value of 10 + 20 + 30 = 60.000000.  

**Constraints:**  
1 <= val.size=wt.size <= 105  
1 <= capacity <= 109  
1 <= val[i], wt[i] <= 104

```java
class Solution {
    // Function to get the maximum total value in the knapsack.
    class Item{
        double val;
        double weight;
        Item(double val,double weight){
            this.val = val;
            this.weight = weight;
        }
    }
    double fractionalKnapsack(List<Integer> val, List<Integer> wt, int capacity) {
        // code here
        int n = val.size();
        Item[] items = new Item[n];
        for(int i=0;i<n;i++){
            int value = val.get(i);
            int weight = wt.get(i);
            items[i] = new Item(value/(double)weight,weight);
        }
        Arrays.sort(items,(a,b)->Double.compare(b.val,a.val));
        int i=0;
        double ans=0.000000;
        while(capacity>0 && i<n){
            if(capacity >= items[i].weight){
                ans+= items[i].val*items[i].weight;
                capacity -= items[i].weight;
            }
            else break;
            i++;
        }
        if(capacity>0 && i<n)ans+=items[i].val*capacity;
        return ans;
    }
}
```


```java
//Other way of sorting
class itemComparator implements Comparator<Item>
{
    @Override
    public int compare(Item a, Item b) 
    {
        double r1 = (double)(a.value) / (double)(a.weight); 
        double r2 = (double)(b.value) / (double)(b.weight); 
        if(r1 < r2) return 1; 
        else if(r1 > r2) return -1; 
        else return 0; 
    }
}
Arrays.sort(arr, new itemComparator());
```