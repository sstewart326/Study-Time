
Let’s consider a service hosting the dynamic and personalized website of a large news organization. Due to some unexpected events, such as 9/11, flash crowds are coming to the website to find out updates. It might be a situation where all the DAUs come in simultaneously. Such a situation will clearly break our usual load assumptions. Can you think of some way to gracefully degrade the service to meet such an unexpected load?

> 	We can abandon per-user personalization for the time being because probably everyone cares about current events. Additionally, we can shift to a static-like website where content is pushed to CDN nodes and updated by the service when new updates come in.
> 	
> 	Doing so makes each request/response fast, and users get their data from the CDN, which will have multiple edge nodes near the customers.
> 	
> 	Service can also reduce the use of multimedia content or use it judiciously so the clients, whose networks might also be congested, could get the information in fewer bytes.

What happens when the primary node fails in [[Data Replication#Single leader/primary-secondary replication|primary/secondary replication]]?

> In case of failure of the primary node, a secondary node can be appointed as a primary node, which speeds up the process of recovering the initial primary node. There are two approaches to select the new primary node: manual and automatic.
> 
> In a **manual approach**, an operator decides which node should be the primary node and notifies all secondary nodes.
> 
> In an **automatic approach**, when secondary nodes find out that the primary node has failed, they appoint the new primary node by conducting an election known as a leader election.