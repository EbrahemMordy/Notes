# Explanation 
## Group by
it same as in SQL but same thing you write it with entities itself not the tables in the db
```java
String q="""
	Select s,e From Student s, Employement e where s.id=e.student.id 
	Group By s.name
	"""
```
## Having
it same as where but the key diff between them is that when they filter the data
```java
String q="""
	Select s,e From Student s, Employement e where s.id=e.student.id 
	Group By s.name
	HAVING s.name LIKE "%e%"
	"""
```
## Order By
```java
String q="""
	Select s,e From Student s, Employement e where s.id=e.student.id 
	Group By s.name
	HAVING s.name LIKE "%e%"
	ORDER BY s.name DESC
	"""
```
## Named Queries 
you add `@NamedQueries` above your entities and add `@NamedQuery` as many you want and add for it `name` and add `query` itself 
```java
@NamedQueries(
	@NamedQuery(
		name="",
		query="""
			Select s from Student s
		"""
	)
)
```
# Source
[Lesson 11 - Group By, Order By, Having](https://www.youtube.com/live/6J6Uy0ckWAQ?si=ZmqfYNFI1Esv4OZX) 