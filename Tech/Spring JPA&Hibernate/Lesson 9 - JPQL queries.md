# Explanation
## Basic Query
in the queries in JPQL, you query with Objects or Entities not the tables in DB

there are two types of basic quires
> can't use insert in the queries, it only allowed with Entity Manager
### One Parameter
this one take only the query and return a `Query` and you must map it to what you want
### Two Parameters 
this one takes two parameters, the query itself and the class of what you query of, and it will do the mapping by itself and return `TypedQuery<T>` 
### Query with custom values as parameters
you can add your custom values in the query by use `:name` in values places and then pass this values to the query
```java
String q="Select p from Product p where p.name = :name";
q.setParaeter("name",5);
```
# Source
[Lesson 9 - JPQL queries](https://www.youtube.com/live/kyAH-75goaY?si=YxHFaje8B-HvZWtA) 