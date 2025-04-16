[[Terms#Replication|Definition]]

* synchronous replication
	* primary node waits for acknowledgement from secondary nodes before reporting to client
	* advantage - data consistency
* asynchronous replication
	* primary node does not wait for acknowledgment from secondary nodes before reporting to client
	* advantage - highly available

### Data Replication Models

##### Single leader/primary-secondary replication
* one node is designated as the primary
	* sends writes to the secondary nodes
* appropriate for read-heavy operations
	* we can add more followers if we need to distribute the read load
	* secondary nodes can still handle read requests if primary is down
* inappropriate if our load is write heavy

###### Primary-secondary replication methods

* Statement-based replication
	* statements are executed by primary and then written to a log for secondary nodes to execute
	* used by MySql for Insert, Update, and Delete
		* downside - nondeterministic functions like NOW() might result in distinct writes across nodes since this is determined by the system clock
* Write-ahead log (WAL) shipping
	* transaction is written to a log file on disk, executed on the primary, and then transmitted to secondary nodes
	* unlike SBR, it uses transaction logs instead of SQL statements which guarantees consistency for nondeterministic functions like NOW
	* Used by PostgreSQL and Oracle
* Logical (row-based) replication
	* changes to the db are captured at the level of individual rows and then replicated to secondary nodes
	* used by PostgreSQL and MySQL

##### Multi-leader Replication

* Downside
	* concurrent client requests to different leaders can create inconsistencies with the data
* Conflict avoidance
	* Last-write wins
	* write a custom handler


##### Peer-to-peer/Leaderless
* each node has equal weight and can initially write
* Quorums
	* write is considered a success when w number of nodes complete the writing
	* read must be read from r number of nodes
	* w + r needs to be > n (number of nodes)
##### Quorums

* 


