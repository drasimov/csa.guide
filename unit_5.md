[Go back to home page](README.md)  
# [previous](unit_4.md) <-- [next](unit_6.md)  
# AP CS A Unit Five: Crafting Classes
## 1. Structure of a Class
A **class** in Java defines a custom data type, serving as a blueprint for objects by encapsulating **attributes (instance variables)** and **methods (behaviors)**. Classes model real-world entities, such as a student's academic profile, making them relatable for students.
```java
public class AcademicProfile {
    // Attributes
    private int studentID;
    // Constructor
    public AcademicProfile(int initialID) {
        studentID = initialID;
    }
    // Method
    public int getStudentID() {
        return studentID;
    }
}
```
## 2. Constructors
Constructors are special methods that initialize new objects. They share the class's name and have no return type, setting up initial attribute values critical for objects like a scholar's academic record.
* **Default constructor**: Automatically provided if no constructors are defined, initializing attributes to default values.
* **Parameterized constructor**: Accepts parameters to set specific initial values.
```java
public class Scholar {
    private String scholarName;
    private int scholarGradeLevel;
    public Scholar(String name, int gradeLevel) {
        scholarName = name;
        scholarGradeLevel = gradeLevel;
    }
}
```
## 3. Documentation with Comments
Effective documentation improves code clarity, a vital skill for AP CS A students collaborating on projects.
* **Single-line comment**: `// Tracks scholar's name`
* **Multi-line comment**:
  ```java
  /* Stores scholar's academic data
     for school records */
  ```
* **JavaDoc comment**: Generates professional documentation for classes and methods:
  ```java
  /**
   * Retrieves the scholar's grade level.
   * @return the scholar's grade level as an integer
   */
  public int getScholarGradeLevel() {
      return scholarGradeLevel;
  }
  ```
## 4. Accessor and Mutator Methods
Encapsulation, a core principle in AP CS A, protects attributes by declaring them `private` and providing controlled access through methods, ensuring data integrity.
* **Accessor (getter)**:
  ```java
  public String getScholarName() {
      return scholarName;
  }
  ```
* **Mutator (setter)**:
  ```java
  public void setScholarGradeLevel(int newGradeLevel) {
      scholarGradeLevel = newGradeLevel;
  }
  ```
## 5. Designing Methods
Methods define a class's functionality, enabling actions like checking academic status, a task relatable to students' experiences.
* Syntax:
  ```java
  public returnType methodName(parameters) {
      // Method implementation
  }
  ```
* Example:
  ```java
  public boolean isHonorRoll() {
      return scholarGradeLevel >= 90;
  }
  ```
## 5.1 Method Decomposition
### Definition
Method decomposition is the practice of breaking a complex method into smaller, more manageable methods. This improves code readability, maintainability, and reusability—key principles in AP CS A for writing clean, modular code.
### Why Decompose Methods?
1. **Readability**: Smaller methods with descriptive names are easier to understand.
2. **Reusability**: Common logic can be extracted into separate methods and reused.
3. **Maintainability**: Changes to specific functionality are isolated to a single method.
4. **Testing**: Smaller methods are easier to test individually.
### Example: Complex Method Before Decomposition
```java
public class GradeCalculator {
    public void processStudentGrades(int[] scores, String[] names) {
        // Complex method doing multiple things
        double sum = 0;
        for (int score : scores) {
            sum += score;
        }
        double average = sum / scores.length;
        System.out.println("Class Average: " + average);
        // Find highest score
        int highest = scores[0];
        String topStudent = names[0];
        for (int i = 1; i < scores.length; i++) {
            if (scores[i] > highest) {
                highest = scores[i];
                topStudent = names[i];
            }
        }
        System.out.println("Top Student: " + topStudent + " with score " + highest);
        // Determine grade distribution
        int aCount = 0, bCount = 0, cCount = 0, dCount = 0, fCount = 0;
        for (int score : scores) {
            if (score >= 90) aCount++;
            else if (score >= 80) bCount++;
            else if (score >= 70) cCount++;
            else if (score >= 60) dCount++;
            else fCount++;
        }
        System.out.println("Grade Distribution: A=" + aCount + ", B=" + bCount + ", C=" + cCount + ", D=" + dCount + ", F=" + fCount);
    }
}
```
### Example: After Decomposition
```java
public class GradeCalculator {
    public void processStudentGrades(int[] scores, String[] names) {
        double average = calculateAverage(scores);
        printAverage(average);
        String topStudent = findTopStudent(scores, names);
        printTopStudent(topStudent, scores, names);
        int[] gradeDistribution = calculateGradeDistribution(scores);
        printGradeDistribution(gradeDistribution);
    }
    private double calculateAverage(int[] scores) {
        double sum = 0;
        for (int score : scores) {
            sum += score;
        }
        return sum / scores.length;
    }
    private void printAverage(double average) {
        System.out.println("Class Average: " + average);
    }
    private String findTopStudent(int[] scores, String[] names) {
        int highest = scores[0];
        String topStudent = names[0];
        for (int i = 1; i < scores.length; i++) {
            if (scores[i] > highest) {
                highest = scores[i];
                topStudent = names[i];
            }
        }
        return topStudent;
    }
    private void printTopStudent(String topStudent, int[] scores, String[] names) {
        int highest = scores[0];
        for (int i = 1; i < scores.length; i++) {
            if (scores[i] > highest) {
                highest = scores[i];
            }
        }
        System.out.println("Top Student: " + topStudent + " with score " + highest);
    }
    private int[] calculateGradeDistribution(int[] scores) {
        int[] distribution = new int[5]; // A, B, C, D, F
        for (int score : scores) {
            if (score >= 90) distribution[0]++;
            else if (score >= 80) distribution[1]++;
            else if (score >= 70) distribution[2]++;
            else if (score >= 60) distribution[3]++;
            else distribution[4]++;
        }
        return distribution;
    }
    private void printGradeDistribution(int[] distribution) {
        System.out.println("Grade Distribution: A=" + distribution[0] + ", B=" + distribution[1] + ", C=" + distribution[2] + ", D=" + distribution[3] + ", F=" + distribution[4]);
    }
}
```
### Best Practices for Method Decomposition
1. **Single Responsibility Principle**: Each method should do one thing well.
2. **Descriptive Names**: Method names should clearly indicate their purpose.
3. **Reasonable Size**: If a method exceeds 20-30 lines, consider decomposition.
4. **Parameter Management**: Avoid passing too many parameters; consider creating helper classes.
5. **Access Modifiers**: Use `private` for helper methods that are only used within the class.
### Benefits in AP CS A
- **Easier Debugging**: Smaller methods make it easier to locate and fix errors.
- **Code Reuse**: Common operations (like calculating averages) can be reused across multiple methods.
- **Collaboration**: Team members can work on different methods simultaneously.
- **Readability**: Makes code more understandable for AP exam readers.
### Common Errors
- **Over-decomposition**: Creating too many tiny methods can make code harder to follow.
- **Poor Naming**: Vague method names like `doStuff()` reduce clarity.
- **Tight Coupling**: Decomposed methods that depend too much on each other's internal details.
---
## 6. Static Variables and Methods
Static members belong to the class, not individual objects, useful for tracking shared data like the total number of scholars in a school.
* **Static variable**:
  ```java
  private static int totalScholars = 0;
  ```
* **Static method**:
  ```java
  public static int getTotalScholars() {
      return totalScholars;
  }
  ```
## 7. Scope and Access Modifiers
Understanding scope and access is critical for AP CS A students to manage data visibility effectively.
* **`private`**: Restricts access to within the class.
* **`public`**: Allows access from any class.
* **Scope**: Determines where variables and methods are accessible (e.g., local to a method, instance-level, or class-level).
## 8. The `this` Keyword
The `this` keyword clarifies references to the current object's attributes, especially when parameter names match attribute names, addressing a common challenge for students.
```java
public void setScholarName(String scholarName) {
    this.scholarName = scholarName;
}
```
## 9. Ethical and Social Implications of Computing
This section encourages students to reflect on computing's broader impact, aligning with AP CS A's emphasis on responsible programming:
* **Data privacy**: Safeguarding scholar records.
* **Algorithmic fairness**: Ensuring unbiased grade calculations.
* **Ethical data use**: Respecting intellectual property in academic systems.
## Extensions for AP CS A Students
### Overloaded Constructors
Overloaded constructors provide flexibility by allowing multiple ways to initialize objects, such as creating a scholar with or without a grade level.
```java
public class Scholar {
    private String scholarName;
    private int scholarGradeLevel;
    // Default constructor
    public Scholar() {
        scholarName = "Unknown";
        scholarGradeLevel = 0;
    }
    // Overloaded constructor
    public Scholar(String name) {
        scholarName = name;
        scholarGradeLevel = 0;
    }
    // Overloaded constructor
    public Scholar(String name, int gradeLevel) {
        scholarName = name;
        scholarGradeLevel = gradeLevel;
    }
}
```
### Class Relationships
Explore how classes interact through **inheritance** (e.g., a `Scholar` class extending a `Person` class) and **composition** (e.g., a `Course` class containing a `Scholar` object).
* **Inheritance** example:
  ```java
  public class Person {
      private String name;
      public Person(String name) {
          this.name = name;
      }
  }
  public class Scholar extends Person {
      private int scholarGradeLevel;
      public Scholar(String name, int gradeLevel) {
          super(name);
          scholarGradeLevel = gradeLevel;
      }
  }
  ```
* **Composition** example:
  ```java
  public class Course {
      private Scholar enrolledScholar;
      public Course(Scholar scholar) {
          enrolledScholar = scholar;
      }
  }
  ```
### Generating JavaDoc Documentation
Students can use JavaDoc to create professional documentation, a practical skill for AP CS A projects.

* Command to generate JavaDoc:
  ```bash
  javadoc -d doc AcademicProfile.java
  ```
* Example JavaDoc for a method:
  ```java
  /**
   * Checks if the scholar qualifies for honor roll.
   * @return true if scholarGradeLevel is 90 or above, false otherwise
   */
  public boolean isHonorRoll() {
      return scholarGradeLevel >= 90;
  }
  ```
---