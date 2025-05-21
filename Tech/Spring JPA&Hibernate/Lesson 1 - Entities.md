# Explanation 

#### What is ORM
Object Relational Mapping, it's the relations between tables in database
#### What is JPA
Jakarta persistence API, it's just a specification on how to implement ORM
#### What is Hibernate 
it's just the implementation for JPA
#### What is JDBC
it's the first way to deal with databases and tables in java
#### how to connect to db with XML
- create folder called META-INF in resources
- create file called persistence.xml in it
- get the content from any documentation 
#### Entity Manager 
it represents the context and allows us to start transaction and commit it and also apply the queries to database
##### how to get entity manager
- get `EntityManagerFactory` 
	- if you use XML use `Presistence.CreateEntityManager(name)` 
#### Entities 
entity it's just a java class that represent the table in database to become java entity to manage and work with
##### how to create entity
- create a class with same name as database table
- mark this class with annotation called `Entity` so java can know that this class represent entity from database
- add each column from table to become attribute in java class
- it's best practice to add `Column` for those attributes and also use `Id` annotation and any other annotations if there.

> Persist is not an insert, it's just adding this query to context and JPA will treat it and maybe end with insert
#### how to connect to db programmatic 
- make a class and implement `PresistenceUnitInfo` 
- override all methods in it
- complete only some methods u will use 
- add data source
	- use `HikariCP` data source
	- add JDBC URL and username and password






# Source
[JPA/Hibernate Fundamentals 2023 - Lesson 1 - Entities](https://www.youtube.com/watch?v=t6n1NwMM8a8&list=PLEocw3gLFc8UYNv0uRG399GSggi8icTL6&index=1&pp=iAQB "JPA/Hibernate Fundamentals 2023 - Lesson 1 - Entities")
