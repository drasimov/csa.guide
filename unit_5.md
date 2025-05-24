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