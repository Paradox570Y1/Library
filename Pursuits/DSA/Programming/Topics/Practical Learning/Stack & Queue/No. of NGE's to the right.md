[Link](https://www.geeksforgeeks.org/problems/number-of-nges-to-the-right/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=number-of-nges-to-the-right)
# Brute
TC-> O(N²)
SC-> O(N)
```java
class Solution {
    
  public static int[] count_NGEs(int N, int arr[], int queries, int indices[]) {
    // code here
    int n = arr.length;
    int[] ans = new int[queries];
    for(int i=0;i<queries;i++){
        int idx = indices[i];
        int ele = arr[idx];
        int cnt=0;
        for(int j=idx+1;j<n;j++){
            if(arr[j]>ele)cnt++;
        }
        ans[i] = cnt;
    }
    return ans;
  }
}
```


# Better 
- Only in case of no duplicates

```java
class Solution {
  private static void merge(int[] arr,int low,int mid,int high,int[] hash){
     int left = low;
     int right = mid+1;
     List<Integer> li = new ArrayList<>();
     while(left<=mid && right<=high){
         if(arr[left]<arr[right]){
            li.add(arr[left]);
            hash[arr[left++]]+=(high-right+1);
         }
         else{
            li.add(arr[right++]);
         }
     }
     while(left<=mid){
         li.add(arr[left++]);
     }
     while(right<=high){
         li.add(arr[right++]);
     }
     for(int i=low;i<=high;i++){
         arr[i] = li.get(i-low);
     }
     return;
  }
  private static void mergeSort(int[] arr,int low,int high,int[] hash){
      if(low>=high)return;
      int mid = (low+high)>>1;
      mergeSort(arr,low,mid,hash);
      mergeSort(arr,mid+1,high,hash);
      merge(arr,low,mid,high,hash);
  }
  public static int[] count_NGEs(int N, int arr[], int queries, int indices[]) {
    // code here
    int maxi = Integer.MIN_VALUE;
    int temp[] = new int[N];
    for(int i=0;i<N;i++){
        maxi = Math.max(maxi,arr[i]);
        temp[i] = arr[i];
    }
    int hash[] = new int[maxi+1];
    mergeSort(temp,0,N-1,hash);
    int ans[] = new int[queries];
    for(int i=0;i<queries;i++){
        ans[i] = hash[arr[indices[i]]];
    }
    return ans;
  }
}
```

- In case of duplicates make use of custom class or data types

```java
// User function Template for Java

class Solution {
    static int hash[];
    static class Pair{
        int val;
        int idx;
        Pair(int x,int y){
            val=x;
            idx=y;
        }
    }
    private static void merge(Pair[] arr,int low,int mid ,int high){
        int left = low;
        int right = mid+1;
        List<Pair> li =new ArrayList<>();
        while(left<=mid && right <=high){
            if(arr[left].val<arr[right].val){
                li.add(arr[left]);
                hash[arr[left].idx]+=(high-right+1);
                left++;
            }
            else{
                li.add(arr[right]);
                right++;
            }
        }
        while(left<=mid){
            li.add(arr[left]);
            left++;
        }
        while(right<=high){
            li.add(arr[right]);
            right++;
        }
        for(int i=low;i<=high;i++){
            arr[i] = li.get(i-low);
        }
    }
    private static void mergeSort(Pair[] arr,int low,int high){
        if(low>=high)return;
        int mid = (low+high)>>1;
        mergeSort(arr,low,mid);
        mergeSort(arr,mid+1,high);
        merge(arr,low,mid,high);
    }
    public static int[] count_NGEs(int N, int arr[], int queries, int indices[]) {
        // code here
        hash = new int[N];
        Pair copy[] = new Pair[N];
        for(int i=0;i<N;i++){
            copy[i] = new Pair(arr[i],i);
        }
        mergeSort(copy,0,N-1);
        int[] ans = new int[queries];
        for(int i=0;i<queries;i++){
            ans[i] = hash[indices[i]];
        }
        return ans;
    }
}

```
# Optimal using Stack
TC-> O(N)
SC - > O(N)
```java
class Solution {
  public static int[] count_NGEs(int N, int arr[], int queries, int indices[]) {
    // code here
    Stack<Integer> asc = new Stack<>();
    Stack<Integer> des = new Stack<>();
    int greaterCnt[] = new int[N];
    for(int i=N-1;i>=0;i--){
        while(!asc.isEmpty() && asc.peek()<=arr[i])des.add(asc.pop());
        greaterCnt[i] = asc.size();
        des.add(arr[i]);
        while(!des.isEmpty())asc.add(des.pop());
    }
    int res[] = new int[queries];
    for(int i=0;i<queries;i++){
        res[i] = greaterCnt[indices[i]];
    }
    return res;
  }
}
```