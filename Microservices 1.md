link playlist - https://www.youtube.com/watch?v=PXkdFs2GSwE&list=PLq3uEqRnr_2EDsuxPboP9_WtVRR_TaMrF&index=3

**Monolith advantage** - 
Easy to develop all the components with less no of developers
Easy to test and deployment is easy
Cost of infrastructure is less 
Latency will be less
Easy to horizontal scale for small code base 

**Disadvantage** -
Time to release a new feature will be more as code changes involved in lot of places
Once complexity increase scaling will be difficult
Crash in one module will take down entire system as its a single point of failure
Reliance on developers as complexity increases
New team member learning curve will be more and error prone
Stuck with one technology
Tightly coupled 
Once complexity increased and have large code based it will be difficult to scale as it increases cost of computation.

**Principles**:
Independent/Autonomous 
- Small team size
- clear contract API's
- Parallel development
- Individual deployment
Resilient/Fault tolerant/Design for failure 
- Once analyzing the failures we know the failures and capture all the use cases of failures and design the system to avoid those failures
- Avoid single point of failure
- Avoid cascading failure
- consider failure as events and analyze in future
Observable 
- Centralized monitoring
- Centralized logging
- Health check
Discoverable
- All the services should register to the service discovery service
- It makes client life easy when looking for service
Domain driven 
 - Focused on business
 - Focused on core domain 
 - Focus on domain logic
Decentralization
 - Database for each service
 - Choice of database depends on the nature of particular service
 High cohesion
 - Do one thing only
 - Single responsibility principle
 - A business function
 - A business domain
 - easy to take new feature
Single source of truth
- Each services should have unique data present in the database like order id should be unique and should not mingle with product service. Passing order id will give the order details from order service.
- This helps in avoiding duplication of data.

Things to take care - 
Available
Scalable
Resilient 
Efficient that is it response immediately.

Different patterns - 
- Decomposition
	- Domain based migration of services - size of the service based on business functionality 
	- sub-domain based
	- common classes called god classes should be separated
	- Strangler pattern - Having a route logic which will send 10 percentage to new microservice and 90 percentage to monolith module.
		- [[Strangler pattern]]
	- Sidecar - logging to centralized system, monitoring of cpu memory, proxy for remote service, failure isolation, configuration, tracing. All common services like these will be handled by sidecar. 
		- Sidecar code can be deployed as shared library or better as separate service or traditional daemon service in the host machine.
		- Should framework or technology agnostics
	- Service mesh - 
		- Service discovery
		- configuration
		- logging
		- monitoring
		- proxy service
		- caching
		- Language agnostics
		- Istio is one of opensource service mesh. Which has control plane for configuration and data plane for communication on east-west services.
- Observability
- Database
	- Shared database per service
		- Private table per service
		- Schema per service
		- database server per service
	 - command query request segregation - segregating the create, update and delete part of the operation of product and order services to be handled in the domain service and view part of the operations will be done by the history service by having a separate service with database which will be read optimized and synched with the main service.
		 - Two ways - Handle service event at service, database triggers and procedure to update the database of history database. 
		 - Replication delay
		 - Extra complexity
		 - Code duplication
		 **Advantages**
		 - Easy to scale
		 - Simpler command and query model
		 - Flexibility to choose database for view
		![[Pasted image 20240925220036.png]]
	 - Data consistency in distributed systems
		- Eventual consistency - one node will get updated and return success. Replication will happen to other database nodes if any failure it will affect that database node.
		- Strong consistency - Guarantee latest data with higher latency. Each node has to be updated if any failure it will fail the actual transaction.
	 - Event driven architecture - Event sent to message broker like rabbitmq or kafka
	 - Event sourcing architecture - All the operations are captured and stored as events hence we can go to the state of system at any point of time. It uses asynchronous communication like message broker. 
	 - Two-phase commit - Two phase one is preparing for commit where each service will hold the resources with lock, second phase it sends the action to commit or abort which will commit or abort and release the lock. One transaction manager which will be single point of failure which will takes care of distribute transaction guarantee. 
	 -![[Pasted image 20240925233855.png]]
	 - Saga pattern 
		 - Choreography pattern
		 - Orchestrator pattern
		 -
- communication among services
- Integration - How to integrate different services data and aggregate and send to customer when client request for a data to once service it may need to aggregate from multiple services.
- Deployment
- Cross-cutting concern
