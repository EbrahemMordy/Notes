# Explanation
It's when you write native quires in SQL and want to run it in the spring or backend side
> don't use it, only use it when you must use it
## How to write native query
- use entity manager to create it with `em.createNativeQuery()` 
- you can store it as only `Query` not `TypedQuery` 
- you can run it when you want
## Avoid Native Query
### Views
to avoid the native query in your project, you can use **Views** and make it as entities and use it in your JPQL and remove the native parts you need to use
#### How to use
- split the large query and try to make it with view 
- use view as an entity, make sure you only add **Get** as views can not edited 
- use the view with JPQL as you use entities in usual 
### Procedure Query
It's something in databases, and you can easily use it, i will check it after learn more about **Procedure** 
# Source
[Lesson 12 - Native queries](https://www.youtube.com/live/6my6f6JN64A?si=I3OC6RPln5TAu9KQ) 