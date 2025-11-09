# Explanation
## Resource Management 
as the number of user are increased by time, the objects and connections in the app will increase as well, so we need a way to manage them as if we didn't, it will cause a problem in concurrency and performance, EJB gives us two ways to manage this one
### Instance Pooling
instead of having number of access as number of connection required, you have one access and pool the connections from it
#### The stateless session bean life cycle 
- **No State** not instantiated yet
- **Pooled State** instantiated and waiting to assigned to any request 
- **Ready State** assigned and ready to responses to the request 

the stateless don't save any state between any requests, so the container can change the bean instances between requests 
when method need an instance to serve it, the pool fetches any instance from it where it's free, then assign it to the request, after finish its returned to the pool to serve another requests in the future, and based on number of requests the pool fetch same number from the pool
![[Pasted image 20250805150122.png]]
#### Message-driven beans and instance pooling
MDB like stateless, so we can treat them as it, but in this case, there are Destinations, each one have its own instance pool assigned to it, so when a message needs to reach some destination, it arrives to the container, and from the container it finds which pool assigned for this destination, after find it, it sends the request to it so it fetches bean instance from it to serve this request and after finished it returned to its pool 
![[Pasted image 20250805151606.png]]
### The Activation Mechanism
in the stateful beans it saves data between calls of clients, so we need a way when some method called and after finish with some time it called again, we need to continue when it stopped, so the activation way is the best way in this case, as it store the data when a bean finish its work in another storage, and when we need to continue it create a new bean and reload data from the saved storage and fill the fields with its saved data 
![[Pasted image 20250805160733.png]]
### Java EE Connector Architecture
EJB vendor had to write custom code for every Enterprise information system they want to support, but with JCA there is no need for that
#### Java EE Connectors 1.5



# Source
[Chapter 3 in Enterprise Java Beans 3.0 5th Ed 2006](https://www.scribd.com/doc/136500914/Enterprise-JavaBeans-3-0-5th-Ed-2006) 