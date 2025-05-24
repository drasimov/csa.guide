[Go back to home page](README.md)
# [previous](unit_7.md)<-->[next](unit_9.md)
# AP CS A Unit Eight: Two-Dimensional Arrays
## 1. Definition and Overview
### Definition
Two-dimensional arrays in Java are arrays whose elements are themselves arrays, forming a grid-like (rows × columns) structure. They facilitate modeling matrices, game boards, image pixels, seating charts, and other tabular data. In AP CS A Unit Eight, the main objective is learning how to declare, initialize, traverse, and manipulate 2D arrays as well as applying algorithms to solve common grid-based problems.
### Curriculum Connection
* Builds on Unit Seven's 1D arrays by introducing nested structures.
* Reinforces nested loops, indexing, and method parameters.
* Prepares for complex data structures like lists of lists.
---
## 2. Declaration and Initialization
### Declaration Syntax
```java
// Declare without allocating
int[][] grid;
String[][] seatingChart;
```
### Allocation (Fixed-size Rectangular)
```java
// Allocate 5 rows, 4 columns
grid = new int[5][4];
```
* `grid.length` returns row count (5).
* `grid[0].length` returns column count (4).
### Inline (Literal) Initialization
```java
int[][] board = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```
* Row lengths must match for a rectangular literal.
### Ragged (Jagged) Arrays
```java
int[][] ragged = new int[3][];
ragged[0] = new int[2]; // row 0 has 2 columns
ragged[1] = new int[4]; // row 1 has 4 columns
ragged[2] = new int[3]; // row 2 has 3 columns
```
* Each row can have different lengths.
---
## 3. Accessing and Modifying Elements
```java
int value = board[2][1];  // Access row 2, col 1 (zero-based)
board[0][0] = 99;         // Modify element at row 0, col 0
```
* Always validate: `0 <= row < arr.length` and `0 <= col < arr[row].length`.
* Invalid indices throw `ArrayIndexOutOfBoundsException`.
---
## 4. Traversal Patterns
### 4.1 Nested Traditional for Loops
```java
for (int r = 0; r < grid.length; r++) {
    for (int c = 0; c < grid[r].length; c++) {
        System.out.print(grid[r][c] + " ");
    }
    System.out.println();
}
```
### 4.2 Enhanced for Loops
```java
for (int[] row : grid) {
    for (int val : row) {
        System.out.print(val + " ");
    }
    System.out.println();
}
```
### 4.3 Row-major vs Column-major
* Java uses row-major order: elements in the same row are stored contiguously.
* Loop ordering affects cache performance (advanced topic).
---
## 5. Core Algorithms on 2D Arrays
### 5.1 Sum of All Elements
```java
public static int total(int[][] arr) {
    int sum = 0;
    for (int[] row : arr)
        for (int v : row)
            sum += v;
    return sum;
}
```
### 5.2 Row and Column Sums
```java
// Row sums
double[] rowSums = new double[arr.length];
for (int r = 0; r < arr.length; r++) {
    for (int v : arr[r]) rowSums[r] += v;
}
// Column sums (rectangular only)
int cols = arr[0].length;
int[] colSums = new int[cols];
for (int r = 0; r < arr.length; r++) {
    for (int c = 0; c < cols; c++) {
        colSums[c] += arr[r][c];
    }
}
```
### 5.3 Searching for a Value
```java
public static boolean contains(int[][] arr, int target) {
    for (int r = 0; r < arr.length; r++) {
        for (int c = 0; c < arr[r].length; c++) {
            if (arr[r][c] == target) return true;
        }
    }
    return false;
}
```
### 5.4 Finding Max/Min
```java
public static int findMax(int[][] arr) {
    int max = Integer.MIN_VALUE;
    for (int[] row : arr)
        for (int v : row)
            if (v > max) max = v;
    return max;
}
```
---
## 6. Advanced Array Operations
### 6.1 Matrix Transpose
```java
public static int[][] transpose(int[][] m) {
    int rows = m.length;
    int cols = m[0].length;
    int[][] t = new int[cols][rows];
    for (int r = 0; r < rows; r++) {
        for (int c = 0; c < cols; c++) {
            t[c][r] = m[r][c];
        }
    }
    return t;
}
```
### 6.2 Matrix Multiplication (Rectangular Matrices)
```java
public static int[][] multiply(int[][] a, int[][] b) {
    int aRows = a.length, aCols = a[0].length;
    int bCols = b[0].length;
    int[][] product = new int[aRows][bCols];
    for (int i = 0; i < aRows; i++) {
        for (int j = 0; j < bCols; j++) {
            for (int k = 0; k < aCols; k++) {
                product[i][j] += a[i][k] * b[k][j];
            }
        }
    }
    return product;
}
```
### 6.3 Flood-Fill (Recursive)
```java
public static void floodFill(int[][] grid, int r, int c, int newVal) {
    int original = grid[r][c];
    if (original == newVal) return;
    fill(grid, r, c, original, newVal);
}
private static void fill(int[][] g, int r, int c, int orig, int newVal) {
    if (r < 0 || r >= g.length || c < 0 || c >= g[r].length) return;
    if (g[r][c] != orig) return;
    g[r][c] = newVal;
    fill(g, r+1, c, orig, newVal);
    fill(g, r-1, c, orig, newVal);
    fill(g, r, c+1, orig, newVal);
    fill(g, r, c-1, orig, newVal);
}
```
---
## 7. Passing 2D Arrays to Methods
* Methods accept `type[][]`, treat as reference. Mutations affect original array.
* Example signature:
  ```java
  public static int countZeros(int[][] grid) { /*...*/ }
  ```
---
## 8. Example Program
```java
public class MatrixDemo {
    public static void main(String[] args) {
        int[][] m1 = {
            {1, 2, 3},
            {4, 5, 6}
        };
        int[][] m2 = {
            {7, 8},
            {9, 10},
            {11, 12}
        };
        System.out.println("m1 Transposed:");
        print(transpose(m1));
        System.out.println("m1 x m2:");
        print(multiply(m1, m2));
        System.out.println("Total of m1: " + total(m1));
    }
    // include print, transpose, multiply, total from above
}
```
**Sample Output**:
```
m1 Transposed:
1 4 
2 5 
3 6 
m1 x m2:
58 64 
139 154 
Total of m1: 21
```
---
## 9. Common Errors and Debugging
* **IndexOutOfBoundsException**: Mixing up row/column bounds or ragged rows.
* **Wrong loop limits**: Using `arr[0].length` on ragged arrays with uneven rows.
* **Mutable side effects**: Unintended modifications when passing arrays to methods.
* **Dimension mismatch**: In matrix multiplication, a's columns must equal b's rows.
---
## 10. Practice Questions
1. **Code Tracing**: What does this print?
   {% raw %}
   ```java
   int[][] x = {{1,2},{3,4}};
   for(int[] row : x) {
       for(int v: row) System.out.print(v*2 + " ");
       System.out.println();
   }
   ```
   {% endraw %}
2. **Method Implementation**: Write `public static int diagonalSum(int[][] m)` that returns sum of `m[i][i]`.
3. **Bug Fixing**: Identify and fix the error in this snippet:
   ```java
   int[][] a = new int[3][3];
   for(int i=0; i<=3; i++) {
       for(int j=0; j<3; j++) a[i][j] = i+j;
   }
   ```
4. **Extension Challenge**: Implement `public static boolean isMagicSquare(int[][] m)`.
---
## 11. Additional Notes
### Best Practices
* Always check both dimensions in loops.
* When using ragged arrays, query each row's length individually.
* Use helper methods (e.g., `print`, `total`) to organize code and avoid duplication.
### Extensions and Beyond AP
Below are practical examples that demonstrate how 2D arrays integrate with advanced Java features and libraries beyond the AP curriculum.
* **Streams API Flattening**
  Use Java 8+ streams to flatten a 2D array into a single stream for concise operations.
  {% raw %}
  ```java
  import java.util.Arrays;
  public class StreamFlatten {
      public static void main(String[] args) {
          int[][] matrix = {{1,2,3},{4,5,6},{7,8,9}};
          int sum = Arrays.stream(matrix)
                          .flatMapToInt(Arrays::stream)
                          .sum();
          System.out.println("Sum via streams: " + sum); // 45
      }
  }
  ```
  {% endraw %}
* **JavaFX Grid Visualization**
  Display a 2D array as a grid of rectangles with JavaFX for simulations (e.g., Game of Life).
  ```java
  import javafx.application.Application;
  import javafx.scene.Scene;
  import javafx.scene.layout.GridPane;
  import javafx.scene.paint.Color;
  import javafx.scene.shape.Rectangle;
  import javafx.stage.Stage;
  public class GridVisualizer extends Application {
      private static final int SIZE = 10;
      private static final int CELL = 20;
      public void start(Stage stage) {
          int[][] grid = new int[SIZE][SIZE];
          // initialize pattern
          grid[4][4] = grid[4][5] = grid[5][4] = 1;
          GridPane pane = new GridPane();
          for (int r = 0; r < SIZE; r++) {
              for (int c = 0; c < SIZE; c++) {
                  Rectangle rect = new Rectangle(CELL, CELL);
                  rect.setFill(grid[r][c] == 1 ? Color.BLACK : Color.WHITE);
                  rect.setStroke(Color.LIGHTGRAY);
                  pane.add(rect, c, r);
              }
          }
          stage.setScene(new Scene(pane));
          stage.setTitle("2D Array Grid");
          stage.show();
      }
      public static void main(String[] args) { launch(); }
  }
  ```
* **Performance Comparison**
  Measure recursive vs iterative flood-fill on large grids using `System.nanoTime()`.
  ```java
  long startRec = System.nanoTime();
  floodFillRecursive(bigGrid, 0, 0, 2);
  long endRec = System.nanoTime();
  System.out.println("Recursive: " + (endRec - startRec) + " ns");
  long startIt = System.nanoTime();
  floodFillIterative(bigGridCopy, 0, 0, 2);
  long endIt = System.nanoTime();
  System.out.println("Iterative: " + (endIt - startIt) + " ns");
  ```
* **BufferedImage Pixel Manipulation**
  Treat a `BufferedImage` as a 2D array of pixels (ARGB) to apply filters.
  ```java
  import java.awt.image.BufferedImage;
  public class ImageFilter {
      public static void invertColors(BufferedImage img) {
          int width = img.getWidth(), height = img.getHeight();
          for (int y = 0; y < height; y++) {
              for (int x = 0; x < width; x++) {
                  int rgba = img.getRGB(x, y);
                  int inverted = (0xFFFFFF - (rgba | 0xFF000000)) | (rgba & 0xFF000000);
                  img.setRGB(x, y, inverted);
              }
          }
      }
  }
  ```
* **Deep Operations with Arrays Utility**
  Use `Arrays.deepToString()` and `Arrays.deepEquals()` for quick debugging and equality checks:
  ```java
  int[][] a = {{1,2},{3,4}};
  int[][] b = {{1,2},{3,4}};
  System.out.println(Arrays.deepToString(a));           // [[1, 2], [3, 4]]
  System.out.println(Arrays.deepEquals(a, b));          // true
  ```
These examples bridge 2D arrays with modern Java techniques, GUI frameworks, performance analysis, and image processing—extending your skills well beyond the AP curriculum.