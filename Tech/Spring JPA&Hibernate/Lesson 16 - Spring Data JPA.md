# Explanation
 is an upper layer above hibernate, it removes unnecessary codes and makes it abstract 
## How to Use
- create an interface and make it extend from `JpaRepository` or `Repository` and add for it the class name and the ID type
- if you want, you can add the query above it if you have a custom query, add `@Query""""""` and add the query itself 
- if query can return null, use `Optional` 
# Source
[Lesson 16 - Spring Data JPA](https://www.youtube.com/live/X7ebBOz7h_s?si=N13DXvNLmREvWx2f) 