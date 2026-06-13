You can move 1 step right or 1 step down.

```java
class Main {
    static int steps(int i){
        if(i<=2)return i;
        return steps(i-1)+steps(i-2);
    }
    public static void main(String[] args) {
        int n = 15;
        System.out.print(steps(n));
    }
}
```