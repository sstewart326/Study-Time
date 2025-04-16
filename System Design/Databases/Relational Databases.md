* adhere to schemas before storing the data
* Structured Query Language (SQL) is used for manipulating the db
* ACID Principles
	* Atomicity - either all statements within a transaction successfully execute or none do
	* Consistency - db should be in a consistent state after each transaction
	* Isolation - multiple parallel transactions should not affect each other
	* Durability - guarantee that the completed transactions survive permanently in the db



### Why Relational DBs?
 
 * Reduce redundancy
	 * related data can be aggregated across tables via foreign keys (normalization)
* Concurrency
	* handled via transactions to ensure data remains consistent
* Backup and Recovery
	* relational DBs guarantee consistency at any time making import and export operations easy