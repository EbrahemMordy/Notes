### Method Chaining
Start by calling a method then keep calling another method for each return 

#### Benefits
- easier to understand and read
- increase performance

#### Key Uses of Java Method Chaining
- simplify complex processes that take several steps to complete
- use it as an alternative to “callback hell”, which describes situations where a developer needs to pass a callback (a function) through multiple nested functions.

#### Understanding Method Return Values
each chained method should return the same type of value that was used for the initial method call

#### Strategies for Avoiding Common Issues with Method Chaining
- if a developer is working with complex chains, it is advisable to split them into multiple lines for clarity and readability
- ensure consistency in return types by including documentation along with your code.
- use meaningful variable names when working with method chaining.
- use defensive coding techniques when working with method chaining.

#### Return this from functions`
you can make the functions return `this` as this will help you to call another functions in same object 
also if there is some final data you can use Builder 

### Enums
is used to have a predefined value i want to use across the project

### Record
its used instead of making a class to only carry some variables in it, it just mark it as record and give it the variables you need to carry, it don't allow set methods, allowed to add new constructors and new methods
