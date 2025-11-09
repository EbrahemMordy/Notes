# Explanations
dependency is that when class depend on another class, like class A use method x from class B so we say class B is dependency of A
![[0_cucRYwx7QS4o2nfm.webp]]
```java
class ClassA {

  ClassB classB = new ClassB();

  int tenPercent() {
    return classB.calculate() * 0.1d;
  }
}
```
## The Dependency Injection Principle
It's nothing but being able to pass (inject) the dependencies when required instead of initializing the dependencies inside the recipient class.
## Setter Injection (Not recommended)
instead of hard code the instance and make it with new, we make it and made a function to take a parameter of this type and assign it to the filed 
```java
class ClassA {

  ClassB classB;

  /* Setter Injection */
  void setClassB(ClassB injected) {
    classB = injected;
  }

  int tenPercent() {
    return classB.calculate() * 0.1d;
  }
}
```
with this way we can assign any instance of class B or any subclass of it with our class A
but with this way we can have a `NPE` if we make an instance of class A without set class B 
## Constructor Injection (Highly recommended)
with this way we inject the filed in the constructor itself 
```java
class ClassA {

  ClassB classB;

  /* Constructor Injection */
  ClassA(ClassB injected) {
    classB = injected;
  }

  int tenPercent() {
    return classB.calculate() * 0.1d;
  }
}
```
### ADVANTAGES:
- The functionality remains intact compared with the `Setter Injection` approach
- We removed the `new` initialization from the `ClassA`.
- We still can inject a specialized subclass of `ClassB` to `ClassA`.
- Now the compiler is going to ask us for the dependencies that we need in compile time.
## Field Injection (Kids don’t try this at home)
The only way for field injection to work is:
- Mutating the field because it’s a non-private and non-final field
- Mutating a final/private field using reflection
## Realistic Example


# Source
[Dependency Injection in Java](https://medium.com/groupon-eng/dependency-injection-in-java-9e9438aa55ae) 