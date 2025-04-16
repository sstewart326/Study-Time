* A **socket** is an interface that creates a two-way channel between processes communicating on different devices.
* The interface (IP address + port) is referred to as a **socket address**.

![[Screenshot 2025-04-15 at 8.01.31 PM.png]]

* Server Socket
	* The **server socket** is configured to remain open and passively listen for incoming traffic by binding to a socket address.
* Client Socket 
	* The **client socket** is created to get data or services from the server socket. The port and IP defined by the server socket must be known before a client socket can establish a connection with a server process