
https://www.youtube.com/watch?v=C842vFY5kRo

## Single Server System:
![[Pasted image 20261001191848.png]] 
# System Design

> Source: [System Design Course – APIs, Databases, Caching, CDNs, Load Balancing & Production Infra](https://www.youtube.com/watch?v=C842vFY5kRo)
>
> Goal: Understand how to design scalable, reliable, secure production systems.

---

# 01. Introduction

## Core Idea

System design is primarily about making **architectural decisions and trade-offs**, not simply writing code.

### System Design Mindset

```text
Requirements
    ↓
Constraints
    ↓
Architecture
    ↓
Components
    ↓
Trade-offs
    ↓
Scalability + Reliability + Security
```

### Key Questions

When designing a system, ask:

1. What does the system need to do?
2. How many users?
3. How much traffic?
4. How much data?
5. What are the latency requirements?
6. What happens when a component fails?
7. What needs to scale?
8. Where should data be stored?
9. What can be cached?
10. How should the system be secured?

---

# 02. Single Server Setup

![[Pasted image 20261001192415.png | 800]]
## Basic Architecture

Start with the simplest possible architecture.

```text
User
  ↓
DNS
  ↓
Server
  ├── Web Application
  ├── API
  ├── Database
  └── Cache
```

The important principle:

> Start simple → identify bottlenecks → introduce complexity only when necessary.

---

## Request Flow

Example:

```text
User
 ↓
Browser / Mobile App
 ↓
DNS
 ↓
Server IP
 ↓
HTTP Request
 ↓
Application Server
 ↓
Database / Cache
 ↓
HTTP Response
 ↓
Client
```

### DNS

DNS translates a domain name into an IP address.

```text
example.com
     ↓
DNS
     ↓
192.168.x.x
```

The client can then communicate with the server.

---

## Web vs Mobile

A server may return different representations depending on the client.

### Browser

```text
Client → Server
        ↓
      HTML
```

### Mobile Application

```text
Mobile App → API
             ↓
            JSON
```

The backend can therefore serve multiple types of clients.

---

# 03. Databases — SQL, NoSQL & Graph

Database selection is an architectural decision.

There is no universally "best" database.

Choose based on:

* Data model
* Query patterns
* Consistency requirements
* Scalability
* Transaction requirements
* Performance
* Relationship complexity

---

## SQL / Relational Databases

Examples:

* PostgreSQL
* MySQL
* Oracle
* SQLite

Data is organized into:

```text
Tables
 ├── Rows
 └── Columns
```

Example:

```text
Users
+----+-------+----------------+
| id | name  | email          |
+----+-------+----------------+
| 1  | Abhi  | abhi@example.com|
+----+-------+----------------+
```

### Strengths

* Structured schema
* Strong relationships
* SQL queries
* Transactions
* ACID guarantees
	* Atomicity: The series of operations considered and a single transaction
	* Consistency : one valid state to another valid state.
	* Isolation : Each transaction run independently without knowing about other transaction
	* Durability : Data Remains even if the system fails
* Complex joins

### Good Use Cases

* Banking
* Payments
* Orders
* Inventory
* Systems requiring strong consistency

---

# 04. NoSQL Databases

NoSQL databases are designed around different data models and scalability requirements.

Major categories:

```text
NoSQL
├── Key-Value
├── Document
├── Wide-Column
└── Graph
```

---

## Key-Value

```text
key → value

"user:123" → {...}
```

Good for:

* Caching
* Sessions
* Fast lookups

Examples:

* Redis
* DynamoDB

---

## Document Database

Data is stored as documents.

Example:

```json
{
  "id": 123,
  "name": "Abhi",
  "skills": [
    "Java",
    "Python"
  ]
}
```

Good when data naturally maps to documents.

Examples:

* MongoDB
* Couchbase

---

## Wide-Column

Data is organized around rows and column families.

Useful for:

* Very large datasets
* High write throughput
* Distributed systems

Examples:

* Cassandra
* HBase

---

## Graph Database

Designed around relationships.

```text
User
 ↓ follows
User
 ↓ likes
Post
 ↓ belongs to
Category
```

Good when relationships are the primary query pattern.

Examples:

* Neo4j
* Amazon Neptune

---

# 05. Vertical vs Horizontal Scaling

Scaling becomes necessary when one server cannot handle the workload.

---

## Vertical Scaling

Also called:

> Scale Up

Increase resources of the existing machine.

```text
Before

Server
├── 4 CPU
└── 8 GB RAM


After

Server
├── 32 CPU
└── 128 GB RAM
```

### Advantages

* Simple
* Minimal architectural changes
* Easy to implement

### Problems

* Hardware limits
* Expensive at large scale
* Single point of failure
* Eventually reaches a ceiling

---

## Horizontal Scaling

Also called:

> Scale Out

Add more servers.

```text
        ┌── Server 1
Client ─┼── Server 2
        └── Server 3
```

### Advantages

* Better scalability
* Better fault tolerance
* Can add servers as demand increases

### Challenge

Application servers should generally be **stateless**.

Bad:

```text
Server 1
 └── User session
```

Because the next request may reach Server 2.

Better:

```text
Server 1 ─┐
Server 2 ─┼── Shared Session Store
Server 3 ─┘
```

---

# 06. Load Balancing

When multiple servers exist, something must decide where requests go.

That component is the:

> Load Balancer

Architecture:

```text
                 ┌── Server 1
Client → LB ─────┼── Server 2
                 └── Server 3
```

## Responsibilities

### 1. Traffic Distribution

Distribute requests among servers.

### 2. Fault Tolerance

If a server fails:

```text
Server 1 → UP
Server 2 → UP
Server 3 → DOWN

LB → Server 1 / Server 2
```

### 3. Scalability

Adding another server becomes easier:

```text
LB
├── Server 1
├── Server 2
├── Server 3
└── Server 4
```

---

# 07. Load Balancing Algorithms

## Round Robin

Requests are distributed sequentially.

```text
Request 1 → Server 1
Request 2 → Server 2
Request 3 → Server 3
Request 4 → Server 1
```

### Good when

Servers have similar capacity and workloads are relatively uniform.

---

## Least Connections

Send the request to the server with the fewest active connections.

```text
Server 1 → 20 connections
Server 2 → 8 connections
Server 3 → 14 connections

New request → Server 2
```

Useful when requests have different processing times.

---

## Least Response Time

Prefer the server currently responding fastest.

Useful when:

* Servers have different performance
* Request latency varies

---

## IP Hash

The client's IP is used to determine the server.

```text
Client IP
   ↓
Hash
   ↓
Server
```

The same client tends to reach the same server.

Useful when some client-specific state exists.

However:

> IP hashing is not a replacement for proper stateless architecture.

---

## Weighted Load Balancing

Servers can receive different amounts of traffic.

```text
Server 1 → Weight 5
Server 2 → Weight 3
Server 3 → Weight 1
```

Useful when servers have different capacities.

---

## Geographic Routing

Route users to geographically appropriate servers.

```text
India User
    ↓
India Region

US User
    ↓
US Region
```

Benefits:

* Lower latency
* Better regional performance
* Useful for globally distributed systems

---

## Consistent Hashing

Maps keys to servers using a hash-based distribution.

Useful for:

* Distributed caches
* Distributed storage
* Systems where minimizing key movement matters when nodes change

---

# 08. Health Checks

Load balancing alone isn't enough.

The load balancer needs to know:

> "Is this server actually healthy?"

Example:

```text
LB
├── Server 1 → HEALTHY
├── Server 2 → HEALTHY
└── Server 3 → UNHEALTHY
```

Traffic is removed from unhealthy servers.

---

## Health Check Flow

```text
Load Balancer
      ↓
Health Check
      ↓
Server
      ↓
Healthy?
  ↙       ↘
YES       NO
 ↓         ↓
Traffic   Remove
```

Typical health check:

```http
GET /health
```

Response:

```http
200 OK
```

A failed health check can cause the load balancer to stop routing traffic to that instance.

---

# 09. Single Point of Failure — SPOF

A **Single Point of Failure** is a component whose failure can bring down the system.

Bad:

```text
          ┌── Server 1
Client → LB
          └── Server 2

        Database
           ↑
           │
      Single DB
```

If the database fails:

```text
Entire system → DOWN
```

The database is therefore a SPOF.

---

## Removing SPOFs

Instead of:

```text
Application
     ↓
Single DB
```

Use redundancy:

```text
Application
     ↓
Primary DB
     ↓
Replica DB
```

Or more sophisticated distributed architectures depending on requirements.

---

## SPOF Checklist

For every component ask:

```text
Can it fail?
     ↓
If it fails, what breaks?
     ↓
Can another component take over?
     ↓
Is failover automatic?
```

Important:

> Redundancy is useful only if the system can actually route around the failed component.

---

# 10. API Design

An API defines how software components communicate.

```text
Client
  ↓
API
  ↓
Backend
  ↓
Database
```

A good API should be:

* Predictable
* Consistent
* Secure
* Versionable
* Easy to consume
* Scalable

---

## API Design Questions

Before designing an API:

1. Who are the clients?
2. What operations are required?
3. What data is exchanged?
4. What protocol should be used?
5. How will authentication work?
6. How will authorization work?
7. How will errors be represented?
8. How will the API evolve?

---

# 11. API Protocols

Common communication approaches include:

```text
HTTP
REST
GraphQL
gRPC
WebSockets
AMQP
```

These are not interchangeable.

Choose based on the communication requirements.

---

# 12. Transport Layer — TCP vs UDP

## TCP

TCP provides reliable, ordered delivery.

```text
Client
  ⇄
TCP
  ⇄
Server
```

Characteristics:

* Connection-oriented
* Reliable
* Ordered
* Retransmission
* Congestion control

Useful when data must arrive correctly.

Examples:

* HTTP/HTTPS
* APIs
* Database connections

---

## UDP

UDP is connectionless and does not provide TCP-style delivery guarantees.

Characteristics:

* Low overhead
* No guaranteed delivery
* No guaranteed ordering
* Faster for certain workloads

Useful where speed matters more than perfect delivery.

Examples:

* Real-time communication
* Streaming
* DNS
* Gaming

---

# 13. RESTful APIs

REST is an architectural style commonly used for HTTP APIs.

Example resource:

```text
/users
```

---

## HTTP Methods

### GET

Retrieve data.

```http
GET /users/123
```

### POST

Create a resource.

```http
POST /users
```

### PUT

Replace/update a resource.

```http
PUT /users/123
```

### PATCH

Partially update a resource.

```http
PATCH /users/123
```

### DELETE

Delete a resource.

```http
DELETE /users/123
```

---

## Resource-Oriented Design

Prefer:

```text
GET /users/123/orders
```

over action-oriented designs such as:

```text
GET /getUserOrders
```

The exact API design depends on the API's semantics, but the resource-oriented model is a common REST convention.

---

## Statelessness

Each request should contain the information necessary to process it.

```text
Request 1 → Server 1

Request 2 → Server 3
```

The server should not depend on local memory from Request 1.

This makes horizontal scaling easier.

---

## Pagination

Do not return millions of records in one request.

Instead:

```http
GET /users?page=1&limit=20
```

or cursor-based pagination:

```http
GET /users?cursor=abc123
```

Pagination reduces:

* Response size
* Database workload
* Network usage
* Client memory usage

---

## Filtering

```http
GET /products?category=shoes
```

---

## Sorting

```http
GET /products?sort=price
```

---

## Versioning

APIs evolve.

Example:

```text
/api/v1/users
/api/v2/users
```

Versioning can allow clients to migrate without immediately breaking older integrations.

---

# 14. GraphQL

GraphQL allows clients to request the data they need.

REST:

```text
GET /user/123
GET /user/123/orders
GET /user/123/profile
```

GraphQL:

```graphql
query {
  user(id: 123) {
    name
    email
    orders {
      id
      total
    }
  }
}
```

---

## Main Advantage

Client controls the requested data shape.

This can reduce:

### Over-fetching

Server returns more data than required.

### Under-fetching

Client needs multiple API calls to obtain required data.

---

## GraphQL vs REST

| REST                          | GraphQL                                      |
| ----------------------------- | -------------------------------------------- |
| Multiple resource endpoints   | Often single GraphQL endpoint                |
| Server defines response shape | Client specifies fields                      |
| Simple HTTP model             | Query language                               |
| Easy HTTP caching patterns    | Caching requires additional consideration    |
| Very common public API style  | Useful for flexible client data requirements |

Use the architecture that matches the problem rather than treating one as universally superior.

---

# 15. Authentication

Authentication answers:

> **Who are you?**

```text
Client
  ↓
Credentials / Token
  ↓
Authentication System
  ↓
Identity
```

Examples:

* Username/password
* Session cookies
* JWT
* OAuth 2.0

---

## Authentication vs Authorization

This distinction is critical.

### Authentication

```text
Who are you?
```

### Authorization

```text
What are you allowed to do?
```

Example:

```text
Login
 ↓
Authentication
 ↓
User = Abhi
 ↓
Authorization
 ↓
Can Abhi delete this resource?
```

---

# 16. Authentication Methods

## Basic Authentication

Credentials are sent with requests using the HTTP Basic scheme.

Because credentials are sensitive, HTTPS is essential.

---

## Session-Based Authentication

```text
Login
 ↓
Server creates session
 ↓
Session ID
 ↓
Cookie
 ↓
Client sends cookie
```

Server maintains session state.

---

## JWT

JSON Web Token can carry claims about the authenticated identity.

Typical flow:

```text
Login
 ↓
Authentication Server
 ↓
JWT
 ↓
Client
 ↓
Authorization header
 ↓
API
```

Example:

```http
Authorization: Bearer <token>
```

JWTs can support stateless verification, but they introduce trade-offs around revocation, expiration, storage, and token size.

---

## OAuth 2.0

OAuth 2.0 is primarily an **authorization framework** for delegated access.

Example:

```text
User
 ↓
Application
 ↓
Authorization Server
 ↓
Access Token
 ↓
Resource Server
```

A common example is allowing an application to access another service on the user's behalf without giving the application the user's password.

---

# 17. Authorization

Authorization determines what an authenticated identity can access.

```text
Authentication
      ↓
Identity
      ↓
Authorization
      ↓
Allowed / Denied
```

---

## RBAC

Role-Based Access Control.

```text
User
 ↓
Role
 ↓
Permissions
```

Example:

```text
Admin
 ├── Create
 ├── Read
 ├── Update
 └── Delete

Viewer
 └── Read
```

Good when permissions naturally map to organizational roles.

---

## ABAC

Attribute-Based Access Control.

Access is determined using attributes.

```text
User attributes
+
Resource attributes
+
Environment/context
        ↓
     Policy
        ↓
 Allow / Deny
```

Example:

```text
department = finance
AND
resource = finance-data
AND
location = corporate-network
```

---

## ACL

Access Control List.

Permissions are attached directly to a resource.

```text
Document
 ├── Abhi → READ
 ├── John → WRITE
 └── Admin → FULL
```

---

# 18. API Security

Security should be considered during system design, not added at the end.

Important areas include:

* HTTPS/TLS
* Authentication
* Authorization
* Input validation
* Rate limiting
* Secure credential handling
* Token management
* Protection against common web attacks
* Logging and monitoring

---

## HTTPS

Use encrypted communication between client and server.

```text
Client
  ⇅
 HTTPS / TLS
  ⇅
Server
```

Protects data while it is transmitted.

---

## Input Validation

Never blindly trust client input.

```text
Client Input
     ↓
Validate
     ↓
Sanitize / Reject
     ↓
Application
```

---

## Rate Limiting

Restrict how many requests a client can make.

```text
Client
 ↓
100 requests/minute
 ↓
Rate Limiter
 ↓
API
```

Useful against:

* Abuse
* Brute-force attacks
* Accidental traffic spikes
* Resource exhaustion

---

## Security Principle

Treat every external request as untrusted.

```text
External Input
      ↓
Validate
      ↓
Authenticate
      ↓
Authorize
      ↓
Process
```

---

# System Design Mental Model

The concepts in this section connect together:

```text
                    ┌───────────────┐
                    │    Clients    │
                    │ Web / Mobile  │
                    └───────┬───────┘
                            │
                            ▼
                         DNS
                            │
                            ▼
                    ┌───────────────┐
                    │ Load Balancer │
                    └───────┬───────┘
                            │
                ┌───────────┼───────────┐
                ▼           ▼           ▼
             Server 1    Server 2    Server 3
                │           │           │
                └───────────┼───────────┘
                            │
                            ▼
                       Cache / API
                            │
                            ▼
                         Database
```

The system evolves by identifying bottlenecks:

```text
Single Server
     ↓
Database Separation
     ↓
Horizontal Scaling
     ↓
Load Balancer
     ↓
Health Checks
     ↓
Remove SPOFs
     ↓
Caching
     ↓
CDN
     ↓
Distributed Systems
```

---

# Interview Framework

When given a system-design problem:

## 1. Clarify Requirements

```text
Functional requirements
+
Non-functional requirements
```

## 2. Estimate Scale

Think about:

* Users
* Requests/sec
* Storage
* Bandwidth
* Read/write ratio

## 3. Start Simple

```text
Client
 ↓
Server
 ↓
Database
```

## 4. Identify Bottlenecks

Ask:

```text
What breaks first?
```

## 5. Scale

Introduce:

* Load balancer
* Multiple servers
* Database scaling
* Cache
* CDN

## 6. Reliability

Ask:

```text
What happens if X fails?
```

## 7. Security

Consider:

* Authentication
* Authorization
* Encryption
* Rate limiting
* Input validation

## 8. Explain Trade-offs

Never just say:

> "Use Redis."

Explain:

> "Redis is useful here because this workload has frequent reads and the data can tolerate the consistency characteristics of a cache."

---

# Core Takeaways

> **Start simple.**

> **Scale only where the bottleneck exists.**

> **Prefer stateless application servers when horizontally scaling.**

> **Redundancy without failover does not provide meaningful fault tolerance.**

> **Authentication = Who are you?**

> **Authorization = What are you allowed to do?**

> **Database choice depends on workload and access patterns.**

> **Load balancing distributes traffic and can provide failure isolation.**

> **System design is fundamentally about trade-offs.**
