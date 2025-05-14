[Go back to home page](README.md)
# [previous](unit_8.md)<-->[next](unit_10.md)
## Inheritance

### Polymorphism
Usual declaration format:  

- ParentClass name = new ChildClass();  

With polymorphism, an object will use the method that is lowest in the inheritance tree, when the child method overrides the parent method.  

However, the method must first exist in the parent class for it to be called. 

If there is no method in the child class, the method can still be called without a problem. 

### Note For Child Class Constructor
**REMEMBER!!!:** for a child class constructor to work, the first line must be *super(param)* if the parent class constructor needs parameters.
