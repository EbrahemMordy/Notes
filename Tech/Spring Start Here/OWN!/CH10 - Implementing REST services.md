# Explanation
## Using REST services to exchange data between apps
Rest Endpoints are like MVC, but now we don't return a viewer, we return just the data of the action in JSON response or any type without search for the viewer
the problem with Rest APIs is that you can not send large data to it as you have only few megabytes to send with it, also if the call takes long time it will time out and fail, also it depends on network and network can fall in anytime so there always a chance that the fail reasons is the network
## implementing a REST endpoint
instead of annotate the class with @Controller we will use @RestController as this will mark the API to be Rest and return response body not viewer 
## Managing the HTTP response
### Sending objects as a response body
in any API you can adjust it to return object not just string or integer, you can make object or class such like Country and return it in the API, the returned object called DTO which is data transfer object, also the default and most used format for responses in APIs are JSON, but you can still return any format you want but the most used is JSON
### Setting the response status and headers
the status of requests are something like:
-  200 OK if no exception was thrown on the server side while processing the request.
- 404 Not Found if the requested resource doesn’t exist.
- 400 Bad Request if a part of the request could not be matched with the way the server expected the data.
- 500 Error on server if an exception was thrown on the server side for any reason while processing the request. Usually, for this kind of exception, the client can’t do anything, and it’s expected someone should solve the problem on the backend.

If we want to edit the response headers in the API we can use the response body class, which spring provides to us so we can add to it what we want
```java
return ResponseEntity
.status(HttpStatus.ACCEPTED)
.header("continent", "Europe")
.header("capital", "Paris")
.header("favorite_food", "cheese and wine")
.body(c);
```
### Managing exceptions at the endpoint level 
#### Basic Try And Catch
The first way to make catch exceptions is in the controller you use `try{}catch()` and if the service throws the exception, and you caught it you return a Response Body and make it bad request and return a class of the error you want, you can create the exception and name it what you want and u must make it extend runtime exception
after that you can return this class direct in the response body, or you can override and take the message from it and add it in another class as you want
```java
@PostMapping("/payment")
public ResponseEntity<?> makePayment() {
	try {
		PaymentDetails paymentDetails =
		paymentService.processPayment();
		return ResponseEntity
			.status(HttpStatus.ACCEPTED)
			.body(paymentDetails);
	}catch (NotEnoughMoneyException e) {
		ErrorDetails errorDetails = new ErrorDetails();
		errorDetails.setMessage("Not enough money to make the payment.");
		return ResponseEntity
			.badRequest()
			.body(errorDetails);
	}
}
```
#### Exception Controller Advice
instead of adding logic in the controller to tell him for every case when service throws an exception what to do
we only treat happy case in the controller and add a new layer or service that will only work when the service throws exception, in this case it will catch it
to make it we create a class and annotate it with `@RestControllerAdvice` annotation, and it will treat as bean and inject automatic when project runs
now in this class if we want to handle case when exception of type X thrown we will add a function that annotated with `@ExceptionHandler(X.Class)` and in this function we treat it as we make in controller
```java
@ExceptionHandler(NotEnoughMoneyException.class)
public ResponseEntity<ErrorDetails> exceptionNotEnoughMoneyHandler() {
	ErrorDetails errorDetails = new ErrorDetails();
	errorDetails.setMessage("Not enough money to make the payment.");
	return ResponseEntity
		.badRequest()
		.body(errorDetails);
	}
}
```
> In production apps, you sometimes need to send information about the exception that occurred, from the controller’s action to the advice. In this case, you can add a parameter to the advice’s exception handler method of the type of the handled exception. Spring is smart enough to pass the exception reference from the controller to the advice’s exception handler method. You can then use any details of the exception instance in the advice’s logic.

In short, if you want to print the message returned to the exception you can add parameter of its type, and it will inject it directly in the function  
## Using a request body to get data from the client
when we want to send large data to the endpoint like details about person want to register we can make it with request parameter, but we will add too many, but we can use `@RequestBody` which will take it in only one object, by default JSON is the default format for spring, so by default spring will take the object and try to cast it to your entity or DTO and if failed it will return an error to the call 
```java
@PostMapping("/payment")
public ResponseEntity<PaymentDetails> makePayment(@RequestBody PaymentDetails paymentDetails)
```
# Source
[[B- Spring Start Here.pdf]] 