Enhance system performance and improve system response
![[Pasted image 20260416225149.png | 800]]
Client-side Cache (Browser / App):
cache stored in users device/browser
In application front end browser stores the HTTP Responses to enable fast retrievel of data
🧠 Client-side Cache
Netflix app stores:
Thumbnails
Last watched positions

CDN: (content delivery Network):
![[Pasted image 20260416225832.png | 600]]

Distributed servers across the world storing static content
used to improve the delivery of static content
Images, videos, CSS/JS files etc
It redue the Latency and Redue backend load
Netflix uses its own CDN called Open Connect
Stores:
Movies
TV shows

👉 When you play a video:

It does NOT come from central server
It comes from a nearby ISP server


Load Balancer
Load Balancer distributes traffic across servers
Sometimes also caches responses
It reduce duplicate requests reaching backend
eg. If 1000 users request same homepage -> LB may server cached version
![[Pasted image 20260416225950.png | 800]]

API Gateway:
Single Entry point for all backend services
Responsible for:
Routing
Authentication
Rate Limiting
Caching responses
It avoides calling microservices repeatedly 


Message Broker (Kafka):
Handles async communication via messages
Not a cache directly, but helps avoid real-time load
Kafka can store massive amount of messages on the disk.
This allow user to retrieve the messages at their own pace
eg. User posts → goes to queue → processed later
Think of it as load absorver, not cache

Distributed cache (Redis):
A centralized, in-memory cache shared across services
Stores: Session data, Frequently accessed DB data, computed results
Rdis can store key-value pairs in memory.
Provide high read/write performance compared to the traditional databases.
eg. User profile fetched once --> stored in Redis --> reused everywhere
Stores:
User recommendations
Session data

Full Text Search:
This is search engine with indexed data.
Stores preprocessed, indexed version of data
Full Text Search like Elastic Search can index data for document search and log search

Database-level cache (Relational DB):
WAL Write ahead log: data is typically written to a WAL before being Indexed in a B-tree
The Buffer pool is a memory area used to cache query results,
while materialized views can precompute query results for faster performance
Transaction log returns all transactions and updated to the databse,
Replication log tracks the replication state in a database cluster.

Even database has internal caching:

🔁 Buffer Pool
Stores frequently accessed data pages in memory
Avoid disk reads
🧾 WAL (Write-Ahead Log)
Logs changes before writing to DB
Helps recovery + performance
📊 Materialized View
Precomputed query results
Avoid expensive joins
🧠 Transaction Log
Tracks all operations
🔄 Replication Log
Sync data across replicas

caching data is an essential technique for optimizing system performance.

Service-level cache (Service A&B):
CPU Cache
L1, L2 cache inside processor
Fastest possible access

 RAM Cache
In-memory objects
Example: HashMap cache inside app

 Disk Cache
Stored on local disk
Slower but persistent

why multiple levels:
Speed hierarchy: CPU > RAM > Disk > Network



Hardware Cache
L1
most fast
L2
L3

Translation Lookaside buffer (TLB)
this stores the cache about translating virtual memory address to physical memory address.

Operating system Level
Page cache
File System caches
Inode cache

Full Reqeust Flow
Client Cache → CDN → Load Balancer → API Gateway → Redis → Service Cache → Database Cache → Disk

Best way to remember
(Client side -> CDN -> Gateway -> DB)
At each step, System tries to avoid going deeper