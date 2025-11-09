# Explanation
## Calling REST endpoints using Spring Cloud OpenFeign
this is the most modern approach in spring to call an external API in your backend app
to start use it you need to add it first in `pom.xml` and as this is part of spring cloud project we will use it from cloud starter
```java
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```
after that you can now create the interface, its like JPA repository style, you just extend some interface and spring will handle everything, in this way, to use OpenFeign you just need to add annotation above your interface which is `@FeignClient` and add to it the name and URL or endpoint you want to call
> one note here, try to make your endpoints URL global in app properties or anything and don't hard code it every time

now the class will look like
```java
@FeignClient(name = "payments", url = "${name.service.url}")
public interface PaymentsProxy {

	@PostMapping("/payment")
	Payment createPayment(
		@RequestHeader String requestId,
		@RequestBody Payment payment);
}
```
after that, you just need to enable the Feign Clients so in your config class, add `@EnableFeignClients` and you can add to it the base packages' path to search and scan
## Calling REST endpoints using RestTemplate
The RestTemplate is the old way before OpenFeign to fetch API in your backend app, it's in his way to be deprecated as its old and now better way come in, but it still used in projects and also still used in new projects as no limit to not use it
so to fetch an API with it, you need to make some steps:
- first you need object of `RestTemplate` 
- after that you need to initialize the URL you will call 
- then create the `HttpHeaders` you will add in the request
- after that you need to create an `HttpEntity` with the object you will have and the headers you created like `HttpEntity<Payment> httpEntity = new HttpEntity<>(payment, headers);` 
- after that you can call with `exchange` method from `RestTemplate`
```java
@Component
public class PaymentsProxy {
    private final RestTemplate rest;
    
    @Value("${name.service.url}")
    private String paymentsServiceUrl;
    
    public PaymentsProxy(RestTemplate rest) {
        this.rest = rest;
    }
    
    public Payment createPayment(Payment payment) {
        String uri = paymentsServiceUrl + "/payment";
        
        HttpHeaders headers = new HttpHeaders();
        headers.add("requestId", UUID.randomUUID().toString());
        
        HttpEntity<Payment> httpEntity = new HttpEntity<>(payment, headers);
        
        ResponseEntity<Payment> response = rest.exchange(
            uri,
            HttpMethod.POST,
            httpEntity,
            Payment.class
        );
        
        return response.getBody();
    }
}
```
```java
@RestController
public class PaymentsController {
    private final PaymentsProxy paymentsProxy;
    
    public PaymentsController(PaymentsProxy paymentsProxy) {
        this.paymentsProxy = paymentsProxy;
    }
    
    @PostMapping("/payment")
    public Payment createPayment(@RequestBody Payment payment) {
        return paymentsProxy.createPayment(payment);
    }
}
```
## Calling REST endpoints using WebClient
this approach is designed for the reactive programs, reactive programs are programs that work with tasks not flow, in other words, the tasks tell the program what is the dependencies it needs to finish, and each task keep tell the program its dependencies, after all programs finish write its dependencies, the program sees which tasks that are free now and don't wait any other dependencies, and start it and after finish it scans again to see if there are new tasks that can start, and keep making this until finish all tasks, in this approach, threads used to make many tasks and don't go idle when it blocked for another task to finish 
so if you use reactive programming, WebClient are the choice you can use, otherwise you can use OpenFeign
okay let's start see how we can implement the proxy with WebClient
we need to add dependency to our project
```java
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-webflux</artifactId>
</dependency>
```
after that you need a bean of type WebClient so you can do it in any way you want, easier one is to add a bean of it in any config file 
after that you can make your proxy and consume the API
```java
@Component
public class PaymentsProxy {
    private final WebClient webClient;
    
    @Value("${name.service.url}")
    private String url;
    
    public PaymentsProxy(WebClient webClient) {
        this.webClient = webClient;
    }
    
    public Mono<Payment> createPayment(String requestId, Payment payment) {
        return webClient.post()
            .uri(url + "/payment")
            .header("requestId", requestId)
            .body(Mono.just(payment), Payment.class)
            .retrieve()
            .bodyToMono(Payment.class);
    }
}
```
after that you can inject it in your controller and work with it
```java
@RestController
public class PaymentsController {
    private final PaymentsProxy paymentsProxy;
    
    public PaymentsController(PaymentsProxy paymentsProxy) {
        this.paymentsProxy = paymentsProxy;
    }
    
    @PostMapping("/payment")
    public Mono<Payment> createPayment(@RequestBody Payment payment) {
        String requestId = UUID.randomUUID().toString();
        return paymentsProxy.createPayment(requestId, payment);
    }
}
```

## Summary
In a real-world backend solution, you often find cases when a backend app needs to call endpoints exposed by another backend app.

Spring offers multiple solutions for implementing the client side of a REST service. Three of the most relevant solutions are as follows:

- **OpenFeign** — A solution offered by the Spring Cloud project that successfully simplifies the code you need to write to call a REST endpoint and adds several features relevant to how we implement services today
- **RestTemplate** — A simple tool used to call REST endpoints in Spring apps
- **WebClient** — A reactive solution for calling REST endpoints in a Spring app

You shouldn't use RestTemplate in new implementations. You can choose between OpenFeign and WebClient to call REST endpoints.

For an app following a standard (nonreactive) approach, the best choice is using OpenFeign.

WebClient is an excellent tool for an app designed on a reactive approach. But before using it, you should deeply understand the reactive approach and how to implement a reactive app with Spring.

# Source
[[B- Spring Start Here.pdf]] 