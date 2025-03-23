More Reading Required : [101 On Aerospike Data Base for Beginners | by Prabhu Rajendran | Everything at Once | Medium](https://medium.com/everythingatonce/101-on-aerospike-data-base-for-beginners-ea0408e0493e)




Medium Article : [Starting out with Aerospike. A intro into into setting up and… | by Bogdan Pistol | Tech Club | Medium](https://medium.com/techclub/starting-out-with-aerospike-10ce0358e955)

Aerospike Docker Image : [aerospike - Official Image | Docker Hub](https://hub.docker.com/_/aerospike)

Aerospike Quick Start : [Aerospike Quick Start | Developer](https://aerospike.com/developer/quickstart?client=java)

![[Pasted image 20250208194340.png]]

##### 1. What is Aerospike?

Aerospike is a modern, high performant, ultra low latency, No SQL Database. 
It is written in C language and one of the main features is the Hybrid Memory Model.
If you are looking for a big storage solution, that can handle terabytes and petabytes of data with milliseconds response time, then have a look at aerospike.

Aerospike is a distributed NoSQL database with blazing fast reads and writes and unmatched uptime. It is designed for real time applications requiring consistent low latency and high availability, through fast and efficient hybrid memory architecture combining memory for indexing and SSDs for storage. Aerospike supports key value, document and graph data modelling and is used extensively for ad tech, fraud detection, recommendations systems, IoT, payment systems and fintech.

Aerospike can store data on any of the following types of media and combinations thereof:
- Dynamic Random Access Memory (DRAM)
- Non-volatile Memory Extended (NVMe) Flash or SSD (Solid State Drive)
- Persistent Memory (PMEM)
- Traditional Spinning Media


##### 2. Aerospike Products

- The **server** refers to the actual database  (just like MySql Server)
- The **clients** are the software libraries that provide a mechanism for connecting to the server. 
  There are multiple clients, supporting a variety of programming languages
- **Aerospike Management Console (AMC)** is a web based tool to monitor/manage an Aerospike cluster
- **Aerospike tools**  is a collection of tools for managing and interacting with the Aerospike Server. We are interested in the AQL Tool - Aerospike Query Look. This will be ours primary mechanism for browsing and querying our data. 


##### 3. Aerospike Data Model
[Data model | Aerospike Documentation](https://aerospike.com/docs/server/architecture/data-model.html)


![[Pasted image 20250209090742.png]]

1. Physical Storage 
	1. You can choose the specific type of storage you want for each namespace. NVMe Flash, DRAM, or Intel Optane Persistent Memory (PMem). Different namespaces in the same cluster can use distinct types of storage. The physical storage medium is also called storage engine.

2. Namespace
	1. These are the top level containers
	2. Schemas in classical RDBMS system
	3. Similar to a tablespace in a RDBMS, a namespace is a collection of records that share one specific storage engine, with common policies such as replication factor, encryption, eviction and more.
	4. A database can contain multiple namespaces.
	5. At least one namespace is mandatory
	6. A namespace in Aerospike is primarily used for managing storage by defining:
		1. Storage Engine (RAM, SSD or hybrid)
		2. Replication factor (how many copies of data exist)
		3. Eviction Policies (when to remove old data)
		4. Persistence Settings (whether data is durable on disk)
		5. Compression and Encryption (for data security)
		6. TTL (Time to Live) (automatic expiration of records)
		7. All records stored within a namespace follow the same storage rules.

3. Set
	1. Similar to tables in relation database, but without explicit schema
	2. Records can be optionally grouped into sets. 
	3. Records can exist without a set.

4. Record
	1. They refer to an actual entry or row in relational database
	2. It is a contiguous storage unit for all the data uniquely identified by a single key

5. Bin
	1. Can be thought of as columns
	2. A record is subdivided into bins, which are similar to columns in an RDBMS. Each bin has its own datatype and those do not need to agree between records. Secondary indexes can be optionally declared on bins.


##### 4. AQL

Used to query the namespaces and sets.
[Aerospike Quick Look (AQL) | Aerospike Documentation](https://aerospike.com/docs/tools/aql/)
AQL does not expose the full capabilities of a Aerospike Server. Some features might be unavailable, for those you will need to use the client.


To query on the basis of a column(bin) name you would need the bin to be a secondary index.
Querying on non primary key bins will require secondary indexes. 
Not able to create secondary index using aql, had to do it using asadm.

How to connect to asadm

```sql

// How to connect?

docker run -it aerospike/aerospike-tools asadm -h $(docker inspect -f '{{.NetworkSettings.IPAddress }}' aerospike) 


// How to create an index?
~~~
Admin> info sindex
Admin> manage sindex create string my_index ns test set testSet bin name
ERROR: User must be in privileged mode to issue "manage" commands.
       Type "enable" to enter privileged mode.
Admin> enable
Admin+> manage sindex create string my_index ns test set testSet bin name
Use 'show sindex' to confirm my_index was created successfully.
Admin+> show sindex
~~~~Secondary Indexes (2025-02-09 04:14:11 UTC)~~~~~
   Index|Namespace|    Set| Bin|   Bin|  Index|State
    Name|         |       |    |  Type|   Type|
my_index|test     |testSet|name|string|default|RW
Number of rows: 1

Admin+>
```

##### 5. Important Pages

-  Data Model : [Data model | Aerospike Documentation](https://aerospike.com/docs/server/architecture/data-model.html)

- Secondary Index  : [Secondary index | Aerospike Documentation](https://aerospike.com/docs/server/architecture/secondary-index.html)
- Secondary Index Queries : [Secondary index queries | Aerospike Documentation](https://aerospike.com/docs/server/guide/query)
   (👆 how to build secondary index using asadm)

- Aerospike Admin Commands
	- [Aerospike Admin (asadm) | Aerospike Documentation](https://aerospike.com/docs/tools/asadm)
