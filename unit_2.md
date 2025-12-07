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
        }
        else {
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
### 2.5 Comparing Objects: equals() vs ==
#### Definition
When comparing objects in Java, it's crucial to understand the difference between the `equals()` method and the `==` operator. This distinction is fundamental in AP CS A for correctly comparing `String` objects and other reference types.
- **`==` Operator**: Compares **references** (memory addresses). Returns `true` only if both references point to the exact same object in memory.
- **`equals()` Method**: Compares **content** or values. For `String` objects, it returns `true` if the sequences of characters are identical.
#### Key Concepts
- **`==` with Primitives**: For primitive types (`int`, `double`, `boolean`), `==` compares values directly.
- **`==` with Objects**: For reference types (`String`, `Integer`, etc.), `==` compares memory addresses, not content.
- **`equals()` Method**: Defined in the `Object` class and overridden by many classes (like `String`) to compare meaningful equality.
- **String Literals vs. `new String()`**: String literals are pooled, so `"hello" == "hello"` may be `true`, but `new String("hello") == "hello"` is `false`.
#### Examples
```java
// Example 1: String literals (may be pooled)
String s1 = "AP";
String s2 = "AP";
System.out.println(s1 == s2);           // true (same object in pool)
System.out.println(s1.equals(s2));      // true (same content)
// Example 2: Explicit new String objects
String s3 = new String("CS");
String s4 = new String("CS");
System.out.println(s3 == s4);           // false (different objects)
System.out.println(s3.equals(s4));      // true (same content)
// Example 3: Mixed literal and new
String s5 = "A";
String s6 = new String("A");
System.out.println(s5 == s6);           // false (different objects)
System.out.println(s5.equals(s6));      // true (same content)
// Example 4: Primitives vs Wrappers
Integer a = 5;
Integer b = 5;
System.out.println(a == b);             // true (autoboxing may cache small values)
Integer c = 500;
Integer d = 500;
System.out.println(c == d);             // false (different objects)
System.out.println(c.equals(d));        // true (same value)
```
#### Best Practices for AP CS A
1. **Always use `equals()` for comparing `String` content**.
   - Correct: `if (str1.equals(str2))`
   - Incorrect: `if (str1 == str2)` (unless intentionally checking same object)
2. **For other objects, check if the class overrides `equals()`**.
   - `Integer`, `Double`, `Boolean` override `equals()` to compare values.
   - Custom classes may need to override `equals()` (covered in Unit 9).
3. **Use `==` for primitives and null checks**.
   - `if (x == 5)` for `int x`
   - `if (obj == null)` to check for null references
#### Common Errors
- **Using `==` to compare strings**: Leads to logical bugs when strings are created differently.
- **NullPointerException with `equals()`**: Calling `str1.equals(str2)` when `str1` is `null`. Use `"constant".equals(variable)` or check for null first.
- **Assuming `==` works for wrapper objects**: For `Integer`, `Double`, etc., `==` may work for small cached values (-128 to 127) but not for larger values.
#### Example Program
```java
public class StringComparisonDemo {
    public static void main(String[] args) {
        String correctPassword = "APCS2025";
        String userInput1 = "APCS2025";
        String userInput2 = new String("APCS2025");
        System.out.println("Testing password validation:");
        System.out.println("correctPassword == userInput1: " + (correctPassword == userInput1));
        System.out.println("correctPassword.equals(userInput1): " + correctPassword.equals(userInput1));
        System.out.println("correctPassword == userInput2: " + (correctPassword == userInput2));
        System.out.println("correctPassword.equals(userInput2): " + correctPassword.equals(userInput2));
        // Safe comparison practice
        boolean isValid = correctPassword.equals(userInput2);
        System.out.println("Password valid? " + isValid);
        // Null-safe comparison
        String maybeNull = null;
        System.out.println("Null-safe check: " + "APCS2025".equals(maybeNull));
    }
}
```
**Output**:
```
Testing password validation:
correctPassword == userInput1: true
correctPassword.equals(userInput1): true
correctPassword == userInput2: false
correctPassword.equals(userInput2): true
Password valid? true
Null-safe check: false
```
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
### 7.1 Wrapper Classes and Autoboxing
#### Definition
Wrapper classes are object representations of primitive data types, allowing primitives to be used in contexts that require objects (e.g., collections like `ArrayList`). In AP CS A, the most commonly used wrapper classes are `Integer`, `Double`, and `Boolean`, corresponding to `int`, `double`, and `boolean` primitives.
#### Key Concepts
- **Autoboxing**: Automatic conversion of a primitive to its corresponding wrapper object.
  ```java
  Integer wrappedScore = 5; // Autoboxing: int 5 becomes Integer object
  ```
- **Unboxing**: Automatic conversion of a wrapper object to its primitive value.
  ```java
  int primitiveScore = wrappedScore; // Unboxing: Integer object becomes int
  ```
- **Common Wrapper Classes**:
  - `Integer` for `int`
  - `Double` for `double`
  - `Boolean` for `boolean`
  - `Character` for `char`
  - `Byte` for `byte`
  - `Short` for `short`
  - `Long` for `long`
  - `Float` for `float`
#### Why Use Wrapper Classes?
1. **Collections Requirement**: `ArrayList` and other Java collections can only store objects, not primitives.
   ```java
   ArrayList<Integer> scores = new ArrayList<Integer>();
   scores.add(95); // Autoboxing: int 95 → Integer
   int first = scores.get(0); // Unboxing: Integer → int
   ```
2. **Object Methods**: Wrapper classes provide useful methods like `Integer.parseInt()` or `Double.isNaN()`.
3. **Nullability**: Wrapper objects can be `null`, representing the absence of a value (primitives cannot be `null`).
#### Important Methods
- **`Integer.parseInt(String s)`**: Converts a `String` to an `int`.
  ```java
  String input = "42";
  int value = Integer.parseInt(input); // value = 42
  ```
- **`Double.parseDouble(String s)`**: Converts a `String` to a `double`.
- **`Integer.toString(int i)`**: Converts an `int` to a `String`.
- **`Integer.MAX_VALUE`, `Integer.MIN_VALUE`**: Constants for maximum and minimum `int` values.
- **`Double.NaN`, `Double.POSITIVE_INFINITY`**: Special double values.
#### Autoboxing/Unboxing Examples
```java
// Autoboxing examples
Integer a = 10; // Primitive int 10 autoboxed to Integer
Double b = 3.14; // Primitive double 3.14 autoboxed to Double
Boolean c = true; // Primitive boolean true autoboxed to Boolean
// Unboxing examples
int x = a; // Integer a unboxed to int
double y = b; // Double b unboxed to double
boolean z = c; // Boolean c unboxed to boolean
// Mixed operations (autoboxing/unboxing happens automatically)
Integer sum = a + 5; // a unboxed to int, addition performed, result autoboxed to Integer
```
#### Caching and Performance
- Java caches wrapper objects for small values (e.g., `Integer` values from -128 to 127) for performance.
- This can lead to surprising results with `==` comparison:
  ```java
  Integer i1 = 127;
  Integer i2 = 127;
  System.out.println(i1 == i2); // true (same cached object)
  Integer i3 = 128;
  Integer i4 = 128;
  System.out.println(i3 == i4); // false (different objects)
  ```
- **Always use `equals()` to compare wrapper objects for value equality**.
#### Common Errors
- **NullPointerException when Unboxing**: Unboxing a `null` wrapper causes `NullPointerException`.
  ```java
  Integer score = null;
  int s = score; // NullPointerException!
  ```
- **Performance Overhead**: Excessive autoboxing/unboxing in loops can impact performance.
- **Incorrect Method Overloading**: Methods overloaded for primitive and wrapper types may behave unexpectedly.
#### Example Program
```java
public class WrapperDemo {
    public static void main(String[] args) {
        // Autoboxing in ArrayList
        ArrayList<Integer> apScores = new ArrayList<Integer>();
        apScores.add(5); // Autoboxing
        apScores.add(4);
        apScores.add(3);
        // Unboxing for calculation
        int total = 0;
        for (Integer score : apScores) {
            total += score; // Unboxing in each iteration
        }
        double average = (double) total / apScores.size();
        System.out.println("Average AP Score: " + average);
        // String conversion
        String input = "95";
        int grade = Integer.parseInt(input);
        System.out.println("Parsed grade: " + grade);
        // Null safety check
        Integer possibleNull = null;
        if (possibleNull != null) {
            int safeValue = possibleNull; // Would throw NPE without check
        }
    }
}
```
### Extensions
- **StringBuilder**: A mutable alternative to `String` for efficient concatenation.
  ```java
  StringBuilder sb = new StringBuilder();
  sb.append("AP").append("CS").append("A");
  String result = sb.toString(); // "APCSA"
  ```
- **Advanced Math**: Use `Math.sin()`, `Math.cos()`, `Math.log()`, `Math.exp()` for scientific calculations.
  ```java
  double angle = Math.PI / 2;
  System.out.println(Math.sin(angle)); // 1.0
  ```