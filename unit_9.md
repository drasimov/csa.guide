[Go back to home page](README.md)
# [previous](unit_8.md)<-->[next](unit_10.md)
# AP CS A Unit Nine: Inheritance
## 1. Overview
Inheritance is a core object-oriented principle where a class (child/subclass) acquires fields and methods of another class (parent/superclass), promoting code reuse and abstraction. In AP CS A Unit Nine, the foci are single inheritance in Java, method overriding, and object interactions across an inheritance hierarchy.
## 2. Polymorphism
### Definition
Polymorphism allows a reference variable of a parent class type to refer to objects of child classes. The actual method invoked is determined at runtime, depending on the object's concrete class.
### Syntax and Behavior
```java
// Declaration using polymorphism
ApExamRecord record = new MultipleChoiceRecord();
```
* **Compile-time type**: `ApExamRecord` (parent)
* **Runtime type**: `MultipleChoiceRecord` (child)
When `record.calculateScore()` is called, Java invokes the lowest override in the hierarchy. If `MultipleChoiceRecord` overrides `calculateScore()`, that implementation runs; otherwise, it falls back to the parent’s version.
```java
public class ApExamRecord {
    public int calculateScore() {
        return 0; // default base behavior
    }
}
public class MultipleChoiceRecord extends ApExamRecord {
    @Override
    public int calculateScore() {
        int[] studentAnswers = {1, 3, 2, 4, 2};
        int[] correctAnswers = {1, 3, 2, 4, 2};
        int totalCorrect = 0;
        for (int i = 0; i < studentAnswers.length; i++) {
            if (studentAnswers[i] == correctAnswers[i]) {
                totalCorrect++;
            }
        }
        return totalCorrect * 2; // 2 points per question
    }
}
```
> **Key Point:** The overridden method must be declared in the parent class to be called polymorphically. New methods in the child require downcasting to invoke.
## 3. Constructors in Inheritance
### Note for Child Class Constructor
**REMEMBER:** If the parent class has a constructor requiring parameters, the first line of every child constructor must call `super(...)` with appropriate arguments before initializing child-specific fields.
```java
public class ApStudent {
    protected String studentName;

    public ApStudent(String studentName) {
        this.studentName = studentName;
    }
}
public class ChemistryStudent extends ApStudent {
    private int labScore;

    public ChemistryStudent(String studentName, int labScore) {
        super(studentName);        // call to parent constructor
        this.labScore = labScore;   // child-specific initialization
    }
}
```
Failure to call `super(...)` causes a compile-time error if no default parent constructor exists.
## 4. Upcasting and Downcasting
* **Upcasting**: Assigning a child object to a parent reference. Implicit and safe.
  ```java
  ApStudent student = new ChemistryStudent("Alex", 95);
  ```
* **Downcasting**: Converting a parent reference back to a child type. Requires an explicit cast and `instanceof` check to avoid `ClassCastException`.
  ```java
  if (student instanceof ChemistryStudent) {
      ChemistryStudent chem = (ChemistryStudent) student;
      int score = chem.getLabScore();
  }
  ```
## 5. Interfaces vs. Abstract Classes
### Abstract Classes
* Can include fields, constructors, concrete methods, and abstract methods.
* A class may extend one abstract class.
```java
public abstract class ApCourse {
    public abstract void takeExam();
    public void joinStudyGroup() {
        System.out.println("Joining study group...");
    }
}
```
### Interfaces
* Cannot have constructors or instance fields (Java 8+ allows `default` methods and `static` fields).
* A class can implement multiple interfaces.
```java
public interface GradingPolicy {
    double calculateGrade(double[] scores);
}
public class ApEnglish implements GradingPolicy {
    @Override
    public double calculateGrade(double[] scores) {
        double sum = 0;
        for (double s : scores) sum += s;
        return sum / scores.length;
    }
}
```
## 6. Inheritance Pitfalls and Best Practices
* **Fragile Base Class**: Changes in the parent can unexpectedly affect all subclasses—maintain clear documentation.
* **Use `@Override` Annotation**: Catches signature mismatches at compile time.
* **Favor Composition Over Inheritance**: Use when reuse can be achieved by containing instances rather than extending.
## 7. Composition Example
Composition involves including existing classes as fields rather than extending them, promoting loose coupling.
```java
public class ApExamReport {
    private ApStudent student;
    private ApExamRecord record;
    public ApExamReport(ApStudent student, ApExamRecord record) {
        this.student = student;
        this.record = record;
    }
    public void printReport() {
        System.out.println(student.studentName + " scored " + record.calculateScore());
    }
}
```
## 8. Extensions to Non-Curricular Topics
### 8.1 How to Use These Principles
1. **Liskov Substitution Principle (LSP)**
   * Ensure subclass methods honor the contracts of superclass methods (preconditions and postconditions).
   * Use tests that treat superclass and subclass instances interchangeably.
2. **Final Classes and Methods**
   * Mark classes/methods `final` to prevent modification or extension when stability is crucial.
   * Example: Utility classes like `java.lang.Math` are `final`.
3. **Design Patterns**
   * **Template Method**: Define a skeleton of an algorithm in an abstract class, deferring steps to subclasses.
     ```java
     public abstract class ExamGrader {
         public final void grade() {
             collectAnswers();
             int score = calculateScore();
             report(score);
         }
         protected abstract void collectAnswers();
         protected abstract int calculateScore();
         private void report(int score) {
             System.out.println("Score: " + score);
         }
     }
     ```
   * **Strategy Pattern**: Define a family of algorithms (interfaces) and make them interchangeable within a context class.
     ```java
     public interface ScoringStrategy {
         int score(int[] ans, int[] key);
     }
     public class StandardScoring implements ScoringStrategy {
         public int score(int[] a, int[] k) {
             int count = 0;
             for (int i = 0; i < a.length; i++) if (a[i] == k[i]) count++;
             return count * 1;
         }
     }
     public class EnhancedScoring implements ScoringStrategy {
         public int score(int[] a, int[] k) {
             int points = 0;
             for (int i = 0; i < a.length; i++) {
                 points += (a[i] == k[i]) ? 2 : -1;
             }
             return Math.max(points, 0);
         }
     }
     public class ExamContext {
         private ScoringStrategy strategy;
         public ExamContext(ScoringStrategy strategy) {
             this.strategy = strategy;
         }
         public int execute(int[] ans, int[] key) {
             return strategy.score(ans, key);
         }
     }
     ```
### 8.2 Examples
* **LSP in Action**:
  ```java
  public class BasePrinter {
      public void print(String text) { System.out.println(text); }
  }
  public class ColorPrinter extends BasePrinter {
      @Override
      public void print(String text) {
          System.out.println("\u001B[31m" + text + "\u001B[0m");
      }
  }
  BasePrinter p1 = new BasePrinter();
  BasePrinter p2 = new ColorPrinter();
  p1.print("Hello"); // normal
  p2.print("Hello"); // colored, still "Hello"
  ```
* **Final Method Example**:
  ```java
  public class SecureExam {
      public final void validateIdentity() {
          // fixed identity checks
      }
  }

  // Any subclass cannot override validateIdentity()
  ```
* **Strategy Pattern Use Case**:
  ```java
  int[] answers = {1,2,3};
  int[] key = {1,2,4};
  ExamContext standard = new ExamContext(new StandardScoring());
  ExamContext enhanced = new ExamContext(new EnhancedScoring());
  System.out.println(standard.execute(answers, key)); // score 2
  System.out.println(enhanced.execute(answers, key)); // score maybe higher
  ```
---
### 8.3 Additional Advanced Topics
4. **SOLID Principles**: A mnemonic for five design principles:
   * **S**ingle Responsibility Principle: A class should have one reason to change.
   * **O**pen/Closed Principle: Classes should be open for extension but closed for modification.
   * **L**iskov Substitution Principle (covered above).
   * **I**nterface Segregation Principle: Clients should not be forced to depend on unused methods—favor smaller, role-specific interfaces.
   * **D**ependency Inversion Principle: Depend upon abstractions, not concrete classes—inject dependencies via constructors or setters.
5. **Reflection and Annotations**:
   * Use the Reflection API (`java.lang.reflect`) to inspect classes, methods, and fields at runtime, enabling dynamic loading or testing frameworks.
     ```java
     Class<?> cls = Class.forName("ApStudent");
     for (Method m : cls.getMethods()) {
         System.out.println(m.getName());
     }
     ```
   * Create custom annotations to add metadata for tools or frameworks:
     ```java
     @Retention(RetentionPolicy.RUNTIME)
     @Target(ElementType.METHOD)
     public @interface TestCase {
         String description();
     }

     public class StudentTests {
         @TestCase(description = "Verify lab score calculation")
         public void testLabScore() { /* ... */ }
     }
     ```
6. **Generics and Bounded Types**:
   * Parameterize classes and methods to work with any type, improving type safety and reuse:
     ```java
     public class GradeBox<T extends Number> {
         private T grade;
         public GradeBox(T grade) { this.grade = grade; }
         public T getGrade() { return grade; }
     }
     ```
7. **Default and Static Interface Methods**:
   * Introduced in Java 8, interfaces can provide default implementations and static helper methods:
     ```java
     public interface Reportable {
         default void report() { System.out.println("Reporting..."); }
         static void log(String msg) { System.out.println("LOG: " + msg); }
     }
     ```
8. **Module System (Java 9+)**:
   * Encapsulate packages into modules using `module-info.java`, controlling visibility and dependencies:
     ```java
     module ap.course { exports com.ap.course; requires java.base; }
     ```
---