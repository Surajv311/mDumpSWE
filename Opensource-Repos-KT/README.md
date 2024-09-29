
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

#### [surajvm1/LearningMicroservices - Major points _al](https://github.com/surajvm1/LearningMicroservices/tree/dev/feat1)

- k6, ab can be used for API load testing. 
  - Commands which we can run to grant permissions to a new user on a db/table: 
  ```
  ## Giving all necessary permissions to our new user which we use to create tables/db. 
  postgresdockerlocal-# grant all privileges on database fapidb to postgresdluser;
  postgresdockerlocal=# GRANT CONNECT ON DATABASE fapidb TO postgresdluser;
  postgresdockerlocal=# GRANT pg_read_all_data TO postgresdluser;
  postgresdockerlocal=# GRANT pg_write_all_data TO postgresdluser;
  postgresdockerlocal=# GRANT ALL PRIVILEGES ON DATABASE "fapidb" to postgresdluser;
  postgresdockerlocal=# GRANT USAGE ON SCHEMA public TO postgresdluser;
  postgresdockerlocal=# GRANT ALL ON SCHEMA public TO postgresdluser;
  postgresdockerlocal=# GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO postgresdluser;
  ```
- List the servers using the port, use: `lsof -i :8000`
- To insert 1M records in postgres; Script to run in db container terminal: 
  - Info: 
  ```
  Query: 
  INSERT INTO tpsqltable (id, name, type, phone, address, created_at)
  SELECT s AS id, 'name_' || s AS name,
  CASE WHEN s % 3 = 0 THEN 'type1'
       WHEN s % 3 = 1 THEN 'type2'
       ELSE 'type3'
  END AS type,
  (CASE WHEN random() < 0.5 THEN 8000000000 ELSE 9000000000 END + s % 1000000) AS phone,
  'address data ' || s AS address,
  '2000-01-01'::timestamp + (s % 3650 || ' days')::interval AS created_at
  FROM generate_series(1, 5000000) AS s;
  
  Similarly, to shuffle all the records in table: 
  -- Step 1: Create a new table with shuffled rows: CREATE TABLE shuffled_table AS SELECT * FROM tpsqltable ORDER BY random();
  -- Step 2: Drop the original table: DROP TABLE tpsqltable;
  -- Step 3: Rename the shuffled table to the original table name: ALTER TABLE shuffled_table RENAME TO tpsqltable;
  ```
- To understand query details we can use 'explain' keyword in pgsql: `fapidb=> explain select * from tpsqltable where phone=9000516507;`
- You can find host machine (in my case macbook) ip using `ping -c 1 $(hostname)` or ifconfig command.
- Each Docker container has its own network stack. localhost within a Docker container refers to the container itself, not the host machine. By default, Docker containers are attached to a default network (bridge network) which isolates them from the host network and from each other unless configured otherwise.
- The IP addresses are given to us by an Internet Service Provider (ISP). You will be able to connect your computer and modem to their network and access the Internet after the ISP visits your home to install your connection. When you launch a Web browser to conduct a Google search or send an email, and everything goes smoothly, you can be sure that everything is functioning as it should. If it initially doesn't work, you might need to engage with your ISP's technical support team to have things resolved. When you establish a new connection, one of the initial things you could do is to check your IP address. Please take note of the IP address, but avoid becoming overly attached because it's possible that your ISP uses a dynamic IP address, that means it could change without warning. To have a static IP you have to tell your ISP provider. But why dynamic IP?: It is solely a numerical issue. There are a countless number of computer users connected to the Internet simultaneously all over the world. Some people use the Internet frequently, while others only occasionally, and occasionally only long enough to write an email. Every person who is available on the internet needs a distinct IP address, as was already mentioned. When you consider all the logistics involved, it would have been extremely costly to assign a fixed, static IP to each and every ISP subscriber. Additionally, the number of static IP addresses might have quickly run out with the current IP address generation (basically IPv4).Dynamic IP addresses were subsequently introduced to the world of the Internet. This made it possible for ISPs to give their customers a dynamic IP address as needed. Every time you go online, that IP address is essentially "loaned" to you; [Reference](https://www.javatpoint.com/why-has-my-ip-address-changed). Hence, you may also observe a change in your macbook/host IP if you switch from wifi to mobile hotspot for your macbook internet connectivity. 
- How is docker able to route the connection from container to host machine via bridge network concept?:
  - Bridge Network Creation: By default, Docker containers are connected to a bridge network. This is an internal virtual network that allows containers to communicate with each other and the host machine. 
  - Container-to-Host Communication: When you specify the host machine's IP address in the container, the container's networking stack knows to route the traffic out of the container to the host machine's network interface. 
  - Network Address Translation (NAT): Docker uses Network Address Translation to map container ports to host ports. When a container tries to access an IP address and port, Docker's networking translates these into appropriate network requests. 
  - To access a service running on the host machine from a Docker container, you specify the host machine's IP address. For example, if your host machine's IP address is 192.168.1.100, you can configure your application to connect to this IP.
- [What is the difference between 0.0.0.0, 127.0.0.1 and localhost?](https://stackoverflow.com/questions/20778771/what-is-the-difference-between-0-0-0-0-127-0-0-1-and-localhost):
  - 127.0.0.1 is normally the IP address assigned to the "loopback" or local-only interface. This is a "fake" network adapter that can only communicate within the same host. It's often used when you want a network-capable application to only serve clients on the same host. A process that is listening on 127.0.0.1 for connections will only receive local connections on that socket.
  - "localhost" is normally the hostname for the 127.0.0.1 IP address. It's usually set in /etc/hosts (or the Windows equivalent named "hosts" usually at C:\Windows\System32\Drivers\etc\hosts). You can use it just like any other hostname - try ping localhost to see how it resolves to 127.0.0.1. 
  - 0.0.0.0 has a couple of different meanings, but in this context, when a server is told to listen on 0.0.0.0 that means "listen on every available network interface". The loopback adapter with IP address 127.0.0.1 from the perspective of the server process looks just like any other network adapter on the machine, so a server told to listen on 0.0.0.0 will accept connections on that interface too.
- CGI (Common Gateway interfaces), WSGI, ASGI:
  - Common Gateway Interface (CGI) is an interface specification that enables web servers to execute an external program to process HTTP or HTTPS user requests. Uvicorn is a web server. It handles network communication - receiving requests from client applications such as users' browsers and sending responses to them. It communicates with FastAPI using the Asynchronous Server Gateway Interface (ASGI), a standard API for Python web servers that run asynchronous code. When a user enters a web site, their browser makes a connection to the site’s web server (this is called the request). The server looks up the file in the file system and sends it back to the user’s browser, which displays it (this is the response). This is roughly how the underlying protocol, HTTP, works. Dynamic web sites are not based on files in the file system, but rather on programs which are run by the web server when a request comes in, and which generate the content that is returned to the user. They can do all sorts of useful things, like display the postings of a bulletin board, show your email, configure software, or just display the current time. These programs can be written in any programming language the server supports. Since most servers support Python, it is easy to use Python to create dynamic web sites. Most HTTP servers are written in C or C++, so they cannot execute Python code directly – a bridge is needed between the server and the program. These bridges, or rather interfaces, define how programs interact with the server. There have been numerous attempts to create the best possible interface, but there are only a few worth mentioning. Not every web server supports every interface. Many web servers only support old, now-obsolete interfaces; however, they can often be extended using third-party modules to support newer ones. This interface, most commonly referred to as “CGI”, is the oldest, and is supported by nearly every web server out of the box. Programs using CGI to communicate with their web server need to be started by the server for every request. So, every request starts a new Python interpreter – which takes some time to start up – thus making the whole interface only usable for low load situations. The upside of CGI is that it is simple – writing a Python program which uses CGI is a matter of about three lines of code. This simplicity comes at a price: it does very few things to help the developer. Using CGI sometimes leads to small annoyances while trying to get these scripts to run. The Web Server Gateway Interface, or WSGI for short, is defined in PEP 333 and is currently the best way to do Python web programming. While it is great for programmers writing frameworks, a normal web developer does not need to get in direct contact with it. When choosing a framework for web development it is a good idea to choose one which supports WSGI. The big benefit of WSGI is the unification of the application programming interface. When your program is compatible with WSGI – which at the outer level means that the framework you are using has support for WSGI – your program can be deployed via any web server interface for which there are WSGI wrappers. You do not need to care about whether the application user uses mod_python or FastCGI or mod_wsgi – with WSGI your application will work on any gateway interface. The Python standard library contains its own WSGI server, wsgiref, which is a small web server that can be used for testing. Another definition: A WSGI server, which stands for Web Server Gateway Interface, is a specification that allows web servers to communicate with Python web applications. It acts as a middleman between the web server (like Nginx or Apache) and the web application written in Python.
- The sequence in which you execute instructions in Dockerfile matters a lot.
- [What exactly is 'Building'?](https://stackoverflow.com/questions/1622506/what-exactly-is-building): 
  - Building means many things to many people, but in general it means starting with source files produced by developers and ending with things like installation packages that are ready for deployment.
- Multi-stage builds are useful to anyone who has struggled to optimize Dockerfiles while keeping them easy to read and maintain. With multi-stage builds, you use multiple FROM statements in your Dockerfile. Each FROM instruction can use a different base, and each of them begins a new stage of the build. You can selectively copy artifacts from one stage to another, leaving behind everything you don't want in the final image.
- [Difference between the 'COPY' and 'ADD' commands in a Dockerfile?](https://stackoverflow.com/questions/24958140/what-is-the-difference-between-the-copy-and-add-commands-in-a-dockerfile):
  - COPY is same as 'ADD', but without the tar and remote URL handling. In other words, they work similarly, just that ADD can do more things.
- [Difference between CMD and ENTRYPOINT in a Dockerfile?](https://stackoverflow.com/questions/21553353/what-is-the-difference-between-cmd-and-entrypoint-in-a-dockerfile):
  - The ENTRYPOINT specifies a command that will always be executed when the container starts. The CMD specifies arguments that will be fed to the ENTRYPOINT.
- Etc etc... 




----------------------------------------------------------------------



