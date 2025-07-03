# Explanation
## Custom ID Generator 
when you want to generate your own custom ID, you can create a custom generator and use it generated value annotation 
### How to create a custom generator
- create a class that implements `IdentifierGenerator` from hibernate
- override `generate` method to return your ID
- add `GeneriecGenerator` annotation
- also use generator 
## Composed Primary Keys
when your ID is not only one column 
> When use composed, don't forget to override hash and equals
### How to create composed key with Id Class
- create a class that implements `Seralizable` and add in it all columns that will be the PK
- in the entity itself mark it with `IdClass` and add the created class to it
- for each column that will be part in PK add `ID` annotation
### How to create composed key with Embeddable 
- create a class that implements `Seralizable` and add in it all columns that will be the PK and also mark this class as `Embeddable` with its annotation
- in the entity i use instance of this class as attribute and also mark it with `EmbeddedId` annotation 
# Sources
[JPA/Hibernate Fundamentals 2023 - Lesson 4 - Primary keys](https://www.youtube.com/watch?v=Tn72TkpxRWs&list=PLEocw3gLFc8UYNv0uRG399GSggi8icTL6&index=4&pp=iAQB) 