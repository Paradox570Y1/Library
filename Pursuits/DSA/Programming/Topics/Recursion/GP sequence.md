Generate sequence for given x,n:
	1+x + x² + x³ + x^(n-1)
```java
class Main {
    static int rec(int n,int x){
		if (n == 1) return 1;
        return rec(n - 1, x) + (int)Math.pow(x, n - 1);
    }
    public static void main(String[] args) {
       int n=5;
       int x =2;
       System.out.print(rec(n,x));
    }
}
```