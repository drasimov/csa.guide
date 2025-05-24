[Go back to home page](README.md)
# [previous](unit_6.md)<-->[next](unit_8.md)
# AP CS A Unit Seven: ArrayLists
## 1. Introduction to ArrayLists
### Definition
In Java, an `ArrayList` is a dynamic, resizable data structure provided in the `java.util` package. Unlike arrays, which have a fixed size, `ArrayLists` can grow or shrink as elements are added or removed. In AP Computer Science A (AP CS A) Unit Seven, `ArrayList` is introduced as a key tool for managing collections of objects, with a focus on `ArrayList<Integer>` and `ArrayList<String>` for storing integers and strings, respectively, particularly in contexts like managing AP exam data or study groups.
### Key Characteristics
- **Dynamic Size**: `ArrayList` automatically adjusts its size, ideal for lists with varying lengths, such as a list of AP exam scores.
- **Generic Type**: Uses generics (e.g., `ArrayList<String>`) to enforce type safety, ensuring only specified types are stored.
- **Reference Types Only**: Stores objects (e.g., `Integer`, `String`), not primitives (e.g., `int`). Autoboxing/unboxing converts between primitives and wrapper classes (e.g., `int` to `Integer`).
- **AP Context**: Useful for managing dynamic data, such as lists of AP course names, exam scores, or study session hours.
### Core Methods for AP CS A
The following methods are emphasized in Unit Seven:
- `ArrayList<Type> list = new ArrayList<Type>();`: Creates a new `ArrayList`.
- `add(E element)`: Appends an element to the end of the list.
  - Example: `apCourses.add("AP Calculus");`
- `add(int index, E element)`: Inserts an element at the specified index.
  - Example: `apCourses.add(0, "AP Physics");`
- `get(int index)`: Returns the element at the specified index.
  - Example: `String course = apCourses.get(0); // Returns "AP Physics"`
- `set(int index, E element)`: Replaces the element at the specified index.
  - Example: `apCourses.set(0, "AP Chemistry");`
- `remove(int index)`: Removes the element at the specified index, shifting subsequent elements.
  - Example: `apCourses.remove(0);`
- `size()`: Returns the number of elements in the list.
  - Example: `int courseCount = apCourses.size();`
- `clear()`: Removes all elements from the list.
  - Example: `apCourses.clear();`
### Key Notes
- **Import**: Requires `import java.util.ArrayList;` at the top of the file.
- **Indexing**: Like arrays, `ArrayList` uses zero-based indexing.
- **Autoboxing**: Adding an `int` to an `ArrayList<Integer>` automatically wraps it as an `Integer`.
- **Performance**: Adding/removing elements at the end is efficient, but inserting/removing at the beginning or middle is slower due to shifting elements.
- **AP Use**: `ArrayList` is ideal for managing dynamic lists, such as tracking AP exam scores or hours spent studying.
### Example Program
```java
import java.util.ArrayList;
public class APStudyTracker {
    public static void main(String[] args) {
        // Create ArrayList for AP courses
        ArrayList<String> apCourses = new ArrayList<String>();
        // Add courses
        apCourses.add("AP Calculus"); // Index 0
        apCourses.add("AP Biology"); // Index 1
        apCourses.add(1, "AP Physics"); // Inserts at index 1
        // Modify and retrieve
        apCourses.set(0, "AP Chemistry"); // Replaces "AP Calculus"
        String firstCourse = apCourses.get(0); // Retrieves "AP Chemistry"
        // Remove and size
        apCourses.remove(1); // Removes "AP Physics"
        int courseCount = apCourses.size(); // Returns 2
        // Print courses
        System.out.println("AP Courses:");
        for (int i = 0; i < apCourses.size(); i++) {
            System.out.println("Course " + (i + 1) + ": " + apCourses.get(i));
        }
        System.out.println("Total Courses: " + courseCount);
        // AP exam scores
        ArrayList<Integer> apScores = new ArrayList<Integer>();
        apScores.add(5); // Score for exam 1
        apScores.add(5); // Score for exam 2
        System.out.println("AP Exam Scores: " + apScores);
    }
}
```
**Output**:
```
AP Courses:
Course 1: AP Chemistry
Course 2: AP Biology
Total Courses: 2
AP Exam Scores: [5, 5]
```
### Common Errors
- **IndexOutOfBoundsException**: Accessing an invalid index, e.g., `apCourses.get(apCourses.size())`.
- **Missing Import**: Forgetting `import java.util.ArrayList;` causes compilation errors.
- **Type Mismatch**: Adding a non-matching type to a generic `ArrayList`, e.g., `ArrayList<Integer> list; list.add("String");` fails.
---
## 2. ArrayList Operations and Loops
### Definition
`ArrayList` operations involve manipulating elements using loops and methods to process dynamic data, such as sorting AP course lists or calculating total study hours. Unit Seven emphasizes iterating over `ArrayList` using `for` loops and enhanced `for` loops.
### Loop Types
1. **Standard For Loop**:
   - Uses an index to access elements, allowing modifications during iteration.
   - Example:
     ```java
     ArrayList<String> apCourses = new ArrayList<String>();
     apCourses.add("AP Chemistry");
     apCourses.add("AP Biology");
     for (int i = 0; i < apCourses.size(); i++) {
         System.out.println(apCourses.get(i));
     }
     ```
2. **Enhanced For Loop**:
   - Simplifies iteration for read-only access, ideal for printing or summing.
   - Example:
     ```java
     ArrayList<Integer> studyHours = new ArrayList<Integer>();
     studyHours.add(10);
     studyHours.add(15);
     int total = 0;
     for (Integer hour : studyHours) {
         total += hour; // Autounboxing to int
     }
     System.out.println("Total Study Hours: " + total);
     ```
### Key Operations
- **Searching**: Check if an element exists using `contains(E element)` or linear search.
  - Example: `if (apCourses.contains("AP Chemistry")) { ... }`
- **Summing**: Calculate totals, e.g., total study hours.
  - Example: Sum hours in an `ArrayList<Integer>` using a loop.
- **Modifying During Iteration**: Use a standard `for` loop to modify elements, as enhanced `for` loops cannot modify the list structure (e.g., adding/removing).
### Example Program
```java
import java.util.ArrayList;
public class APStudyManager {
    public static void main(String[] args) {
        // Initialize ArrayList
        ArrayList<String> apCourses = new ArrayList<String>();
        apCourses.add("AP Chemistry");
        apCourses.add("AP Biology");
        apCourses.add("AP Physics");
        // Search for a course
        String searchCourse = "AP Biology";
        boolean found = apCourses.contains(searchCourse);
        System.out.println(searchCourse + " found: " + found);
        // Calculate total study hours
        ArrayList<Integer> studyHours = new ArrayList<Integer>();
        studyHours.add(10);
        studyHours.add(15);
        studyHours.add(5);
        int totalHours = 0;
        for (Integer hour : studyHours) {
            totalHours += hour;
        }
        System.out.println("Total Study Hours: " + totalHours);
        // Modify list: Remove courses with "AP" in name
        for (int i = apCourses.size() - 1; i >= 0; i--) {
            if (apCourses.get(i).contains("AP")) {
                apCourses.remove(i);
            }
        }
        System.out.println("Courses after removal: " + apCourses);
    }
}
```
**Output**:
```
AP Biology found: true
Total Study Hours: 30
Courses after removal: []
```
### Common Errors
- **ConcurrentModificationException**: Modifying an `ArrayList` (e.g., removing elements) during an enhanced `for` loop causes this error. Use a standard `for` loop instead.
- **Off-by-One Errors**: Incorrect loop bounds, e.g., `i <= list.size()` instead of `i < list.size()`.
- **Null Elements**: Adding `null` to an `ArrayList` can cause `NullPointerException` during operations like `contains`.
---
## 3. Connection to AP CS A Unit Seven
### Curriculum Context
Unit Seven builds on arrays (Unit Six) by introducing `ArrayList` as a more flexible data structure. Key concepts include:
- **Dynamic Lists**: Managing collections with varying sizes, like AP exam scores.
- **Iteration**: Using loops to process `ArrayList` elements.
- **Methods**: Applying `add`, `remove`, `get`, `set`, and `size` for list manipulation.
- **Wrapper Classes**: Understanding autoboxing/unboxing with `Integer` and `Double`.
### Relevance to AP Studies
- `ArrayList` simplifies managing dynamic data, such as adding new AP courses or tracking study hours.
- Loops enable processing lists, e.g., calculating total hours or filtering enrolled courses.
- Methods like `contains` support searching for specific courses, enhancing functionality in AP-related applications.
### Practice Questions
1. **Code Tracing**: What is the output of this code?
   ```java
   ArrayList<Integer> studyHours = new ArrayList<Integer>();
   studyHours.add(10);
   studyHours.add(20);
   int sum = 0;
   for (Integer h : studyHours) {
       sum += h;
   }
   System.out.println(sum);
   ```
   **Answer**: `30`
2. **Error Identification**: Why does this code fail?
   ```java
   ArrayList<String> apCourses = new ArrayList<String>();
   apCourses.add("AP Chemistry");
   for (String course : apCourses) {
       apCourses.remove(0);
   }
   ```
   **Answer**: It throws a `ConcurrentModificationException` because the `ArrayList` is modified during an enhanced `for` loop. Use a standard `for` loop instead.
3. **Coding Exercise**: Write a program that stores AP exam scores in an `ArrayList<Integer>` and calculates the average score, handling empty lists.
---
## 4. Additional Notes
### Best Practices
- Use generics (e.g., `ArrayList<String>`) to ensure type safety.
- Check `size()` before accessing elements to avoid `IndexOutOfBoundsException`.
- Use meaningful names (e.g., `apCourses` instead of `list`) for clarity.
- Comment complex operations, like removing elements during iteration.
### Additional ArrayList Information
- **Additional Methods**:
  - `indexOf(E element)`: Returns the index of the first occurrence of the element, or `-1` if not found.
    - Example: `int index = apCourses.indexOf("AP Chemistry");`
  - `lastIndexOf(E element)`: Returns the index of the last occurrence of the element.
    - Example: `int last = apCourses.lastIndexOf("AP Physics");`
  - `isEmpty()`: Returns `true` if the list is empty.
    - Example: `boolean empty = apCourses.isEmpty();`
  - `toArray()`: Converts the `ArrayList` to an array (advanced, less common in AP CS A).
    - Example: `Object[] courseArray = apCourses.toArray();`
- **Other Characteristics**:
  - **Initial Capacity**: `ArrayList` starts with a default capacity (typically 10) and doubles when needed, improving performance for large lists.
  - **Null Elements**: `ArrayList` allows `null` elements, unlike some other collections.
  - **Thread Safety**: `ArrayList` is not thread-safe; for concurrent access, use `Collections.synchronizedList` (beyond AP CS A scope).
  - **Memory Usage**: Stores references to objects in the heap, with resizing impacting memory efficiency compared to arrays.
- **Sorting**: Use `Collections.sort(list)` (requires `import java.util.Collections;`) to sort elements.
  - Example: `Collections.sort(apCourses);` sorts courses alphabetically.
- **Comparison to Arrays**: Arrays are faster for fixed-size data but lack flexibility; `ArrayList` is preferred for dynamic data in AP applications.