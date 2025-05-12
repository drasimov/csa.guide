[Go back to home page](README.md)
## 1. Primitive Data Types
### Definition
Primitive data types in Java are the most basic data types that store simple values directly in memory. Unlike objects, primitives do not have methods or additional properties; they represent raw values. For AP CS A, you mostly only need to know these primitive data types: `int`, `double`, and `boolean`.
### Types and Characteristics
- **`int`**: Represents a 32-bit integer (whole number) with a range of approximately -2.147 billion to 2.147 billion ($$-2^{31}$$ to $$2^{31}$$-1). Used for counting or indexing.
 -Example: `int gpa=5;`
- **`double`**: Represents a 64-bit floating-point number for decimals. Suitable for precise calculations involving fractions.
 -Example: `double gpa=5.0;`
- **`boolean`**: Represents a logical value, either `true` or `false`. Used for conditional statements and logic.
 -Example: `boolean isFiveInAP=true;`
### Key Notes
- Primitives are stored directly in memory (stack memory), making them efficient for simple operations compared to reference data types such as Strings, which are reference data types that store their reference in the stack and the actual data in the heap.
- Other primitive types (e.g., `char`, `byte`, `short`, `long`, `float`) exist in Java but are almost not covered in AP CS A.
- Variables of primitive types must be declared with a type before use, e.g., `int x=10;`.
### Example in Context
```java
public class PrimitiveExample {
    public static void main(String[] args) {
        int age=16;// Integer for age
        double gpa=3.85;// Decimal for GPA
        boolean isEnrolled=true;// Logical value for enrollment status
        System.out.println("Age: "+age+", GPA: "+gpa+", Enrolled: "+isEnrolled);
    }
}
```
**Output**: `Age: 16, GPA: 3.85, Enrolled: true`
### Common Errors
- **Overflow**: Assigning a value outside the range of `int` or `double` causes compilation or runtime issues.
 -Example: `int x=2147483648;` (exceeds `int` range).
- **Incorrect Type**: Assigning a `double` to an `int` without casting causes a compilation error.
 -Example: `int x=3.14;` (invalid without casting).
---
## 2. Data Type Casting
### Definition
Type casting is the process of converting a value from one data type to another. In Java, casting is often required when working with different primitive types, such as converting a `double` to an `int` or vice versa. Casting can be **implicit** (automatic) or **explicit** (manual).
### Types of Casting
1. **Implicit Casting (Widening Conversion)**:
  -Occurs automatically when converting from a smaller or less precise type to a larger or more precise type (e.g., `int` to `double`).
  -No data loss occurs because the target type can fully represent the original value.
  -Example: 
     ```java
     int num=5;
     double result=num; // Implicitly converts int to double
     System.out.println(result); // Output: 5.0
     ```
2. **Explicit Casting (Narrowing Conversion)**:
  -Required when converting from a larger or more precise type to a smaller or less precise type (e.g., `double` to `int`).
  -Uses the cast operator, such as `(int)` or `(double)`, to explicitly indicate the conversion.
  -May result in data loss (e.g., truncation of decimal places).
  -Examples:
     ```java
     double pi=3.14159;
     int truncatedPi=(int) pi; // Casts double to int, truncates to 3
     System.out.println(truncatedPi); // Output: 3
     ```
     ```java
     int wholeNumber=3;
     double expanded=(double) wholeNumber; // Casts int to double, becomes 3.0
     System.out.println(expanded); // Output: 3.0
     ```
### Key Rules
- **Syntax**: Use parentheses with the target type, e.g., `(int)(expression)` or `(double)(expression)`.
- **Truncation in `double` to `int` Casting**: When casting a `double` to an `int`, the decimal portion is discarded (not rounded).
 -Example: `(int) 3.999` results in `3`, not `4`.
- **No Casting for `boolean`**: `boolean` values cannot be cast to or from other types.
### Rounding Doubles to Nearest Integer
To round a `double` to the nearest integer (rather than truncating), use the following formulas:
- **For positive numbers**: `(int)(x+0.5)`
 -Adds 0.5 to shift the value, then truncates the decimal.
 -Example: `(int)(3.6+0.5)`->`(int)(4.1)`->`4`
- **For negative numbers**: `(int)(x-0.5)`
 -Subtracts 0.5 to shift the value, then truncates.
 -Example: `(int)(-3.6-0.5)`->`(int)(-4.1)`->`-4`
### Example Program
```java
public class CastingExample {
    public static void main(String[] args) {
        // Explicit casting: double to int
        double value=3.14159;
        int truncated=(int) value;
        System.out.println("Truncated: "+truncated); // Output: 3
        // Rounding positive double
        double positive=3.6;
        int roundedPositive=(int)(positive+0.5);
        System.out.println("Rounded Positive: "+roundedPositive); // Output: 4
        // Rounding negative double
        double negative=-3.6;
        int roundedNegative=(int)(negative-0.5);
        System.out.println("Rounded Negative: "+roundedNegative); // Output: -4
        // Implicit casting: int to double
        int whole=5;
        double expanded=whole;
        System.out.println("Expanded: "+expanded); // Output: 5.0
    }
}
```
### Common Errors
- **Missing Cast**: Attempting a narrowing conversion without explicit casting causes a compilation error.
 -Example: `int x=3.14;` (requires `(int)`).
- **Incorrect Rounding Logic**: Applying the positive rounding formula to negative numbers (or vice versa) yields incorrect results.
 -Example: `(int)(-3.6+0.5)`->`(int)(-3.1)`->`-3` (incorrect; should be `-4`).
---
## 3. Connection to AP CS A Unit 1
### Curriculum Context
Unit 1 of AP CS A introduces students to Java programming fundamentals, including:
- **Variables and Data Types**: Declaring and using `int`, `double`, and `boolean` variables.
- **Basic Operations**: Arithmetic operations (`+`, `-`, `*`, `/`, `%`) often involve type casting for mixed types.
- **Input/Output**: Using `System.out.println` to display values, which may require casting for formatting.
- **Program Structure**: Writing `main` methods and simple programs to manipulate primitive types.
### Relevance of Casting
- Many AP CS A problems involve calculations with mixed types (e.g., averaging `int` values to get a `double` result).
- Casting is critical for handling user input (e.g., converting `String` to `int` or `double` using `Scanner`) and formatting output.
- Rounding techniques are useful for real-world applications, such as converting floating-point results to integers for display.
### Practice Questions
1. **Code Tracing**: What is the output of the following code?
   ```java
   double x=7.8;
   int y=(int)(x+0.5);
   System.out.println(y);
   ```
   **Answer**: `8`
2. **Error Identification**: Why does the following code fail to compile?
   ```java
   double d=9.99;
   int i=d;
   ```
   **Answer**: A `double` cannot be assigned to an `int` without explicit casting. Correct code: `int i=(int) d;`.
3. **Coding Exercise**: Write a program that takes a `double` input and rounds it to the nearest integer, handling both positive and negative numbers correctly.
---
## 4. Additional Notes
- **Best Practices**:
 -Use meaningful variable names (e.g., `temperature` instead of `t`) to improve code readability.
 -Comment code to explain complex casting or rounding logic.
 -Test edge cases (e.g., `0.5`, `-0.5`, large numbers) when rounding.
- **Extensions**:
 -Explore the `Math` class (e.g., `Math.round`, `Math.floor`, `Math.ceil`) for alternative rounding methods, though these are typically introduced later in AP CS A.
 -Understand how casting affects arithmetic operations, e.g., `(double) 5 / 2` yields `2.5`, while `5 / 2` yields `2`.
---
