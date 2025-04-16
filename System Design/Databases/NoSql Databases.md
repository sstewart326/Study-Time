* Handle unstructure or semi-structured data well
* Can be a good option if we need to support low-latency requirements where the data would not be retrieved efficiently in a relational db due to multiple joins

### Why Non-relational (NoSql) DBs?

* simple - no need to join tables to access data
* horizontal scaling - easier to scale horizontally as all the data is present in one doc and not across tables
* Availability - node replacement can be performed without application downtime
* support for unstructured or semi-structured data
* Cost - many NoSql dbs are open source

### Types of NoSql DBs?

##### Key-Value
* use key-value methods like hash tables to store data
* easy partitioning and horizontal scaling
* Amazon DynamoDB, Redis, MemcachedDB

##### Document
* store and retrieve document formats like XML, JSON, BSON, etc
* MongoDB, Google Cloud Firestore

##### Graph
* nodes represent entities and edges show relationships between entities 
* allows us to store the data once and interpret differently based on relationships
* Neo4J, OrientDB, InfiniteGraph

##### Columnar
* store data in columns rather than rows
* only reading the columns that we are interested in makes aggregation and data analytics effiecient
* HBase, Hypertable, Amazon Redshift

### Drawbacks of NoSql DBs?

* lack of standardization
	* porting from one type to another might be a challenge
* Consistency
	* Data might not be strongly consistent but may use a eventual consistent model
	* 