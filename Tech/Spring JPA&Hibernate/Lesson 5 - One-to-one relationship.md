# Explanation
## Types of relationships
- one way: which is one entity know about the other, but the other doesn't know anything about the first one, it's like you have `passportId` in person and don't have anything related to person in passport
- bidirectional way: each entity have info about the other
## One To One
It's when one entity have only one instance of other entity and the reverse
### Create a one-to-one relation
to create the relation
- if it's one way you create attribute in one entity of other type and then mark it with `OneToOne` annotation 
- also you can change name of it with `JoinColumn` and write your name
- if you create from both, in the second entity when use `OneToOne` annotation you need to add `mappedby` and add the field name which is written with `JoinColumn` 
### Cascading
is way that you make one entity have same operations as other entity that have a relation with
this one add-in `OneToOne` annotation with `cascade` and choose what you want.
> Don't Overuse it
### Secondary Table
when we have two tables, but there is no relation between them, but the other one contain data for the first one, so the second one is just some info about the first but normalized to be two tables
> This can replace DTO

# Sources
[JPA/Hibernate Fundamentals 2023 - Lesson 5 - One-to-one relationship](https://www.youtube.com/live/FabE0xjjqd4?si=BdjpPqP41QPnVHyT) 