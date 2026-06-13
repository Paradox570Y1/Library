- Brute Force
   ![[Pasted image 20240701234241.png|400]]
   here TC => O(min(n1,n2))
   
- __Euclidean Algorithm__
  ![[Pasted image 20240701234103.png|500]]
  ![[Pasted image 20240701234457.png|500]]
  ![[Pasted image 20240701234902.png|400]]
     - if a becomes 0 then b is gcd and vice versa. 

  Implementation
  ![[Pasted image 20240702000249.png|250]]
  TC => ![[Pasted image 20240702000431.png|300]]

- Alternatively
  ![[Pasted image 20240702163723.png|500]]

- ![[Pasted image 20240704202148.png|500]]

```java
import java.util.*;

public class t {
    static int gcd(int m, int n) {
        if (m % n == 0) {
            return n;
        } else {
            return gcd(n % m, m);
        }

    }

    public static void main(String[] args) {
        int a, b;
        Scanner sc = new Scanner(System.in);
        a = sc.nextInt();
        b = sc.nextInt();
        System.out.println(gcd(a, b));
    }
}
```
  
  
  