[[BitSet in Java]]
- How to handle `return ans % 10000003`
```java
return (int)((1L * (high + 1) * B) % 10000003); (Correct)
return  ((high+1)*B) % 10000003; (Wrong)
```
- To implement set and keep natural order of adding the elements
```java
Set<String> s = new LinkedHashSet<>();
```

- To implement set and keep sorted order of elements
	- In case of strings sorted order will be lexicographically.
```java
Set<String> st = new TreeSet<>(); //Sorted alphabetically
```

- Strings are sorted lexicographically in `Arrays.sort()` , `TreeMap<>()` , `TreeSet<>()`
```java
//for casesensitive lexicographically sorting
Arrays.sort(arr,String.CASE_INSENSITIVE_ORDER);

//for sorting integer array lexicographically
Arrays.sort(numbers, (a, b) -> String.valueOf(a).compareTo(String.valueOf(b)));//asc order
```

- `String.valueOf()` is a **static method** used to **convert different data types into their string representation**.
- For Int Primitive array `int[]` , java only support natural ascending order.
- But in `Integer[]` you can use comparator as well.
- But in case of 2D array `int[][]` , comparator can be used as here the data type of each element is an object `int[]`.

```java
//converting int[] to Integer[]
int[] arr = {5, 2, 9, 1, 3};
Integer[] boxed = new Integer[arr.length];
for (int i = 0; i < arr.length; i++) {
    boxed[i] = arr[i];  // Auto-boxing: int → Integer
}
```


# To count Quantity / rate

```java
for(int pile:piles){
    cnt += Math.ceil((double)pile/rate);
}
OR
private long getTime(int[] piles,int rate){
        long cnt=0;
        for(int pile:piles){
            cnt += (pile+rate-1)/rate;
        }
        return cnt;
    }
```


# Library functions for ArrayList

![Pasted image 20250612135352.png](app://2639eeec8a8abe4944f35213ee3da9c1dcfe/C:/Users/Apurav%20Gautam/OneDrive/Obsidian/Lessons/Pasted%20image%2020250612135352.png?1749716632230)

![Pasted image 20250612135402.png](app://2639eeec8a8abe4944f35213ee3da9c1dcfe/C:/Users/Apurav%20Gautam/OneDrive/Obsidian/Lessons/Pasted%20image%2020250612135402.png?1749716642786)

# To return upto 2 decimal places while removing trailing zeroes.

![[Pasted image 20250612150457.png|500]]


# StringBuilder methods

```java
//to delete characters
sb.deleteCharAt(idx);
	//best way to delete the last character
sb.setLength(sb.length()-1);
```



