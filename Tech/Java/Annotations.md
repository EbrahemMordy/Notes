# Explanation
## what is java annotations
Annotation used to provide metadata for the java code in the runtime, and it doesn't affect the execution 
## uses of java annotations
annotation used in multi cases:
- Compiler instructions
- Build-time instructions
- Runtime instructions
## Accessing Java Annotations via Java Reflection
Java annotations are not available after the build and compilation, however we can access it using [Java Reflection](https://jenkov.com/tutorials/java-reflection/index.html) in runtime
## Annotation Basics
Annotation looks like `@Name` where `@` tell compiler that this is an annotation and `Name` is the name of this annotation 
### Annotations Elements
annotation can have parameters in it, and you can assign values to it like `@Entity(tableName = "vehicles")` and you can add more than one parameter and separate them by `,` 
## Annotation Placement
annotation can place in anywhere above classes, interfaces, methods, fields or local variables 
## Creating Your Own Java Annotations
to create your own annotation 
```java
@interface Test{
	String name();
	int age();
}
```
to specify your annotation to be available in runtime you can add `@Rentention` and make it with `@Rentention(RetentionPolicy.RUNTIME)` 
to mark your annotation to work with only some specific targets you use `@Target()` above annotation declaration and add what you want with `@Target({ElementType.METHOD})` 
`@Inherited` mean that if the super class have this annotation, any subclass will inherit from it will inherit this annotation too
to make your annotation visible in Javadoc you add this `@Documented` 
# Source
[Jenkov Blog](https://jenkov.com/tutorials/java/annotations.html) 