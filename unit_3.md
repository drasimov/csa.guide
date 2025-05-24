[Go back to home page](README.md)
# [previous](unit_2.md)<-->[next](unit_4.md)
# AP CS A Unit Three: Boolean Expressions and Conditional Statements
## 1. Boolean Expressions
### Definition
A Boolean expression in Java evaluates to either `true` or `false`, forming the foundation for decision-making in programs. In AP Computer Science A (AP CS A) Unit Three, Boolean expressions are used to control the flow of execution through conditional statements, enabling programs to respond dynamically to different inputs or conditions, such as determining a student's eligibility for a course based based on their grades.
### Components of Boolean Expressions
Boolean expressions are constructed using:
- **Relational Operators**: Compare two values and return a `boolean` result.
  - `==`: Equals (e.g., `score == 90` checks if `score` is 90).
  - `!=`: Not equals (e.g., `score != 100` checks if `score` is not 100).
  - `<`, `>`: Less than, greater than (e.g., `grade < 60`, `grade > 90`).
  - `<=`, `>=`: Less than or equal to, greater than or equal to (e.g., `score <= 85`).
- **Logical Operators**: Combine or modify Boolean expressions.
  - `&&`: Logical AND (e.g., `score >= 90 && score <= 100` checks if `score` is between 90 and 100, inclusive).
  - `||`: Logical OR (e.g., `score < 60 || score > 100` checks if `score` is outside the valid range).
  - `!`: Logical NOT (e.g., `!isPassing` inverts the value of `isPassing`).
- **Boolean Variables**: Store `true` or `false` directly (e.g., `boolean isEnrolled = true;`).
- **Compound Expressions**: Combine multiple conditions using logical operators (e.g., `(score >= 90 && attendance >= 80)`).
### Key Notes
- Boolean expressions must evaluate to a `boolean` type;expressions like `score = 90` (assignment) are not valid in conditions.
- Parentheses can clarify the order of operations in compound expressions (e.g., `(score >= 90) && (attendance >= 80)`).
- Short-circuit evaluation applies: For `&&`, if the left operand is `false`, the right is not evaluated;for `||`, if the left is `true`, the right is not evaluated.
### Example
```java
int score = 85;
boolean isPassing = score >= 60;// true
boolean isHonors = score >= 90 && score <= 100;// false
boolean isInvalid = score < 0 || score > 100;// false
boolean notPassing = !isPassing;// false
System.out.println("Passing: " + isPassing);
System.out.println("Honors: " + isHonors);
System.out.println("Invalid: " + isInvalid);
System.out.println("Not Passing: " + notPassing);
```
**Output**:
```
Passing: true
Honors: false
Invalid: false
Not Passing: false
```
### Common Errors
- **Using `=` Instead of `==`**: `if (score = 90)` assigns 90 to `score` and evaluates to a non-Boolean, causing a compilation error. Use `if (score == 90)`.
- **Operator Precedence**: Logical operators may lead to unexpected results without parentheses. Example: `score >= 90 && score <= 100 || isExempt` may need parentheses to clarify intent.
- **Invalid Comparisons**: Comparing incompatible types (e.g., `String` with `==`) is covered later in AP CS A but can cause errors if attempted.
---
## 2. Conditional Statements
### Definition
Conditional statements (`if`, `else if`, `else`) allow a program to execute different blocks of code based on the evaluation of Boolean expressions. They are essential for implementing decision-making logic, such as assigning grades based on a score or determining eligibility for a program.
### Types of Conditional Statements
1. **Simple `if` Statement**:
   - Executes a block of code if the condition is `true`.
   - Example:
     ```java
     int score = 85;
     if (score >= 60) {
         System.out.println("You passed!");
     }
     ```
     **Output**: `You passed!`
2. ** `if-else` Statement**:
   - Executes one block if the condition is `true`, another if `false`.
   - Example:
     ```java
     int score = 55;
     if (score >= 60) {
         System.out.println("You passed!");
     }
     else {
         System.out.println("You did not pass.");
     }
     ```
     **Output**: `You did not pass.`
3. ** `if-else if-else` Statement**:
   - Tests multiple conditions sequentially, executing the first `true` block or the `else` block if none are `true`.
   - Example:
     ```java
     int score = 92;
     if (score >= 90) {
         System.out.println("Grade: A");
     }
     else if (score >= 80) {
         System.out.println("Grade: B");
     }
     else if (score >= 70) {
         System.out.println("Grade: C");
     }
     else {
         System.out.println("Grade: F");
     }
     ```
     **Output**: `Grade: A`
4. **Nested Conditionals**:
   - Conditionals within conditionals, used for complex logic.
   - Example:
     ```java
     int score = 95;
     boolean isEnrolled = true;
     if (isEnrolled) {
         if (score >= 90) {
             System.out.println("Eligible for honors!");
         }
         else {
             System.out.println("Not eligible for honors.");
         }
     }
     else {
         System.out.println("Not enrolled.");
     }
     ```
     **Output**: `Eligible for honors!`
### Key Notes
- Each `if`, `else if`, `else` block forms a single logical unit. Only one block executes per conditional structure.
- Braces `{}` define the scope of each block. Omitting them for single-statement blocks is legal but risky, as adding statements later may cause errors.
- Conditions are evaluated sequentially;once a `true` condition is found, subsequent conditions are skipped.
- Nested conditionals increase complexity and should be used judiciously to maintain readability.
### Common Errors
- **Dangling `else`**: Misplaced `else` statements can bind to the wrong `if`. Example:
  ```java
  if (score >= 90)
      if (score <= 100)
          System.out.println("A");
  else
      System.out.println("Not A");
  ```
  The `else` binds to the inner `if`, not the outer one. Use braces to clarify intent.
- **Missing Braces**: Omitting braces can lead to unexpected behavior when adding statements. Example:
  ```java
  if (score >= 60)
      System.out.println("Pass");
      System.out.println("Check score");// Executes regardless of condition
  ```
- **Redundant Conditions**: Overlapping conditions (e.g., `if (score >= 90)` followed by `else if (score >= 80 && score <= 90)`) can be simplified.
---
## 3. De Morgan's Laws
### Definition
De Morgan's Laws describe the relationship between logical operators and their negations, allowing simplification or transformation of Boolean expressions. They are critical for optimizing conditional logic and understanding complex conditions in AP CS A.
### Rules
- **First Law**: The complement of the conjunction of two conditions is equivalent to the disjunction of their complements.
  - Formal: `!(A && B) == !A || !B`
  - Example: `!(score >= 90 && attendance >= 80)` is equivalent to `score < 90 || attendance < 80`.
- **Second Law**: The complement of the disjunction of two conditions is equivalent to the conjunction of their complements.
  - Formal: `!(A || B) == !A && !B`
  - Example: `!(score < 60 || score > 100)` is equivalent to `score >= 60 && score <= 100`.
### Application
De Morgan's Laws are used to:
- Simplify complex conditions for readability or performance.
- Rewrite conditions to avoid nested negations.
- Verify the equivalence of Boolean expressions in program logic.
### Example
```java
int score = 85;
boolean attendance = true;
// Original condition
boolean notEligible = !(score >= 90 && attendance);
// Using De Morgan's Law: !(score >= 90 && attendance) == score < 90 || !attendance
boolean equivalent = score < 90 || !attendance;
System.out.println("Not Eligible: " + notEligible);// true
System.out.println("Equivalent: " + equivalent);// true
```
**Output**:
```
Not Eligible: true
Equivalent: true
```
### Common Errors
- **Incorrect Negation**: Misapplying De Morgan's Laws, such as writing `!(A && B)` as `!A && !B` (incorrect) instead of `!A || !B`.
- **Forgetting Parentheses**: Negating compound expressions without parentheses can lead to operator precedence issues.
---
## 4. Ternary Operator
### Definition
The ternary operator (`?:`) provides a concise alternative to an `if-else` statement for assigning a value based on a condition. It is an advanced feature in AP CS A, typically used for simple conditional assignments.
### Syntax
```java
variable = condition ? valueIfTrue : valueIfFalse;
```
- If `condition` is `true`, `valueIfTrue` is assigned;otherwise, `valueIfFalse` is assigned.
### Example
```java
int score = 85;
String status = score >= 60 ? "Pass" : "Fail";
System.out.println("Status: " + status);// Output: Pass
```
This is equivalent to:
```java
String status;
if (score >= 60) {
    status = "Pass";
}
else {
    status = "Fail";
}
```
### Key Notes
- The ternary operator is best for simple, single-expression assignments.
- Overusing it for complex logic can reduce readability.
- Both `valueIfTrue` and `valueIfFalse` must be of compatible types.
### Common Errors
- **Type Mismatch**: The two values must be assignable to the target variable (e.g., `int x = score >= 60 ? 1 : "Pass";` fails).
- **Overcomplication**: Nesting ternary operators (e.g., `a ? b ? c : d : e`) is hard to read and should be avoided.
---
## 5. Example Program
This program demonstrates Boolean expressions, conditional statements, De Morgan's Laws, and the ternary operator in the context of a student grading system.
```java
public class GradeCalculator {
    public static void main(String[] args) {
        // Input variables
        int score = 92;
        int attendance = 85;
        boolean isEnrolled = true;
        // Boolean expressions
        boolean isPassing = score >= 60;
        boolean isHonors = score >= 90 && attendance >= 80;
        boolean isInvalid = score < 0 || score > 100;
        boolean validScore = !(score < 0 || score > 100);// Using De Morgan's: score >= 0 && score <= 100
        // Conditional statements
        String grade;
        if (score >= 90) {
            grade = "A";
        }
        else if (score >= 80) {
            grade = "B";
        }
        else if (score >= 70) {
            grade = "C";
        }
        else if (score >= 60) {
            grade = "D";
        }
        else {
            grade = "F";
        }
        // Nested conditional
        String eligibility;
        if (isEnrolled) {
            if (isHonors) {
                eligibility = "Eligible for honors";
            }
            else {
                eligibility = "Not eligible for honors";
            }
        }
        else {
            eligibility = "Not enrolled";
        }
        // Ternary operator
        String status = isPassing ? "Pass" : "Fail";
        // Output
        System.out.println("Student Grade Report:");
        System.out.println("Score: " + score);
        System.out.println("Attendance: " + attendance);
        System.out.println("Enrolled: " + isEnrolled);
        System.out.println("Passing: " + isPassing);
        System.out.println("Honors: " + isHonors);
        System.out.println("Invalid Score: " + isInvalid);
        System.out.println("Valid Score (De Morgan's): " + validScore);
        System.out.println("Grade: " + grade);
        System.out.println("Eligibility: " + eligibility);
        System.out.println("Status: " + status);
    }
}
```
**Output**:
```
Student Grade Report:
Score: 92
Attendance: 85
Enrolled: true
Passing: true
Honors: true
Invalid Score: false
Valid Score (De Morgan's): true
Grade: A
Eligibility: Eligible for honors
Status: Pass
```
---
## 6. Connection to AP CS A Unit Three
### Curriculum Context
AP CS A Unit Three introduces control structures, focusing on:
- **Boolean Expressions**: Constructing conditions using relational and logical operators to evaluate program state (e.g., grading criteria).
- **Conditional Statements**: Implementing decision-making logic to handle different scenarios, such as assigning letter grades or checking eligibility.
- **Program Logic**: Combining expressions and conditionals to create robust programs, a foundation for later units like loops and methods.
- **De Morgan's Laws and Ternary Operator**: Advanced tools for optimizing and simplifying code, preparing students for complex problem-solving.
### Relevance
- Boolean expressions and conditionals are critical for real-world applications, such as determining academic outcomes or validating user input.
- Understanding logical equivalence (via De Morgan's Laws) enhances code efficiency and clarity.
- Conditional logic is a prerequisite for loops (Unit 4) and method control flow (Unit 5).
### Practice Questions
1. **Code Tracing**: What is the output of this code?
   ```java
   int score = 75;
   if (score >= 80) {
       System.out.println("High");
   }
   else if (score >= 60) {
       System.out.println("Medium");
   }
   else {
       System.out.println("Low");
   }
   ```
   **Answer**: `Medium`
2. **Error Identification**: Why does this code fail?
   ```java
   int score = 90;
   if (score = 100) {
       System.out.println("Perfect");
   }
   ```
   **Answer**: Uses `=` (assignment) instead of `==` (comparison), causing a compilation error. Correct: `if (score == 100)`.
3. **Coding Exercise**: Write a program that takes a score (0–100) and an attendance percentage (0–100), and determines if a student is eligible for a scholarship (score ≥ 85 and attendance ≥ 90). Use De Morgan's Laws to print if the student is *not* eligible.
---
## 7. Additional Notes
### Best Practices
- Use clear, descriptive variable names (e.g., `isPassing` instead of `b`) to enhance readability.
- Add comments to explain complex conditional logic or De Morgan's Law applications.
- Test edge cases (e.g., `score = 90`, `attendance = 0`) to ensure robustness.
- Avoid overly nested conditionals;consider refactoring into methods (introduced in Unit 5) for clarity.
### Extensions
The following advanced concepts are intended for programmers seeking to deepen their understanding of Boolean expressions and conditional statements:
1. **Short-Circuit Evaluation in Depth**  
   Short-circuit evaluation optimizes code by halting evaluation once the outcome is determined. For `&&`, if the left operand is `false`, the right is skipped;for `||`, if the left is `true`, the right is skipped. This is useful for preventing errors, such as division by zero.  
   **Example**:
   ```java
   int denominator = 0;
   int numerator = 10;
   if (denominator != 0 && numerator / denominator > 2) {
       System.out.println("Result is large");
   }
   else {
       System.out.println("Cannot divide or result too small");
   }
   ```
   **Output**: `Cannot divide or result too small`  
   Here, `denominator != 0` is `false`, so `numerator / denominator` is not evaluated, avoiding a runtime error.
2. **Compound Boolean Expressions with Precedence**  
   Logical operators have precedence: `!` (highest), `&&`, then `||` (lowest). Without parentheses, this can lead to unexpected results. Always use parentheses to ensure clarity.  
   **Example**:
   ```java
   int score = 85;
   boolean exempt = true;
   boolean result = score >= 90 && score <= 100 || exempt;
   boolean clearResult = (score >= 90 && score <= 100) || exempt;
   System.out.println("Result: " + result);// true
   System.out.println("Clear Result: " + clearResult);// true
   ```
   Without parentheses, `score >= 90 && score <= 100 || exempt` is evaluated as `(score >= 90 && score <= 100) || exempt`, but parentheses make intent explicit.
3. **Using Boolean Methods in Conditions**  
   Methods that return `boolean` can be used directly in conditional statements, encapsulating complex logic. This previews Unit 5 (Methods) and promotes modularity.  
   **Example**:
   ```java
   public class GradeChecker {
       public static boolean isEligibleForScholarship(int score, int attendance) {
           return score >= 85 && attendance >= 90;
       }
       public static void main(String[] args) {
           int score = 88;
           int attendance = 92;
           if (isEligibleForScholarship(score, attendance)) {
               System.out.println("Scholarship eligible");
           }
           else {
               System.out.println("Not eligible");
           }
       }
   }
   ```
   **Output**: `Scholarship eligible`
4. **Ternary Operator in Complex Expressions**  
   The ternary operator can handle nested conditions, but overuse reduces readability. Use it for concise, clear assignments.  
   **Example**:
   ```java
   int score = 75;
   String grade = score >= 90 ? "A" : score >= 80 ? "B" : score >= 70 ? "C" : "F";
   System.out.println("Grade: " + grade);// C
   ```
   This is equivalent to nested `if-else` statements but is less readable. Prefer `if` statements for complex logic.
5. **Logical Equivalence and Optimization**  
   Beyond De Morgan's Laws, other logical transformations can simplify code. For example, `A && (B || C)` can sometimes be rewritten as `(A && B) || (A && C)` (distributive property) to reduce evaluations.  
   **Example**:
   ```java
   int score = 85;
   int attendance = 75;
   boolean original = score >= 90 && (attendance >= 80 || score >= 95);
   boolean optimized = (score >= 90 && attendance >= 80) || (score >= 95 && attendance >= 80);
   System.out.println("Original: " + original);// false
   System.out.println("Optimized: " + optimized);// false
   ```
   The optimized form may be clearer or more efficient in specific contexts, especially when combined with short-circuit evaluation.