# Chapter 9: Using Spring Web Scopes

## What are web scopes:

- In chapter 5 we talked about bean scopes.
- For beans working in web applications, there are scopes (ways of managing a bean's life cycle) that are defines **relative to HTTP requests**

## Request Scope

- Request scoped beans are created for each individual HTTP request recieved, and spring can only use the instance for the request for which it was created for

- request scoped should not contain logic that needs alot of time in its constructor because many instances are created in the app.

- This type of scope is good for holding data that you don't want laying around (credentials) or to hold data that you don't want race conditions on without sychornization methods

- Request scoped beans are declared with the `@RequestScope` annoation
```java
    @Component 
    @RequestScope 
    public class RequestScopedBean{
        ...
    }
```

## Session scope

- A session scoped bean is instatiated for each HTTP session connected to the server

- Each session scoped bean is associated with a single session

- If multiple sessions are active, Spring handles injecting the correct session scoped bean depending on what session the request belongs to (it will inject the bean associted with the session to which the request belongs)

- Session scoped beans could be used to store session dependant state such as the current' user's username

- even if it's the same client, a client can send multiple concurrent HTTP requests and so synchronization should be implemented in a session scoped bean to avoid race conditions

- session scoped beans are declared with the `@SessionScope` annoation
```java
    @Component 
    @SessionScope 
    public class RequestScopedBean{
        ...
    }
```

## Application Scope

- An application scope bean is shared by all client requests

- It is simillar to a singlton bean; however, there cannot be more that one instance of the same type

- Immutabale data should be used or else synchornization should be implemented to avoid race conditions

- Application scoped beans should not be used in production and instead a presistance layer should be used

- Application scoped beans are declared with the `@ApplicationScope` annoation
```java
    @Component 
    @SessionScope 
    public class RequestScopedBean{
        ...
    }
```

## Handling Different Scopes

- A question may arise, how can a request scoped bean be injected into a longer lived bean such as a sesison scoped bean

- if the session scoped bean is only created per session and multiple requests of the same session are sent, this means that the same request scoped bean is used because is has only been injected once right? well this is wrong

- In such cases, spring injects a proxy object. The proxy object is indeed injected once, but each time a method in the proxy is called, it will crate a new instance of the request scoped object and delegate the work to it.

- This proxying mechanism is used for any bean that depends on a shorter lived bean getting injected into it.

*note: both session and application scoped beans cause the request to be denpendant on each other and thus the application needs to manage their state and make sure it is valid and correct. This stateful nature needs to be put into consideration when developing the app and so finding stateless alternatives may be a better course of action that one should think off*