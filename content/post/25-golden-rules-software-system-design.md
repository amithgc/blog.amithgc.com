---
title: "25 Golden Rules for Software System Design"
date: 2023-02-16T10:33:14+05:30
description: 25 Golden Rules for Software System Design
authorbox: true
sidebar: false
pager: true
thumbnail: "img/sw-design.avif"
categories:
  - "Knowledge"
  - "Development"
tags:
  - "DEVELOPMENT"
---

# Software architecting 

Software architecting is the process of designing and planning the structure, behavior, and functionality of software systems. It is required for several reasons, including:

1. **Scalability**: As software systems grow, it becomes increasingly important to have a well-designed architecture that can handle the additional load and scale appropriately. Good software architecture can make it easier to add new features and scale the system as needed.

2. **Maintainability**: A well-architected software system is easier to maintain and update over time. It can be challenging to make changes to a system that was not well-designed in the first place, leading to increased technical debt and difficulty in maintaining the system.

3. **Reliability**: Good software architecture can improve the reliability and stability of a system by reducing the likelihood of errors and improving fault tolerance.

4. **Performance**: Proper software architecture can help to ensure that a system performs efficiently, making it faster and more responsive to user needs.

5. **Communication**: Good software architecture can help facilitate communication between developers, stakeholders, and other team members. It provides a common language and framework for discussing the system's structure and behavior, leading to more effective collaboration.

In summary, software architecting is required to ensure that software systems are scalable, maintainable, reliable, performant, and well-communicated.

---

### Read-Heavy System? Consider using a *Cache*.

In today's data-driven world, systems that handle a large amount of read requests are quite common. These types of systems are known as read-heavy systems. In a read-heavy system, most of the requests are reads and very few writes occur. *For example*, a web application that serves news articles, product information, or stock prices is a read-heavy system. Caching is a technique that can be used to improve the performance of read-heavy systems.

A **cache** is a temporary storage area that stores frequently accessed data. When a read request is made, the system first checks the cache for the data. If the data is found in the cache, it can be served directly from the cache, rather than going to the primary data source, which could be a database or an API. This can significantly reduce the time it takes to serve the request.

> *For example*, consider a web application that displays the top-selling products on a homepage. If this data is stored in a database and retrieved every time a user visits the homepage, it can cause significant delays in serving the request. However, if the top-selling products are cached, the application can serve the request much faster. The cache can be updated periodically or whenever new products become popular.

Caching is not limited to data that is stored in a database. It can also be used to store the results of complex calculations, API responses, and other frequently accessed data. By caching data, read-heavy systems can achieve significant performance improvements and reduce the load on the primary data source.

*In conclusion*, if you are dealing with a read-heavy system, it's good to consider using a cache. Caching can help reduce the response time, improve the performance of the system, and reduce the load on the primary data source. However, it's important to design the cache strategy carefully, considering factors such as cache expiration, cache size, and cache consistency, to ensure that the system performs optimally.

---

### Need low latency? Consider using a *Cache* & *CDN*.

In today's fast-paced world, users expect quick and responsive systems. When designing a system that needs to respond quickly to user requests, low latency is crucial. Latency is the time it takes for a request to be processed and a response to be sent back to the user. A system that requires low latency should consider using a cache and a content delivery network (CDN).

A cache is a temporary storage area that stores frequently accessed data, as we discussed in the previous topic. When a read request is made, the system first checks the cache for the data. If the data is found in the cache, it can be served directly from the cache, reducing the response time significantly. This is especially beneficial for systems with high traffic.

A **content delivery network (CDN)** is a distributed network of servers that delivers content to users based on their geographic location. When a user requests content, the CDN delivers it from a server that is located geographically closest to the user, reducing the distance the content has to travel and the time it takes to deliver it. This can significantly reduce the latency for users located far away from the server where the content is stored.

> *For example*, a web application that serves images or videos can benefit from using a CDN. By using a CDN, the images or videos can be delivered quickly to users all around the world. Similarly, a financial application that requires quick responses can use a cache to store frequently accessed data, such as stock prices, to reduce the response time.

*In conclusion*, if a system needs low latency, it's good to consider using a cache and a CDN. Caching can help reduce the response time by storing frequently accessed data, while a CDN can help deliver content quickly by using a distributed network of servers. By using these techniques, systems can achieve low latency and improve the user experience.

---

### Write-Heavy system? Use a *Message Queue for Async processing*

In some systems, such as financial trading systems or e-commerce systems, a significant amount of write operations occur, making them write-heavy systems. In such cases, using a message queue for asynchronous processing can be a useful strategy.

A **message queue** is a communication tool that allows different components of a system to communicate asynchronously by passing messages between them. In the context of a write-heavy system, a message queue can be used to queue write requests, which can then be processed asynchronously by a worker or consumer process.

> *For example*, consider an e-commerce system that receives orders from customers. In a write-heavy system, the system may become overwhelmed by the volume of requests, causing delays in processing orders. By using a message queue, the order requests can be queued and processed asynchronously, allowing the system to handle a large volume of requests without becoming overloaded.

Another example is a financial trading system that receives a large volume of stock trading requests. By using a message queue, the trading requests can be processed asynchronously, allowing the system to handle the high volume of requests without delays.

Using a message queue for asynchronous processing can also provide other benefits, such as fault tolerance and scalability. If a worker process fails or becomes overloaded, the message queue can simply reassign the task to another worker, ensuring that requests are processed without interruptions.

*In conclusion*, if a system is dealing with a significant amount of write operations, using a message queue for asynchronous processing can be an effective strategy. By queuing write requests and processing them asynchronously, the system can handle a high volume of requests without becoming overloaded or experiencing delays. This approach can also provide fault tolerance and scalability benefits.

---

### Need to be ACID complaint?, Go for *RDBMS or SQL Database*

ACID compliance is a fundamental property of a database system that ensures that the database transactions are processed reliably, consistently and with integrity. ACID stands for Atomicity, Consistency, Isolation, and Durability. The Atomicity property ensures that all transactions are treated as a single unit of work, and either all the changes in the transaction are committed to the database or none at all. Consistency ensures that the database remains in a valid state before and after the transaction. Isolation ensures that the concurrent transactions do not interfere with each other. Durability ensures that once a transaction is committed, its changes are permanently stored in the database.

**Relational Database Management Systems (RDBMS)** or SQL databases are the most popular options for implementing ACID compliance. Examples of RDBMS or SQL databases include Oracle, MySQL, Microsoft SQL Server, and PostgreSQL. These databases provide a high level of data integrity and consistency, and they are widely used in many industries, including finance, healthcare, and e-commerce.

> *For example*, a banking system that needs to ensure that all transactions are processed correctly and reliably would benefit from using an RDBMS or SQL database. This is because the ACID properties guarantee that every transaction is processed accurately and completely, ensuring that there are no inconsistencies in the database.

Another example is an e-commerce website that needs to ensure that all orders are processed correctly and that customer data is kept secure. An RDBMS or SQL database would be an ideal choice as it provides ACID compliance, which guarantees the consistency, reliability, and security of the data.

*In conclusion*, an RDBMS or SQL database is an excellent choice for applications that require ACID compliance. These databases ensure that the data is processed reliably and consistently, making them an ideal choice for applications where data integrity and security are critical.

---

### Unstructured data? Go for *NO-SQL Database*

**NoSQL databases** are designed to store and manage unstructured data. Unlike relational databases, NoSQL databases do not use a fixed schema and do not enforce ACID properties. Instead, they provide flexible data models, horizontal scalability, and high availability. This makes NoSQL databases a good choice for storing and processing large volumes of unstructured data. If the data is unstructured and does not require ACID properties, a NoSQL database is a suitable option. 

> *For example*, a social media platform that generates large amounts of unstructured data, such as posts, comments, and likes, would benefit from using a NoSQL database. These databases are designed to handle a high volume of data and can easily scale horizontally to accommodate growth.

> *Another example* is an IoT (Internet of Things) application that collects sensor data from a variety of sources. The data generated by these devices is often unstructured and doesn't require ACID properties. A NoSQL database would be an excellent choice to store this data as it can handle large volumes of unstructured data and provide fast data access.

NoSQL databases come in many types, such as document-oriented, key-value, column-family, and graph databases. Some examples of popular NoSQL databases include MongoDB, Cassandra, Redis, and Neo4j. These databases provide different features and are optimized for different use cases.

*In conclusion*, if the data is unstructured and does not require ACID properties, a NoSQL database is an excellent option. These databases are designed to handle large volumes of unstructured data and provide flexible data models, horizontal scalability, and high availability. When choosing a NoSQL database, it's important to consider the specific use case and the database's features to ensure the best fit for the application.

---

### Complex data in the form of videos, images, files etc? Go for *Blob/Object storage*

When it comes to storing complex data such as videos, images, files, or any large binary objects, a Blob/Object Storage system is the most efficient and scalable solution. Unlike traditional file systems, which are designed to manage smaller data objects, blob/object storage systems are optimized for storing and retrieving large binary objects that can range in size from a few megabytes to terabytes or petabytes.

**Blob/Object storage** systems provide a scalable and cost-effective way to store and manage complex data. They offer built-in features such as high-availability, redundancy, and durability. With blob/object storage, the data is broken down into smaller parts or chunks that are distributed across multiple servers. This means that the data is always available, even in the event of a hardware failure or other issue.

Some examples of blob/object storage systems include Amazon S3, Microsoft Azure Blob Storage, and Google Cloud Storage. These platforms provide secure, durable, and scalable object storage solutions, designed to handle any type of unstructured data. They offer a wide range of features such as object versioning, object-level security, and data access control. These platforms also provide a high level of data durability, ensuring that the data is always protected and available.

*In conclusion*, if your system has complex data in the form of videos, images, files, or any large binary objects, a Blob/Object Storage system is the most effective solution. These systems provide scalable and cost-effective ways to store and manage unstructured data, with built-in features for high-availability, redundancy, and durability. When choosing a Blob/Object Storage system, it's important to consider the specific use case and the storage provider's features to ensure the best fit for the application.

---

### Requires complex pre-computation like a news feed? Use a *Message Queue & Cache*

In a system that requires complex pre-computation, such as generating a news feed, using a Message Queue and Cache can significantly improve performance and scalability. A Message Queue is a system that allows different components of a distributed system to communicate asynchronously with each other. A Cache is a temporary data storage system that keeps frequently accessed data close to the compute resources that require it. By using these two technologies, the system can optimize the pre-computation of data and reduce the workload on the compute resources.

A **Message Queue** system can be used to handle the incoming data feeds, such as user actions, news articles, or other events. The data can be processed asynchronously and passed to a pre-computation system that generates the news feed. The pre-computation system can then store the results in a Cache for fast access, eliminating the need for repeated computation.

> *Some good examples* of using a Message Queue and Cache in pre-computation systems include social media platforms like Twitter and Facebook, where a news feed is generated for each user based on their interests and activity. The incoming data feed can be processed by a message queue system, which passes it to a pre-computation system that generates the news feed. The pre-computed data is then stored in a cache for fast retrieval.

> *Another example* is e-commerce platforms like Amazon or eBay, where personalized recommendations are generated based on user behavior. The incoming data feed can be processed by a message queue system, which passes it to a pre-computation system that generates the personalized recommendations. The pre-computed data is then stored in a cache for fast retrieval.

*In conclusion*, using a Message Queue and Cache system can significantly improve performance and scalability in pre-computation systems that require complex computations. By using a message queue to handle the incoming data feeds and a cache to store the pre-computed data, the workload on the compute resources can be reduced, resulting in a more efficient and faster system. Social media and e-commerce platforms are good examples of applications that can benefit from this technology.

---

### Requires searching data in high volume? Consider using a *search index* (*Elasticsearch*)

In systems that require searching data in high volume, traditional database systems can often be slow and inefficient. To improve performance, it is recommended to use a search index, tries, or a search engine like Elasticsearch, which are designed to handle high-volume search queries quickly and efficiently.

**Search indexes** and tries are data structures that allow for efficient searching of large data sets. Search indexes, also known as inverted indexes, store a mapping of each term in the dataset to the location of that term in the data. Tries are a tree-like data structure that can efficiently store and search for strings.

Search engines like Elasticsearch are built on top of search indexes and provide a more complete solution to searching large data sets. Elasticsearch can store and search data across multiple indexes and has features for faceted search, full-text search, and geospatial search.

> *Good examples* of systems that use search indexes and engines include e-commerce platforms like Amazon or eBay, where users need to search for products based on keywords or other criteria. Social media platforms like Twitter also use search indexes and engines to search for tweets based on hashtags or other keywords. In the medical field, search indexes and engines are used to search through large amounts of medical data for specific symptoms or diseases.

*In conclusion*, search indexes, tries, and search engines like Elasticsearch provide efficient and scalable solutions for searching data in high volume. By using these technologies, complex search queries can be processed quickly and efficiently, resulting in faster and more accurate search results. Examples of applications that use these technologies include e-commerce, social media, and medical research.

---

### Should Scale SQL Database? Use *Database Sharding*

In systems that require high scalability, traditional SQL databases can often become a bottleneck due to their centralized architecture. One way to address this is by using database sharding, which is a technique that divides a single database into smaller, independent databases known as shards, each handling a subset of the data. This allows for more efficient scaling of the database while maintaining the ability to perform complex queries across the entire dataset.

**Database sharding** has several benefits, including increased scalability, improved performance, and better fault tolerance. By distributing the data across multiple shards, the system can handle larger volumes of data and more concurrent users. This can lead to faster query response times and improved overall system performance.

> *Good examples* of systems that use database sharding include social media platforms like Instagram and Twitter, which handle large volumes of data and users. In these systems, the user data is sharded across multiple databases, allowing for efficient scaling while maintaining fast query response times.

> *Another example* is e-commerce platforms like Etsy, which use database sharding to handle large volumes of product and customer data. In this case, the data is sharded based on categories or other criteria, allowing for efficient scaling while maintaining complex querying capabilities.

*In conclusion*, database sharding is an effective technique for scaling SQL databases to handle high volumes of data and users. By dividing the data into smaller, independent databases, the system can maintain performance and scale efficiently. Good examples of systems that use this technique include social media and e-commerce platforms.

---

### Need High Availability, Performance, & Throughput? Use a *Load Balancer*

In systems that require high availability, performance, and throughput, a load balancer is an effective solution. Load balancing is the process of distributing incoming network traffic across multiple servers or computing resources, known as a cluster, to optimize resource utilization, maximize throughput, and minimize response time.

**Load balancers** provide several benefits, including improved availability and reliability of the system, better utilization of resources, and improved scalability. By distributing traffic across multiple servers or resources, the load balancer can ensure that the system is available and responsive, even in the event of failures or spikes in traffic. Additionally, load balancers can optimize resource utilization by directing traffic to the most available and least loaded server, improving overall system performance and throughput.

> *Good examples* of systems that use load balancers include e-commerce platforms like Amazon and Netflix, which handle high volumes of traffic and require high availability and performance. In these systems, load balancers distribute traffic across multiple servers, allowing for efficient handling of requests and improved system performance.

> *Another example* is cloud computing platforms like Amazon Web Services and Microsoft Azure, which provide load balancing services to manage network traffic and distribute it across multiple instances or resources.

*In conclusion*, load balancing is an effective solution for ensuring high availability, performance, and throughput in systems that handle high volumes of traffic. Good examples of systems that use load balancers include e-commerce and cloud computing platforms, among others. By using load balancing techniques, these systems can ensure high availability and performance, even under heavy traffic loads.

---

### Requires faster data delivery globally, reliability, high availability, & performance? Use *CDN*

**Content Delivery Networks (CDNs)** are a distributed system of servers that are designed to provide faster data delivery, high availability, and reliability by caching and serving content from servers that are geographically closer to end-users. CDNs reduce the latency of content delivery by caching and serving content from the server that is closest to the end-user, thereby reducing the amount of time required to fetch content from a remote server.

CDNs provide several benefits, including improved website performance, faster content delivery, and better reliability. By distributing content across multiple servers, CDNs can handle high traffic volumes, ensure faster data delivery globally, and provide high availability, even in the event of a server failure. Additionally, CDNs provide an added layer of security against DDoS attacks by spreading the traffic across multiple servers.

> *Good examples* of systems that use CDNs include media streaming platforms like Netflix, YouTube, and Hulu, which need to deliver high-quality video content to millions of users across the globe. In these systems, CDNs are used to reduce the latency of content delivery and improve the overall user experience. E-commerce websites like Amazon and Walmart also use CDNs to ensure faster content delivery, high availability, and reliability, improving the overall user experience.

*In conclusion*, CDNs are an effective solution for faster data delivery, reliability, high availability, and performance in systems that require global delivery of content. Good examples of systems that use CDNs include media streaming and e-commerce platforms, among others. By using CDNs, these systems can provide a better user experience, improve the availability and reliability of content delivery, and enhance the performance of the system.

---

### Data with nodes, edges, and relationships like friend lists, & road connections? Use *Graph Database*

In systems that require modeling data with nodes, edges, and relationships, such as friend lists, social networks, and road connections, a graph database is a powerful solution. Unlike traditional relational databases, graph databases allow for efficient modeling, querying, and analyzing of complex relationships between data points.

A **graph database** stores data in a graph-like structure, where nodes represent entities, edges represent relationships between those entities, and properties represent attributes of those entities and relationships. This structure allows for efficient querying and analysis of complex data relationships, such as finding the shortest path between two nodes in a road network or identifying common friends in a social network.

> *Good examples* of systems that use graph databases include social networks like Facebook and LinkedIn, which require modeling complex relationships between users and their connections. In these systems, graph databases are used to efficiently store, query, and analyze data related to user connections, interests, and activities.

> *Another example* is transportation systems like Uber and Lyft, which use graph databases to model complex road networks, including road connections, traffic patterns, and optimal routes between locations. In these systems, graph databases are used to efficiently store, query, and analyze data related to the road network and provide optimal routing and navigation to drivers and passengers.

*In conclusion*, graph databases are a powerful solution for systems that require modeling data with nodes, edges, and relationships. Good examples of systems that use graph databases include social networks and transportation systems, among others. By using graph databases, these systems can efficiently store, query, and analyze complex data relationships, providing valuable insights and improving the overall system performance.

---

### System needs scaling of various components like servers, databases, etc? Use *Horizontal Scaling*

Horizontal scaling, also known as scaling out, is a technique used to increase the capacity of a system by adding more resources, such as servers, databases, or storage nodes. In horizontal scaling, additional resources are added in parallel, allowing the system to handle more requests and improve performance.

**Horizontal scaling** is particularly useful for systems that need to handle variable or unpredictable workloads, as it allows the system to dynamically scale up or down to meet demand. It also provides increased resilience and availability, as a failure in one component can be isolated and the remaining components can continue to function.

> *Good examples* of systems that use horizontal scaling include cloud-based services like Amazon Web Services (AWS) and Google Cloud Platform (GCP), which allow users to dynamically scale up or down their resources based on demand. These platforms use horizontal scaling to provide high availability, resilience, and performance to their users.

> *Another example* is social media platforms like Twitter and Facebook, which experience large spikes in traffic during popular events or breaking news. In these systems, horizontal scaling is used to dynamically add more resources to handle the increased workload, ensuring that the system remains responsive and available to users.

*In conclusion*, horizontal scaling is an effective technique for scaling various components like servers, databases, and storage nodes in a system. Good examples of systems that use horizontal scaling include cloud-based services and social media platforms, among others. By using horizontal scaling, these systems can provide high availability, performance, and resilience, while also allowing for dynamic scaling in response to changing demand.

---

### Requires high-performing database queries? Use *Database Indexes*

Database indexes are a powerful tool for improving the performance of database queries in systems that require high-performing data access. Indexes provide a way to quickly locate data in a database, reducing the amount of time needed to perform queries and improving the overall system performance.

A **database index **is a data structure that stores a subset of data from a table, organized in a way that allows for faster searching and sorting. Indexes can be created on one or more columns of a table, and can significantly improve the performance of queries that involve those columns.

> *Good examples* of systems that use database indexes include e-commerce websites like Amazon and eBay, which require fast access to large amounts of product data. In these systems, indexes are used to optimize search queries, allowing users to quickly find and purchase products.

> *Another example* is financial trading systems, which require fast access to large amounts of real-time data. In these systems, indexes are used to optimize queries that involve trading data, allowing traders to quickly analyze market trends and make informed decisions.

*In conclusion*, database indexes are a powerful tool for improving the performance of database queries in systems that require high-performing data access. Good examples of systems that use database indexes include e-commerce websites and financial trading systems, among others. By using indexes, these systems can provide fast access to large amounts of data, improving the overall system performance and user experience.

---

### Bulk job processing? Use *Batch Processing & Message Queues*

Batch processing is a technique used in systems that require the processing of large amounts of data or time-consuming tasks, such as generating reports, analyzing large datasets, or performing backups. Batch processing involves executing a large number of jobs or tasks in a batch or group, instead of processing them individually.

**Batch processing** is commonly used in systems that require bulk job processing, as it allows for the efficient processing of large volumes of data or tasks. Batch processing can also be combined with message queues to ensure that jobs are executed in a reliable and efficient manner.

> *Good examples* of systems that use batch processing and message queues include financial transaction processing systems, which process large volumes of transactions on a daily basis. In these systems, batch processing is used to perform tasks like reconciliation, reporting, and analysis, while message queues are used to manage the flow of transactions through the system.

> *Another example* is cloud-based systems like Amazon Web Services (AWS), which provide batch processing services like AWS Batch and AWS Lambda. These services allow users to easily execute large-scale batch jobs in the cloud, using message queues to manage the flow of data and ensure reliability.

*In conclusion*, batch processing and message queues are powerful tools for processing large volumes of data or time-consuming tasks in systems that require bulk job processing. Good examples of systems that use these techniques include financial transaction processing systems and cloud-based services like AWS. By using batch processing and message queues, these systems can efficiently and reliably process large amounts of data, improving the overall system performance and user experience.

---

### Requires reducing server load and preventing DOS attacks, Use a *Rate Limiter*

A rate limiter is a tool used in systems to control the rate at which requests are made to a server. By limiting the rate of requests, a rate limiter can reduce the load on a server, prevent denial of service (DoS) attacks, and ensure that the server is able to operate efficiently.

A **rate limiter** works by enforcing a limit on the number of requests that can be made within a given time period. When a client exceeds this limit, the rate limiter will block further requests from that client, preventing them from overwhelming the server.

> *Good examples* of systems that use rate limiters include web servers, APIs, and cloud-based services. In these systems, rate limiters are used to control the rate at which requests are made to the server, preventing DoS attacks and reducing server load. For example, popular web services like Twitter and Facebook use rate limiters to prevent users from sending too many requests and overloading their servers.

> *Another example* is online payment systems, which use rate limiters to prevent fraudulent transactions. By limiting the rate at which transactions can be made, payment systems can detect and prevent fraudulent activity in real-time, ensuring the security and reliability of the system.

*In conclusion*, rate limiters are a powerful tool for reducing server load and preventing DoS attacks in systems that require efficient and reliable operation. Good examples of systems that use rate limiters include web servers, APIs, and online payment systems. By using rate limiters, these systems can ensure the security and reliability of the system, providing a better user experience for their clients.

---

### System has a single point of failure? Implement *Redundancy* in that component

A single point of failure (SPOF) is a component of a system that, if it fails, can cause the entire system to fail. To prevent the failure of the entire system, redundancy can be implemented in that component. Redundancy is the process of creating backup components that can take over the function of the failed component in case it fails.

> *Good examples* of systems that use redundancy include data centers, servers, and storage devices. In a data center, redundancy can be achieved by having multiple power sources, cooling systems, and internet connections. In a server, redundancy can be achieved by having multiple power supplies, hard drives, and network cards. In a storage device, redundancy can be achieved by using RAID (redundant array of independent disks) technology.

By implementing **redundancy** in a system, the impact of a failure can be minimized, and the system can continue to operate even if a component fails. For example, in a data center, if one power source fails, the backup power source can take over, preventing the entire data center from going down.

> *Another example* is in a server cluster. By using load balancing and redundancy, traffic can be distributed across multiple servers, ensuring that if one server fails, the traffic can be automatically redirected to a backup server, preventing downtime and ensuring the continuity of service.

*In conclusion*, implementing redundancy in a system can help prevent single points of failure and ensure the continuity of service in the event of a component failure. Good examples of systems that use redundancy include data centers, servers, and storage devices. By implementing redundancy, these systems can operate with high availability, reducing downtime and improving the user experience.

---

### Need to be fault-tolerant & durable? we should implement *Data Replication*

**Data replication** is the process of creating multiple copies of data on different servers, making the system fault-tolerant and durable. By replicating data, the system can continue to operate even if one or more servers fail. This is because the data is stored on multiple servers, and in case of a failure, the system can continue to operate using the replica copies of the data.

> *Good examples* of systems that use data replication include distributed databases and cloud storage systems. In a distributed database, data is stored on multiple servers, and changes made to one copy are automatically replicated to other copies, ensuring consistency and durability. In cloud storage systems, data is replicated across multiple data centers, ensuring that even if one data center goes down, the data is still available from another data center.

Data replication can also be used in disaster recovery scenarios. In this case, a backup data center is set up in a different geographic location, and data is replicated from the primary data center to the backup data center. In case of a disaster at the primary data center, the system can failover to the backup data center, ensuring the continuity of service.

*In conclusion*, data replication is a useful technique for creating fault-tolerant and durable systems. Good examples of systems that use data replication include distributed databases and cloud storage systems. By replicating data, these systems can continue to operate even in the event of a server failure, ensuring the continuity of service and improving the user experience.

---

### System needs user-to-user communication in a fast way? Use *Websockets*

Websockets are a communication protocol that allows for real-time, bi-directional communication between a client and a server. They are often used in applications that require fast and responsive user-to-user communication, such as chat applications, gaming platforms, and collaborative work environments.

**Websockets** enable a persistent connection between the client and server, which allows for the efficient and fast transmission of data. This is in contrast to HTTP, which requires a new connection to be established for each request and response. By using Websockets, applications can achieve near-instant communication, allowing for a more seamless and natural user experience.

> *Good examples* of applications that use Websockets include chat applications like Slack, gaming platforms like Discord, and collaborative work environments like Google Docs. These applications require fast and responsive communication between users, and Websockets provide a reliable and efficient means of achieving this.

Websockets are supported by most modern web browsers, and many server-side frameworks and libraries offer built-in support for Websockets. This makes it easy to integrate Websockets into new or existing applications.

*In conclusion*, Websockets are a powerful tool for enabling fast and responsive user-to-user communication in applications that require it. Good examples of applications that use Websockets include chat applications, gaming platforms, and collaborative work environments. By leveraging Websockets, developers can create more efficient and seamless user experiences, improving the overall usability of their applications.

---

### Detect failures in a distributed system? Implement a *Heartbeat*

In distributed systems, where components are spread across multiple machines or networks, it is crucial to be able to detect and respond to failures quickly. One way to accomplish this is by implementing a heartbeat mechanism.

A **heartbeat** is a signal sent at regular intervals between the components of a distributed system to indicate that they are still functioning correctly. If a component does not receive a heartbeat signal from another component, it can assume that the other component has failed and take appropriate action, such as failing over to a backup or initiating a recovery process.

> *Good examples* of systems that use a heartbeat mechanism include Apache ZooKeeper, a distributed coordination service, and Apache Hadoop, a distributed computing platform. Both of these systems rely on a heartbeat to detect and respond to failures in a distributed environment.

Implementing a heartbeat mechanism typically requires setting up a separate component or service that is responsible for sending and receiving heartbeat signals. This can be done using various tools and technologies, such as network protocols like TCP/IP or specialized libraries and frameworks like Apache Curator or Consul.

*In conclusion*, implementing a heartbeat mechanism is an essential tool for detecting and responding to failures in a distributed system. Examples of systems that use a heartbeat mechanism include Apache ZooKeeper and Apache Hadoop. By leveraging heartbeat signals, developers can ensure that their distributed systems remain reliable and functional, even in the face of failures or unexpected events.

---
   
### Ensure data integrity? Use *Checksum Algorithm*

Ensuring data integrity is a critical requirement for many systems. One way to achieve this is by using a checksum algorithm, which is a mathematical function that generates a fixed-size digital fingerprint of a data set. This fingerprint can then be used to verify the integrity of the data by comparing it to the checksum generated from the same data set at a later point in time.

> *A good example* of a system that uses a **checksum algorithm** is the Git version control system. Git uses a cryptographic hash function to generate a checksum for every version of a file, which is used to detect any changes to the file. If any changes are made to the file, the checksum will no longer match, indicating that the file has been modified.

> *Another example* of a system that uses a checksum algorithm is the ZFS file system, which uses checksums to ensure the integrity of data stored on disk. When data is written to disk, a checksum is calculated and stored along with the data. When the data is read back from disk, the checksum is calculated again and compared to the original checksum. If the checksums do not match, it indicates that the data has been corrupted and needs to be restored from a backup.

*In conclusion*, checksum algorithms are an effective way to ensure data integrity. Examples of systems that use checksum algorithms include Git and the ZFS file system. By using checksums to detect data corruption, developers can ensure that their systems remain reliable and secure.

---

### Transfer data between various servers in a decentralized way? we should go for the *Gossip Protocol*

The Gossip Protocol is a distributed communication protocol that enables nodes in a network to exchange information with each other in a decentralized way. Each node shares information with a few randomly selected neighbors, who in turn share the information with their neighbors, creating a "gossip" effect that spreads the information throughout the network.

The **Gossip Protoco**l is well-suited for systems that require decentralized communication between multiple servers, such as distributed databases or blockchain networks. One example of a system that uses the Gossip Protocol is Apache Cassandra, a highly scalable NoSQL database. In Cassandra, nodes use the Gossip Protocol to exchange information about the state of the cluster, allowing the database to scale horizontally across multiple servers.

> *Another example* of a system that uses the Gossip Protocol is the Ethereum blockchain. Ethereum uses a variant of the Gossip Protocol called Whisper to enable communication between nodes on the network. Whisper allows nodes to exchange messages in a decentralized way, ensuring that the network remains resilient and fault-tolerant.

*In conclusion*, the Gossip Protocol is a powerful tool for enabling decentralized communication between servers. Examples of systems that use the Gossip Protocol include Apache Cassandra and the Ethereum blockchain. By leveraging the Gossip Protocol, developers can create highly scalable and fault-tolerant systems that can operate in a decentralized and distributed environment.

---

### Scale servers with add/removal of nodes efficiently, with no hotspots? we should implement *Consistent Hashing*

**Consistent Hashing** is a technique used for distributing data among a large number of servers in a way that allows for efficient scaling and easy addition or removal of nodes. In Consistent Hashing, a hash function is used to map each data item to a position on a ring, and each server is also mapped to a position on the ring. When a new data item is added or a server is removed or added to the system, only a small portion of the data needs to be rehashed, allowing for fast and efficient scaling.

> *One example* of a system that uses Consistent Hashing is the Apache Cassandra NoSQL database. Cassandra uses Consistent Hashing to distribute data across a cluster of servers, allowing for easy scaling and fault-tolerance. Another example of a system that uses Consistent Hashing is the Amazon DynamoDB database, which also uses Consistent Hashing to distribute data across a large number of servers.

Consistent Hashing is a powerful tool for creating scalable and fault-tolerant systems. By leveraging the properties of hash functions and a ring topology, Consistent Hashing allows for efficient distribution of data and nodes, with no hotspots or bottlenecks. This makes it an ideal choice for systems that need to scale with the addition or removal of nodes, such as distributed databases or web applications with high traffic.

---

### Deal with a location like maps, nearby resources? Use *Quadtree, Geohash*, etc

When dealing with geographic data, such as maps, locations, or nearby resources, it is essential to use an efficient data structure to store and retrieve the information quickly. Two popular data structures for dealing with location-based data are Quadtree and Geohash.

A Quadtree is a tree-like data structure in which each node has exactly four children, dividing a two-dimensional space into four equal parts. It is commonly used in applications such as maps, image processing, and video games. The Quadtree can be used to index points, polygons, and lines based on their geographic location, and it enables fast location-based queries such as finding all nearby resources or points within a certain radius.

**Geohash** is a hierarchical spatial data structure that encodes a geographic location into a short string of letters and digits. The shorter the string, the higher the accuracy. It is used to represent a location as a single value, enabling easy storage, retrieval, and indexing of geographic data. Geohash can be used to search for resources or points within a certain geographic area, and it is commonly used in location-based services, such as ride-sharing apps and social media.

> *For example*, if we are building a food delivery app that needs to provide users with nearby restaurants, we could use a Quadtree to index the locations of all restaurants and enable fast location-based queries. Similarly, we could use Geohash to encode the locations of all restaurants and enable fast searches within a certain radius.

---

### Has microservices? Use an *API Gateway* (Auth, SSL Termination, Routing etc)

In a microservices architecture, each service is responsible for a specific functionality, and multiple services work together to deliver the desired result. As the number of microservices grows, it becomes increasingly challenging to manage, maintain, and secure them. This is where an API Gateway comes into the picture.

An **API Gateway** is a service that provides a single entry point to access multiple microservices. It acts as a reverse proxy, intercepting and forwarding client requests to the appropriate microservices. API Gateways provide various features, including authentication, SSL termination, load balancing, routing, and caching.

Using an API Gateway offers several benefits. Firstly, it provides a simplified way for clients to access multiple microservices. Secondly, it provides a centralized location for handling common concerns, such as authentication and SSL termination, which reduces the complexity of individual services. Additionally, an API Gateway can handle cross-cutting concerns such as rate limiting, caching, and routing, which simplifies the development and deployment of microservices.

> *One of the popular examples* of an API Gateway is Netflix's Zuul. Zuul provides various features, including load balancing, rate limiting, and routing, among others. Another example is Kong, which is an open-source API Gateway that provides various features, including authentication, caching, and logging, among others. In summary, an API Gateway provides an effective way to manage microservices and handle cross-cutting concerns efficiently.

---

### Conclusion

In this blog post, we have learned 25 golden rules of software system design that can help us create better, faster, and more reliable systems. These rules cover various aspects of design, such as requirements, architecture, modularity, scalability, security, testing, documentation, and maintenance. By following these rules, we can avoid common pitfalls and ensure that our systems meet the needs of our users and stakeholders.

I hope you enjoyed reading this blog post and found it helpful for your own projects. Thank you for reading!

---


