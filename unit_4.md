[Go back to home page](README.md)
# [previous](unit_3.md)<-->[next](unit_5.md)
## Unit 4
### For loop: 
```java
for(initial condition; test condition; loop code){ 
	//code that is run each iteration 
} 
```
* Just to clarify for some dinners: if the test condition is met, the loop code will be run. If the test condition is still met after that, then the code will be run 
> **TOP TIP**
> There is usually no need to set special if statements, since you can set up the test condition in such a way that the loop will not be run, ex 
  
### Enhanced For (For-each) loop:  
```java
for(DataType i: NameOfArrayOrList){ 
//whatever is in the loop  
}  
```
* An Enhanced For Loop is also unable to modify array elements or know what the index of the current entry being accessed is. 
> **TOP TIP**
> i is just the object or value on that place of the list, not the index in the array (this information cannot be accessed) 

### Search and Sort 
* **Linear Search**: goes through the list until the target has been found. 
* **Binary Search**: search through a sorted (What to note: SORTED) list by repeatedly dividing and searching the list in half, much more efficient than linear search for large input 
* **Merge Sort**: Divide and Conquer algorithm. Divide an unsorted array into smaller parts and merge them together. Usually implemented with recursion 
* **Selection Sort**: Use a nested for loop to find the smallest value in the array and put it at the current position, so that the sorted list is gradually built up. 
* **Insertion Sort**: Use a while loop within a for loop to examine each element one by one. It will then move all the elements that are before the element and larger than the element backwards one. The element being examined would then be placed in the empty spot generated. 
