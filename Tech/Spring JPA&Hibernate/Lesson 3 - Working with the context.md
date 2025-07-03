# Explanation
## Entity manager properties
- `hibarnate.show_sql` 
- `hibarnate.hbd2ddl.auto` never ever use it in production 
	- `create` delete then create
	- `update` if not exist create it
	- `none` don't make anything, disabled
## Find Vs get Reference
the `getReference` initialize the connection between the database and java for this tuple or query and never run it until you try to use this tuple then the query will run first
## ID Generation 
in any entity you can use generated value for ID and there are two types of generated values first on is `strategy` the second one is custom generator 
### strategy types
- `AUTO` rely on defaults 
- `IDENTITY` allow DBMS to generate the ID for you, doesn't work with all DBMS every time check if it's allowed with your DBMS
- `SEQUENCE` good one with databases that allow sequences 
- `TABLE` create a sequence into DB and always make the ID based on the last one in this table, **Worst One** 
- `UUID` useful when the rows can be unlimited 
# Sources
[JPA/Hibernate Fundamentals 2023 - Lesson 3 - Working with the context](https://www.youtube.com/watch?v=eWjobgcuQFo&list=PLEocw3gLFc8UYNv0uRG399GSggi8icTL6&index=3&t=1s&pp=iAQB ) 