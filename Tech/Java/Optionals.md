# Explanation
Instead of use null or exceptions to notify that this value doesn't exist, we can use Optional 
## Purpose
when we have a function that return non primitives value it can return a null and this can cause a problem if we didn't handle it, so for every function that can return null we need to check first if the returned value is null or not and this lead to a lot of lines that are boilerplate code so instead we can use Optionals
### `Optional` Class
optional introduced in java 7 and gives us the ability to handle null value returned by methods
if we call a method that return `Optional<>` we must handle the case when this is null with something like `orElse()` or `orElseThrow()` if we want to throw exception in this case 
### Client Responsibility
when we make method return optional we make the client response of handle the case of null as if he wants to create a default value or just throw and error in this case
### `null` `Optional` Objects
sometimes the developer of the method return null directly from a method that return optional, this case is not correct, the optional will always be optional and can not be null, so it's the responsibility of developer of method to return empty optional instead of null
## Important Methods
there are a lot of methods in the optional class, but they are mapped to some categories 
### Creation Methods
#### `of`
it used to create an optional from non-null exist object and if we try to use it with null object it will throw and exception
```java
Optional<Foo> foo = Optional.of(new Foo());  // populated Optional
Optional<Foo> foo = Optional.of(null);      // throws NullPointerException
```
#### `ofNullable`
when pass non-null value it will work as `of` but when pass a null value it will not throw exception instead it will create an empty optional
```java
Optional<Foo> foo1 = Optional.ofNullable(new Foo());  // populated Optional
Optional<Foo> foo2 = Optional.ofNullable(null);       // empty Optional
```
#### `empty`
it creates an empty optional and is same as use `ofNullable` method with null, it also used when we know that no value needed 
```java
Optional<Foo> foo = Optional.empty();    // empty Optional
Optional<Foo> foo = Optional.ofNullable(null);
```
### Instance Methods
#### `isPresent` & `isEmpty`
those methods check if the optional is populated or its empty, they are the reverse of the other
```java
Optional<Foo> populated = // ...populated Optional...
populated.isPresent();    // true
populated.isEmpty();      // false
```
#### `get`
it gets the type of the optional, if we have `Optional<X>` it gives us the X itself or throw `NoSuchElementException` if the optional is empty 
in practice it better to use this one after checking if the optional is present or empty
```java
Optional<Foo> possibleFoo = doSomething();
if (possibleFoo.isPresent()) {
    Foo foo = possibleFoo.get();
    // ...use the foo object...
}
else {
    // ...handle case of missing Foo...
}
```
this pattern return us to the problem if try and catch for null so it's better to use `orElse` or `orElseThrow` instead of `get` 
#### `orElse` Family
it used when we can have an empty value for the optional so we can add a default value in this case 
but in most cases this cause a bad performance as it will create the default value even if we didn't need it, so the optional class introduced `orElseGet` method which take a Supplier, and it will only create the default value when we need it so it will solve the performance problem
```java
Optional<Foo> possibleFoo = doSomething();
Foo foo = possibleFoo
	.orElse(new Foo());
Foo foo = possibleFoo
    .orElseGet(() -> { /* ...lazily create a Foo object... */ });
```
#### `orElseThrow` Family
its like `orElse` but in this case it used to throw an exception when the optional in empty, and its better to use over `get` 
it can have two forms, first one is `orElseThrow()` and this will throw an `NoSuchElementException` by default, the other one take a parameter of custom exception you want to throw 
```java
Optional<Foo> possibleFoo = doSomething();
Foo foo = possibleFoo
	.orElseThrow();
Foo foo = possibleFoo
    .orElseThrow(() -> { /* ...lazily create a Foo object... */ });
```
#### `ifPresent` Family
it will make some action if the optional is populated only, also there is another one called `ifPresentOrElse` which takes two parameters, first one will be done if the optional is populated and the other one will done if the optional is empty
```java
Optional<Foo> possibleFoo=doSomething();
possibleFoo.ifPresent();
possibleFoo.ifPresentOrElse();
```
#### `map`
map is used when we are trying to convert from one form to another in some cases, like if we have an DTO, and we want to create the object from it, we can use map and add for it a function 
```java
public class Person {
    private String firstName;
    private String lastName;
    // ...getters & setters...
}
public class PersonDto {
    private String name;
    // ...getters & setters...
}
public class PersonMapper {
    public Person fromDto(PersonDto dto) {
        String[] names = dto.getName().split("\\s+");
        Person person = new Person();
        person.setFirstName(names[0]);
        person.setLastName(names[1]);
        return person;
    }
}
public class Database {
    public Optional<PersonDto> findPerson() {
        // ...return populated DTO if DTO is found...
    }
}
Database db = new Database();
PersonMapper mapper = new PersonMapper();
Optional<Person> person = db.findPerson()
    .map(mapper::fromDto);
```
there is a case as the map return a value, and it can return a null, and it will handle it and make it empty optional, but this is not best practice, the best practice is use `flatmap` 
#### `flatMap`
this is same as map, but it now makes it your responsibility to return optional not value and auto convert to optional, so now if you want to return a person it must return as optional of person, and now you can't return null, you must return empty optional and if you return null it will throw `NPE` 
```java
Optional<Person> person = db.findPerson()
    .flatMap(dto -> {
        if (dtoCanBeConverted()) {
            Person person = return dao.fromDto(dto);
            return Optional.ofNullable(person);
        }
        else {
            return Optional.empty();
        }
    });
```
#### `filter`
we only return the optionals that satisfied some conditions 
```java
public class Bar {
    private int number;
    public Bar(int number) {
        this.number = number;
    }
    // ...getters & setters...
}
Predicate<Bar> greaterThanZero = bar -> bar.getNumber() > 0;

Optional.of(new Bar(1))
    .filter(greaterThanZero)
    .isPresent();              // true
Optional.of(new Bar(-1))
    .filter(greaterThanZero)
    .isPresent();              // false
```
#### `stream`
you can transform the optional to a stream to work with it as usual streams
```java
Set<Person> people = findPerson().stream()
    .filter(/* ... */)
    .map(/* ... */)
    .flatMap(/* ... */)
    .collect(Collectors.toSet());
```
## When and When Not To Use
### Return Values
it the case where the optional is created for, and it's the most case we use optional in, like when working with db and queries the queries will return optional as there is a case where we don't have value in db
1. It is expected that a value may or may not be present
2. It is not an error if a value is missing
3. The client is responsible for handling the case of a missing value
### Fields
not recommended using in fields in classes as optional is not serializable, but the most used technique is to make the getter return optional 
```java
public class Bar {
    private Foo foo;
    public Optional<Foo> getFoo() {
        return Optional.ofNullable(foo);
    }
}
```
### Parameters
don't use it with parameters, but instead you can use method overloading to allow all cases when the object is populated or its empty
## Alternatives
### `null`
it's the problem from the first but in some cases use null is easier of optional and the overhead of handle optional is large, but in most cases, use optional as returned value from methods 
### Null Object
make an object that inherit from the real object but override it to be null case and return new one if it when it comes to null case 
### Exceptions
the easier one and straightforward is to throw exception when the value is missing 
# Source
[Optionals for Justin Albano](https://dzone.com/articles/optional-in-java) 