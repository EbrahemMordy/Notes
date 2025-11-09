# Explanation 
spring have more than 2 bean scopes, it has singleton and prototype, but it also has request, session and application scopes
## Using the request scope in a Spring web app
in this scope spring create new instance of the entity or class as service or anything per request, so each request has his own beans that serve him alone
to mark a component to request scope you can use `@RequestScope` above it
## Using the session scope in a Spring web app 
spring will create one instance to the whole session, so every time you send request in the same session, it will assign to you the same instances used in last request of this session 
it can use in a lot of cases like *login* or *cart* in shopping app 
to use you only need to mark the component as `@SessionScope` 
## Using the application scope in a Spring web app 
it only one instance per the application, you can't create new instance of this class, it's like singleton but with only one instance of same type
to make a bean of it you only need to mark it with `@ApplicationScope` 
# Source
[[B- Spring Start Here.pdf]] 