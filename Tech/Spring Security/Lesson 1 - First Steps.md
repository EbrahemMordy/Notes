# Explanation 

![[Pasted image 20250519065133.png]]

>App Level Security have two main things Authentication and authorization 
#### Authentication
it's the step of check who are the user that try to access the app
#### Authorization
it's the step which check if you are valid to do this action or now allowed for your role 
#### Roles
it represents who are you in the app
#### Authority
it's something you have in the app like read write
#### Different Between Things
- Encoding
	- reverse able function any time without any keys
- Encrypt
	- when you have the output and want to get the input you need a **secret key** to get the correct input 
- Hash Functions
	- you can never get from the output to the input as it's random key
	- and always same input give us the same output anytime we try it
#### HTTP Basic Authentication
it's the basic one and the one used when you add security to your app and don't add any security 
#### User Details Service 
it's the component that mange user details in the app 
##### How to create it
- create a class and name it whatever you want
- mark it with annotation `Configuration` 
- add bean of type `UserDetailsService` 
- if you don't have DB you can use `InMemoryUserDetailsManager` 
- create a `UserDetails` with `User.withUsername()` and add all you want to have in it then `build`
- after that use manager to create this user `createUser(user)` 
- add bean of type `PasswordEncoder` and return an instance of any password encoder
# Sources
[Spring Security Fundamentals - Lesson 1 - First steps](https://www.youtube.com/watch?v=nSu9ElsnNtY&list=PLEocw3gLFc8X_a8hGWGaBnSkPFJmbb8QP&index=1&t=1s&pp=iAQB "Spring Security Fundamentals - Lesson 1 - First steps") 
