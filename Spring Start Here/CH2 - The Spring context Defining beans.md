## The context : 
also known as the application context in a Spring app, imagine the context as a place in the memory of your app in which we add all the object instances that we want the framework to manage.

## Using the @Bean annotation to add beans into the Spring context

![[Pasted image 20250425203759.png]]

> When you have multiple beans of the same kind in the Spring context, you can make one of them primary. You mark the bean you want to be primary using the @Primary annotation. A primary bean is the one Spring will choose if it has multiple options, and you don’t specify a name


## Using stereotype annotations to add beans to the Spring context

![[Pasted image 20250425204827.png]]

![[Pasted image 20250425205335.png]]

## Programmatically adding beans to the Spring context

![[Pasted image 20250425221834.png]]

![[Pasted image 20250425221941.png]]


## Summary
- The first thing you need to learn in Spring is adding object instances (which we call beans) to the Spring context. You can imagine the Spring context as a bucket in which you add the instances you expect Spring to be able to manage. Spring can see only the instances you add to its context.
- You can add beans to the Spring context in three ways: using the @Bean annotation, using stereotype annotations, and doing it programmatically. 
	- Using the @Bean annotation to add instances to the Spring context enables you to add any kind of object instance as bean , and even multiple instances of the same kind to the Spring context. From this point of view, this approach is more flexible than using stereotype annotations. Still, it requires you to write more code because you need to write a separate method in the configuration class for each independent instance added to the context.
	- Using stereotype annotations, you can create beans for only the application classes with a specific annotation (e.g., @Component). This configuration approach requires writing less code, which makes your configuration more comfortable to read. You’ll prefer this approach over the @Bean annotation for classes that you define and can annotate.
	- Using the registerBean() method enables you to implement custom logic for adding beans to the Spring context. Remember, you can use this approach only with Spring 5 and later

