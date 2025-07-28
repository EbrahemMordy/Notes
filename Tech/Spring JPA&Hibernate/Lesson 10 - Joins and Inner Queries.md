# Explanation
you can write the joins as you would do in the SQL itself, but in this you use the entities itself for writing it

also beware of this can generate **N+1 problem** as this can happen if you have relations in your entities 
```java
String q="""
	Select s,e From Student s, Employement e where s.id=e.student.id
	"""
```
## Projection in Queries 
if you want to select more than one entity like `s,e` you can make an **DTO** with those entities and return it 
```java
String q="""
	Select new ES(s,e) From Student s, Employement e where s.id=e.student.id
	"""
```
in this case i used record and pass it the entities i want to be added in it, in same way we can use it as classes
## Sub Queries 
it same style as normal SQL
```java
String q="""
	Select s From Student s where (
	SELECT COUNT(e) from Employement e where s.id=e.student.id
	) > 2
	"""
```

# Source
[Lesson 10 - Joins and Inner Queries](https://www.youtube.com/live/kjx0CxJzmmM?si=Z3-7Tk3rFRESd_E6) 