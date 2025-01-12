	-Hussein Nasser
	
	
	
	I have been a backend engineer for over 20 years and I have witness technologies come and go. One thing however, always remains constant:

The first principles the tech is built on.

I don’t really mean tools, frameworks or even languages. Those evolve and change but the fundamental infrastructure on which the tools are built rarely does.

For example knowing how to setup Apache or IIS is one thing, understanding the commonalities and differences between the two web servers is another.

In this article I explore some of the

[fundamentals of backend engineering](https://backend.husseinnasser.com/)

that are at the root of everything we use. You may choose to have basic understanding of all these fundamentals and become a jack-of-all-trades backend engineer or go vertical in one at deeper level and become expert in that area. There is no wrong or right, it all depends on what moves you.

The way to become a better backend engineer is never clean and straightforward. In fact, it is messy, it is full of trial and errors and experimentations that only you have to experience. There is no book, no course, no YouTube video or a medium article that can teach you everything there is about backend engineering. You have to experience it yourself.

If you are a recent graduate interested in backend engineering, you may find one or more of these fundamentals interesting and decide to pursue it.

The best way is to get your hands dirty. Let us get started.

# 

Communication Protocols

Communications protocols link the frontend to the backend. Understanding how protocols work is a good skill to have for an engineer especially if they want to build a resilient backend application.

Almost all the protocols we use and love on the backend are either built on top of TCP or UDP.That is why understanding the differences between this two help the engineer make the right choice. For instance, TCP is a stream-based connection-oriented protocol while UDP is a message based and connectionless. TCP provides reliable delivery at a cost of connection setup and retransmission. While UDP starts faster but doesn’t have guaranteed delivery. Anything you build on top of these two protocols must adhere to their fundamental properties. TCP is not better than UDP, and UDP is not better than TCP. It all depends on what you are building.

Moving up the stack, the HTTP protocol was originally built on top of TCP because we wanted to send requests and responses reliably. As the web evolved and resources become richer, one connection was not sufficient to concurrently send multiple requests. So browsers started to establish more and more connections, the cost of connection setup for each request became so high.

HTTP/2 introduced application level streams so multiple requests can be sent on the same connection. Later HTTP/2 evolved and had to be rewritten on top of UDP with HTTP/3 to solve the TCP head of line problem. There are reasons for everything, the fundemental feature of TCP was the culprit of this move. It doesn’t mean TCP is bad the web has evolved in a way that TCP is no longer suitable. If we didn’t know how TCP works we would not have improved the HTTP protocol.

It is also important to know that using any protocol comes with a cost especially while building APIs. Understanding that cost will help you make better informed decisions. For example, using HTTP/2 might give you more HTTP request throughput, but the work the application needs to do to assemble the streams taxes the CPU, something

[Lucidchart](https://www.lucidchart.com/techblog/2019/04/10/why-turning-on-http2-was-a-mistake/)

learned the hard way.

Sometimes the backend architecture requires real-time Bidirectional communication protocols to build chatting, gaming apps or just communicating between two services. Protocols such as WebSockets, gRPC or just raw TCP/UDP can be used. If you know how a protocol works and what is the strength and weaknesses you will know when to use it.

Ultimately, learning communication protocols is important for a backend engineer, and it is possible to go as deep as desired in any protocol. Maybe one day you will write an RFC proposing a new protocol.

# 

Web Servers

Web servers are becoming increasingly important as backend infrastructure relays on HTTP web communications. Web servers deliver static or dynamic content served on top of the HTTP protocol. If you build a Web API you may spin up your own web server in your language of choice or use a web framework such as Express or Django.

Modern web servers support both HTTP/1.1 and HTTP/2. HTTP/3 is slowly getting support as its newer protocol. Configuring your web server with the appropriate protocol is critical for performance and resilience of your backend application; And it all depends on the environment. For example, Do you expect multiple concurrent requests from the same client? or do you expect fewer requests but from many clients? Based on that, you can pick multiplexing HTTP/2 or vanilla simple HTTP/1.1.

The internal architecture of web servers can also differ. Web servers can be single or multithreaded. They can have one thread or multiple listener threads. There are many ways client connections can be accepted and distributed among the threads. If you choose an off-the-shelf web server you are stuck with its architecture. If you build your own from scratch you get to choose the architecture that is right for you. I wrote an article going through multiple designs for threading and connection management in

[backend servers](https://medium.com/@hnasr/threads-and-connections-in-backend-applications-a225eed3eddb)

, you may want to check it out.

Additionally, web servers can set any where in the stack. For example, a CDN is a web server that acts like a cache and communicate with the origin backend web server to get the content. An API gateway is a web server that authenticate user and serve API responses from backend web servers.

Examples of off-the-shelf web servers are Apache Tomcat, Apache httpd, and

[NGINX](https://medium.com/@hnasr/the-architecture-of-nginx-2b32fc0b7877)

. The latter can act as both a web server and a proxy. You may build your own web server in any language by listening on a TCP port and understand how to speak the HTTP protocol, you can of course use an HTTP library that does most of the work for you.

# 

Database Engineering

Database engineering is a vast field of study. At its core the idea of a database is simple; Allow multiple users to store and retreive data consistently and in a durable fashion. That is why understanding the four properties of

[ACID](https://database.husseinnasser.com/)

: atomicity, consistency, isolation, and durability is fundamental to database engineering.

One must understand that nothing is written on stone and following these properties isn’t a must. For example, relational databases are fully ACID and require a schema while MongoDB was built as a document based database, with basic atomicity (document level) and no schema. Redis built a fanstatic high performance cache by sacrificing durability by default.

No database system is complete without indexes and at their core B+Trees is the data structure of choice. How data is organized in tables, documents or graphs all end up as file system pages at the end of the day. Understanding how to get most of your disk I/O read is the core of database engineering.

If you are interested in database engineering, there are many areas you can specialize in. You can pick one database and know everything about it. You can build a better indexing techniques (LSM is a good example). You can build a new database system specialized in a specific workload.

I have been working with databases for 20 years and to this day I learn something new all the time. This field is vast.

# 

Proxies

Proxies are becoming increasingly popular in the engineering world, especially with the introduction of micro-services. The main purpose of a proxy is it receives requests from a client and forward the requests to backend servers. The proxy hides the network layer identity of the original client from the destination server.

There are two levels of proxying: layer 4 and layer 7 proxying. Layer 4 proxying works at the transport layer, while layer 7 proxying works at the application level. Each layer provides different capabilities and can be used for different purposes. Layer 7 proxying require the proxy to understand the application protocol while layer 4 proxying works with any application protocol because it works at the transport layer (TCP or UDP).

You might have heard the forward proxy and reverse proxy used interchangeably. Both the forward proxy and the reverse proxy, receive requests from clients and forward the request to a backend. In the forward proxy, the client explicitly asks for a particular backend server and the proxy fulfills this request. Forward proxies must be configured in the client network proxy section for them to work. In the reverse proxy the client doesn’t know the final backend server, to the client the final destination is the reverse proxy. The client doesn’t know there are more servers on the backend.

A common uses cases of proxies are caching, API gateways, authentication, load balancing and much more. For example a content delivery network (CDN) is a reverse proxy that sends request to the origin backends. Fiddler or MITM are proxies configured on the client side and all requests* get sent to them first. Service meshes are essentially a proxy and a reverse proxy. Learn more about proxies

[here](https://youtu.be/SqqrOspasag)

.

> *I say all requests but in fact only requests that the proxy are configured to support. Mostly here we refer to HTTP proxy, so all HTTP requests get forwarded.

Example of proxies are

[NGINX](https://medium.com/@hnasr/the-architecture-of-nginx-2b32fc0b7877)

, HAProxy and Envoy. Proxies are one of the most interesting topics in backend engineering and one can specialize in learning and improving them. Cloudflare

[recently](https://youtu.be/QbOAHkaFU6w)

moved away from NGINX, their primary reverse proxy, and built their own proxy because of certain limitations in NGINX. I discussed that in details in an episode of the

[backend engineering show.](https://youtu.be/QbOAHkaFU6w)

# 

Messaging Systems

Messaging systems are becoming increasingly important as we move towards interconnected systems and services. As services start to communicate to each other, coupling and dependencies increase which increases the complexity of building scalable backend applications. Messaging systems are designed to remove this coupling

Messaging systems at their core support a feature called publish-subscribe where a client can publish a message and other clients can subscribe to consume this content. The choice of architecting how publishing and consumption is made is up to the messaging system. For example,

[Kafka](https://youtu.be/R873BlNVUB4)

use long-polling model while

[RabbitMQ](https://youtu.be/Cie5v59mrTg)

uses push model, both has pros and cons.

Consuming a message also comes with an interesting and hard to solve problem. How do you make sure the consumer reads the message only once? These guarantees complicates the messaging system design.

Messaging systems are truly interesting piece of technology that is fundamentals to backend engineering. This field might interest you.

# 

Message Formats

Message formats go hand in hand with communication protocols; They describe in-wire format of the message being sent. They usually broken down into two types human readable and non-human readable. Examples are XML, JSON and

[protocol buffers](https://youtu.be/46O73On0gyI)

.

When a client sends a message to a backend, it needs to serialize the message from the language data structure to the on-wire message format. When the backend receives the message it needs to then deserialize the message from this format to the language data structure.

That is why it is absoluity fine to have a Javascript client communicates with a C# backend using JSON as a message format. The native JSON object of javascript will be converted to a JSON byte string in the wire, the C# backend then deserializes the byte string to a C# structure representing a dictionary. It is important to understand the cost associated with serializing and deserializing message format.

XML was one of the original message formats designed to be human-readable. However, computers had difficulty dealing with XMLs, so protocol buffers format was created to make the message format smaller and more friendly. Protocol buffers became very popular and were designed to solve the problem of high bandwidth messages. Protocol buffers minimize the payload so fewer bytes can be sent. It also speeds up the serialization and deserialization process.

Becoming specialized in message formats is also an option. You may invent the next message format that may become the standard to serve us for the next 50 years.

# 

Security

Security is an important topic in the field of software engineering. There are many different aspects to security. You can secure communications with encryption or TLS. You can prevent network intrusion with firewall rules and proper network configuration. You can study common software vulnerabilities and protect against denial of service attacks. As a software engineer, it is important to be familiar with the different types of security risks and how to mitigate them.

One type of security risk is a man-in-the-middle attack. This is where an attacker intercepts communication between two parties and tries to eavesdrop or modify the data being exchanged. To prevent this type of attack, it is important to encrypt and authenticate the communicated parties using Transport Layer Security (TLS).

Another type of security risk is a denial of service attack. This is where an attacker tries to prevent legitimate users from accessing a service by flooding it with requests or through finding a way to crash the backend by sending a special payload. To prevent this type of attack, it is important to have a firewall or a layer 7 DDOS protection layer in place to block illegitimate requests. Cloudflare has great services to detect DDOS traffic. This is of course made possible through layer 7 inspection.

Of course its hard to summarize all possible security attacks. There is a client side security attacks such as XSS (cross side scripting), there are server side security attacks such as SQL injection.

Security is an important topic in the field of software engineering. There are many aspects to security. As a software engineer, it is important to be familiar with the different types of security risks and how to mitigate them.

# 

Conclusion

In conclusion, as a backend engineer, it is important to explore different technologies to find what interests you and where your strengths are. Don’t be afraid to experiment and build something cool, even if it’s with a language that may be considered unconventional.

What we discussed in this article are what I believe are some of the fundamentals that will always remain here, understanding them makes you a better engineer.

As you gain more experience and expertise, focus on deepening your knowledge in a specific area to become known for your skill in that field. Ultimately, it is important to follow your interests to succeed in the rapidly-evolving world of software engineering.

Always remember, nothing is written in stone, you can change anything. There is no right and wrong way to design or build applications, it all depends on what you are trying to do. You may run into a situation where the technologies we have today work for you. But you might also reach a dead end and might need to invent something that has never been invented before.

Just read the

[Homa paper](https://youtu.be/nEFOni_87Yw)

, this protocol attempts to completely replaces the fundamental protocol TCP because data centers workloads are completely unsuitable for TCP.

I hope you enjoyed this article. I wish you the best in your career.

If you are interested to learn more about backend engineering consider getting my

[Fundamentals of Backend Engineering Udemy course](https://backend.husseinnasser.com/)

.

[link]([(1) Hussein Nasser on X: "How to Become a Good Backend Engineer (Fundamentals)" / X](https://x.com/hnasr/status/1852537428227375482))

