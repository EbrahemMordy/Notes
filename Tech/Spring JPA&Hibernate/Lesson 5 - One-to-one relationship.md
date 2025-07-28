# Explanation
## Types of relationships
- one way: which is one entity know about the other, but the other doesn't know anything about the first one, it's like you have `passportId` in person and don't have anything related to person in passport
- bidirectional way: each entity have info about the other
## One To One
It's when one entity have only one instance of other entity and the reverse
### Create a one-to-one relation
to create the relation
- **One directional**
- you add an instance of the other entity and mark it with `OneToOne` annotation 
- if you want to change the name of its column you can change it with `JoinColumn` and write your own name, the default is `name_id` 
---
- **Bidirectional**
- same things as one directional but in the second entity we add instance of the other entity and use the `mappedBy` and add the name of attribute marked with `JoinColumn` 
### Cascading
is way that you make one entity have same operations as other entity that have a relation with
this one add-in `OneToOne` annotation with `cascade` and choose what you want.
> Don't Overuse it
### Secondary Table
when we have two tables, but there is no relation between them, but the other one contain data for the first one, so the second one is just some info about the first but normalized to be two tables
```java
@SecondryTable(
	name="name"
	pkJoinColumns=@PrimaryKeyJoinColumn(name="id")
	//you can make it composed key
)
.
.
.
// then mark your filed with @Column and use "table = name" 
```
> This can replace DTO

# Source
[JPA/Hibernate Fundamentals 2023 - Lesson 5 - One-to-one relationship](https://www.youtube.com/live/FabE0xjjqd4?si=BdjpPqP41QPnVHyT) 