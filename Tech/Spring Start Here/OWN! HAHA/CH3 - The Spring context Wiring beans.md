## Implementing relationships among beans defined in the configuration file

### Wiring the beans using a direct method call between the @Bean methods

![[Pasted image 20250425234510.png]]

### Wiring the beans using the @Bean annotated method’s parameters

![[Pasted image 20250425234818.png]]


## Using the @Autowired annotation to inject beans

### Using @Autowired to inject the values through the class fields
![[Pasted image 20250506174920.png]]
#### Why is this approach not desired in production code?
It’s not totally wrong to use it, but you want to make sure you make your app maintainable and testable in production code. By injecting the value directly in the field: 
you don’t have the option to make the field final (see next code snippet), and this way, make sure no one can change its value after initialization
```java
@Component
 public class Person {
  private String name = "Ella";
  @Autowired   
  private final Parrot parrot;  //This doesn’t compile. You cannot define a final field without an initial value.
}
```
It’s more difficult to manage the value yourself at initialization.

### Using @Autowired to inject the values through the constructor
![[Pasted image 20250506175445.png]]
### Using dependency injection through the setter
```java
 @Component
 public class Person {
  private String name = "Ella";
  private Parrot parrot;
  // Omitted getters and setters
  @Autowired
  public void setParrot(Parrot parrot) {
    this.parrot = parrot;
  }
 }
```

## Dealing with circular dependencies
**Circular Dependency** : a situation in which, to create a bean (let’s name it Bean A), Spring needs to inject another bean that doesn’t exist yet (Bean B). But Bean B also requests a dependency to Bean A. So, to create Bean B, Spring needs first to have Bean A. Spring is now in a deadlock. It cannot create Bean A because it needs Bean B, and it cannot create Bean B because it needs Bean A.
![[Pasted image 20250506175918.png]]

## Choosing from multiple beans in the Spring context
Use **@Qualifier** when you have more than one bean with different names

