# Explanation

#### Create Users
- create DB table
- create config file and add `PasswordEncoder` bean
- create user entity
- create `SecurityUser` that implement `UserDetails` and inject a user into it and also override the methods 
- create a user repository and make a find by username query
- create a service that implement `UserDetailsService` and add bean to context with annotation or with bean in config
- inject user repository into `UserDetailsService` 
- find the user by username into override method
- map the `User` to become `UserDetails` or throw error 
#### Create Authorities 
it may be 
- Roles it's a badge which represent who are u
- Authorities it's an action that user can do 

how to make
- create a table in db for authorities
- create authorities entity
- create a join table between users and authorities
- create relationship between them
- create class which implement `GrantedAuth` and override the method
- override method `getAuthorities` in `SecurityUser` to return the authorities as list
# Sources
[Spring Security Fundamentals - Lesson 2 - Managing users](https://www.youtube.com/watch?v=dFvbHZ8CuKM&list=PLEocw3gLFc8X_a8hGWGaBnSkPFJmbb8QP&index=2&pp=iAQB "Spring Security Fundamentals - Lesson 2 - Managing users") 
