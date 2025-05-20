[Go back to home page](README.md)
# [previous](unit_5.md) <--> [next](unit_7.md)
# AP CS A Unit Six: Arrays
## 1. Arrays
### Definition
An **array** in Java is a fixed-size container that holds multiple values of the same type. Arrays are used to efficiently organize and access related data using an index-based system.
### Syntax
```java
// Declaration and instantiation
int[] apScores = new int[5];
// Declaration with initialization
int[] studentScores = {5, 4, 4, 3, 5};
```
### Accessing Elements
* Arrays use **zero-based indexing**.
* Access and assign values with index notation `array[index]`.
```java
System.out.println(studentScores[0]); // prints 5
studentScores[2] = 5; // updates third score to 5
```
### Example: Printing All Scores
```java
for (int i = 0; i < studentScores.length; i++) {
    System.out.println("Score " + (i + 1) + ": " + studentScores[i]);
}
```
---
## 2. Traversing Arrays
### Traditional For Loop
```java
for (int i = 0; i < apScores.length; i++) {
    System.out.println("AP Score: " + apScores[i]);
}
```
### Enhanced For Loop
Used for **read-only** access:
```java
for (int score : apScores) {
    System.out.println("Score: " + score);
}
```
---
## 3. Array Algorithms
### Sum and Average
```java
int total = 0;
for (int score : studentScores) {
    total += score;
}
double average = (double) total / studentScores.length;
System.out.println("Average Score: " + average);
```
### Finding the Maximum
```java
int maxScore = studentScores[0];
for (int i = 1; i < studentScores.length; i++) {
    if (studentScores[i] > maxScore) {
        maxScore = studentScores[i];
    }
}
System.out.println("Top Score: " + maxScore);
```
### Counting Occurrences
```java
int fives = 0;
for (int score : studentScores) {
    if (score == 5) {
        fives++;
    }
}
System.out.println("Number of 5s: " + fives);
```
---
## 4. Arrays and Methods
Arrays can be passed to and returned from methods:
```java
public static int sumScores(int[] scores) {
    int sum = 0;
    for (int score : scores) {
        sum += score;
    }
    return sum;
}
```
---
## 5. Common Errors and Tips
### Index Out of Bounds
Accessing an invalid index causes a runtime error:
```java
int score = apScores[5]; // Error: only indices 0-4 are valid
```
### Uninitialized Elements
Elements are automatically initialized to:
* `0` for numeric arrays
* `false` for `boolean` arrays
* `null` for object arrays
### Fixed Size
Array size cannot be changed after creation. Use `ArrayList` (in Unit 7) for dynamic resizing.
---
## 6. AP Exam Connections
Arrays appear frequently in both multiple choice and free response questions:
* **FRQs** may involve traversing arrays, computing values, or modifying elements.
* Understanding both index-based and enhanced for loops is crucial.
---
## 7. Example Program: AP Exam Analysis
```java
public class ExamStats {
    public static void main(String[] args) {
        int[] apScores = {5, 4, 3, 5, 2};
        // Print scores
        for (int i = 0; i < apScores.length; i++) {
            System.out.println("Exam " + (i + 1) + ": " + apScores[i]);
        }
        // Calculate average
        int sum = 0;
        for (int score : apScores) {
            sum += score;
        }
        double average = (double) sum / apScores.length;
        System.out.println("Average Score: " + average);
        // Find highest score
        int max = apScores[0];
        for (int i = 1; i < apScores.length; i++) {
            if (apScores[i] > max) {
                max = apScores[i];
            }
        }
        System.out.println("Top Score: " + max);
    }
}
```
**Sample Output**:
```
Exam 1: 5
Exam 2: 4
Exam 3: 3
Exam 4: 5
Exam 5: 2
Average Score: 3.8
Top Score: 5
```
---
## 8. Extensions (Beyond Scope but Useful)
### Two-Dimensional Arrays
Used for grid-based data, like a matrix of AP practice scores:
```java
int[][] studentScores = {
    {5, 4, 4},
    {3, 3, 4},
    {5, 5, 5}
};
System.out.println(studentScores[1][2]); // prints 4
```
### Array Utility Methods
* `Arrays.toString(array)` for quick printing.
```java
import java.util.Arrays;
System.out.println(Arrays.toString(apScores));
```
* `Arrays.sort(array)` to sort scores.
### Array Copying
To avoid modifying the original array:
```java
int[] copy = Arrays.copyOf(apScores, apScores.length);
```
---
## 9. Practice Questions
1. **Code Tracing**: What is the output?
   ```java
   int[] scores = {3, 4, 5};
   for (int i = scores.length - 1; i >= 0; i--) {
       System.out.print(scores[i] + " ");
   }
   ```
   **Answer**: `5 4 3`
2. **Bug Fixing**: What's wrong here?
   ```java
   int[] ap = new int[3];
   ap[3] = 5;
   ```
   **Answer**: Index `3` is out of bounds. Valid indices are `0`, `1`, and `2`.
3. **Write a Method**: Write a method that counts how many `5`s are in an array of AP scores.
4. **Challenge**: Write a method that returns the index of the lowest score.
---