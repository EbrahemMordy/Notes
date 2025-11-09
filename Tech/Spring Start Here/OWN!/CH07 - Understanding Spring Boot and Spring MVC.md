# Explanation
## What is Web Apps
web app is composed of server side and client side
the client side is side that user see and interact with, in other words this is what shown in browser, the front end in web dev 
the server side is the side that receive the request and handle what is want and logic and business code, the back end in web dev
### Ways to implement Web Apps
the two ways to implement is:
- backend app return the data formatted and ready to shown in the browser 
- backend app that return raw data and wait for front end to format it and display it
### Using Servlet Container In web apps 
Servlet container is a translator of HTTP for java app, one of famous apps in it is Tomcat
it's a layer before our backend project, it receives the request and translate it then pass it to spring project to process then receive the response and return it to the browser or frontend  
## The Magic of Spring Boot
those days spring boot is the way to remove the configuration of servlet container and only focus on the business code and logic  
the features it gives:
- simplified project creation as you can get the run able project in few seconds
- dependency starter, you can easily start with things you need without care about the versions
- default configuration based on dependency you choose
### Using Project Initialization service to create a spring boot project 
you can use [Spring Initializr](https://start.spring.io/) to start your project and choose dependency you need to use, and it will create the files you need as `pom.xml` or `application.properties` and so on
### Using Dependency Starters to simplify the dependency management 
this way, or spring starter group is a way to make it easy to add the dependency you need to start a project with something like web or security or JPA and so on, this one group the dependencies you need in only one dependency so you include it only
### Using Auto configuration by convention based on dependencies 
based on the dependencies you added the spring will understand and if you run the project without make anything other than download the project, it will start and can access it
## Implementing a web app with Spring MVC
after you initialize the project that doesn't mean that this is a web app, you need to add a page and URL to access this page
to start add pages:
- add an HTML file in `resources/static` and fill it with what you want to be shown in the browser
- after that you need to add and API or endpoint that can be accessed from the browser and shown the response of it
now what is the flow of the call from the start until the end:
- client make an HTTP request via browser or Post man or any other method
- Tomcat get this request and call `Dispatcher Servlet` which is servlet component
- Dispatcher Servlet is the main gate in spring app, any request must first reach it, and it works as router to route each request to its controller to process it and return the response to it to also send it to the method that call it from the first
- when Dispatcher Servlet have a request, it searches in the `handler mapping` to find the controller that have this request associated to it
- after it find the controller it calls the action or method that represent this API 
- after that it receive the HTML page name or the View
- then it finds what is that view with `View Resolver` and return it's content as rendered HTML
# Source
[[B- Spring Start Here.pdf]] 