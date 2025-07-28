# Chapter 3: The Spring Context: Wiring Beans

- In our applications we usually want one object to refer to the other in order to delegate some functionality and tasks to that other object

- In the previous chapter we used `getBean()` to retrieve beans from context

- In real life we usually want to link together objects in a cleaner manner and we would want to use the dependency injection (DI) and IoC capabilites of spring to do so.

- This chapter is dedicated to how to satisfy objects dependent on other objects using Ioc and DI i.e **wiring beans**

lets start by an example that shows why we need to wire beans in the first place


the follwing config class declares two classes `Person` and `Parrot`. The class `Person` depends on Parrot by composition
```java
public class Person {
    private String name;
    private Parrot parrot;
    // Omitted getters and setters
}
#########################################
public class Parrot {
    private String name;
    // Omitted getters and setters
    @Override
    public String toString() {
        return "Parrot : " + name;
    }
}
#########################################
@Configuration
public class ProjectConfig {
    @Bean
    public Parrot parrot() {
        Parrot p = new Parrot();
        p.setName("Koko");
        return p;
    }

    @Bean
    public Person person() {
        Person p = new Person();
        p.setName("Ella");
        return p;
    }
}
```
executing the follwoing code will shows that the parrot field has not been initilazed with an object
```java
public static void main(String[] args) {
    var context = new AnnotationConfigApplicationContext (ProjectConfig.class);
    Person person = context.getBean(Person.class);
    Parrot parrot = context.getBean(Parrot.class);
    System.out.println("Person's name: " + person.getName());
    System.out.println("Parrot's name: " + parrot.getName());
    System.out.println("Person's parrot: " + person.getParrot());
}
```

the output of the above code is

```
Person's name: Ella
Parrot's name: Koko
Person's parrot: null
```
notice that the person's parrot is null, meaning that the parrot object has not been initlized by the context.

This is the problem we try to solve in this chapter
## Ways of Wiring Beans

### 1. Through calling the `@Bean` Method in the dependant `@Bean`

In this method we call the `@Bean` method that instantiates the dependency in the Config Class directly inside the dependant bean

```java
@Configuration
public class ProjectConfig {
    @Bean
    public Parrot parrot() {
        Parrot p = new Parrot();
        p.setName("Koko");
        return p;
    }
    @Bean
    public Person person() {
        Person p = new Person();
        p.setName("Ella");
        p.setParrot(parrot()); #notice the method call
        return p;
    }
}
```
spring is smart enough to not create a second instance of Parrot when we call `parrot()` inside the dependant class.

spring will look in the context, if it found an instance of parrot it will return it in the second function call. if it didn't it will create a new one and return the newly created instance.

### 2. Through specifing the `@Bean` method parameters

another way of wiring beans is by specifig parameters for the depedant `@Bean` method in the Config Class

```java
@Configuration
public class ProjectConfig {
    @Bean
    public Parrot parrot() {
        Parrot p = new Parrot();
        p.setName("Koko");
        return p;
    }
    @Bean
    public Person person(Parrot parrot) {
        Person p = new Person();
        p.setName("Ella");
        p.setParrot(parrot);
        return p;
    }
}
```
- This uses IoC in the form of DI as spring is now going to inject (simply pass an object to the method) the method with an object from the context with the type specified in the paramter (multiple instances of the same type will be dealt with later)
- This method is more flexibly than method 1 because it allows the dependecy to be a bean declared using the prototype annotations such as `@Component` not only `@Bean` methods

### 3. Using the `@Autowired` annotation

#### 3.1 Using `@Autowired` on the class field
```java
@Component
public class Person {
    private String name = "Ella";
    @Autowired
    private Parrot parrot;
    // Omitted getters and setters
}
```
This method is usally only used for proofs of conecpt and is not desirable to use in production because:
- It stops you from declaring the field as final
- It's more difficult to manage the instances manually at initilization which makes testing harder

#### 3.2 Using `@Autowired` on the class constructor
```java
@Component
public class Person {
    private String name = "Ella";
    private final Parrot parrot;
    @Autowired
    public Person(Parrot parrot){
        this.parrot = parrot;
    }
}
```

#### 3.3 Using `@Autowired` on the class setter
```java
@Component
public class Person {
    private String name = "Ella";
    private final Parrot parrot;
    @Autowired
    public void setParrot(Parrot parrot){
        this.parrot = parrot;
    }
}
```
- This method of using `@Autowired` is not common
- This method also doesn't allow the fild to be final and doesn't help make testing easier

## Chosing Between Multiple Beans of The Same Type
- when the context contains multiple beans of the same type the context can't specify which bean to inject simply by examining the type
- This can be solved in multiple ways

### 1. The Identifer in the parameter matches the Bean name
```java
@Configuration
public class ProjectConfig {
    @Bean
    public Parrot parrot1() {
        Parrot p = new Parrot();
        p.setName("Koko");
        return p;
    }

    @Bean
    public Parrot parrot2() {
        Parrot p = new Parrot();
        p.setName("Miki");
        return p;
    }

    @Bean
    public Person person(Parrot parrot2){
        Person p = new Person();
        p.setName("Ella");
        p.setParrot(parrot2);
        return p;
    }
}
```
In the above code spring will inject the instance with the `name` field equivalent to `Miki` because the identifier matches the name of the Bean i.e `parrot2`

### 2. Declaring `@Primary`
If the identifier name doens't match any Bean name, then if one of the instances was annotated with `@Primary` then spring injects that insatance 

### 3. Using the `@Qualifier` annotation
```java
@Configuration
public class ProjectConfig {
    @Bean
    public Parrot parrot1() {
        Parrot p = new Parrot();
        p.setName("Koko");
        return p;
    }

    @Bean
    public Parrot parrot2() {
        Parrot p = new Parrot();
        p.setName("Miki");
        return p;
    }

    @Bean
    public Person person(@Qualifier("parrot2" Parrot parrot)){
        Person p = new Person();
        p.setName("Ella");
        p.setParrot(parrot);
        return p;
    }
}
```
- Using this notations makes your intentions clear that you are wiring a specific intance and so stops problems that may arise by someone changing the parameter identifier thinking its name is not significant 

**VIP NOTE:** All of the follwing methods for specifig an instance from mulitple insatnces work with any method of wiring beans.


## Ciruclar Dependency
- The term circular dependency refers to the situation where one components needs the other to initilize and vice versa.
- In this situations Spring throws and exception and you must refactor your code
- Cirulucalr dependencies are generaly a sign of a bad class design

```java
@Component
public class Person {
    private final Parrot parrot;

    @Autowired
    public Person(Parrot parrot) {
        this.parrot = parrot;
    }
// Omitted code
}
#########################################
public class Parrot {
    private String name = "Koko";
    private final Person person;

    @Autowired
    public Parrot(Person person) {
        this.person = person;
    }
    // Omitted code
}
```
The above code with throw and exception