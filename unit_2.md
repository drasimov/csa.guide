[Go back to home page](README.md)
# [previous](unit_1.md)<-->[next](unit_3.md)
# AP CS A Unit Two: Objects, Strings, and Math
The basics of trash code: long and unwinded code that does nothing.
## 1. Objects and Reference Variables
### Definition
An **object** is a composite entity in Java, bundling data and behaviors (methods) into a single unit. Objects are instances of **classes**, and **reference variables** store memory addresses pointing to these objects, not the objects themselves. When no reference variables point to an object, it becomes inaccessible and is eligible for **garbage collection**.
**TOP TIP**: Reference variables are *not* objects! They're like campus maps, holding the address of where the object (the lecture hall) resides in memory. Each reference variable has a specific class type it refers to, like `String` or `Math`.
### Key Notes
- Objects are stored in **heap memory**, with reference variables in **stack memory** pointing to them.
- Assigning one reference variable to another copies the address, not the object, so both point to the same object.
- AP CS A Unit Two introduces objects through the `String` and `Math` classes, laying the foundation for object-oriented programming.
### Example Program
```java
public class AcademicObjectQuest {
    public static void main(String[] args) {
        String studentName = new String("@drasimov"); // Reference to a String object
        String alias = studentName; // Points to the same object
        System.out.println("Student: " + studentName);
        System.out.println("Alias: " + alias);
        studentName = null; // Object still exists via alias
        System.out.println("Alias after nulling: " + alias);
        alias = null; // Object now eligible for garbage collection
        // System.out.println(studentName.toUpperCase()); // NullPointerException!
    }
}
```
**Output**:
```
Student: @drasimov
Alias: @drasimov
Alias after nulling: @drasimov
```
### Common Errors
- **NullPointerException**: Accessing methods on a `null` reference. Example: `String name = null; name.length();`.
- **Misunderstanding References**: Assuming assigning a reference copies the object. Example: `String a = b;` makes `a` and `b` point to the same object.
---
## 2. String Class
### Definition
The `String` class represents immutable sequences of characters. Strings are objects, created using literals (e.g., `"Hello"`) or the `new` keyword. Their immutability means operations like concatenation create new `String` objects rather than modifying existing ones.
### Common Methods
- `int length()`: Returns the number of characters.
- `String substring(int start, int end)`: Returns a substring from `start` (inclusive) to `end` (exclusive).
- `String substring(int start)`: Returns a substring from `start` to the end.
- `int indexOf(String str)`: Returns the first index of `str`, or -1 if not found.
- `String toUpperCase()`, `String toLowerCase()`: Converts to upper or lower case.
- `char charAt(int index)`: Returns the character at `index`.
- `int compareTo(String other)`: Compares strings lexicographically (returns negative, zero, or positive).
### Key Notes
- Strings are immutable, so methods return new strings rather than modifying the original.
- Concatenation with `+` creates new `String` objects, which can be inefficient in loops.
- String literals are stored in the **string pool** for efficiency.
### Trash Code Example
Here's some *epic trash code* that overcomplicates extracting a student's initials:
```java
public class EpicInitialsExtractor {
    public static void main(String[] args) {
        String fullName = "Alan Turing"; // The genius of CS
        String initials = ""; // Prepare for the ultimate initial quest
        int spaceIndex = -1; // Where's that space hiding?
        for (int i = 0; i < fullName.length(); i++) { // Super slow space hunt
            if (fullName.charAt(i) == ' ') {
                spaceIndex = i;
                break; // Gotcha!
            }
        }
        if (spaceIndex != -1) { // Only if we found a space
            initials = initials + fullName.charAt(0); // First initial
            initials = initials + fullName.charAt(spaceIndex + 1); // Last initial
        } else {
            initials = fullName.charAt(0) + ""; // Fallback for single names
        }
        System.out.println("Super Complex Initials: " + initials.toUpperCase());
        // Easter Egg: Congrats, you survived the trash code maze!
    }
}
```
**Output**:
```
Super Complex Initials: AT
```
**Why It's Trash**: A simple `initials = "" + fullName.charAt(0) + fullName.charAt(fullName.indexOf(" ") + 1);` would suffice, but we took the scenic route!
### Common Errors
- **IndexOutOfBoundsException**: Accessing invalid indices. Example: `"Hi".substring(3);`.
- **NullPointerException**: Calling methods on a `null` String. Example: `String s = null; s.length();`.
- **Inefficient Concatenation**: Using `+` in loops creates multiple `String` objects.
---
## 3. Math Class
### Definition
The `Math` class provides static methods and constants for mathematical operations. It's a utility class, not instantiated, and is crucial for calculations in AP CS A.
### Key Methods and Constants
- `double random()`: Returns a random `double` in [0.0, 1.0).
- Random integer in range `[min, max]`: `(int)(Math.random() * (max - min + 1)) + min`.
- `double abs(double x)`: Returns the absolute value.
- `double pow(double base, double exponent)`: Returns `base` raised to `exponent`.
- `double sqrt(double x)`: Returns the square root.
- `double min(double a, double b)`, `double max(double a, double b)`: Returns the minimum or maximum.
- `double PI`: Constant for π (approximately 3.14159).
### Extended Methods
- `double sin(double radians)`, `double cos(double radians)`: Trigonometric functions.
- `double log(double x)`: Natural logarithm.
- `double exp(double x)`: Returns `e^x`.
### Key Notes
- All `Math` methods are `static`, called as `Math.methodName()`.
- `Math.random()` is pseudo-random, sufficient for AP CS A applications.
- Extended methods are useful for advanced calculations, though less common in Unit Two.
### Trash Code Example
Here's a *ridiculously verbose* way to generate a random AP score (1 to 5):
```java
public class RandomAPScoreGenerator {
    public static void main(String[] args) {
        double randomValue = Math.random(); // The magic number
        double scaledValue = randomValue * (5 - 1 + 1); // Scale to 1-5
        double shiftedValue = scaledValue + 1; // Shift to start at 1
        int apScore = (int) shiftedValue; // Truncate to int
        String scoreMessage = ""; // Build the ultimate message
        for (int i = 0; i < 1; i++) { // Why loop? Because trash!
            scoreMessage = "Your randomly generated AP score is: " + apScore;
        }
        System.out.println(scoreMessage);
        // Easter Egg: Did you just roll a 5? GPA vibes!
    }
}
```
**Output**:
```
Your randomly generated AP score is: 3
```
**Why It's Trash**: A single line `(int)(Math.random() * 5 + 1)` would do, but we savored every unnecessary step!
### Common Errors
- **Off-by-One Errors**: Incorrect range in random number generation. Example: `(int)(Math.random() * 5)` gives 0 to 4.
- **Casting Oversight**: Forgetting to cast `Math.random()`'s `double` to `int`. Example: `int score = Math.random() * 5;`.
---
## 4. Methods
### Definition
A **method** is a reusable block of code that performs a specific task, often taking **parameters** (inputs) and returning a value (or `void` if no return). In Unit Two, methods are introduced via `String` and `Math` class methods and basic user-defined methods.
### Key Concepts
- **Declaration**: `returnType methodName(parameterType param) { ... }`.
- **Return Types**: `int`, `double`, `String`, etc., or `void` for no return.
- **Parameters**: Variables passed to the method, e.g., `substring(int start)`.
- **Calling Methods**: Use `object.methodName(args)` for instance methods (e.g., `String`) or `Class.methodName(args)` for static methods (e.g., `Math`).
### Example Program
```java
public class GPACalculator {
    public static double boostGPA(double currentGpa, double bonus) {
        return currentGpa + bonus; // Simple GPA boost
    }
    public static void main(String[] args) {
        double gpa = 3.5;
        double boostedGpa = boostGPA(gpa, 0.5); // Call our method
        System.out.println("Original GPA: " + gpa);
        System.out.println("Boosted GPA: " + boostedGpa);
        // Easter Egg: Max GPA achieved? You're an AP legend!
    }
}
```
**Output**:
```
Original GPA: 3.5
Boosted GPA: 4.0
```
### Common Errors
- **Incorrect Return Type**: Returning a `double` from an `int` method. Example: `int method() { return 3.5; }`.
- **Missing Return**: Omitting a return statement in a non-`void` method.
- **Parameter Mismatch**: Passing wrong types or number of arguments.
---
## 5. Scope and Null References
### Scope
- **Local Variables**: Declared inside a method, accessible only within it.
- **Instance Variables**: Declared in a class, accessible to all methods (introduced later in AP CS A).
- **Block Scope**: Variables in `{}` blocks (e.g., loops) are limited to that block.
### Null References
- A reference variable set to `null` points to no object.
- Accessing methods on a `null` reference causes a `NullPointerException`.
- Use `if (variable != null)` to check before accessing.
### Example Program
```java
public class StudentRecord {
    public static void main(String[] args) {
        String studentName = "Grace Hopper";
        if (studentName != null) { // Safe check
            String scopeDemo = studentName.toUpperCase(); // Local variable
            System.out.println("Name: " + scopeDemo);
        }
        // System.out.println(scopeDemo); // Error: scopeDemo out of scope
        studentName = null;
        // studentName.length(); // NullPointerException!
        System.out.println("Record cleared.");
        // Easter Egg: Null? Like forgetting your AP exam date!
    }
}
```
**Output**:
```
Name: GRACE HOPPER
Record cleared.
```
### Common Errors
- **Scope Violation**: Accessing a variable outside its scope. Example: Using a loop variable after the loop.
- **NullPointerException**: Not checking for `null` before method calls.
---
## 6. Connection to AP CS A Unit Two
### Curriculum Context
AP CS A Unit Two builds on Unit 1 by introducing:
- **Objects**: Using `String` and `Math` to explore reference variables and methods.
- **String Manipulation**: Processing text for academic applications (e.g., formatting names).
- **Math Operations**: Performing calculations like random score generation.
- **Methods**: Calling and defining simple methods for reusable logic.
- **Scope and Null**: Understanding variable accessibility and safe object handling.
### Relevance
- `String` methods are essential for text processing in AP problems (e.g., parsing input).
- `Math` methods support calculations like averages or random selections.
- Understanding references and scope prevents common errors like `NullPointerException`.
### Practice Questions
1. **Code Tracing**: What is the output?
   ```java
   String name = "AP CS A";
   System.out.println(name.substring(0, 2));
   ```
   **Answer**: `AP`
2. **Error Identification**: Why does this fail?
   ```java
   String s = null;
   System.out.println(s.length());
   ```
   **Answer**: `NullPointerException` because `s` is `null`. Check with `if (s != null)`.
3. **Coding Exercise**: Write a method that takes a `String` name and returns its first three characters, or the full name if shorter.
---
## 7. Additional Notes
### Best Practices
- Use meaningful variable names (e.g., `studentName` instead of `s`) for clarity.
- Check for `null` before calling object methods.
- Avoid excessive string concatenation in loops; consider `StringBuilder` (see extensions).
- Comment trash code to explain its glorious inefficiency.
### Extensions
- **StringBuilder**: A mutable alternative to `String` for efficient concatenation.
  ```java
  StringBuilder sb = new StringBuilder();
  sb.append("AP").append("CS").append("A");
  String result = sb.toString(); // "APCSA"
  ```
- **Wrapper Classes**: `Integer`, `Double`, `Boolean` wrap primitives for object-oriented use.
  ```java
  Integer apScore = 5; // Autoboxing
  int score = apScore; // Unboxing
  ```
- **Advanced Math**: Use `Math.sin()`, `Math.cos()`, `Math.log()`, `Math.exp()` for scientific calculations.
  ```java
  double angle = Math.PI / 2;
  System.out.println(Math.sin(angle)); // 1.0
  ```