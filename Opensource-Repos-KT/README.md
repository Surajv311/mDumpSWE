
# Opensource_Github_repos_knowledge_extraction 


#### [donnemartin/system-design-primer _al](https://github.com/donnemartin/system-design-primer)

- A service is scalable if it results in increased performance in a manner proportional to resources added. Generally, increasing performance means serving more units of work, but it can also be to handle larger units of work, such as when datasets grow. Another way to look at performance vs scalability: If you have a performance problem, your system is slow for a single user. If you have a scalability problem, your system is fast for a single user but slow under heavy load.

- Latency is the time to perform some action or to produce some result. Throughput is the number of such actions or results per unit of time. Generally, you should aim for maximal throughput with acceptable latency.

- CAP Theorem: Also note that in a distributed computer system, you can only support two of the following guarantees:
  - Consistency - Every read receives the most recent write or an error
  - Availability - Every request receives a response, without guarantee that it contains the most recent version of the information
  - Partition Tolerance - The system continues to operate despite arbitrary partitioning due to network failures

- With multiple copies of the same data, we are faced with options on how to synchronize them so clients have a consistent view of the data. Consistency: Weak (After a write, reads may or may not see it), Eventual (After a write, reads will eventually see it (typically within milliseconds); Data is replicated asynchronously), Strong (After a write, reads will see it; Data is replicated synchronously) 

- There are two complementary patterns to support high availability: 
  - fail-over:
    - In active-passive fail-over, heartbeats are sent between the active and the passive server on standby. If the heartbeat is interrupted, the passive server takes over the active's IP address and resumes service. The length of downtime is determined by whether the passive server is already running in 'hot' standby or whether it needs to start up from 'cold' standby. Only the active server handles traffic. Active-passive failover can also be referred to as master-slave failover.
    - In active-active fail-over, both servers are managing traffic, spreading the load between them. If the servers are public-facing, the DNS would need to know about the public IPs of both servers. If the servers are internal-facing, application logic would need to know about both servers. Active-active failover can also be referred to as master-master failover.
  - replication:
    - In master-slave, master serves reads and writes, replicating writes to one or more slaves, which serve only reads. Slaves can also replicate to additional slaves in a tree-like fashion. If the master goes offline, the system can continue to operate in read-only mode until a slave is promoted to a master or a new master is provisioned. 
    - In master-master, both masters serve reads and writes and coordinate with each other on writes. If either master goes down, the system can continue to operate with both reads and writes.
  - All of above have their own set of advantages/disadvantages.  

- Availability is often quantified by uptime (or downtime) as a percentage of time the service is available. 99.9% availability qualifies to having acceptable downtime of 43m 49.7s/month. In case of 99.99%, acceptable downtime is 4m 23s/month. 
  - If a service consists of multiple components prone to failure, the service's overall availability depends on whether the components are in sequence or in parallel.
    - In sequence: `Availability (Total) = Availability (Foo) * Availability (Bar)`
    - In parallel: `Availability (Total) = 1 - (1 - Availability (Foo)) * (1 - Availability (Bar))`

- Domain Name System (DNS) translates a domain name such as www.example.com to an IP address. DNS is hierarchical, with a few authoritative servers at the top level. Your router or ISP provides information about which DNS server(s) to contact when doing a lookup. Lower level DNS servers cache mappings, which could become stale due to DNS propagation delays. DNS results can also be cached by your browser or OS for a certain period of time, determined by the time to live (TTL).
    - NS record (name server) - Specifies the DNS servers for your domain/subdomain.
    - MX record (mail exchange) - Specifies the mail servers for accepting messages.
    - A record (address) - Points a name to an IP address.
    - CNAME (canonical) - Points a name to another name or CNAME (example.com to www.example.com) or to an A record.
  - Services such as CloudFlare and Route 53 provide managed DNS services. Some DNS services can route traffic through various methods: Weighted round robin, Latency-based, Geolocation-based
  - (Disadvantages): Accessing a DNS server introduces a slight delay, although mitigated by caching described above. And DNS server management could be complex. Also, DNS services have recently come under DDoS attack, preventing users from accessing websites such as Twitter without knowing Twitter's IP address(es).

- Content Delivery Network (CDN) is a globally distributed network of proxy servers, serving content from locations closer to the user. Generally, static files such as HTML/CSS/JS, photos, and videos are served from CDN, although some CDNs such as Amazon's CloudFront support dynamic content. The site's DNS resolution will tell clients which server to contact. Serving content from CDNs can significantly improve performance in two ways:
    - Users receive content from data centers close to them
    - Your servers do not have to serve requests that the CDN fulfills
  - Push CDNs receive new content whenever changes occur on your server. You take full responsibility for providing content, uploading directly to the CDN and rewriting URLs to point to the CDN. You can configure when content expires and when it is updated. Content is uploaded only when it is new or changed, minimizing traffic, but maximizing storage. Sites with a small amount of traffic or sites with content that isn't often updated work well with push CDNs. Content is placed on the CDNs once, instead of being re-pulled at regular intervals.
  - Pull CDNs grab new content from your server when the first user requests the content. You leave the content on your server and rewrite URLs to point to the CDN. This results in a slower request until the content is cached on the CDN. A time-to-live (TTL) determines how long content is cached. Pull CDNs minimize storage space on the CDN, but can create redundant traffic if files expire and are pulled before they have actually changed. Sites with heavy traffic work well with pull CDNs, as traffic is spread out more evenly with only recently-requested content remaining on the CDN.
  - (Disadvantages): CDN costs could be significant depending on traffic, although this should be weighed with additional costs you would incur not using a CDN. Content might be stale if it is updated before the TTL expires it. CDNs require changing URLs for static content to point to the CDN.

- Load balancers distribute incoming client requests to computing resources such as application servers and databases. In each case, the load balancer returns the response from the computing resource to the appropriate client. Load balancers are effective at:
    - Preventing requests from going to unhealthy servers
    - Preventing overloading resources
    - Helping to eliminate a single point of failure
    - Load balancers can be implemented with hardware (expensive) or with software such as HAProxy.
  - Additional benefits include:
    - SSL termination - Decrypt incoming requests and encrypt server responses so backend servers do not have to perform these potentially expensive operations
    - Session persistence - Issue cookies and route a specific client's requests to same instance if the web apps do not keep track of sessions. Note that to protect against failures, it's common to set up multiple load balancers, either in active-passive or active-active mode.
  - Load balancers can route traffic based on various metrics, including: Random, Least loaded, Session/cookies, Round robin or weighted round robin, Layer 4, Layer 7. 
  - Layer 4 load balancers look at info at the transport layer to decide how to distribute requests. Generally, this involves the source, destination IP addresses, and ports in the header, but not the contents of the packet. Layer 4 load balancers forward network packets to and from the upstream server, performing Network Address Translation (NAT).
  - Layer 7 load balancers look at the application layer to decide how to distribute requests. This can involve contents of the header, message, and cookies. Layer 7 load balancers terminate network traffic, reads the message, makes a load-balancing decision, then opens a connection to the selected server. For example, a layer 7 load balancer can direct video traffic to servers that host videos while directing more sensitive user billing traffic to security-hardened servers.
  - Load balancers can also help with horizontal scaling, improving performance and availability. But disadvantages for horizontal scaling is: It introduces complexity and involves cloning servers - hence servers should be stateless: they should not contain any user-related data like sessions or profile pictures and sessions can be stored in a centralized data store such as a database (SQL, NoSQL) or a persistent cache (Redis, Memcached); Downstream servers such as caches and databases need to handle more simultaneous connections as upstream servers scale out
  - (Disadvantages): The load balancer can become a performance bottleneck if it does not have enough resources or if it is not configured properly. Introducing a load balancer to help eliminate a single point of failure results in increased complexity. A single load balancer is a single point of failure, configuring multiple load balancers further increases complexity.

- Reverse Proxy: It is a web server that centralizes internal services and provides unified interfaces to the public. Requests from clients are forwarded to a server that can fulfill it before the reverse proxy returns the server's response to the client.
  - (Benefits): Increased security - Hide information about backend servers, blacklist IPs, limit number of connections per client; Increased scalability and flexibility - Clients only see the reverse proxy's IP, allowing you to scale servers or change their configuration; SSL termination - Decrypt incoming requests and encrypt server responses so backend servers do not have to perform these potentially expensive operations; Compression - Compress server responses; Caching - Return the response for cached requests Static content - Serve static content directly like html/css, photos, videos. 
  - Deploying a load balancer is useful when you have multiple servers. Often, load balancers route traffic to a set of servers serving the same function. Reverse proxies can be useful even with just one web server or application server, opening up the benefits described in the previous section. Solutions such as NGINX and HAProxy can support both layer 7 reverse proxying and load balancing.
  - [Reverse proxy vs API Gateway vs Load Balancer _vl](https://www.youtube.com/watch?v=RqfaTIWc3LQ)

- Microservices: Can be described as a suite of independently deployable, small, modular services. Each service runs a unique process and communicates through a well-defined, lightweight mechanism to serve a business goal. Pinterest, for example, could have the following microservices: user profile, follower, feed, search, photo upload microservices, etc.

- Caching improves page load times and can reduce the load on your servers and databases. In this model, the dispatcher will first lookup if the request has been made before and try to find the previous result to return, in order to save the actual execution. Databases often benefit from a uniform distribution of reads and writes across its partitions. Popular items can skew the distribution, causing bottlenecks. Putting a cache in front of a database can help absorb uneven loads and spikes in traffic.
  - We can have caching at: Client, Web server, Database, CDN, Application, Database query level, Object level caching.
  - When to update the cache: 
    - Cache-aside: The application is responsible for reading and writing from storage. The cache does not interact with storage directly. In short: Look for entry in cache -> resulting in a cache miss -> Load entry from the database -> Add entry to cache -> Return entry. Cache-aside is also referred to as lazy loading. Only requested data is cached, which avoids filling up the cache with data that isn't requested.
    - Write-through: The application uses the cache as the main data store, reading and writing data to it, while the cache is responsible for reading and writing to the database. In short: Application adds/updates entry in cache -> Cache synchronously writes entry to data store -> Return
    - Write-behind (write-back): In write-behind, the application does the following, In short: Add/update entry in cache -> Asynchronously write entry to the data store -> thereby improving write performance
    - Refresh-ahead: You can configure the cache to automatically refresh any recently accessed cache entry prior to its expiration. Refresh-ahead can result in reduced latency vs read-through if the cache can accurately predict which items are likely to be needed in the future.
    - All have their own set of advantages, disadvantages. 

- Asynchronism
  - Message queues receive, hold, and deliver messages. If an operation is too slow to perform inline, you can use a message queue with the following workflow:
      - An application publishes a job to the queue, then notifies the user of job status
      - A worker picks up the job from the queue, processes it, then signals the job is complete
    - The user is not blocked and the job is processed in the background. During this time, the client might optionally do a small amount of processing to make it seem like the task has completed. For example, if posting a tweet, the tweet could be instantly posted to your timeline, but it could take some time before your tweet is actually delivered to all of your followers.
    - Eg: Redis is useful as a simple message broker but messages can be lost. RabbitMQ is popular but requires you to adapt to the 'AMQP' protocol and manage your own nodes. Amazon SQS is hosted but can have high latency and has the possibility of messages being delivered twice.
  - Tasks queues receive tasks and their related data, runs them, then delivers their results. They can support scheduling and can be used to run computationally-intensive jobs in the background. Celery has support for scheduling and primarily has python support.
  - Back pressure: If queues start to grow significantly, the queue size can become larger than memory, resulting in cache misses, disk reads, and even slower performance. Back pressure can help by limiting the queue size, thereby maintaining a high throughput rate and good response times for jobs already in the queue. Once the queue fills up, clients get a server busy or HTTP 503 status code to try again later. Clients can retry the request at a later time, perhaps with exponential backoff.


#### [surajv311/myCS-NOTES _al](https://github.com/Surajv311/myCS-NOTES)

- [Horizontal vs Vertical scaling _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(1).jpg) 
- [2 phase vs 3 phase commit _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(10).jpg) 
- [Pub-Sub model _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(11).jpg) 
- [Cascading failure in Distributed Systems, CDN _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(13).jpg) 
- [Forward Proxy, Reverse Proxy _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(16).jpg) 
- [Service Mesh _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(17).jpg) 
- [How DNS works? _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(19).jpg) 
- [Consistent hashing _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(2).jpg) 
- [L4 and L7 load balancing _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(20).jpg) 
- [System Design Algos _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(22).jpg) 

- Paxos is an algorithm that enables a distributed set of computers (for example, a cluster of distributed database nodes) to achieve consensus over an asynchronous network.
- A split brain situation occurs when a distributed system, such as Elasticsearch, loses communication between its nodes. This can happen for a variety of reasons, such as network issues, hardware failures, or software bugs.
- Cross-origin resource sharing (CORS) is a mechanism for integrating applications. CORS defines a way for client web applications that are loaded in one domain to interact with resources in a different domain.
- A Bloom filter is a space-efficient probabilistic data structure that is used to test whether an element is a member of a set.
- Forward Proxy (Proxies on behalf of clients), Reverse Proxy(Proxies on behalf of servers)
- Service Mesh: In short, it manages communication between microservices. 
- A canary deployment is a progressive rollout of an application that splits traffic between an already-deployed version and a new version, rolling it out to a subset of users before rolling out fully.
- NAT stands for network address translation. It's a way to map multiple private addresses inside a local network to a public IP address before transferring the information onto the internet. Organizations that want multiple devices to employ a single IP address use NAT, as do most home routers.
- A port number is a way to identify a specific process to which an internet or other network message is to be forwarded when it arrives at a server.
- Message/Task queue, Monoliths, Microservices, ACID-BASE, Cache, Sharding, Architectures, etc. also covered in the repo. 


----------------------------------------------------------------------





















