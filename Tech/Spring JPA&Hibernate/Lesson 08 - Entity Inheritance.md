# Explanation 
when an entity inherit from another entity 
## Inheritance Strategy 
if you have a class that will be a parent for another classes or entities, you mark it with `Inheritance` annotation and choose the strategy you want
> if you will not query the parent, you can mark it as `MappedSuperClass` 
### Joined **Most Used** 
each class will have his own table and the queries use joins to get answers
### Table Per Class
create only tables for Children's, but for each child it will contain all attributes even inherited ones, so it will duplicate all columns for each table
> It uses union when you query on the parent, JPQL doesn't support it
### Single Table
only create one table and have discriminator column that tell you this what is the type of this row
> you don't need to add this column in your query, JPA will auto select type you want
## Creation of parent entity
you start by creating an entity and add in it all fields that you want to make it in children's, and also you can mark it as *`abstract`* as you can make it not available to create an object of it
after that you make each entity extend from the parent 
# Source
[Lesson 8 - Entity Inheritance](https://www.youtube.com/live/KK2XErh1Dr0?si=hsSDL9F9zHqxR-1X) 
