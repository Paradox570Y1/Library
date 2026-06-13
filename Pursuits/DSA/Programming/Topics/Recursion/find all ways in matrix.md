You can move right or down and you need to reach from (0,0) -> (row-1, col-1)

```java
class Main {
    static int matrix(int row,int col){
        if(row==0 || col==0)return 1;
        return matrix(row-1,col)+matrix(row,col-1);
    }
    public static void main(String[] args) {
        System.out.print(matrix(2,2));
    }
}
```