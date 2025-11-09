# Explanation
## Server Side Components
is a way that use OOP to built software pieces that can run independent and combined with other like Lego pieces to build the business logic we want in our software 
## Persistence and Entity Beans
before EJB 3.0 the older version are hard to map objects in java to tables in databases, but in 3.0 they use ORM and JPA to allow them to mapping entities which is java objects that are mapped to tables in database and also can add relations between them as objects in java with same relations in database
## Asynchronous Messaging
systems need to send messages between components in it in a way that make it so easy, in the synchronous messaging system you can send your message in a channel that called detestation and any component are interested and follow this channel will receive this message and also can send messages in it to

it uses message-oriented middleware (MOM) to send messages as it allow them to have a lot of features as fault-tolerance, load-balancing, scalability, and transactional support

MOM have two components are used Java Message Service (JMS) and message-driven
### Java Message Service **JMS** 
is an API that allow you to do what you want without care about what MOM vendor you use
### Message-Driven Beans and JCA 1.5
message-driven bean is a bean of JMS, it sends JMS messages and can interact with any EJB 
with the new Java Connector Architecture 1.5, EJB can work with any message-driven bean
## Web Services
it's a way to make a system that use a lot of service and each one can be written by any programming language, and they can interact with each other using a standard protocols like SOAP and WSDL 
# Source
[Chapter 1 in Enterprise Java Beans 3.0 5th Ed 2006](https://www.scribd.com/doc/136500914/Enterprise-JavaBeans-3-0-5th-Ed-2006) 