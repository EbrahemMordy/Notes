## The Entity Bean
Entity is an object, usual called POJO which represent real life model, like user, item etc…

Entities can be serialized and sent in the network
### How to implement an Entity 
-  Create a class and mark it with `@javax.presistence.Entity` 
- make a field and mark it with `@javax.presistence.Id` 
- make any field you want as in DB
```java
import javax.persistence.* ;

@Entity
@Table(name="CABIN")
public class Cabin {
    private int id;
    private String name;
    private int deckLevel;

    @Id
    @GeneratedValue
    @Column(name="CABIN_ID")
    public int getId( ) { return id; }

    public void setId(int pk) { this.id = pk; }

    @Column(name="CABIN_NAME")
    public String getName( ) { return name; }

    public void setName(String str) { this.name = str; }

    @Column(name="CABIN_DECK_LEVEL")
    public int getDeckLevel( ) { return deckLevel; }

    public void setDeckLevel(int level) { this.deckLevel = level; }
}
```
### How to interact with Entities 
You use `EntityMannager` which are responsible for any type of queries and operations with the entities
## The Enterprise Bean Component 
there are two types of beans in the server side 
### Session Beans
is responsible for managing the interactions with the Entities itself
### Message Driven Beans
is responsible for managing the messages sent to the system
### Classes and interfaces 
#### Remote Interface
it defines the methods that can be accessed from outside 
`@javax.ejb.Remote` 

```java
import javax.ejb.Remote;

@Remote
public interface CalculatorRemote {
    public int add(int x, int y);
    public int subtract(int x, int y);
}
```
#### Local Interface
it can access with same level of services like in spring
`@javax.ejb.Local` 
#### Endpoint Interface
it represents the APIs in the project which can be accessed from outside by SOAP
`@javax.ejb.WebService` 
#### Message Interface
it used to work with messages like JMS
`@javax.ejb.MessageDriven` 
#### Bean Class
it defines the business logic as functions that can be accessed with objects running in same level and same jvm
`@javax.ejb.Stateful`
`@javax.ejb.Stateless`
```java
import javax.ejb.*;

@Stateless
public class CalculatorBean implements CalculatorRemote {
    public int add(int x, int y) {
        return x + y;
    }
    public int subtract(int x, int y) {
        return x - y;
    }
}
```
### The EJB Container
```
Client Code
    ↓ (calls method)
Proxy Stub (implements interface)
    ↓ (routes call + handles networking)
EJB Container
    ↓ (applies security, transactions, lifecycle)
Bean Instance (your @Stateless/@Stateful class)
    ↓ (executes business logic)
Response flows back up the chain
```
#### Detailed Flow:
1. **Client** calls `calculator.add(2, 3)`
2. **Proxy Stub** intercepts the call
    - For remote: Serializes parameters, sends over network
    - For local: Routes within same JVM
3. **EJB Container** receives the call and:
    - Checks security permissions
    - Starts transaction if needed
    - Gets/creates bean instance from pool
4. **Bean Instance** executes `add(2, 3)` business logic
5. **Response** flows back through the same chain
## Using Enterprise and Entity Beans 
### Modeling Task flow with Session Beans
we try to minimize the number of calls over the network 
so we try to make it with as much abstractions as we can 
so instead of make 3 or 5 calls for booking(Fine-Grained) we only use one call and inside it, we call directly the services we need(Coarse-Grained)
```java
// Get the credit card number from the text field.
String creditCard = textField1.getText( );
int cabinID = Integer.parseInt(textField2.getText( ));
int cruiseID = Integer.parseInt(textField3.getText( ));

Customer customer = new Customer(name, address, phone);

// Create a new TravelAgent session, passing in a reference to a
// customer entity bean.
TravelAgentRemote travelAgent = ...; // Use JNDI to get a reference
travelAgent.setCustomer(customer);
// Set cabin and cruise IDs.
travelAgent.setCabinID(cabinID);
travelAgent.setCruiseID(cruiseID);

// Using the card number and price, book passage.
// This method returns a Reservation object.
Reservation res = travelAgent.bookPassage(creditCard, price);
```
### Stateful and stateless session beans
**Stateful** is bean or session that have a history and each call depend on the previous one 
**Stateless** is self depend session, it only depends on the passed parameters to it
### Message-Driven Beans
its like I/O in OS, you send message like open file, and keep what you're doing, after OS finish, it will reply, but in this case, message Driven didn't reply to the sender 
## The Bean-Container Contract
Enterprise JavaBeans (EJB) uses three bean types within a managed container. Entity Beans represent business data/objects (customers, cabins) and map to database records. Session Beans manage business processes and taskflow, coordinating operations between entities through coarse-grained interfaces while handling complex business logic and hiding implementation details from clients. Message-Driven Beans process asynchronous JMS messages for external system integration without requiring direct client connections. The Container provides runtime services (transactions, security, concurrency) and manages bean lifecycles through callbacks and context objects. This separates business logic from infrastructure concerns, reducing network traffic, improving reusability, and enabling both synchronous and asynchronous enterprise operations.