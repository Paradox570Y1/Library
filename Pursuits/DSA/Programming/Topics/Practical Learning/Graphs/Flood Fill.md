[733. Flood Fill](https://leetcode.com/problems/flood-fill/)
You are given an image represented by an `m x n` grid of integers `image`, where `image[i][j]` represents the pixel value of the image. You are also given three integers `sr`, `sc`, and `color`. Your task is to perform a **flood fill** on the image starting from the pixel `image[sr][sc]`.

To perform a **flood fill**:

1. Begin with the starting pixel and change its color to `color`.
2. Perform the same process for each pixel that is **directly adjacent** (pixels that share a side with the original pixel, either horizontally or vertically) and shares the **same color** as the starting pixel.
3. Keep **repeating** this process by checking neighboring pixels of the _updated_ pixels and modifying their color if it matches the original color of the starting pixel.
4. The process **stops** when there are **no more** adjacent pixels of the original color to update.

Return the **modified** image after performing the flood fill.

**Example 1:**

**Input:** image = `[[1,1,1],[1,1,0],[1,0,1]]`, sr = 1, sc = 1, color = 2

**Output:** `[[2,2,2],[2,2,0],[2,0,1]]`

**Explanation:**

![](https://assets.leetcode.com/uploads/2021/06/01/flood1-grid.jpg)

From the center of the image with position `(sr, sc) = (1, 1)` (i.e., the red pixel), all pixels connected by a path of the same color as the starting pixel (i.e., the blue pixels) are colored with the new color.

Note the bottom corner is **not** colored 2, because it is not horizontally or vertically connected to the starting pixel.

**Example 2:**

**Input:** image = `[[0,0,0],[0,0,0]]`, sr = 0, sc = 0, color = 0

**Output:** `[[0,0,0],[0,0,0]]`

**Explanation:**

The starting pixel is already colored with 0, which is the same as the target color. Therefore, no changes are made to the image.

**Constraints:**

- `m == image.length`
- `n == image[i].length`
- `1 <= m, n <= 50`
- `0 <= image[i][j], color < 216`
- `0 <= sr < m`
- `0 <= sc < n`



# Using BFS

#Brute
```java
class Solution {
    class Pixel{
        public int x;
        public int y;
        Pixel(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
        Queue<Pixel> queue = new LinkedList<>();
        int baseColor = image[sr][sc];
        image[sr][sc] = color;
        queue.offer(new Pixel(sr, sc));
        int op[][] = {{0,1},{1,0},{-1,0},{0,-1}};
        int rows = image.length;
        int cols = image[0].length;
        while(!queue.isEmpty()){
            Pixel cur = queue.poll();
            for(int i = 0; i < 4; i++) {
                int x = cur.x + op[i][0];
                int y = cur.y + op[i][1];
                if (x >= 0 && x < rows && y >= 0 && y < cols && image[x][y] == baseColor) {
                    image[x][y] = -1;
                    queue.offer(new Pixel(x, y));
                }
            }
        }
        for (int i = 0; i < rows; i++) {
            for(int j = 0; j < cols; j++) {
                if(image[i][j] == -1) {
                    image[i][j] = color;
                }
            }
        }
        return image;
    }
}
```


#Better
```java
class Solution {
    class Pixel{
        public int x;
        public int y;
        Pixel(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
        int baseColor = image[sr][sc];
        if(baseColor == color) return image;
        Queue<Pixel> queue = new LinkedList<>();
        image[sr][sc] = color;
        queue.offer(new Pixel(sr, sc));
        int op[][] = {{0,1},{1,0},{-1,0},{0,-1}};
        int rows = image.length;
        int cols = image[0].length;
        while(!queue.isEmpty()){
            Pixel cur = queue.poll();
            for(int i = 0; i < 4; i++) {
                int x = cur.x + op[i][0];
                int y = cur.y + op[i][1];
                if (x >= 0 && x < rows && y >= 0 && y < cols && image[x][y] == baseColor) {
                    image[x][y] = color;
                    queue.offer(new Pixel(x, y));
                }
            }
        }
        return image;
    }
}
```


# Using DFS

#Optimal
```java
class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
        if (image[sr][sc] == color) {
            return image;
        }
        helper(image, sr, sc, color, image[sr][sc]);
        return image;
    }
    private void helper(int[][] image, int sr, int sc, int color, int baseColor) {
        if (sr < 0 || sc < 0 || sr == image.length || sc == image[0].length || baseColor != image[sr][sc]) {
            return;
        }
        image[sr][sc] = color;
        helper(image, sr + 1, sc, color, baseColor);
        helper(image, sr, sc + 1, color, baseColor);
        helper(image, sr - 1, sc, color, baseColor);
        helper(image, sr, sc - 1, color, baseColor);
    }
}
```