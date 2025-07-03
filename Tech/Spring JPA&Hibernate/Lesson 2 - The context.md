# Explanation 
#### The context
collection of instances of entities which we work with
the name of table in the context is the name with `Entity(name='')` 

#### Annotation for Entities 
##### Entity
to mark this class as Entity
##### Table
to assign which table in database that class represent
##### Id
to mark which attribute represent the ID of the table and each table must have an ID
##### Column 'Best Practice is not to use'
to assign for each attribute the column in database which it represents

#### Entity Manager 
- Find
	- find data from the context with ID or from database
- persist
	- save to context **new one**
- Update
	- There is a save method but no need to use as in the end of the transaction it will automatically save
- Remove
	- remove the user from the context and by the end from the database
- merge
	- merge entity to the context if the entity is already in the context
- refresh
	- mirror the context from database
- detach
	- remove from the context
# Sources
[JPA/Hibernate Fundamentals 2023 - Lesson 2 - The context](https://www.youtube.com/watch?v=BkhGRpozJ5Y&list=PLEocw3gLFc8UYNv0uRG399GSggi8icTL6&index=2&pp=iAQB) 