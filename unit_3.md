[Go back to home page](README.md)
## Unit 3
### Conditional Statements 
> **TOP TIP**
> Each `if()/else if()/else()` forms one logical block for the computer to process 
> For example, if you have two if statements then one else statement, the else statement will run if the second if statement is not met 

### De Morgan’s Laws  
* Complement of the union of two sets is the intersection of their complements. 
* Complement of the intersection of two sets is the union of their complements. 
    * `!(A && B) == !A || !B `
    * `!(A || B) == !A && !B `

### Extension (for advanced programmers only): 
```java
if(condition){  
    return a;  
}  
else{  
    return b;  
}  
```
Can be written as 
```java 
return condition ? a:b;
```
