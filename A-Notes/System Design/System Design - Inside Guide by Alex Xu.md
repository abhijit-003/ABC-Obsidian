[System Design Interview An Insider’s Guide by Alex Xu (z-lib.org).pdf](https://github.com/mukul96/System-Design-AlexXu/blob/master/System%20Design%20Interview%20An%20Insider%E2%80%99s%20Guide%20by%20Alex%20Xu%20(z-lib.org).pdf)
[Medium](https://medium.com/@iam-abdulmoiz/system-design-interview-an-insider-guide-by-alex-xu-chapter-1-7496adb09fb5)

# What is System Design
- System Design is the process of designing software architecture that can handle users, data, traffic, and failures efficiently.
- It includes:
	- Architecture
	- Database
	- APIs
	- Scalability
	- Performance
	- Reliability
	- Security
	- Communication between services

# Chapter 1: Scale From Zero to Millions of Users
## 1. Single Server Setup
- Every big journey starts with the small setup
- In system design we start with the simplest possible setup
- In single server setup everything runs on single server: database, web app, cache etc
- ![[Pasted image 20260511221138.png]]
1. when user sends the request which goes to DNS provider, which are basically third party services. 
2. DNS basically translate human readable txt into machine understandable IP address
3. Once receive IP address then request goes to the server which share the response in the form of HTML JSON

**Web Applications:**: These are the basically combination or server side languages (java, python, node etc) to handle business logic, storage etc and Client side languages (html, css, js) to handle User Interface,

**Mobile Applications:** Mobile app are basically the application which stored on mobile which uses HTTP protocol to communicate between mobile app and the web server. **JSON** is the widely used for API reponse.

## 2. Databse:
- With the growth of the users one server is not enough. we required multiple servers
- One server for web traffic and another for the database.
- Separating Mobile/Web traffic(web tier) and database (data tier) servers allows them to be scaled independently
- ![[Pasted image 20260511230100.png]]

#### There are two types of Database:
1. **Relational Database**: this is basically Relational Database Management System (RDBMS)
	- It stored the structured data in row and columns format
	- eg. MySQL, Oracle SQL, PostgreSQL etc
2. **Non-Relational Database**:
	- These are also called and no-sql databases
	- When the data is un-structured then No SQL database is used
	- eg. CouchDB, Neo3j, Amazon DynamoDB HBase etc

## Scaling
#### 1. Vertical Scaling
- Vertical scaling considered as "Scale Up" the system which mean increasing the Database, CPU size and adding more power to existing resources
- When traffic is low vertical scaling is good
- Vertical scaling is come up with the limitation
- i.e we can't scale up unlimited to single server and also it does not handle the failover and redundancy 
#### 2.Horizontal Scaling
- Horizontal scaling considered as "Scale Out" the system, means adding more number of resources, i'e more database, more servers.
- Horizontal scaling overcomes the limitations of Vertical Scaling

## Load Balancer:
- If many users tries to access the url simultaneously then network traffic will increase and system will slow down
- In this case Load Balancer will best use
- Load balancer distributes the network traffic among different server to avoid load on single machine
- ![[Pasted image 20260512220620.png]]
	- In this diagram users connects to Load Balancer directly via a public IP
	- Then Load Balance connect to the server via a **Private IP**
	- For better security private IPs are used. 
	- These IPs are only accessible within the network. 
	- Private IP is a IP which is reachable only between servers in the same network, however it is unreachable over the internet

Till this point we handled the web tier, i.e failover will not occur as when one server goes down load balance will re-direct the traffic to another server.

Now what about **Data Tier**, there is only one database. when it fails the failover can't be avoided. Now **Database Replication** comes in place

## Database Replication
- The Process of copying and maintaining database from a primary (master) database to secondary (slave) database.
- Database replication mainly include **Master** database and **Slave** database
- **Master Database:**:
	- This database mainly handles the Write operations
	- All the Insert, update, create etc commands are directed to Master Database
- **Slave Database:**
	- This database mainly handles Read operations
- In larger system usually there are large number of read operations over write operations
- Therefore most Database Replications include one Master database and Multiple slave nodes
- ![[Pasted image 20260512221956.png]]
- Here: when slave database fails then request redirect to other slave DB or Master DB temporarily.
- If Master DB fails, then one of the slave node promoted as Master node
- Disadvantage: 
- In Production it is bit complicated to promote slave DB to Master as there is possibility of bi different data on both the DBs
- For this, the Multi-Master or Circular replication methods are used
- Circular Replication:
	- This is the replication method where data is replicated in circular manner
	- i.e DB1 --> DB2, DB2 --> DB3, DB3 --> DB1

##### Server Setup with Multiple Node and Database Replication:
![[Pasted image 20260512222746.png]]

Now the system is stable and avoiding the failover. But, now performance comes in place. This can be done by adding cache layer and shifting static content (JS/CSS/Images/Videos files) to the **Content Delivery Network (CDN)**

## Cache
- A Cache is a temporarily storage which stores the most expensive response or frequently called accessed data in temporarily memory so that subsequent requests are served more quickly.
- When we have to load the web page then every time request goes to the database to fetch the data and larger and frequent database call = lower performance
- The cache mitigate this problem

### Cache Tier
- Cache tier is a temporarily storage layer, much faster than the database.
- This improves the performance of the system, reduces the database workload and it have ability to scale the cache tier independently
- ![[Pasted image 20260512223804.png]]
- Working:
	- If user sends request if first come to cache layer
	- It checks whether the requested data is present or not,
	- if present then it send back response else it will query the database.
	- This caching strategy is called a read-through cache
- **Expiration Policy:**
	- This decided how long data will store in cache
	- It is recommended to use appropriate value, not less and not permanent.
- **Consistency:**
	- This involves keeping the data store and the cache sync.
	- Inconsistency can happen because data-modification operation on data store and cache are not is a single transaction.
	- In large system it is bit complicated to sync the data in cache continuously
- **Mitigation Failures:**
	- A single cache server represents a potential **single point of failure (SPOF)**
	- **SPOF**: A SPOF is a part of a system that, if it fails, will stop the entire system from working.
	- So for this, it is best to have multiple cache servers across different data centers
	- another recommended approach is to to over provision the required memory by certain percentages. This provides a buffer as the memory usages increases.
	- ![[Pasted image 20260512225147.png]]
- **Eviction Policy:**
	- When cache storage is full there is possibility that for new data the present cache data will be removed. This is called the Eviction Policy.
	- **Least Recently Used (LRU)** is the most popular cache eviction policy
	- other policies are:
		- Least Frequently Used(LFU)
		- First in First Out (FIFO)
## Content Delivery Network (CDN):
- A system of distributed servers that delivers content from the nearest server to the user
- Eg. When you access the Netflix from pune then data will be accessed from nearest Indian server instead of USA server
- ![[Pasted image 20260512230032.png]]
- CDN companies:
	- Cloudflare
	- Akamai Technologies
	- Amazon Web Services CloudFront

#### Architecture after adding CDN and Cache
![[Pasted image 20260512230444.png]]

## Stateless Web Tier:
- A web server architecture where server does not store client session/state locally between requests. 
- Each request  is treated as completely independent
- In this we move the state (session data) out of the web tier.
- Best practice is to store data in persistent storage such as RDBMS or NoSQL.
- In this server does not store user session in memory, login state locally and request history locally.
- Instead it uses, Database, Redis, JWT Token etc
- It helps horizontal scaling and we can add/remove any servers anytime
- **Request Flow**
	- Client → Load Balancer → Any Web Server
- eg.
	- In Instagram when user sends requests:
		- Req 1 may hit Server A
		- Req 2 may hit Server C
	- Still works because session is stored centrally (Redis/DB/JWT), not inside the server memory

### Stateful Architecture:
- A stateful server remembers client data (state) from one request to the next.
- ![[Pasted image 20260513214155.png]]
- eg.
	- If users A's data is stored on Server 1 then to authenticate user A, HTTP requests must be routed to server 1.
	- If the request routed to server 2 then authentication will fail as server 2 dont' have A user data.
### Stateless Architecture
- Stateless server keeps no state information
- ![[Pasted image 20260513214528.png]]
- In stateless architecture, HTTP request can be sent to any server.
- Server uses the shared data store.

## Updated Architecture with Stateless web tier
- ![[Pasted image 20260513214808.png]]

- Now this is the well designed system which will handle the failover and will improve performance.

- When website grows rapidly and attracts a significant number of users internationally. 
- To Improve availability and provide a better user experience across wider geographical areas, supporting multiple data centers is crucial.
## Data Centers
- In normal operation, users are **geoDNS-routed**, also known as geo-routed.
- This splits X% to East-India and (100-X)% in West-India.
- **geoDNS:**
	- This is a DNS service that allows domain names to be resolved to IP addresses based on the location of a user.
	- ![[Pasted image 20260513215745.png]]
	- Data Synchronization is the most important thing in the data centers setup, as if any of the node fails and all the request transfers to the another server then, another server should have the session data.
	- For the Data replication is the most used technique

## Message Queue:
- 