
[ZooKeeper: Because Coordinating Distributed Systems is a Zoo](https://zookeeper.apache.org/doc/current/zookeeperOver.html)



[What is ZooKeeper? - Coordination Services | Systems Design Interview 0 to 1 with Ex-Google SWE](https://www.youtube.com/watch?v=F06tdYgcz_A&ab_channel=Jordanhasnolife) 

[Zookeeper Tutorial — With Practical Example | by Bikas Katwal | Medium](https://bikas-katwal.medium.com/zookeeper-introduction-designing-a-distributed-system-using-zookeeper-and-java-7f1b108e236e)

[distributed computing - Explaining Apache ZooKeeper - Stack Overflow](https://stackoverflow.com/questions/3662995/explaining-apache-zookeeper) 


##### 1. Zookeeper: A Distributed Coordination Service for Distributed Applications

Zookeeper is a distributed, open source coordination service for distributed applications. It exposes a simple set of primitives that distributed applications can build upon to implement higher level services for synchronization, configuration maintenance and groups and naming.

It is designed to be easy to program to, and uses a data model styled after the familiar directory tree structure of file systems. It runs in Java and has bindings for both Java and C.

Coordination services are notoriously hard to get right. They are especially prone to errors such as race conditions and deadlock. The motivation behind zookeeper is to relieve distributed applications the responsibility of implementing coordination services from scratch.


##### 2. Design Goals

**Zookeeper is simple.**  Zookeeper allows distributed processes to coordinate with each other through a shared hierarchical namespace which is organized similar to a standard file system.

The namespaces consists of data registers called znodes, in Zookeeper parlance, and these are similar to files and directories. Unlike a typical file system which is designed for storage, Zookeeper data is kept in memory, which means zookeeper can achieve high throughput and low latency numbers.

The zookeeper implementation puts a premium on high performance, highly available, strictly ordered access. The performance aspects of zookeeper mean it can be used in large distributed systems. The reliability aspects keep it from being a single point of failure. The strict ordering means that sophisticated synchronization primitives can be implemented at the client. 

**Zookeeper is replicated.** Like the distributed processes it coordinates, Zookeeper itself is intended to be replicated over a set of hosts called an ensemble.

![[Pasted image 20250118120116.png]]

The servers that make up the zookeeper service must all know about each other. They maintain an in-memory image of state, along with a transaction logs and snapshots in a persistent store. As long as a majority of the servers are available, the Zookeeper service will be available.

Clients connect to a single zookeeper server. The client maintains a TCP Connection through which it sends request, gets responses, gets watch events and sends heart beats. If the TCP connection to the server breaks, the client will connect to a different server.

**Zookeeper is ordered.** Zookeeper stamps each update with a number that reflects the order of all zookeeper transactions. Subsequent operations can use the order to implement higher level abstractions, such as synchronization primitives.

**Zookeeper is fast.** It is especially fast in "read dominant" workloads. Zookeeper applications run on thousands of machines and it performs best where reads are more common than writes, at ratios of around 10:1.

##### 3. Data model and hierarchical namespace

The namespace provided by zookeeper is much like that of standard file system. A name is a sequence of path elements separated by a slash (/). Every node in Zookeeper's namespace is identified by a path.

Zookeeper Hierarchical Namespace

![[Pasted image 20250118121230.png]]


##### 4. Nodes and ephemeral nodes
Unlike standard file systems, each node in zookeeper namespace can have a data associated with it as well as children. It is like having a file system that allows a file to also be a directory. (Zookeeper was designed to store coordination data : status information, configuration, local information, etc, so the data stored at each node is usually small, in the byte to kilobyte range).
We use the term znode to make it clear that we are talking about Zookeeper data nodes.

Znodes maintain a stat structure that includes version numbers for data changes, ACL changes, and timestamps, to allow cache validations and coordinated updates. Each time a znode's data changes, the version number increases. For instance whenever a client retrieves data it also receives a version of the data.

The data stored at each znode in a namespace is read and written atomically.  Reads get all the data bytes associated with a znode and a write replaces all the data. Each node has an access control list (ACL) that restricts who can do what.

Zookeeper also has the notion of ephemeral nodes. Theses znodes exist as long as the session that created the znode is active. When the session ends the znode is deleted.

##### 4. Conditional Updates and Watches

Zookeeper supports the concept of watches. Clients can set a watch on a znode. A watch will be triggered and removed when the znode changes. When the watch is triggered the client receives the packet saying that the znode has changed. If the connection between the client and one of the zookeeper servers is broken, the client will recieve a local notification.

New in 3.6.0: Clients can also set permanent, recursive watches on a znode that are not removed when triggered and that trigger for changes on the registered znode as well as any children znodes recursively.


##### 5. Guarantees

Zookeeper is very fast and very simple. Since its goal, though, is to be a basis for the construction of more complicated services, such as synchronization, it provides a set of guarantees. These are: 

- Sequential Consistency - Updates from the client will be applied in the order that they were sent
- Atomicity - Updates either succeed or fail, no partial results
- Single System Image - A client will see the same view of the services regardless of the server it connects to i.e. a client will never see an older view of the system even if the client fails over to a different server with the same session
- Reliability - Once an update has been applied, it will persist from that time forward until a client overwrites the update.
- Timeliness - The clients view of the system is guaranteed to be up to date within a certain time bound.

##### 6. Simple API

One of the design  goals of zookeeper is providing a very simple programming interface. As a result it supports only these operations:

- create : creates a node at the location in the tree
- delete : deletes a node
- exists : tests if a node exists at a location
- get data : reads the data from the node
- set data : writes data to a node
- get children : retrieves a list of children of a node
- sync : waits for data to be propagated


##### 7. Implementation

A high level components of zookeeper service. With the exception of the request processor, each of the servers that make up the zookeeper service replicates its own copy of each of these components. 

![[Pasted image 20250118125314.png]]


The replicated database is an in-memory database containing the entire data tree. Updates are logged to disk for recoverability, and writes are serialized to disk before they are applied to the in memory database.

Every zookeeper server services clients. Clients connect to exactly one server to submit requests. Read requests are serviced from the local replica of each server database. 

Requests that change the state of the service, write requests, are processed by an agreement protocol.

As part of the agreement protocol all write requests from clients are forwarded to a single server, called the leader. The rest of the zookeeper servers called the followers, receive message proposals from the leader and agree upon message delivery. The messaging layer takes care of replacing leaders on failures and syncing followers with leaders.

Zookeeper uses a custom atomic messaging protocol. Since the messaging layer is atomic, Zookeeper can gurantee that the local replicas will never diverge.  When the leader recieves a write request, it calculates what state of the system when write is to be applied and transforms this into a transaction that captures this new state.




---
What did you understand : 

1. it is a platform on which complex services can be build
2. it has a tree like strucuture
3. z node - a node in the tree
4. a node which is only present in a active session is called an ephemeral node
5. servers are distributed
6. collection of servers is called ensemble
7. clients have different type of request
8. a client conencts to only one server
9. in memory storage happens of state
10. there is one leader server
11. read happens from local replical
12. write happens with agreement protcol
13. messaging protocol update the leader server


Yes, most of these points about Apache ZooKeeper are correct, but a few need slight clarification or refinement. Here's a point-by-point review:

1. **It is a platform on which complex services can be built**: ✅
    
    - Correct. ZooKeeper provides primitives for synchronization, configuration, and coordination, which are used to build higher-level distributed services like leader election, locking, or service discovery.
2. **It has a tree-like structure**: ✅
    
    - Correct. ZooKeeper organizes data in a hierarchical structure, much like a file system, where each node is called a znode.
3. **Znode - a node in the tree**: ✅
    
    - Correct. A znode is a data node in ZooKeeper's tree structure. It can hold data and have child nodes.
4. **Servers are distributed**: ✅
    
    - Correct. ZooKeeper is designed to run on a distributed ensemble of servers to ensure fault tolerance and high availability.
5. **Collection of servers is called ensemble**: ✅
    
    - Correct. The group of ZooKeeper servers working together is referred to as an ensemble.
6. **Clients have different types of requests**: ✅
    
    - Correct. ZooKeeper clients can make various requests, such as creating znodes, deleting znodes, reading data, writing data, and setting watches.
7. **A client connects to only one server**: ✅
    
    - Correct. A client establishes a session with a single ZooKeeper server at a time. However, if the connected server becomes unavailable, the client can reconnect to another server in the ensemble.
8. **In-memory storage happens of state**: ✅
    
    - Correct. ZooKeeper stores the entire data tree in memory to ensure high performance for read and write operations. The state is also periodically persisted to disk for durability.
9. **There is one leader server**: ✅
    
    - Correct. In an ensemble, there is always one leader server responsible for handling all write requests, while followers handle read requests.
10. **Read happens from local replica**: ✅
    

- Correct. Reads can happen from any server (leader or followers) because all servers maintain a synchronized replica of the data tree.

11. **Write happens with agreement protocol**: ✅

- Correct. Write operations use a consensus algorithm (ZooKeeper's atomic broadcast protocol, based on Zab) to ensure consistency across the ensemble.

12. **Messaging protocol updates the leader server**: ❌ (Clarification needed)

- This is not entirely accurate. The leader server itself coordinates and propagates updates to the followers through the ZooKeeper Atomic Broadcast (Zab) protocol. The messaging protocol ensures that all servers eventually reach the same state, but updates originate from the leader.

### Final Notes:

Most of the points are correct. The last one could be rephrased as:  
_"The leader server coordinates updates and uses the messaging protocol (Zab) to synchronize these updates with the followers."_

4o

##### You said:

and what about this a node which is only present in a active session is called an ephemeral node

###### ChatGPT said:

ChatGPT

✅ **Correct**:

An **ephemeral node** in Apache ZooKeeper is a type of znode that exists only for the duration of the session of the client that created it. Once the client's session ends (due to disconnection, timeout, or explicit closure), the ephemeral node is automatically deleted by ZooKeeper.

### Key Characteristics of Ephemeral Nodes:

- **Session-Scoped**: The lifespan of an ephemeral node is tied to the session of the client that created it.
- **No Children Allowed**: Ephemeral nodes cannot have child nodes; they are always leaf nodes.
- **Common Use Case**: They are often used for **service registration** or **leader election**, where the presence of the ephemeral node indicates that a service or client is active.
- **Automatic Cleanup**: If the session ends or the client becomes unreachable, ZooKeeper cleans up the ephemeral node automatically, ensuring the state remains consistent.

### Example:

If a client creates an ephemeral node at `/services/service1`, and its session ends unexpectedly, ZooKeeper will automatically remove `/services/service1`. This is useful for scenarios like service discovery, where the presence of a node indicates the service is alive and reachable.



















--- 


Coordination Services

In a nutshell, zookeeper helps you build distributed applications.


Apache Zookeeper is an open source coordination and synchronization service designed to manage distributed systems and applications.




**How It Works**
Zookeeper is a replicated synchronization service with eventual consistency. 

It is robust, since the persisted data is distributed between multiple nodes (this set of nodes is called an "ensemble")