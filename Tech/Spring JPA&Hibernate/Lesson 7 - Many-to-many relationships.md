# Explanation
when multi users have multi groups this is many-to-many relationship
## How to create Many-To-Many relationship 
- create the entities based on the tables that are in db and add `Table` Annotation if table names are different
---
- **One Way Relation**
- you add List of the other entity and add `ManyToMany` and also `JoinTable` 
---
- **Two Way Relation**
- you add List of the other entity in two entities
- in one entity add `JoinTable` and in the other add `mappedBy` 

# Sources
[Lesson 7 - Many-to-many relationships](https://www.youtube.com/live/zHKoGludC20?si=ihh9jRyJyoGOBVr8) 