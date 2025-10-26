# 90-Day System Design Study Guide
## Complete Concepts Breakdown for Every Day

This guide provides detailed concepts, practice tasks, and key questions for each day of your system design preparation journey.

---

## Table of Contents
- [Week 1: Foundation & Prerequisites (Days 1-7)](#week-1)
- [Week 2: Core System Components (Days 8-14)](#week-2)
- [Week 3: Distributed Systems & Advanced Patterns (Days 15-21)](#week-3)
- [Week 4: Modern Architecture Patterns (Days 22-28)](#week-4)
- [Week 5-8: System Design Practice](#week-5-8)
- [Week 9-12: Interview Mastery](#week-9-12)

---
# Week 1: Foundation & Prerequisites (Days 1-7)

### Day 1: Programming Fundamentals Review

#### 🎯 Core Concepts to Learn:

**Object-Oriented Programming:**
- 4 Pillars of OOP:
  - **Encapsulation**: Bundle data and methods, hide internal details
  - **Abstraction**: Show only essential features, hide implementation
  - **Inheritance**: Create new classes from existing ones (IS-A relationship)
  - **Polymorphism**: Same interface, different implementations
- Classes vs Objects vs Interfaces
- Composition vs Inheritance (prefer composition over inheritance)
- SOLID Principles (overview):
  - Single Responsibility
  - Open/Closed
  - Liskov Substitution
  - Interface Segregation
  - Dependency Inversion

**Data Structures:**
- **Arrays**: 
  - Static vs Dynamic arrays
  - O(1) access by index
  - O(n) insertion/deletion (except at end)
- **Linked Lists**:
  - Singly linked (one pointer)
  - Doubly linked (two pointers)
  - O(n) access, O(1) insertion/deletion if you have pointer
- **Hash Tables**:
  - Key-value mapping
  - Hash function maps key to index
  - Collision handling:
    - Separate chaining (linked list at each bucket)
    - Open addressing (linear probing, quadratic probing)
  - Average O(1) insert/search/delete
- **Trees**:
  - Binary tree (max 2 children)
  - Binary Search Tree: left < parent < right
  - Balanced trees: AVL, Red-Black
  - Traversals: Inorder, Preorder, Postorder
- **Stacks & Queues**:
  - Stack: LIFO (Last In First Out) - push/pop
  - Queue: FIFO (First In First Out) - enqueue/dequeue

**Time & Space Complexity:**
- **Big O Notation**:
  - O(1): Constant - array access
  - O(log n): Logarithmic - binary search
  - O(n): Linear - simple loop
  - O(n log n): Linearithmic - merge sort
  - O(n²): Quadratic - nested loops
  - O(2ⁿ): Exponential - recursive fibonacci
- **Analysis Types**:
  - Best case: minimum time
  - Average case: expected time
  - Worst case: maximum time
- **Space-Time Tradeoffs**:
  - Use more memory to save time (caching)
  - Use more time to save memory (recompute)
- **Amortized Analysis**: Average time per operation over sequence

#### 💻 Practice Tasks:
1. Implement hash table with separate chaining
   - Create array of linked list buckets
   - Implement hash function
   - Handle collisions
   - Implement dynamic resizing (when load factor > 0.75)

2. Implement Binary Search Tree
   - Insert operation (maintain BST property)
   - Delete operation (handle 3 cases: leaf, one child, two children)
   - Search operation
   - Inorder traversal (should print sorted)

3. Solve LeetCode Problems:
   - #1 Two Sum (use hash table for O(n) solution)
   - #217 Contains Duplicate (use hash set)

#### 📖 Resources & Key Questions:
- **Resources**:
  - Big O Cheat Sheet: https://www.bigocheatsheet.com/
  - VisuAlgo: https://visualgo.net/ (visualize data structures)
  - GeeksforGeeks OOP concepts

- **Key Questions**:
  - Why is hash table average O(1) but worst case O(n)?
  - When would you use linked list over array?
  - What's the difference between O(n) and O(2n)?

---

### Day 2: Network Fundamentals

#### 🎯 Core Concepts to Learn:

**HTTP/HTTPS Protocol:**
- **HTTP Request Methods**:
  - GET: Retrieve data (idempotent, can be cached)
  - POST: Create new resource (not idempotent)
  - PUT: Update entire resource (idempotent)
  - PATCH: Partial update
  - DELETE: Remove resource (idempotent)
  - HEAD: Same as GET but no response body
  - OPTIONS: Describes communication options

- **HTTP Status Codes**:
  - 2xx Success:
    - 200 OK
    - 201 Created
    - 204 No Content
  - 3xx Redirection:
    - 301 Moved Permanently
    - 302 Found (temporary redirect)
    - 304 Not Modified (use cached version)
  - 4xx Client Errors:
    - 400 Bad Request
    - 401 Unauthorized
    - 403 Forbidden
    - 404 Not Found
    - 429 Too Many Requests
  - 5xx Server Errors:
    - 500 Internal Server Error
    - 502 Bad Gateway
    - 503 Service Unavailable
    - 504 Gateway Timeout

- **Important HTTP Headers**:
  - **Request Headers**:
    - Host: Domain name
    - User-Agent: Client information
    - Accept: Response types client can handle
    - Authorization: Credentials (Bearer token, Basic auth)
    - Cookie: Stored state from previous response
    - Content-Type: Format of request body
  - **Response Headers**:
    - Content-Type: Format of response body
    - Set-Cookie: Store data in client
    - Cache-Control: Caching directives
    - Location: Redirect URL
    - Access-Control-Allow-Origin: CORS header

- **HTTPS**:
  - HTTP + TLS/SSL encryption
  - SSL Handshake Process:
    1. Client sends supported cipher suites
    2. Server selects cipher suite, sends certificate
    3. Client verifies certificate with CA
    4. Exchange keys
    5. Encrypted communication starts
  - Port 443 (HTTP uses port 80)

- **HTTP Versions**:
  - HTTP/1.1: Text-based, one request per connection (or keep-alive)
  - HTTP/2: Binary, multiplexing (multiple requests on one connection), server push
  - HTTP/3: Uses QUIC (UDP-based), better performance on poor networks

**TCP vs UDP:**
- **TCP (Transmission Control Protocol)**:
  - Connection-oriented
  - 3-way handshake: SYN → SYN-ACK → ACK
  - Reliable: Guarantees delivery, order, error checking
  - Flow control: Sender won't overwhelm receiver
  - Congestion control: Adapts to network conditions
  - Use cases: HTTP, HTTPS, Email, File Transfer
  - Slower but reliable

- **UDP (User Datagram Protocol)**:
  - Connectionless
  - No handshake, just send packets
  - Unreliable: No guarantee of delivery or order
  - No flow/congestion control
  - Use cases: Video streaming, Gaming, DNS, VoIP
  - Faster but can lose packets

- **TCP 3-Way Handshake**:
  1. Client sends SYN (synchronize)
  2. Server responds SYN-ACK (synchronize-acknowledge)
  3. Client sends ACK (acknowledge)
  4. Connection established

**Client-Server Architecture:**
- **Request-Response Model**:
  - Client initiates requests
  - Server processes and responds
  - Synchronous communication
- **Stateless vs Stateful**:
  - Stateless: Server doesn't remember previous requests (HTTP)
  - Stateful: Server maintains session state (WebSockets)
- **Connection Pooling**:
  - Reuse TCP connections
  - Avoid handshake overhead for each request

**DNS (Domain Name System):**
- **Purpose**: Translate domain names to IP addresses
- **DNS Hierarchy**:
  - Root servers (13 logical servers)
  - TLD servers (.com, .org, .net)
  - Authoritative name servers (actual domain records)
- **DNS Resolution Process**:
  1. Check browser cache
  2. Check OS cache
  3. Query recursive resolver (ISP)
  4. Resolver queries root → TLD → authoritative
  5. IP address returned and cached
- **DNS Records**:
  - **A**: Maps domain to IPv4 address
  - **AAAA**: Maps domain to IPv6 address
  - **CNAME**: Alias (maps domain to another domain)
  - **MX**: Mail exchange server
  - **TXT**: Text records (SPF, DKIM)
  - **NS**: Name server

- **DNS Caching**:
  - Browser cache (5 minutes typically)
  - OS cache
  - ISP cache
  - TTL (Time To Live) controls cache duration

#### 💻 Practice Tasks:
1. **Analyze HTTP with curl**:
   ```bash
   curl -I https://google.com
   curl -v https://api.github.com
   ```
   - Identify status codes
   - Examine headers
   - Check redirect chains

2. **Build HTTP Server**:
   - Create simple server (Python/Node.js)
   - Handle GET and POST requests
   - Return different status codes
   - Parse request headers
   - Build HTTP client that displays response headers

3. **DNS Investigation**:
   ```bash
   nslookup google.com
   dig google.com
   ```
   - Trace DNS resolution
   - Identify name servers
   - Check DNS caching

4. **TCP Communication**:
   - Implement basic TCP client-server
   - Observe 3-way handshake with Wireshark
   - Compare TCP vs UDP packet loss

#### 📖 Resources & Key Questions:
- **Resources**:
  - MDN HTTP Documentation
  - Julia Evans' "How DNS Works" comic
  - TCP/IP Illustrated (book)

- **Key Questions**:
  - Why is HTTPS handshake expensive?
  - When would you use UDP over TCP?
  - How does HTTP/2 multiplexing work?
  - What happens if DNS server is down?

---

### Day 3: Database Fundamentals

#### 🎯 Core Concepts to Learn:

**Relational Databases:**
- **Core Components**:
  - **Table**: Collection of related data (rows and columns)
  - **Row**: Single record
  - **Column**: Attribute/field
  - **Schema**: Structure definition (tables, columns, relationships)

- **Keys**:
  - **Primary Key**: Unique identifier for row (e.g., user_id)
    - Cannot be NULL
    - One per table
  - **Foreign Key**: References primary key in another table
    - Maintains referential integrity
    - Creates relationships between tables
  - **Composite Key**: Primary key made of multiple columns
  - **Candidate Key**: Column(s) that could be primary key
  - **Unique Key**: Column with unique values (can be NULL)

- **Normalization** (Eliminate Redundancy):
  - **1NF (First Normal Form)**:
    - Atomic values (no arrays or lists in columns)
    - Each column has unique name
  - **2NF (Second Normal Form)**:
    - Must be in 1NF
    - No partial dependencies (all non-key columns depend on entire primary key)
  - **3NF (Third Normal Form)**:
    - Must be in 2NF
    - No transitive dependencies (non-key columns don't depend on other non-key columns)

- **Denormalization**:
  - Intentionally add redundancy for performance
  - Trade-off: Faster reads, slower writes
  - Use cases: Read-heavy systems, analytics

**ACID Properties:**
- **Atomicity**: All or nothing
  - Example: Bank transfer - both debit and credit happen, or neither
  - Implementation: Transaction logs, rollback
  
- **Consistency**: Database remains in valid state
  - Constraints always satisfied
  - Example: Balance can't be negative (CHECK constraint)
  
- **Isolation**: Concurrent transactions don't interfere
  - **Isolation Levels**:
    - Read Uncommitted: Can read uncommitted changes (dirty reads)
    - Read Committed: Only read committed changes
    - Repeatable Read: Same read within transaction returns same result
    - Serializable: Strictest, transactions appear serial
  - Phenomena:
    - Dirty Read: Reading uncommitted data
    - Non-Repeatable Read: Row changes between reads
    - Phantom Read: New rows appear between reads
  
- **Durability**: Committed data persists after crashes
  - Written to disk (not just memory)
  - Write-Ahead Logging (WAL)

**SQL Operations:**
- **CRUD Operations**:
  ```sql
  CREATE TABLE users (id INT PRIMARY KEY, name VARCHAR(100));
  INSERT INTO users VALUES (1, 'Alice');
  SELECT * FROM users WHERE id = 1;
  UPDATE users SET name = 'Bob' WHERE id = 1;
  DELETE FROM users WHERE id = 1;
  ```

- **JOINs**:
  - **INNER JOIN**: Only matching rows from both tables
  - **LEFT JOIN**: All from left + matching from right
  - **RIGHT JOIN**: All from right + matching from left
  - **FULL OUTER JOIN**: All rows from both tables
  - **CROSS JOIN**: Cartesian product

- **Aggregate Functions**:
  ```sql
  SELECT COUNT(*), AVG(price), SUM(quantity), MAX(price), MIN(price)
  FROM orders
  GROUP BY customer_id
  HAVING SUM(quantity) > 10;
  ```

- **Subqueries**:
  ```sql
  SELECT name FROM users 
  WHERE id IN (SELECT user_id FROM orders WHERE total > 100);
  ```

- **CTEs (Common Table Expressions)**:
  ```sql
  WITH high_value_customers AS (
    SELECT customer_id, SUM(total) as lifetime_value
    FROM orders
    GROUP BY customer_id
    HAVING SUM(total) > 10000
  )
  SELECT * FROM high_value_customers;
  ```

**Indexes:**
- **B-Tree Index** (Most Common):
  - Sorted tree structure
  - Good for: Range queries, sorting
  - O(log n) lookups
  - Used by default in most databases

- **Hash Index**:
  - Hash table
  - Good for: Exact match lookups
  - O(1) lookups
  - Not good for range queries

- **Composite Index**:
  - Index on multiple columns
  - Order matters: (last_name, first_name) ≠ (first_name, last_name)
  - Leftmost prefix rule

- **When to Use Indexes**:
  - ✅ Columns in WHERE clause
  - ✅ Columns in JOIN conditions
  - ✅ Columns in ORDER BY
  - ❌ Small tables (full scan is faster)
  - ❌ Columns with low cardinality (few unique values)
  - ❌ Frequently updated columns (index maintenance overhead)

- **Index Drawbacks**:
  - Takes storage space
  - Slows down writes (INSERT, UPDATE, DELETE)
  - Maintenance overhead

- **EXPLAIN Query Plan**:
  ```sql
  EXPLAIN SELECT * FROM users WHERE email = 'test@example.com';
  ```
  - Shows how database will execute query
  - Identifies if indexes are used
  - Shows estimated cost

#### 💻 Practice Tasks:
1. **Design E-commerce Schema**:
   - Tables: users, products, categories, orders, order_items, reviews
   - Define primary keys, foreign keys
   - Create relationships (one-to-many, many-to-many)
   - Normalize to 3NF

2. **Write Complex Queries**:
   - Get all orders for a user with product details (JOIN)
   - Calculate total revenue per product (GROUP BY, SUM)
   - Find top 10 customers by lifetime value
   - Get products with average rating > 4.0

3. **Index Optimization**:
   - Create indexes on: user email, product category_id, order user_id
   - Use EXPLAIN to verify index usage
   - Compare query speed with and without indexes
   - Analyze index overhead on INSERT performance

4. **Design Twitter Schema**:
   - Tables: users, tweets, follows, likes
   - Challenges:
     - How to model self-referential relationship (follows)?
     - How to efficiently query "tweets from people I follow"?
     - How to count likes efficiently?

#### 📖 Resources & Key Questions:
- **Resources**:
  - Use The Index, Luke (https://use-the-index-luke.com/)
  - PostgreSQL Documentation
  - SQL Zoo for practice

- **Key Questions**:
  - When should you denormalize your database?
  - What's the cost of having too many indexes?
  - How do databases implement ACID?
  - What's the difference between INNER JOIN and LEFT JOIN?
  - Why are writes slower with indexes?

---

### Day 4: System Building Blocks Introduction

#### 🎯 Core Concepts to Learn:

**Architecture Patterns:**
- **Monolithic Architecture**:
  - Single codebase, single deployable unit
  - All features in one application
  - **Pros**:
    - Simple to develop and test
    - Easy deployment
    - No network overhead between components
  - **Cons**:
    - Hard to scale (must scale entire app)
    - Long build/deploy times
    - Technology stack lock-in
    - Hard to maintain as codebase grows
  - **When to use**: Small teams, simple applications, startups (MVP)

- **Distributed Architecture**:
  - Multiple services/components
  - Communicate over network
  - **Pros**:
    - Scalable (scale individual services)
    - Flexible technology choices
    - Isolated failures
    - Independent deployment
  - **Cons**:
    - Complex debugging
    - Network latency
    - Data consistency challenges
    - Operational overhead
  - **When to use**: Large teams, complex applications, high scale

- **Trade-offs**:
  - Start monolith → migrate to distributed as needed
  - Don't build microservices until you need them

**Load Balancers:**
- **Purpose**:
  - Distribute incoming traffic across multiple servers
  - Improve availability and reliability
  - No single point of failure

- **Benefits**:
  - **High Availability**: If one server fails, others handle traffic
  - **Scalability**: Add more servers as traffic grows
  - **Resource Utilization**: Distribute load evenly
  - **Zero Downtime**: Deploy updates without taking site offline

- **Basic Algorithms**:
  - **Round Robin**: Requests go to servers sequentially
  - **Least Connections**: Send to server with fewest active connections
  - **IP Hash**: Same client always goes to same server

- **Health Checks**:
  - Load balancer periodically checks server health
  - Remove unhealthy servers from rotation
  - Re-add when they recover

**Caching Basics:**
- **What is Cache?**:
  - Fast, temporary storage
  - Store frequently accessed data
  - Trade-off: Use memory to save time

- **Benefits**:
  - Reduce latency (faster response)
  - Reduce database load
  - Handle more traffic with same resources

- **Cache Hit vs Miss**:
  - **Hit**: Data found in cache
  - **Miss**: Data not in cache, must fetch from source

- **Common Cache Locations**:
  - **Browser Cache**: Static assets (images, CSS, JS)
  - **CDN Cache**: Content delivery network (geographically distributed)
  - **Application Cache**: Redis/Memcached (API responses)
  - **Database Cache**: Query result cache

- **When to Use Cache**:
  - Frequently accessed data
  - Expensive to compute/fetch data
  - Data doesn't change often

**Message Queues:**
- **Purpose**:
  - Decouple components
  - Asynchronous communication
  - Buffer traffic spikes

- **Producer-Consumer Pattern**:
  - **Producer**: Sends messages to queue
  - **Queue**: Holds messages
  - **Consumer**: Processes messages

- **Benefits**:
  - **Decoupling**: Components don't need to know about each other
  - **Async Processing**: Producer doesn't wait for consumer
  - **Load Leveling**: Queue buffers traffic spikes
  - **Reliability**: Messages persist if consumer crashes

- **Use Cases**:
  - Email sending (don't make user wait)
  - Image processing (thumbnails, compression)
  - Order processing (payment → fulfillment → shipping)
  - Log processing

- **Examples**:
  - RabbitMQ, Apache Kafka, AWS SQS, Azure Service Bus

#### 💻 Practice Tasks:
1. **Draw Architecture Diagrams**:
   - Simple web app: Client → Server → Database
   - Add load balancer: Client → LB → Servers → Database
   - Add cache: Client → LB → Servers → Cache → Database
   - Add queue: Client → Server → Queue → Workers → Database

2. **Identify Bottlenecks**:
   - Single database (can't scale writes)
   - No caching (every request hits database)
   - No load balancing (single server failure = downtime)
   - Synchronous processing (slow operations block user)

3. **Design Improvements**:
   Given: Web app with 100K users, slow responses, frequent database crashes
   - Add: Redis cache for frequently accessed data
   - Add: Database read replicas
   - Add: Load balancer with 3 app servers
   - Add: Message queue for async tasks

4. **Compare Architectures**:
   - When is monolith better than microservices?
   - Draw evolution: Monolith → Modular Monolith → Microservices

#### 📖 Resources & Key Questions:
- **Resources**:
  - System Design Primer (GitHub)
  - AWS Well-Architected Framework
  - Martin Fowler's blog on architecture patterns

- **Key Questions**:
  - What is a Single Point of Failure (SPOF)?
  - When would you NOT use a cache?
  - How does a load balancer know if a server is healthy?
  - What's the difference between sync and async processing?

---

### Day 5: Scalability Fundamentals

#### 🎯 Core Concepts to Learn:

**Horizontal vs Vertical Scaling:**

- **Vertical Scaling (Scale Up)**:
  - Add more power to existing machine (CPU, RAM, SSD)
  - **Pros**:
    - Simple (no code changes)
    - No distributed system complexity
    - Lower licensing costs (one database instance)
  - **Cons**:
    - Hardware limits (can't scale infinitely)
    - Expensive (high-end hardware costs more per unit)
    - Single point of failure
    - Downtime during upgrades
  - **Use cases**: Databases (when sharding is complex), legacy systems

- **Horizontal Scaling (Scale Out)**:
  - Add more machines to pool
  - **Pros**:
    - No theoretical limit (add more servers)
    - Cost-effective (commodity hardware)
    - Fault tolerance (lose one server, others continue)
    - Can scale up/down based on demand
  - **Cons**:
    - Complex architecture (load balancing, data distribution)
    - Network overhead
    - Data consistency challenges
    - More operational complexity
  - **Use cases**: Web servers, microservices, big data

- **Which to Choose?**:
  - Start vertical (simpler)
  - Move to horizontal when:
    - Hit hardware limits
    - Need high availability
    - Need to scale indefinitely

**Stateless vs Stateful Services:**

- **Stateless Services**:
  - Don't store session data on server
  - Each request is independent
  - **Example**: REST API that uses tokens (JWT)
  - **Pros**:
    - Easy to scale horizontally (any server can handle any request)
    - Simple load balancing
    - Server failures don't lose data
  - **Cons**:
    - Must validate token/session on every request
    - May need external session store

- **Stateful Services**:
  - Store session data on server
  - Client must return to same server
  - **Example**: WebSocket connections, in-memory sessions
  - **Pros**:
    - Faster (no external lookups)
    - Can maintain real-time connections
  - **Cons**:
    - Hard to scale (need sticky sessions)
    - Server failure loses sessions
    - Uneven load distribution

- **Making Services Stateless**:
  - Store sessions in external cache (Redis)
  - Use JWT tokens instead of sessions
  - Store state in client (cookies)

**Load Distribution Strategies:**

- **Geographic Distribution**:
  - Multiple data centers in different regions
  - Benefits: Low latency for global users, disaster recovery
  - Challenges: Data synchronization, cost

- **Service-Based Distribution**:
  - Different services on different servers
  - Example: Auth servers, API servers, static file servers
  - Benefits: Optimize resources per service type

- **Database Distribution**:
  - **Read Replicas**: Copy of database for read queries
  - **Master-Slave**: Master for writes, slaves for reads
  - Benefits: Scale reads, reduce master load

**Performance Metrics:**

- **QPS/RPS (Queries/Requests Per Second)**:
  - Number of requests system handles per second
  - Formula: `(Daily Active Users × Actions per User) / 86400`
  - Example: 1M users × 10 actions/day = 116 QPS average
  - **Peak QPS** typically 2-3× average

- **Latency**:
  - Time to complete single request
  - Measure percentiles:
    - **p50 (median)**: 50% of requests faster
    - **p95**: 95% of requests faster (important for user experience)
    - **p99**: 99% of requests faster (worst case for most users)
  - Why percentiles matter: Average hides outliers

- **Throughput**:
  - Amount of work done per unit time
  - Example: 1000 requests/second, 50 MB/second

- **Availability**:
  - Percentage of time system is operational
  - **99% (2 nines)** = 3.65 days downtime/year
  - **99.9% (3 nines)** = 8.76 hours downtime/year
  - **99.99% (4 nines)** = 52.6 minutes downtime/year
  - **99.999% (5 nines)** = 5.26 minutes downtime/year
  - Formula: `Uptime / (Uptime + Downtime)`

- **Error Rate**:
  - Percentage of failed requests
  - Monitor 4xx (client errors) and 5xx (server errors) separately

#### 💻 Practice Tasks:

1. **Calculate Capacity**:
   - **Problem**: E-commerce site with 1M daily active users
   - Each user: 5 page views, 1 search, 0.1 orders
   - Calculate:
     - Average QPS: (1M × 6.1) / 86400 = 71 QPS
     - Peak QPS: 71 × 3 = 213 QPS
     - If each request takes 100ms, how many servers needed?

2. **Design Scaling Strategy**:
   - **1K users → 1M users → 100M users**:
     - 1K: Single server (monolith)
     - 100K: Add load balancer, 3 app servers, database replica
     - 1M: Add cache layer, multiple database replicas, CDN
     - 10M: Microservices, database sharding, multiple data centers
     - 100M: Global CDN, advanced caching, message queues, specialized databases

3. **Identify Bottlenecks**:
   - Given system diagram, identify:
     - Single points of failure
     - Scalability limits (database writes, network bandwidth)
     - Resource constraints (CPU, memory, disk I/O)

4. **Convert Stateful to Stateless**:
   - App currently stores sessions in server memory
   - Redesign to store sessions in Redis
   - Benefits: Can add/remove app servers freely

#### 📖 Resources & Key Questions:

- **Key Formulas**:
  ```
  QPS = (DAU × Actions/User) / 86400
  Peak QPS ≈ 2-3× Average QPS
  Servers Needed = (Peak QPS × Response Time) / 1
  Availability = Uptime / (Uptime + Downtime)
  ```

- **Resources**:
  - Latency Numbers Every Programmer Should Know
  - Scalability Lecture by David Malan (CS75)
  - High Scalability blog

- **Key Questions**:
  - When would you choose vertical over horizontal scaling?
  - Why measure p99 latency instead of average?
  - How much does 99.99% availability cost vs 99.9%?
  - What's the difference between latency and throughput?

---

### Day 6: Introduction to Distributed Systems

#### 🎯 Core Concepts to Learn:

**Distributed System Challenges:**

- **Network Unreliability**:
  - Messages can be lost
  - Messages can be delayed (arbitrarily long)
  - Messages can be duplicated
  - Messages can arrive out of order
  - **Implication**: Can't assume message was received

- **Partial Failures**:
  - Some nodes fail while others work
  - Can't distinguish between slow node and crashed node
  - **Implication**: Must handle failures gracefully

- **No Global Clock**:
  - Each machine has its own clock
  - Clocks drift apart over time
  - Can't determine exact order of events across nodes
  - **Implication**: Use logical clocks (Lamport timestamps, vector clocks)

- **Concurrency Issues**:
  - Multiple nodes accessing/modifying same data
  - Race conditions at scale
  - **Implication**: Need coordination mechanisms (locks, transactions)

**Network Partitions:**

- **What is Network Partition?**:
  - Network split: some nodes can't communicate with others
  - Not a complete failure - nodes still alive, just can't talk

- **Split-Brain Problem**:
  - Two groups of nodes think they're in charge
  - Both accept writes
  - Conflicting data
  - **Solution**: Quorum systems (majority rule)

- **Designing for Partitions**:
  - Must assume partitions will happen
  - CAP theorem: Can't have all three (Consistency, Availability, Partition Tolerance)
  - Choose AP (Available + Partition Tolerant) or CP (Consistent + Partition Tolerant)

**Consistency Basics:**

- **Strong Consistency** (Linearizability):
  - All nodes see same data at same time
  - After write completes, all reads return that value
  - **Example**: Bank account balance
  - **Implementation**: Synchronous replication, wait for all replicas
  - **Pros**: Simple to reason about, no conflicts
  - **Cons**: Slower (must wait for all nodes), lower availability

- **Eventual Consistency**:
  - Nodes eventually converge to same state
  - Temporary inconsistencies are okay
  - **Example**: Social media likes/views count
  - **Implementation**: Asynchronous replication
  - **Pros**: Fast, highly available
  - **Cons**: Complex to reason about, must handle conflicts

- **Trade-off**:
  - Strong consistency = Slower, more consistent
  - Eventual consistency = Faster, less consistent
  - Choose based on use case

- **Read-Your-Writes Consistency**:
  - User sees their own writes immediately
  - But others might see old data temporarily
  - Common middle ground

**Fault Tolerance:**

- **Replication**:
  - Keep copies of data on multiple nodes
  - If one fails, use another
  - **Replication Factor**: Number of copies (e.g., 3)
  - **Types**:
    - Synchronous: Wait for all replicas (strong consistency)
    - Asynchronous: Don't wait (faster, eventual consistency)

- **Redundancy**:
  - No single point of failure
  - Every component has backup
  - **Example**: Multiple load balancers, multiple databases

- **Failover**:
  - Automatic switch to backup when primary fails
  - **Types**:
    - Active-Passive: Standby does nothing until failover
    - Active-Active: Both handle traffic
  - **Challenges**: Detecting failures, avoiding split-brain

- **Health Checks & Heartbeats**:
  - Nodes send periodic "I'm alive" signals
  - If no signal: assume failed
  - **Timeout**: How long to wait before declaring dead?
    - Too short: False alarms (network blip)
    - Too long: Slow failure detection

**Replication Strategies:**

- **Single-Leader (Master-Slave)**:
  - One master accepts writes
  - Replicas copy from master
  - Reads from replicas
  - **Pros**: Simple, consistent
  - **Cons**: Master is bottleneck, single point of failure for writes

- **Multi-Leader (Master-Master)**:
  - Multiple masters accept writes
  - Replicas sync with each other
  - **Pros**: Better write performance, no single point of failure
  - **Cons**: Conflict resolution needed

- **Leaderless (Quorum-Based)**:
  - No master, all nodes equal
  - Write to N nodes, wait for W responses
  - Read from N nodes, wait for R responses
  - If R + W > N: guaranteed to see latest
  - **Examples**: Cassandra, Dynamo
  - **Pros**: High availability
  - **Cons**: Complex conflict resolution

#### 💻 Practice Tasks:

1. **Design Fault-Tolerant System**:
   - Requirements: 99.9% availability
   - Design with 3 replicas
   - How many failures can system tolerate?
   - Calculate: If one server has 99% uptime, what's 3-server uptime?
     - Formula: 1 - (failure rate)^3 = 1 - 0.01^3 = 99.9999%

2. **Analyze Failure Scenarios**:
   - Given 5-node cluster:
     - What if 1 node fails?
     - What if 2 nodes fail?
     - What if network partition splits into 2-node and 3-node groups?
   - For each scenario:
     - Can system accept writes?
     - Can system serve reads?
     - Is data consistent?

3. **Plan Recovery Strategies**:
   - How to detect failures?
     - Heartbeat timeout: 5 seconds
     - Consecutive failures: 3
   - How to recover?
     - Failover to replica
     - Redirect traffic
     - Alert on-call engineer
   - How to avoid split-brain?
     - Quorum: Majority must agree

4. **Design Health Check System**:
   - Load balancer pings servers every 2 seconds
   - Mark unhealthy after 3 consecutive failures
   - Remove from rotation
   - Re-add after 2 consecutive successes
   - Code implementation

#### 📖 Resources & Key Questions:

- **Key Terms**:
  - **Replication Factor**: Number of copies (typically 3)
  - **Quorum**: Majority agreement (N/2 + 1)
  - **Split-Brain**: Multiple nodes think they're master
  - **Failover**: Automatic switch to backup

- **Resources**:
  - Designing Data-Intensive Applications (Chapter 5: Replication)
  - Fallacies of Distributed Computing
  - CAP Theorem explained

- **Key Questions**:
  - What's the difference between slow node and crashed node?
  - How do you prevent split-brain?
  - If you have 5 replicas, how many can fail and still serve requests?
  - What's the trade-off between synchronous and asynchronous replication?

---

### Day 7: Week 1 Review & Assessment

#### 🎯 Review Checklist:

**Programming Fundamentals:**
- [ ] Can explain Big O notation with examples?
- [ ] Know when to use array vs linked list vs hash table?
- [ ] Understand OOP principles (encapsulation, abstraction, inheritance, polymorphism)?
- [ ] Can implement hash table with collision handling?
- [ ] Can implement BST operations?

**Networking:**
- [ ] Understand HTTP request methods (GET, POST, PUT, DELETE)?
- [ ] Know common HTTP status codes (200, 404, 500)?
- [ ] Can explain HTTPS handshake process?
- [ ] Understand TCP 3-way handshake?
- [ ] Know difference between TCP and UDP?
- [ ] Can explain DNS resolution process?

**Databases:**
- [ ] Understand ACID properties with examples?
- [ ] Can design normalized database schema (3NF)?
- [ ] Know when to use indexes?
- [ ] Understand different types of JOINs?
- [ ] Can explain trade-off between normalization and denormalization?

**System Design:**
- [ ] Understand horizontal vs vertical scaling?
- [ ] Can explain stateless vs stateful services?
- [ ] Know what load balancer does?
- [ ] Understand cache benefits and drawbacks?
- [ ] Can explain message queue use cases?

**Distributed Systems:**
- [ ] Understand challenges of distributed systems?
- [ ] Know difference between strong and eventual consistency?
- [ ] Can explain replication and fault tolerance?
- [ ] Understand network partitions and split-brain?

#### 💻 Mini Project: URL Shortener (Basic Version)

**Requirements:**
- Shorten long URLs to short codes
- Redirect short URLs to original URLs
- Basic analytics (click count)

**API Design:**
```
POST /api/shorten
Request: { "url": "https://very-long-url.com/..." }
Response: { "shortUrl": "https://short.ly/abc123" }

GET /{shortCode}
Redirect to original URL
```

**Architecture:**
```
Client → Load Balancer → API Servers → Cache → Database
```

**Implementation Steps:**

1. **URL Encoding**:
   - **Option 1**: Hash-based (MD5/SHA)
     - Hash long URL
     - Take first 6-7 characters
     - Risk of collisions (handle with check-and-retry)
   - **Option 2**: Base62 encoding (recommended)
     - Use auto-incrementing ID (1, 2, 3, ...)
     - Convert to base62 (0-9, a-z, A-Z)
     - Example: ID 125 → "b9"
     - Benefits: No collisions, short codes

2. **Database Schema**:
   ```sql
   CREATE TABLE urls (
     id BIGINT PRIMARY KEY AUTO_INCREMENT,
     short_code VARCHAR(10) UNIQUE NOT NULL,
     original_url TEXT NOT NULL,
     created_at TIMESTAMP,
     clicks BIGINT DEFAULT 0,
     INDEX(short_code)
   );
   ```

3. **API Implementation**:
   - **POST /shorten**:
     1. Generate ID (database auto-increment)
     2. Convert ID to base62
     3. Store in database
     4. Return short URL
   
   - **GET /{shortCode}**:
     1. Check cache for short code
     2. If miss: Query database
     3. Store in cache (TTL: 1 hour)
     4. Increment click counter (async)
     5. Redirect (HTTP 302)

4. **Caching Layer**:
   - Use Redis for frequently accessed URLs
   - Cache-aside pattern
   - TTL: 1 hour
   - Reduces database load

5. **Analytics**:
   - Increment click counter
   - Don't make user wait (async)
   - Use message queue for updates

**Scalability Considerations:**

1. **How to scale to 1M URLs?**
   - Single database can handle
   - Add Redis cache for popular URLs
   - Use CDN for static assets

2. **How to scale to 1B URLs?**
   - Database sharding (shard by short_code)
   - Multiple Redis caches
   - Distributed ID generation (Twitter Snowflake)

3. **Performance Optimization**:
   - Read-heavy: Cache popular URLs
   - Write-heavy: Async processing, batch inserts
   - Bottleneck: Database writes (use write-through cache)

**Questions to Answer:**
- How to handle 1000 requests/second?
- How to ensure short codes are unique?
- How to handle database failures?
- How to track analytics without slowing redirects?
- How much storage for 1B URLs? (estimate 1KB per URL = 1TB)

#### 📖 Assessment:

**Self-Test Questions:**
1. Design cache invalidation strategy for URL shortener
2. How would you handle 100K requests/second?
3. What if database goes down?
4. How to prevent abuse (spam, malicious URLs)?
5. How to implement custom short codes (e.g., "myname")?

**Next Steps:**
- Identify weak areas from checklist
- Review concepts you struggled with
- Practice drawing architecture diagrams
- Ready for Week 2: Core System Components!

---

# Week 2: Core System Components (Days 8-14)

---

## Day 8: Load Balancing Strategies

### 🎯 Core Concepts to Learn:

#### What is Load Balancing?
- **Purpose:** Distribute incoming traffic across multiple servers
- **Benefits:**
  - Better performance (no single server overwhelmed)
  - High availability (if one server fails, others continue)
  - Scalability (add more servers as needed)
  - Fault tolerance (handle server failures gracefully)
- **Without LB:** Single server overwhelmed, single point of failure
- **With LB:** Traffic distributed, system survives individual server failures

#### Load Balancing Algorithms:

**1. Round Robin:**
- Distribute requests equally in circular order
- Server 1 → Server 2 → Server 3 → Server 1 (repeat)
- **Pros:** Simple, fair distribution
- **Cons:** Doesn't consider server load or capacity differences
- **Use when:** All servers have equal capacity, similar request processing time

**2. Weighted Round Robin:**
- Assign weights based on server capacity
- More powerful servers get proportionally more requests
- Example: Server A (weight 3) : Server B (weight 1) = 3:1 ratio
- **Use when:** Servers have different hardware capabilities

**3. Least Connections:**
- Send request to server with fewest active connections
- Dynamically adjusts based on current server load
- Better for long-lived connections
- **Use when:** Request processing time varies significantly (some requests take 1 second, others take 30 seconds)

**4. Least Response Time:**
- Combine active connections + response time
- Send to server that's both least loaded AND fastest
- Most optimal but requires active health checks
- **Use when:** Need best user experience, willing to add monitoring overhead

**5. IP Hash:**
- Hash client IP address to determine server
- Same client always goes to same server (session affinity)
- **Pros:** Good for session persistence
- **Cons:** Uneven distribution if few clients, problematic if server goes down
- **Use when:** Need sticky sessions without external session store

**6. Consistent Hashing:**
- Minimize redistribution when servers added/removed
- Virtual nodes for better distribution
- Only K/N keys remapped when adding/removing servers (K=total keys, N=nodes)
- **Use when:** Frequently scaling servers, caching scenarios (minimize cache invalidation)

#### Layer 4 vs Layer 7 Load Balancing:

**Layer 4 (Transport Layer - TCP/UDP):**
- Routes based on: IP address and port only
- Cannot inspect packet content (doesn't look at URL, headers)
- **Pros:**
  - Faster (less processing)
  - Lower latency
  - Can handle any protocol
- **Cons:**
  - Cannot route based on content
  - Cannot do SSL termination
  - No URL-based routing
- **Examples:** AWS Network Load Balancer, HAProxy (L4 mode)
- **Use when:** Maximum performance needed, simple routing sufficient

**Layer 7 (Application Layer - HTTP/HTTPS):**
- Routes based on: URL, headers, cookies, request content
- Can inspect full request
- **Capabilities:**
  - Route `/api/*` to API servers, `/images/*` to image servers
  - SSL termination (decrypt HTTPS, forward HTTP)
  - Content-based routing
  - Header manipulation
- **Pros:**
  - Intelligent routing
  - Can optimize for specific content types
  - SSL offloading reduces backend load
- **Cons:**
  - Slower (must parse content)
  - Higher CPU usage
- **Examples:** AWS Application Load Balancer, Nginx, HAProxy (L7 mode)
- **Use when:** Need content-based routing, SSL termination, HTTP-specific features

#### Health Checks and Failover:

**Active Health Check:**
- Load balancer periodically pings servers to verify health
- **Types:**
  - **TCP Check:** Can server accept TCP connection? (basic)
  - **HTTP Check:** Does server return 200 OK? (better)
  - **Custom Check:** Application-specific endpoint (e.g., `/health`) (best)
- **Configuration:**
  - Interval: Every 10 seconds
  - Timeout: Wait 3 seconds for response
  - Threshold: Mark unhealthy after 3 consecutive failures

**Passive Health Check:**
- Monitor real traffic instead of separate health checks
- Mark server unhealthy after N failed real requests
- Faster detection of issues
- Lower overhead (no extra requests)

**Failover Strategy:**
- **Detection:** Health check identifies failed server
- **Action:** Stop sending new requests to failed server
- **Retry:** Periodically check if server recovered
- **Circuit Breaker:** Stop trying after repeated failures, wait longer before retry

#### Session Persistence (Sticky Sessions):

**The Problem:**
- User logs in → Session stored on Server 1
- Next request routed to Server 2 → User appears logged out
- Session data not available on Server 2

**Solutions:**

**Option 1: IP-Based Stickiness**
- Use IP Hash algorithm
- Same client IP → Same server
- **Problem:** User IP can change (mobile switching networks)

**Option 2: Cookie-Based Stickiness**
- Load balancer sets cookie (e.g., `SERVER_ID=server1`)
- Routes requests with same cookie to same server
- Better than IP-based (survives IP changes)
- **Problem:** What if server crashes? Session lost.

**Option 3: External Session Store (Best Practice)**
- Store sessions in shared database (Redis, database)
- Any server can access any user's session
- No stickiness needed → Full load balancing flexibility
- **Trade-off:** Extra network hop to fetch session

#### Global Server Load Balancing (GSLB):

**Purpose:** Route users to nearest data center geographically

**How it works:**
- DNS-based load balancing
- User in US → Gets IP of US data center
- User in Europe → Gets IP of EU data center
- User in Asia → Gets IP of Asia data center

**Benefits:**
- Lower latency (shorter physical distance)
- Disaster recovery (if one DC fails, route to another)
- Compliance (data stays in region)

**Implementation:**
- GeoDNS: Return different IP based on user location
- Latency-based routing: Measure latency, return fastest
- Health-based routing: Don't route to unhealthy DC

### 💻 Practice Tasks:

1. **Algorithm Selection:**
   - E-commerce checkout flow: Which algorithm? (Least Connections - variable processing time)
   - Static content delivery: Which algorithm? (Round Robin - fast, equal requests)
   - Long-lived WebSocket connections: Which algorithm? (Least Connections)

2. **Design Load Balancer for Video Streaming:**
   - Long connections (streaming video for hours)
   - Variable bandwidth requirements
   - Which algorithm to use? (Least Connections)
   - Layer 4 or Layer 7? (Layer 4 for performance)

3. **Session Handling Design:**
   - Compare sticky sessions vs external session store
   - When to use each approach?
   - Design Redis-based session store architecture

4. **Capacity Calculation:**
   - 3 servers: Server A (100 req/sec), Server B (200 req/sec), Server C (300 req/sec)
   - Using weighted round robin, what weights? (A:1, B:2, C:3)
   - Total capacity? (600 req/sec)

5. **Health Check Strategy:**
   - How often to check? (Every 10-30 seconds)
   - What to check? (HTTP endpoint returning 200)
   - Failover threshold? (3 consecutive failures)
   - Recovery strategy? (Check every 30 seconds when down)

6. **Global Load Balancing:**
   - Design GSLB for 3 data centers: US-East, EU-West, Asia-Pacific
   - User in New York → Which DC? (US-East)
   - User in London → Which DC? (EU-West)
   - What if EU-West is down? (Route to US-East)

7. **Layer 4 vs Layer 7 Decision:**
   - Scenario: Need to route `/api` to API servers, `/static` to CDN
   - Which layer? (Layer 7 - need content-based routing)
   - Scenario: Need maximum performance, simple routing
   - Which layer? (Layer 4 - faster)

### 📖 Key Questions to Answer:

1. Which load balancing algorithm for long-lived connections?
   - **Answer:** Least Connections (accounts for varying connection duration)

2. When to use consistent hashing?
   - **Answer:** Caching scenarios, distributed systems where adding/removing nodes is frequent

3. Layer 4 vs Layer 7 - when to use each?
   - **Answer:** Layer 4 for performance, Layer 7 for intelligent content-based routing

4. How to handle server failures automatically?
   - **Answer:** Health checks + automatic failover (stop routing to failed servers)

5. Why are sticky sessions problematic?
   - **Answer:** Uneven load distribution, session loss on server crash, complicates scaling

6. How does global load balancing work?
   - **Answer:** DNS returns different IPs based on user geographic location or latency

7. What's the difference between active and passive health checks?
   - **Answer:** Active sends separate health check requests, passive monitors real traffic

8. How to implement session persistence without sticky sessions?
   - **Answer:** External session store (Redis/database) accessible to all servers

---

## Day 9: API Gateway & Proxies

### 🎯 Core Concepts to Learn:

#### What is API Gateway?

**Definition:**
- Single entry point for all client requests
- Reverse proxy with additional features
- Sits between clients and microservices

**Purpose:**
- Centralize cross-cutting concerns
- Simplify client code
- Provide unified interface to multiple services

**Examples:** Kong, AWS API Gateway, Apigee, Azure API Management, Google Cloud Endpoints

#### API Gateway Responsibilities:

**1. Request Routing:**
- Route `/users/*` → User Service
- Route `/products/*` → Product Service
- Route `/orders/*` → Order Service
- Path-based or header-based routing

**2. Authentication & Authorization:**
- Verify JWT tokens or API keys
- Check user permissions
- Reject unauthorized requests
- Centralize auth logic (don't duplicate in each service)

**3. Rate Limiting:**
- Prevent abuse (limit requests per user/IP)
- Different tiers: Free (100/hour), Premium (10,000/hour)
- Return 429 (Too Many Requests) when limit exceeded

**4. Request/Response Transformation:**
- Convert XML to JSON or vice versa
- Add/remove headers
- Modify request/response structure
- Example: Legacy backend returns XML, clients need JSON

**5. Protocol Translation:**
- HTTP to gRPC (clients use HTTP, backend uses gRPC)
- REST to SOAP (modern clients, legacy backends)
- WebSocket to HTTP (maintain WebSocket with client, HTTP to backend)

**6. API Composition (Aggregation):**
- Combine multiple service calls into one response
- Example: Product page needs data from 3 services
  - Product info (Product Service)
  - Reviews (Review Service)
  - Recommendations (Recommendation Service)
- Gateway calls all three, combines results, returns single response
- Reduces round trips for client

**7. Caching:**
- Cache responses to reduce backend load
- Example: Cache product details for 5 minutes
- Cache-Control headers
- Invalidation strategies

**8. Logging & Monitoring:**
- Centralized logging for all API requests
- Metrics: Latency, error rate, request count
- Distributed tracing (assign request ID)

**9. SSL Termination:**
- Handle HTTPS at gateway
- Forward HTTP to backend services
- Reduce SSL overhead on backend

**10. Load Balancing:**
- Distribute requests across service instances
- Health checks for backend services

#### Reverse Proxy vs Forward Proxy:

**Forward Proxy:**
- Client → Proxy → Internet
- **Purpose:** Acts on behalf of clients
- **Use cases:**
  - Hide client identity (anonymity)
  - Access blocked websites (VPN)
  - Cache content for multiple clients (corporate proxy)
- **Example:** Company proxy server, Squid proxy
- Client configures proxy settings

**Reverse Proxy:**
- Client → Proxy → Backend Servers
- **Purpose:** Acts on behalf of servers
- **Use cases:**
  - Hide server identity (security)
  - Load balancing
  - SSL termination
  - Caching
  - DDoS protection
- **Example:** Nginx, Apache, API Gateway
- Client unaware of proxy (transparent)

**Key Difference:**
- Forward proxy serves clients
- Reverse proxy serves servers

#### Request Aggregation Pattern:

**Problem:**
- Mobile app needs data from 5 microservices
- 5 separate HTTP requests = slow, high bandwidth
- Mobile networks have high latency

**Solution:**
- Client makes 1 request to API Gateway
- Gateway makes 5 requests to services (in parallel)
- Gateway waits for all responses
- Gateway combines results into single JSON
- Returns to client

**Example - Product Page:**
```
Client Request: GET /products/123/page

API Gateway:
1. Call Product Service: GET /products/123 → Product details
2. Call Review Service: GET /reviews?product=123 → Reviews
3. Call Recommendation Service: GET /recommendations?product=123 → Similar products
4. Call Inventory Service: GET /inventory/123 → Stock status
5. Call Pricing Service: GET /pricing/123 → Current price

Wait for all responses (parallel execution)

Combined Response:
{
  "product": {...},
  "reviews": [...],
  "recommendations": [...],
  "inventory": {...},
  "pricing": {...}
}
```

**Benefits:**
- Fewer round trips (1 instead of 5)
- Less mobile bandwidth
- Simpler client code
- Gateway handles failures (if one service fails, return partial data)

**Trade-offs:**
- Gateway becomes more complex
- Single point of failure
- Latency = slowest service response time

#### Backend for Frontend (BFF) Pattern:

**Concept:**
- Separate API gateway per client type
- Each gateway tailored to specific client needs

**Example:**
- **Mobile BFF:**
  - Minimal data (smaller payloads)
  - Aggregated calls (fewer round trips)
  - Optimized for slow networks
- **Web BFF:**
  - More detailed data
  - Less aggregation (web can make multiple calls)
  - Richer features
- **IoT BFF:**
  - Minimal data (limited bandwidth)
  - Simplified responses
  - Different authentication

**Benefits:**
- Optimize for each client type
- Independent evolution (change mobile API without affecting web)
- Team ownership (mobile team owns mobile BFF)

**Trade-offs:**
- More gateways to maintain
- Potential code duplication
- More infrastructure

#### Circuit Breaker Pattern (in Gateway):

**Purpose:** Prevent cascade failures when service is down

**States:**
1. **Closed (Normal):**
   - Requests flow through normally
   - Track failures

2. **Open (Failing):**
   - After N consecutive failures, open circuit
   - Immediately return error without calling service
   - Prevent overwhelming failing service
   - Wait timeout period (e.g., 30 seconds)

3. **Half-Open (Testing):**
   - After timeout, allow one test request
   - If succeeds → Close circuit (back to normal)
   - If fails → Open circuit (back to failing)

**Example:**
- Payment Service goes down
- After 5 failed requests, circuit opens
- Next requests immediately return error (don't try Payment Service)
- After 30 seconds, try one request
- If succeeds, resume normal operation

**Benefits:**
- Fast failure (don't wait for timeout)
- Protect failing service from more requests
- Give service time to recover

#### API Gateway Challenges:

**1. Single Point of Failure:**
- If gateway down, all APIs unavailable
- **Solution:** Deploy multiple gateway instances behind load balancer

**2. Performance Bottleneck:**
- All traffic flows through gateway
- Gateway can become bottleneck
- **Solution:** Scale horizontally, optimize gateway code, use caching

**3. Latency:**
- Extra hop adds latency (~5-10ms)
- **Solution:** Keep gateway "thin", push logic to services

**4. Complexity:**
- Gateway accumulates features, becomes complex
- **Solution:** Keep gateway focused on cross-cutting concerns only

**5. Deployment Complexity:**
- Changes to gateway affect all services
- **Solution:** Version gateway, use feature flags, gradual rollouts

### 💻 Practice Tasks:

1. **Design API Gateway for E-commerce:**
   - What features needed? (Auth, rate limiting, routing, aggregation, caching)
   - Which endpoints to expose? (/products, /cart, /orders, /users, /payments)
   - What to cache? (Product catalog, categories)
   - How to handle authentication? (JWT validation)

2. **Request Aggregation Design:**
   - Mobile app needs: User profile, notifications, friend list, messages, newsfeed
   - Design single endpoint that aggregates all
   - How to handle if one service fails? (Return partial data with error flag)
   - Optimize for slow mobile networks

3. **BFF Pattern Implementation:**
   - Design separate gateways for Mobile, Web, IoT
   - Mobile BFF: What data to include/exclude?
   - Web BFF: How is it different from mobile?
   - Shared code: What can be reused?

4. **Circuit Breaker Logic:**
   - Define states: Closed, Open, Half-Open
   - Failure threshold: How many failures before opening? (5 consecutive)
   - Timeout: How long before testing recovery? (30 seconds)
   - Success threshold: How many successes to close? (2 consecutive)

5. **Authentication Flow:**
   - User logs in → Gets JWT token
   - Subsequent requests include token in header
   - Gateway validates JWT
   - Gateway extracts user_id, passes to backend services
   - What if token expired? (Return 401, client refreshes token)

6. **Rate Limiting Strategy:**
   - Anonymous users: 10 requests/hour
   - Authenticated users: 100 requests/hour
   - Premium users: 10,000 requests/hour
   - Per API limits: Search (expensive) vs Get by ID (cheap)

7. **Compare API Gateway vs Service Mesh:**
   - API Gateway: North-south traffic (client to services)
   - Service Mesh: East-west traffic (service to service)
   - When to use each? (Both for large systems, gateway for external, mesh for internal)

### 📖 Key Questions to Answer:

1. What problems does API Gateway solve?
   - **Answer:** Centralize auth, rate limiting, routing, aggregation; simplify clients

2. Forward proxy vs reverse proxy - what's the difference?
   - **Answer:** Forward acts for clients (anonymity), reverse acts for servers (load balancing, security)

3. When to use BFF pattern?
   - **Answer:** When different client types need different APIs (mobile vs web vs IoT)

4. How does circuit breaker prevent cascade failures?
   - **Answer:** Stops calling failing service immediately, prevents overwhelming it

5. What are disadvantages of API Gateway?
   - **Answer:** Single point of failure, potential bottleneck, added latency, complexity

6. How to prevent gateway from becoming bottleneck?
   - **Answer:** Horizontal scaling, caching, keep gateway thin, use Layer 4 LB where possible

7. Should business logic be in gateway?
   - **Answer:** No - keep gateway thin, only cross-cutting concerns (auth, rate limiting, routing)

8. How does request aggregation benefit mobile apps?
   - **Answer:** Reduces round trips (1 request instead of 5), saves bandwidth, lower latency

---

## Day 10: Rate Limiting & Throttling

### 🎯 Core Concepts to Learn:

#### Why Rate Limiting?

**Primary Reasons:**
1. **Prevent Abuse:** Stop malicious users from overwhelming system
2. **Fair Usage:** Ensure all users get fair share of resources
3. **Cost Control:** Limit expensive operations (API calls, compute)
4. **Protect Backend:** Prevent overload on databases and services
5. **SLA Enforcement:** Different tiers (free, paid) get different limits

**Without Rate Limiting:**
- Single user can consume all resources
- DDoS attacks can bring down system
- No control over costs
- Unpredictable performance

#### Rate Limiting Algorithms:

**1. Token Bucket:**

**How it works:**
- Bucket starts with tokens (e.g., 100 tokens)
- Tokens refill at constant rate (e.g., 10 per second)
- Each request consumes 1 token
- If bucket empty, reject request
- Bucket has maximum capacity (can't accumulate infinite tokens)

**Characteristics:**
- Allows bursts (if bucket full, can use all tokens at once)
- Example: 100 token bucket, refill 10/sec
  - Can handle burst of 100 requests immediately
  - Then sustains 10 requests/second
- Smooth over time

**Real-world usage:** AWS API throttling, Stripe API

**2. Leaky Bucket:**

**How it works:**
- Requests enter bucket (queue)
- Requests leak out at constant rate
- If bucket full, reject new requests
- Think of bucket with hole at bottom

**Characteristics:**
- Enforces steady rate (no bursts)
- Example: Process 10 requests/second, queue up to 100
  - Even if 100 requests arrive at once, processed at 10/sec
- Smooths traffic spikes

**Difference from Token Bucket:**
- Token bucket allows bursts
- Leaky bucket enforces constant rate

**3. Fixed Window:**

**How it works:**
- Allow N requests per time window
- Example: 100 requests per minute
- Window: 10:00:00 to 10:00:59
- Counter resets at 10:01:00

**Characteristics:**
- Simple to implement
- Fixed window boundaries

**Boundary Problem:**
- User makes 100 requests at 10:00:59
- Window resets at 10:01:00
- User makes 100 requests at 10:01:01
- Result: 200 requests in 2 seconds!
- Violates the spirit of "100 per minute"

**4. Sliding Window Log:**

**How it works:**
- Store timestamp of each request
- When new request comes, remove timestamps older than window
- Count remaining timestamps
- If count < limit, allow request

**Characteristics:**
- Most accurate (no boundary problem)
- Memory intensive (store all timestamps)
- Example: Allow 100 requests per minute
  - Store all request timestamps in sorted list
  - On new request at 10:05:30, remove timestamps before 10:04:30
  - Count remaining, if < 100, allow

**5. Sliding Window Counter (Hybrid):**

**How it works:**
- Combine fixed window + sliding log
- Keep counters for previous and current window
- Estimate sliding window count

**Formula:**
```
CurrentCount = 
  PreviousWindowCount × OverlapPercentage + CurrentWindowCount
```

**Example:**
- Current time: 10:00:30 (halfway through minute)
- Previous window (9:59-10:00): 80 requests
- Current window (10:00-10:01): 30 requests
- Overlap: 50% of previous window falls in sliding window
- Estimated count: 80 × 0.5 + 30 = 70 requests
- Limit: 100, so allow request

**Benefits:**
- More accurate than fixed window
- Less memory than sliding log
- Good balance

#### Distributed Rate Limiting:

**Challenge:**
- Multiple API gateway instances
- Need to coordinate limits across all instances
- User shouldn't exceed limit by hitting different servers

**Solution 1: Centralized (Redis):**
- Store counters in Redis (shared state)
- All gateways increment same counter
- Atomic operations (INCR in Redis)

**Implementation:**
```
Key: rate_limit:{user_id}:{window}
Value: Request count
TTL: Window duration

On request:
1. Increment counter in Redis
2. If counter > limit, reject (return 429)
3. If counter == 1, set TTL to window duration
```

**Pros:** Accurate, strong consistency
**Cons:** Redis is single point (use Redis Cluster for HA), network latency

**Solution 2: Local + Periodic Sync:**
- Each gateway has local counter
- Periodically sync with central system
- Distribute limit across gateways (e.g., 10 gateways, 1000 limit = 100 per gateway)

**Pros:** Lower latency, less load on central system
**Cons:** Less accurate, can exceed limit temporarily

**Solution 3: Gossip Protocol:**
- Gateways share state with each other
- Eventually consistent
- No central point

**Pros:** No SPOF, decentralized
**Cons:** Complex, eventually consistent (not strongly)

#### Rate Limit Headers:

**Standard Headers (returned in response):**

**X-RateLimit-Limit:** Maximum requests allowed in window
- Example: `X-RateLimit-Limit: 1000`

**X-RateLimit-Remaining:** Requests remaining in current window
- Example: `X-RateLimit-Remaining: 247`

**X-RateLimit-Reset:** Unix timestamp when window resets
- Example: `X-RateLimit-Reset: 1640995200` (2022-01-01 00:00:00)

**Retry-After:** (for 429 response) Seconds to wait before retrying
- Example: `Retry-After: 60`

**Example Response:**
```
HTTP/1.1 200 OK
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 247
X-RateLimit-Reset: 1640995200

or

HTTP/1.1 429 Too Many Requests
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1640995260
Retry-After: 60
```

**Benefits:**
- Clients know their limits
- Clients can throttle themselves
- Prevents hitting rate limit

#### Throttling Strategies:

**1. Hard Throttling:**
- Strictly enforce limit
- Reject all requests over limit
- Return 429 (Too Many Requests)
- Example: 1000 requests/hour hard limit

**2. Soft Throttling:**
- Allow brief bursts over limit
- Example: Allow 10% over limit temporarily
- Track "debt", reduce limit in next window

**3. Dynamic Throttling:**
- Adjust limits based on system load
- High CPU usage → Reduce limits
- Low usage → Increase limits
- Adaptive to current conditions

**4. Elastic Throttling:**
- Allow temporary overages
- Track debt, must "repay" in future windows
- Example: Use 1200 this hour, next hour limit is 800

#### Different Limit Tiers:

**Tiered System:**
1. **Anonymous Users:** 10 requests/hour
2. **Free Tier:** 100 requests/hour
3. **Basic Tier:** 1,000 requests/hour ($10/month)
4. **Premium Tier:** 10,000 requests/hour ($100/month)
5. **Enterprise:** Custom limits or unlimited

**Per-API Limits:**
- Some APIs more expensive than others
- **Search API:** 10 requests/hour (expensive, complex query)
- **Get by ID:** 1,000 requests/hour (cheap, simple lookup)
- **Create resource:** 100 requests/hour (writes are costly)

**Per-User vs Per-IP:**
- **Per-User:** Requires authentication, more accurate
- **Per-IP:** Works for anonymous users, but shared IPs problematic (NAT, corporate proxy)
- **Combination:** Per-IP for anonymous, per-user for authenticated

### 💻 Practice Tasks:

1. **Token Bucket Implementation:**
   - Bucket capacity: 100 tokens
   - Refill rate: 10 tokens/second
   - Request arrives when bucket has 5 tokens → Allow or reject? (Allow, bucket now has 4)
   - What if 10 requests arrive simultaneously? (Allow 5, reject 5)
   - How to handle refill logic? (Background thread or lazy refill on request)

2. **Compare Algorithms:**
   - Which algorithm allows bursts? (Token Bucket)
   - Which enforces steady rate? (Leaky Bucket)
   - Which has boundary problem? (Fixed Window)
   - Which is most accurate but memory-intensive? (Sliding Window Log)

3. **Design Distributed Rate Limiting with Redis:**
   - Redis key structure: `rate_limit:{user_id}:{timestamp}`
   - How to increment atomically? (Redis INCR command)
   - How to handle race conditions? (Redis atomic operations)
   - What if two gateways check limit simultaneously? (Both see count=99, both increment, count=101)
   - Solution: Use Lua script in Redis for atomic check-and-increment

4. **Design Rate Limit for Different Tiers:**
   - Anonymous: 10/hour
   - Free: 100/hour
   - Basic: 1,000/hour
   - Premium: 10,000/hour
   - How to identify tier? (API key or JWT claims)
   - How to enforce? (Lookup tier, apply limit)

5. **Fixed Window Boundary Problem:**
   - User at 12:59:59 makes 100 requests
   - Window resets at 13:00:00
   - User at 13:00:01 makes 100 requests
   - Total: 200 requests in 2 seconds
   - How does this violate "100 requests per minute"?

6. **Dynamic Throttling Design:**
   - Normal: 1000 requests/hour
   - If CPU > 80%: Reduce to 500 requests/hour
   - If CPU < 50%: Allow 1500 requests/hour
   - How to implement? (Monitor metrics, adjust limits dynamically)

7. **Rate Limit Response:**
   - User exceeds limit
   - What HTTP status code? (429 Too Many Requests)
   - What headers to include? (X-RateLimit-*, Retry-After)
   - What error message? ("Rate limit exceeded. Try again in 60 seconds")

### 📖 Key Questions to Answer:

1. Token bucket vs leaky bucket - which allows bursts?
   - **Answer:** Token bucket allows bursts (can use accumulated tokens), leaky bucket enforces constant rate

2. What's the boundary problem in fixed window?
   - **Answer:** User can make 2× requests in short time at window boundary (e.g., 100 at 12:59:59, 100 at 13:00:01)

3. How to implement rate limiting in distributed system?
   - **Answer:** Centralized with Redis (shared counter), or local counters with periodic sync

4. What HTTP status code for rate limited?
   - **Answer:** 429 Too Many Requests

5. How to communicate rate limits to clients?
   - **Answer:** Use headers (X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset, Retry-After)

6. Where to implement rate limiting - gateway vs service?
   - **Answer:** Typically at gateway (centralized), but can also have service-level limits for specific expensive operations

7. How to rate limit per user vs per IP?
   - **Answer:** Per-user requires authentication (more accurate), per-IP works for anonymous but has shared IP issues

8. What's the difference between rate limiting and throttling?
   - **Answer:** Often used interchangeably; throttling can include slowing down requests (not just rejecting), rate limiting is strict quota enforcement

---

## Day 11: Message Queues & Async Processing

### 🎯 Core Concepts to Learn:

#### Why Message Queues?

**Problems Solved:**
1. **Decoupling:** Producer and consumer don't need to know about each other
2. **Asynchronous Processing:** Producer doesn't wait for consumer to finish
3. **Load Leveling:** Queue absorbs traffic spikes, consumers process at steady rate
4. **Reliability:** Messages persisted until successfully processed
5. **Scalability:** Scale producers and consumers independently

**Real-world Example:**
- User uploads photo
- **Without Queue:** User waits while system resizes image, generates thumbnails (slow!)
- **With Queue:** User gets immediate response, processing happens asynchronously

#### Message Queue vs Pub/Sub:

**Message Queue (Point-to-Point):**
- **Pattern:** One producer → Queue → One consumer
- **Message lifecycle:** Consumed once, then deleted
- **Use case:** Task distribution, job processing
- **Example:** 
  - Producer: Web server adds "send email" task
  - Queue: Holds tasks
  - Consumer: Email worker picks up task, sends email, deletes message
- **Popular tools:** RabbitMQ, AWS SQS, Azure Queue Storage

**Pub/Sub (Publish-Subscribe):**
- **Pattern:** One publisher → Topic → Multiple subscribers
- **Message lifecycle:** Each subscriber gets copy
- **Use case:** Event notifications, broadcasting
- **Example:**
  - Publisher: Order Service publishes "OrderPlaced" event
  - Subscribers: 
    - Inventory Service (reduce stock)
    - Email Service (send confirmation)
    - Analytics Service (track conversion)
- **Popular tools:** Apache Kafka, AWS SNS, Google Pub/Sub, Redis Pub/Sub

**Key Difference:**
- Queue: One message consumed by one consumer
- Pub/Sub: One message delivered to all subscribers

#### Message Queue Patterns:

**1. Work Queue:**
- **Purpose:** Distribute tasks across multiple workers
- **How:** Multiple workers consume from same queue, each task processed by one worker
- **Use case:** 
  - Background job processing
  - Email sending
  - Image processing
- **Benefit:** Parallel processing, auto load balancing

**2. Priority Queue:**
- **Purpose:** Process important messages first
- **How:** Messages have priority levels (high, medium, low)
- **Example:**
  - High priority: Payment confirmation emails
  - Medium: Marketing emails
  - Low: Newsletter
- **Implementation:** Separate queues per priority or priority field in message

**3. Dead Letter Queue (DLQ):**
- **Purpose:** Store messages that can't be processed
- **How:** 
  - Worker tries to process message
  - If fails after N retries (e.g., 3 attempts)
  - Move to Dead Letter Queue
- **Benefits:**
  - Don't lose failed messages
  - Don't block queue with "poison messages"
  - Investigate and fix issues
- **What to do with DLQ:** Monitor, investigate failures, fix and replay

**4. Delayed Queue:**
- **Purpose:** Process message after delay
- **How:** Message not visible until specified time
- **Use case:**
  - Scheduled tasks
  - Reminders ("Send email in 1 hour")
  - Retry with backoff (retry in 5 min, then 15 min, then 1 hour)

#### Message Delivery Guarantees:

**1. At-Most-Once:**
- **Guarantee:** Message delivered 0 or 1 times
- **May lose messages** (if delivery fails, don't retry)
- **How:** 
  - Send message
  - Don't wait for acknowledgment
  - Don't retry on failure
- **Pros:** Fastest, lowest overhead
- **Cons:** Message loss possible
- **Use when:** Loss acceptable (metrics, logs, non-critical data)

**2. At-Least-Once:**
- **Guarantee:** Message delivered 1 or more times
- **May have duplicates**
- **How:**
  - Send message
  - Wait for acknowledgment
  - Retry if no ack (network failure, consumer crash)
- **Pros:** No message loss
- **Cons:** Consumer must handle duplicates (idempotency)
- **Use when:** Most common choice, balance between reliability and complexity

**3. Exactly-Once:**
- **Guarantee:** Message delivered exactly 1 time
- **No loss, no duplicates**
- **How:** 
  - Complex coordination
  - Two-phase commit or distributed transactions
  - Track message IDs, deduplicate
- **Pros:** Perfect reliability
- **Cons:** 
  - Very complex to implement
  - Performance overhead
  - May not be truly "exactly-once" in all failure scenarios
- **Use when:** Financial transactions, critical operations

**Which to choose:**
- Default: At-least-once (most common)
- If loss acceptable: At-most-once
- If absolutely no duplicates: Exactly-once (prepare for complexity)

#### Idempotency (Critical for At-Least-Once):

**Definition:**
- Operation produces same result if executed once or multiple times

**Why important:**
- At-least-once delivery means duplicates possible
- Consumer must handle duplicates gracefully

**Examples:**

**Not Idempotent:**
- `balance = balance + 100` (running twice adds 200)
- `counter++` (running twice increments by 2)
- `insert into database` (duplicate records)

**Idempotent:**
- `balance = 500` (setting absolute value, same result if repeated)
- `delete user with id=123` (deleting twice = same as deleting once)
- `insert with unique key` (second insert fails or is ignored)

**How to Make Operations Idempotent:**

**1. Use Message ID:**
- Every message has unique ID
- Store processed message IDs (Redis, database)
- Before processing, check if already processed
- Example:
  ```
  message_id = "msg-12345"
  if already_processed(message_id):
      return  # Skip processing
  process_message(message)
  mark_processed(message_id)
  ```

**2. Use Natural Idempotency:**
- PUT is naturally idempotent (set absolute value)
- DELETE is naturally idempotent (deleting already deleted item = no change)

**3. Database Constraints:**
- Unique constraints prevent duplicate inserts
- Example: Payment ID as primary key, second insert fails

#### Message Ordering:

**Challenge:**
- Multiple consumers process messages in parallel
- Messages may arrive out of order

**Solutions:**

**1. Single Consumer:**
- Only one consumer, processes sequentially
- **Pros:** Guaranteed order
- **Cons:** No parallelism, slow

**2. Partition by Key:**
- Messages with same key go to same partition
- Each partition has one consumer
- Example (Kafka):
  - All orders for user A → Partition 1 → Consumer 1
  - All orders for user B → Partition 2 → Consumer 2
- **Pros:** Ordered per key, parallelism across keys
- **Cons:** Hot keys can overload one partition

**3. Sequence Numbers:**
- Each message has sequence number
- Consumer reorders based on sequence
- **Pros:** Flexible
- **Cons:** Complex consumer logic, buffering needed

**Kafka's Approach:**
- Messages within partition are ordered
- Use key to route related messages to same partition

#### Backpressure and Flow Control:

**Problem:**
- Producer too fast, consumer too slow
- Queue fills up, messages pile up
- Memory exhaustion

**Solutions:**

**1. Queue Size Limit:**
- Limit queue size (e.g., 10,000 messages)
- When full, reject new messages
- **Pros:** Prevents memory issues
- **Cons:** Lose messages or producer must retry

**2. Consumer Prefetch Limit:**
- Limit messages pulled by consumer at once
- Example: Consumer fetches 10 messages, processes, fetches 10 more
- **Pros:** Prevents overwhelming consumer
- **Cons:** Throughput may be lower

**3. Producer Rate Limiting:**
- Throttle producer to match consumer speed
- **Pros:** Prevents queue buildup
- **Cons:** Producer must wait

**4. Auto-Scaling Consumers:**
- Monitor queue depth
- If queue growing, add more consumers
- If queue empty, remove consumers
- **Pros:** Elastic, handles traffic spikes
- **Cons:** Complexity, cost

**5. Drop or Sample Messages:**
- If queue full, drop low-priority messages
- Or sample (keep 1 in 10 messages)
- **Use for:** Non-critical data (metrics, logs)

#### Use Cases:

**1. Async Processing:**
- User uploads image
- Queue: Process image (resize, thumbnail, filters)
- User doesn't wait for processing

**2. Email Sending:**
- User signs up
- Queue: Send welcome email
- User gets immediate response

**3. Order Processing:**
- Order placed
- Queue: Validate → Charge payment → Update inventory → Ship
- Each step is async task

**4. Log Aggregation:**
- Multiple services send logs
- Queue: Centralize logs
- Consumer: Store in Elasticsearch

**5. Event-Driven Architecture:**
- Order placed
- Pub/Sub: Notify multiple services
  - Inventory Service
  - Shipping Service
  - Analytics Service
  - Email Service

### 💻 Practice Tasks:

1. **Design Image Processing Pipeline:**
   - User uploads image (Web Server)
   - Queue: Resize, generate thumbnails, apply filters
   - Workers: Process images
   - Store: Upload to S3
   - What delivery guarantee? (At-least-once)
   - How to handle duplicates? (Check if already processed using image hash)

2. **Design Email Sending System:**
   - Producer: Web server enqueues email tasks
   - Queue: Email queue
   - Consumer: Email worker sends via SendGrid
   - What if SendGrid fails? (Retry with exponential backoff)
   - Dead Letter Queue: After 3 retries, move to DLQ
   - How to handle duplicates? (Track email_id to prevent double-send)

3. **Compare Message Queue vs Pub/Sub:**
   - **Scenario 1:** Send email after user signs up
     - Pattern: Message Queue (one consumer processes)
   - **Scenario 2:** Order placed, notify inventory, shipping, analytics
     - Pattern: Pub/Sub (multiple subscribers)
   - **Scenario 3:** Process uploaded videos
     - Pattern: Message Queue (one worker processes each video)

4. **Design Order Processing with Idempotency:**
   - Order placed with order_id = "order-12345"
   - Queue task: Charge payment
   - Consumer: Check if payment already processed for this order_id
   - If not, charge; if yes, skip
   - Mark as processed in database

5. **Design Priority Queue:**
   - High priority: Payment confirmations (process immediately)
   - Medium priority: Shipping updates (process within 1 hour)
   - Low priority: Marketing emails (process within 24 hours)
   - Implementation: 3 separate queues, consumers prioritize high queue

6. **Calculate Scaling Needs:**
   - Queue receives 10,000 messages/second
   - Consumer processes 1,000 messages/second
   - Queue growing at 9,000 messages/second
   - How many consumers needed? (10 consumers total)
   - How to monitor? (Queue depth, age of oldest message)

7. **Design Backpressure Mechanism:**
   - Queue size limit: 100,000 messages
   - Consumer prefetch: 10 messages at a time
   - What if queue reaches 100,000? (Reject new messages, alert, auto-scale consumers)
   - What if consumers can't keep up? (Add more consumers or increase instance size)

### 📖 Key Questions to Answer:

1. Message queue vs pub/sub - when to use each?
   - **Answer:** Queue for one-to-one task distribution, pub/sub for one-to-many event broadcasting

2. What's the difference between at-least-once and exactly-once?
   - **Answer:** At-least-once may deliver duplicates (must be idempotent), exactly-once guarantees single delivery (complex, expensive)

3. Why is idempotency important?
   - **Answer:** At-least-once delivery causes duplicates; consumers must handle gracefully to avoid double-processing

4. How to ensure message ordering?
   - **Answer:** Single consumer (slow), partition by key (Kafka), or sequence numbers (complex)

5. What is a dead letter queue and why needed?
   - **Answer:** Store failed messages after retries; prevents blocking queue with poison messages, allows investigation

6. How to handle backpressure (fast producer, slow consumer)?
   - **Answer:** Queue size limits, consumer prefetch limits, rate limiting, auto-scaling consumers

7. When to use synchronous vs asynchronous communication?
   - **Answer:** Sync when immediate response needed, async for background tasks, long-running operations, decoupling

8. How does message queue improve reliability?
   - **Answer:** Persists messages until processed, retry on failure, survives consumer crashes

---

## Day 12: CDN & Static Content Delivery

### 🎯 Core Concepts to Learn:

#### What is CDN (Content Delivery Network)?

**Definition:**
- Geographically distributed network of servers (edge servers)
- Cache content close to users
- Serve content from nearest location

**Components:**
- **Origin Server:** Where original content lives (your web server, S3)
- **Edge Servers:** Distributed globally, cache content
- **PoP (Point of Presence):** Data center location with edge servers

**Examples:** Cloudflare, Akamai, AWS CloudFront, Azure CDN, Fastly

#### Why Use CDN?

**1. Reduced Latency:**
- Content served from nearby edge server
- Physical distance matters (speed of light is finite)
- Example: User in Sydney gets content from Sydney edge, not San Francisco origin

**2. Lower Bandwidth Costs:**
- Edge servers handle most requests
- Less traffic to origin server
- Reduced bandwidth charges

**3. High Availability:**
- Multiple edge servers worldwide
- If one fails, route to another
- Origin server can go down, edge servers still serve cached content

**4. DDoS Protection:**
- Traffic absorbed at edge
- Malicious requests filtered before reaching origin
- Distribute attack across many servers

**5. Improved Performance:**
- Faster page loads
- Better user experience
- SEO benefits (page speed is ranking factor)

#### How CDN Works:

**First Request (Cache Miss):**
1. User requests `example.com/image.jpg`
2. DNS routes to nearest CDN edge server
3. Edge server doesn't have image (cache miss)
4. Edge server fetches from origin server
5. Edge server caches image
6. Edge server serves image to user
7. Sets TTL (Time To Live) for cache

**Subsequent Requests (Cache Hit):**
1. Another user requests same `image.jpg`
2. Edge server has it cached (cache hit)
3. Serve directly from cache (fast!)
4. No request to origin server

**Cache Miss vs Cache Hit:**
- **Cache Miss:** First time content requested from edge, must fetch from origin (slow)
- **Cache Hit:** Content already cached at edge (fast)
- **Cache Hit Ratio:** Percentage of requests served from cache (e.g., 90% hit rate)

#### CDN Caching Strategies:

**1. Static Content (Immutable):**
- Images, CSS, JavaScript files
- Content never changes (or rarely)
- **TTL:** Long (days, weeks, or even years)
- **Strategy:** Cache forever, use versioned URLs
- **Example:** 
  - `style.v1.css` → Cache forever
  - When updated → `style.v2.css` (new URL)
- **Benefit:** Perfect cache hit ratio

**2. Semi-Dynamic Content:**
- Product pages, blog posts
- Content changes occasionally
- **TTL:** Medium (hours, 1 day)
- **Strategy:** Cache but purge on update
- **Example:** 
  - Product page cached for 1 hour
  - When product updated → Purge cache

**3. Dynamic Content:**
- User-specific data (personalized dashboard)
- Changes constantly
- **TTL:** Short (minutes) or no cache
- **Strategy:** 
  - Don't cache at all, or
  - Cache with user-specific key (cache per user)
- **Example:** User dashboard not cached (different for each user)

**4. API Responses:**
- GET requests: Cacheable (if idempotent)
- POST/PUT/DELETE: Not cacheable (change state)
- **Example:** 
  - `GET /products` → Cache for 5 minutes
  - `POST /orders` → Never cache

#### Cache Invalidation in CDN:

**The Challenge:**
- Content cached at edge servers worldwide
- How to update when content changes?

**Solutions:**

**1. TTL Expiration (Passive):**
- Content expires after TTL
- Next request fetches fresh content
- **Pros:** Simple, automatic
- **Cons:** May serve stale content until TTL expires
- **Use when:** Acceptable to serve slightly stale content

**2. Purge/Invalidate (Active):**
- Manually remove content from all edge servers
- **How:** Call CDN API to purge
- **Example:** 
  - Content updated on origin
  - Call CloudFront API: `CreateInvalidation` for `/images/logo.png`
- **Pros:** Immediate update
- **Cons:** 
  - Expensive operation (can take minutes to propagate)
  - May have costs (some CDNs charge for invalidations)
- **Use when:** Must update immediately (critical bug fix)

**3. Versioned URLs (Best Practice):**
- Change URL when content changes
- **Strategies:**
  - Version number: `style.v1.css` → `style.v2.css`
  - Git commit hash: `app.a1b2c3d.js`
  - Content hash: `bundle.md5hash.js`
- **Pros:** 
  - Infinite TTL (never invalidate)
  - Perfect cache behavior
  - Old and new versions coexist (gradual rollout)
- **Cons:** Requires build process to update URLs
- **Use when:** Possible (best practice for static assets)

#### Push vs Pull CDN:

**Push CDN:**
- **How:** You proactively upload content to CDN
- **When:** When content created/updated, push to CDN
- **Example:** Upload all images to CDN manually
- **Pros:**
  - Full control over what's cached
  - No cache misses (content already on edge)
  - Good for small, infrequently changing content
- **Cons:**
  - Manual process
  - Must track what's on CDN
- **Use when:** Small amount of content, infrequent changes

**Pull CDN (Origin Pull):**
- **How:** CDN fetches content from origin when requested (lazy loading)
- **When:** First request (cache miss) fetches from origin
- **Example:** User requests image, CDN pulls from your server
- **Pros:**
  - Automatic (no manual upload)
  - Easy to set up (just point CDN to origin)
  - Good for large, frequently changing content
- **Cons:**
  - First request slow (cache miss)
  - Must keep origin server available
- **Use when:** Large amount of content, frequent changes (most common)

#### CDN Features:

**1. Geo-blocking:**
- Restrict content by country
- **Use case:** Licensing restrictions (Netflix content varies by country)
- **Implementation:** Check user's country from IP, allow/deny

**2. Token Authentication (Signed URLs):**
- Private content requires authentication
- Generate signed URL with expiration
- **Example:** 
  - S3 bucket is private
  - Generate signed CloudFront URL
  - URL works for 1 hour, then expires
- **Use case:** Paid content, private documents

**3. Image Optimization:**
- Auto-resize images based on device
- Format conversion (JPEG → WebP for supported browsers)
- Compression
- **Example:** Mobile device gets smaller image than desktop

**4. Compression:**
- Gzip or Brotli compression
- Reduce file size by 60-80%
- **Example:** 1 MB JavaScript → 200 KB compressed

**5. HTTP/2 and HTTP/3:**
- Modern protocols
- Multiplexing (multiple requests over single connection)
- Faster than HTTP/1.1

**6. SSL/TLS:**
- HTTPS everywhere
- Free certificates (Let's Encrypt)
- End-to-end encryption

**7. DDoS Protection:**
- Absorb attack traffic at edge
- Filter malicious requests
- Rate limiting
- **Benefit:** Origin server protected

**8. Web Application Firewall (WAF):**
- Filter malicious requests
- Protect against OWASP Top 10 vulnerabilities
- SQL injection, XSS prevention

#### When NOT to Use CDN:

**1. Highly Dynamic, User-Specific Content:**
- Personalized dashboard (different for each user)
- Real-time data (stock prices updating every second)
- **Why:** Can't cache, no benefit

**2. Small, Regional Application:**
- All users in single city
- **Why:** No latency benefit from global distribution

**3. Frequently Changing Content:**
- Content changes every second
- **Why:** Cache always stale, constant invalidations

**4. Internal Applications:**
- Not internet-facing (corporate intranet)
- **Why:** No benefit from public CDN

**5. Very Low Traffic:**
- Few users, low bandwidth
- **Why:** CDN cost may exceed savings

### 💻 Practice Tasks:

1. **Design CDN Strategy for E-commerce:**
   - **What to cache:**
     - Product images: TTL 1 day (products rarely change)
     - CSS/JS: TTL infinite (use versioned URLs)
     - Product pages: TTL 1 hour (prices may change)
     - Cart: Don't cache (user-specific)
   - **Cache invalidation:** 
     - Product images: Purge when product updated
     - CSS/JS: No purge needed (versioned URLs)

2. **Compare Push vs Pull CDN:**
   - **Scenario 1:** Blog with 100 posts, updated weekly
     - **Choice:** Pull CDN (easy, automatic)
   - **Scenario 2:** App with 50 images, never change
     - **Choice:** Push CDN (full control, no cache misses)
   - **Scenario 3:** News site with thousands of articles, updated hourly
     - **Choice:** Pull CDN (too many to push manually)

3. **Calculate Bandwidth Savings:**
   - Without CDN:
     - 10 million users
     - Each loads 1 MB page
     - Total: 10 million × 1 MB = 10 TB bandwidth
   - With CDN (90% cache hit rate):
     - 90% served from CDN edge (no origin bandwidth)
     - 10% fetched from origin
     - Origin bandwidth: 10 TB × 10% = 1 TB
     - **Savings:** 9 TB (90%)

4. **Design CDN for Video Streaming:**
   - **Content:** Large video files (100 MB - 1 GB each)
   - **Users:** Millions worldwide
   - **Strategy:**
     - Use pull CDN (too large to push all videos)
     - Cache popular videos at edge
     - TTL: 1 day (videos rarely change)
     - Adaptive bitrate: Cache multiple qualities
   - **Benefit:** 
     - Lower latency (serve from nearby edge)
     - Reduce origin load (most requests to edge)

5. **Design Content Delivery for Global News Site:**
   - **Requirements:** 
     - Breaking news (update every minute)
     - Worldwide readers
   - **Strategy:**
     - Use CDN with short TTL (1-5 minutes)
     - Purge cache when breaking news published
     - Or use versioned URLs for article pages
   - **Trade-off:** 
     - Short TTL = More cache misses
     - But ensures fresh content

6. **Design Signed URLs for Private Content:**
   - **Scenario:** Video streaming platform, paid content
   - **Implementation:**
     - User purchases access
     - Generate signed CloudFront URL
     - URL expires in 24 hours
     - User can watch within 24 hours
   - **Security:** URL can't be shared (expires)

7. **Cache Invalidation Strategy:**
   - **Option 1:** Purge on every update
     - **Pros:** Always fresh
     - **Cons:** Expensive, can take minutes
   - **Option 2:** Short TTL (5 minutes)
     - **Pros:** Automatic, simple
     - **Cons:** May serve stale content for up to 5 minutes
   - **Option 3:** Versioned URLs
     - **Pros:** Best cache behavior, no invalidation needed
     - **Cons:** Requires build process
   - **Recommendation:** Use versioned URLs for static assets, short TTL for dynamic content

### 📖 Key Questions to Answer:

1. How does CDN reduce latency?
   - **Answer:** Serves content from geographically closer edge server, reducing physical distance and network hops

2. What's the difference between cache hit and cache miss?
   - **Answer:** Hit = content already cached (fast), Miss = must fetch from origin (slow)

3. Push CDN vs Pull CDN - when to use each?
   - **Answer:** Push for small, infrequent changes; Pull for large, frequent changes (most common)

4. How to invalidate CDN cache?
   - **Answer:** Wait for TTL expiration, purge/invalidate via API, or use versioned URLs (best)

5. What content should be cached in CDN?
   - **Answer:** Static assets (images, CSS, JS), semi-dynamic content (product pages), but NOT user-specific data

6. Why use versioned URLs instead of cache purging?
   - **Answer:** Infinite TTL, no invalidation needed, perfect cache behavior, old and new coexist

7. How does CDN help with DDoS attacks?
   - **Answer:** Absorb attack traffic at distributed edge servers, filter malicious requests, protect origin

8. When should you NOT use CDN?
   - **Answer:** Highly dynamic/user-specific content, low traffic, small regional app, internal applications

---

## Day 13: Security Fundamentals

### 🎯 Core Concepts to Learn:

#### Authentication vs Authorization:

**Authentication (AuthN):**
- **Question:** Who are you?
- **Purpose:** Verify identity
- **Methods:**
  - Password (something you know)
  - SMS code (something you have)
  - Biometric (something you are)
  - OAuth (identity provider like Google, Facebook)
- **Example:** Login with username and password

**Authorization (AuthZ):**
- **Question:** What can you do?
- **Purpose:** Check permissions
- **Happens after authentication**
- **Example:** 
  - User authenticated as "john"
  - Check if "john" can delete posts (role-based)
- **Methods:**
  - Role-Based Access Control (RBAC): Users have roles (admin, editor, viewer)
  - Attribute-Based Access Control (ABAC): Check attributes (department, clearance level)

**Key Difference:**
- **Authentication:** Prove identity
- **Authorization:** Check permissions

#### Session-based vs Token-based Authentication:

**Session-based (Stateful):**

**How it works:**
1. User logs in with username/password
2. Server creates session, stores in memory/database/Redis
3. Server returns session ID in cookie
4. Client includes cookie in subsequent requests
5. Server looks up session ID to verify user

**Characteristics:**
- **Stateful:** Server must store session
- **Cookie-based:** Session ID in HTTP cookie
- **Server-side:** Server controls session (can revoke anytime)

**Pros:**
- Easy to revoke (delete session)
- Server has full control
- Can store complex session data

**Cons:**
- Hard to scale (need shared session store like Redis)
- CSRF vulnerable (if not using proper tokens)
- Doesn't work across domains easily

**Token-based (Stateless):**

**How it works:**
1. User logs in with username/password
2. Server generates signed token (JWT)
3. Server returns token to client
4. Client stores token (localStorage, memory)
5. Client includes token in header (`Authorization: Bearer <token>`)
6. Server verifies signature, trusts token

**Characteristics:**
- **Stateless:** Server doesn't store anything
- **Header-based:** Token in `Authorization` header
- **Client-side:** Client stores token

**Pros:**
- Scalable (no server-side storage)
- Works across domains (CORS-friendly)
- Microservices-friendly (any service can verify token)
- Mobile-friendly

**Cons:**
- Hard to revoke (token valid until expiration)
- Larger than session ID (payload included)
- If stolen, attacker has access until expiration

#### JWT (JSON Web Token):

**Structure:** `header.payload.signature`

**Example JWT:**
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJ1c2VySWQiOiIxMjMiLCJyb2xlIjoiYWRtaW4iLCJleHAiOjE2NDA5OTUyMDB9.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

**Part 1: Header (base64-encoded JSON):**
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```
- `alg`: Signing algorithm (HS256 = HMAC SHA-256)
- `typ`: Token type (JWT)

**Part 2: Payload (base64-encoded JSON):**
```json
{
  "userId": "123",
  "role": "admin",
  "exp": 1640995200
}
```
- **Claims:** Data about user
- **Standard claims:**
  - `sub`: Subject (user ID)
  - `exp`: Expiration timestamp
  - `iat`: Issued at timestamp
  - `iss`: Issuer
- **Custom claims:** Add any data (role, permissions, etc.)

**Part 3: Signature:**
```
HMACSHA256(
  base64UrlEncode(header) + "." + base64UrlEncode(payload),
  secret_key
)
```
- Ensures token not tampered with
- Server verifies signature using secret key

**Security Notes:**
- JWT is NOT encrypted, only signed (base64 is encoding, not encryption)
- Anyone can decode and read payload
- **Never store sensitive data in JWT** (passwords, credit cards)
- Signature prevents tampering

**Expiration:**
- Set `exp` claim (e.g., 15 minutes, 1 hour)
- Short expiration for security (if stolen, limited damage)
- Use refresh tokens for longer sessions

**Refresh Tokens:**
- Access token: Short-lived (15 min)
- Refresh token: Long-lived (days, weeks), securely stored
- When access token expires, use refresh token to get new access token
- Refresh token can be revoked (stored in database)

#### OAuth 2.0 Flow:

**What is OAuth?**
- Standard authorization protocol
- Used for "Login with Google", "Login with Facebook"
- Delegate authentication to trusted provider

**Roles:**
- **Resource Owner:** User
- **Client:** Your application
- **Authorization Server:** Google, Facebook (issues tokens)
- **Resource Server:** Google APIs, Facebook APIs (protected resources)

**Authorization Code Flow (Most Common):**

**Steps:**
1. **User clicks "Login with Google"**
   - Your app redirects to Google login page

2. **User logs in to Google**
   - Enters Google username/password
   - Google authenticates user

3. **User approves permissions**
   - "Allow MyApp to access your email and profile?"
   - User clicks "Allow"

4. **Google redirects back with authorization code**
   - Redirect to: `https://yourapp.com/callback?code=AUTHORIZATION_CODE`
   - Authorization code is temporary, single-use

5. **Your server exchanges code for access token**
   - Server makes POST request to Google:
     ```
     POST https://oauth2.googleapis.com/token
     code=AUTHORIZATION_CODE
     client_id=YOUR_CLIENT_ID
     client_secret=YOUR_CLIENT_SECRET
     ```
   - Google returns access token

6. **Use access token to call Google APIs**
   - `Authorization: Bearer ACCESS_TOKEN`
   - Get user profile, email, etc.

**Benefits:**
- No password sharing (user never gives you their Google password)
- Granular permissions (request only what you need)
- Revocable (user can revoke access anytime)
- Trusted authentication (delegate to Google, Facebook)

#### Common Security Vulnerabilities:

**1. SQL Injection:**

**Attack:**
- Inject SQL code in user input
- Example:
  ```
  Username: admin' OR '1'='1
  Password: anything
  
  Query becomes:
  SELECT * FROM users WHERE username='admin' OR '1'='1' AND password='...'
  Returns all users (always true)
  ```

**Prevention:**
- **Use parameterized queries / prepared statements**
- Never concatenate SQL strings
- Example (safe):
  ```sql
  SELECT * FROM users WHERE username=? AND password=?
  ```
  Database escapes values automatically

**2. XSS (Cross-Site Scripting):**

**Attack:**
- Inject JavaScript in user input
- Example:
  ```
  Comment: <script>alert('Hacked!');</script>
  ```
- When page displays comment, script executes
- Can steal cookies, redirect user, modify page

**Prevention:**
- **Escape HTML in user input**
- Convert `<` to `&lt;`, `>` to `&gt;`
- Use templating engines that auto-escape
- Content Security Policy (CSP) header

**3. CSRF (Cross-Site Request Forgery):**

**Attack:**
- Trick user into making unwanted request
- Example:
  - User logged into bank.com
  - User visits evil.com
  - evil.com has hidden form:
    ```html
    <form action="https://bank.com/transfer" method="POST">
      <input name="to" value="attacker" />
      <input name="amount" value="1000" />
    </form>
    <script>document.forms[0].submit();</script>
    ```
  - Form submits automatically, money transferred (user's cookie included)

**Prevention:**
- **CSRF tokens:** Include random token in forms, verify on server
- **SameSite cookies:** `Set-Cookie: session=...; SameSite=Strict`
- **Check Referer header:** Verify request came from your site

**4. DDoS (Distributed Denial of Service):**

**Attack:**
- Overwhelm server with massive traffic
- Thousands of requests per second
- Legitimate users can't access service

**Prevention:**
- Rate limiting (per IP, per user)
- CDN (absorb traffic at edge)
- DDoS protection service (Cloudflare, AWS Shield)
- Auto-scaling (add capacity)
- CAPTCHA for suspicious traffic

#### Encryption Basics:

**Encryption in Transit:**
- **Purpose:** Protect data traveling over network
- **How:** HTTPS / TLS (SSL/TLS)
- **Example:** 
  - User submits password
  - Encrypted before sending
  - Decrypted by server
- **Benefit:** Even if intercepted, attacker can't read

**Encryption at Rest:**
- **Purpose:** Protect data stored on disk
- **How:** Encrypt database files, encrypt disk
- **Example:** 
  - Database files encrypted on disk
  - Even if disk stolen, data unreadable
- **Tools:** Database encryption (MySQL, PostgreSQL), disk encryption (LUKS, BitLocker)

**Hashing vs Encryption:**

**Hashing:**
- **One-way:** Can't decrypt
- **Use for:** Passwords
- **Example:** 
  - Password: "mypassword"
  - Hash: "$2b$10$N9qo8uLOickgx2ZMRZoMye..."
  - Can't reverse to get original password
- **Verification:** Hash input password, compare with stored hash

**Encryption:**
- **Two-way:** Can encrypt and decrypt
- **Use for:** Sensitive data you need to retrieve (credit cards, SSN)
- **Example:**
  - Credit card: 4111 1111 1111 1111
  - Encrypted: "encrypted_blob"
  - Can decrypt when needed

**Password Hashing:**
- **Never store plaintext passwords!**
- **Use slow hashing algorithms:**
  - bcrypt (most common)
  - scrypt
  - Argon2 (latest, best)
- **Why slow?** Makes brute-force attacks impractical
- **Salt:** Random string added before hashing
  - Prevents rainbow table attacks
  - Each user has unique salt
  - Example: hash(password + salt)

#### HTTPS and TLS:

**What is TLS (Transport Layer Security)?**
- Encrypts communication between client and server
- Formerly called SSL (Secure Sockets Layer)
- HTTPS = HTTP + TLS

**How it works:**

**1. TLS Handshake:**
- Client: "Hello, here are my supported encryption methods"
- Server: "Hello, let's use AES-256, here's my certificate"
- Client: Verifies certificate (issued by trusted CA)
- Client and server: Establish encryption keys

**2. Encrypted Communication:**
- All data encrypted with agreed-upon keys
- Only client and server can decrypt

**Certificate:**
- Proves server identity
- Issued by Certificate Authority (CA): Let's Encrypt, DigiCert, Comodo
- Contains: Server domain, public key, CA signature

**Benefits:**
- **Privacy:** Data encrypted, can't be read if intercepted
- **Integrity:** Data can't be modified without detection
- **Authentication:** Verifies server identity (not impersonator)

**Let's Encrypt:**
- Free SSL certificates
- Automated renewal
- Used by millions of websites

#### API Security Best Practices:

**1. Use HTTPS Everywhere:**
- Never send sensitive data over HTTP
- Redirect HTTP to HTTPS

**2. Authentication:**
- Require authentication for sensitive endpoints
- Use OAuth 2.0 or JWT

**3. Authorization:**
- Check permissions on every request
- Don't trust client-side validation

**4. Rate Limiting:**
- Prevent brute-force attacks
- Limit requests per user/IP

**5. Input Validation:**
- Validate all inputs (type, length, format)
- Prevent SQL injection, XSS

**6. CORS (Cross-Origin Resource Sharing):**
- Restrict which domains can call your API
- Don't use `Access-Control-Allow-Origin: *` in production

**7. Logging:**
- Log authentication failures
- Log suspicious activity
- Monitor logs for attacks

**8. Keep Dependencies Updated:**
- Patch vulnerabilities promptly
- Use tools like Snyk, Dependabot

**9. API Keys or Tokens:**
- Track usage per client
- Revoke if compromised

**10. Sensitive Data:**
- Don't log passwords, credit cards
- Mask sensitive fields in logs

### 💻 Practice Tasks:

1. **Design Authentication Flow:**
   - User logs in with email/password
   - Server verifies credentials
   - Server generates JWT (15 min expiration)
   - Server also generates refresh token (7 days, stored in database)
   - Client stores both tokens
   - When access token expires, use refresh token to get new one

2. **Design OAuth 2.0 Flow:**
   - User clicks "Login with Google"
   - Redirect to Google with `client_id` and `redirect_uri`
   - User logs in, approves permissions
   - Google redirects back with authorization code
   - Server exchanges code for access token (POST to Google)
   - Server uses access token to get user profile
   - Server creates session or issues JWT

3. **Compare Session vs Token Auth:**
   - **Session-based:**
     - Good for: Traditional web apps, need server control
     - Bad for: Mobile apps, microservices, scaling
   - **Token-based (JWT):**
     - Good for: Mobile apps, microservices, scaling
     - Bad for: Revocation, larger size
   - **Hybrid:** Session-based for web, token-based for mobile

4. **Design Password Reset Flow:**
   - User requests reset (enters email)
   - Server generates random token (UUID), stores with expiration (1 hour)
   - Server emails link: `https://app.com/reset?token=TOKEN`
   - User clicks link, enters new password
   - Server verifies token (not expired, not used)
   - Server hashes new password, saves
   - Server invalidates token

5. **Design API Security:**
   - **Authentication:** Require API key or JWT
   - **Rate Limiting:** 1000 requests/hour per key
   - **Input Validation:** Validate all parameters
   - **Logging:** Log all API calls (IP, user, endpoint, timestamp)
   - **HTTPS:** Enforce HTTPS only
   - **CORS:** Whitelist allowed domains

6. **Protect Against Common Attacks:**
   - **SQL Injection:** Use parameterized queries
   - **XSS:** Escape HTML, use Content Security Policy
   - **CSRF:** Use CSRF tokens, SameSite cookies
   - **DDoS:** Rate limiting, CDN, auto-scaling

7. **Design Encryption Strategy:**
   - **In Transit:** HTTPS for all endpoints
   - **At Rest:** 
     - Database: Encrypt sensitive columns (credit cards, SSN)
     - Disk: Encrypt database files
   - **Passwords:** Hash with bcrypt, unique salt per user
   - **Sensitive Data:** Encrypt credit cards, can decrypt when needed

### 📖 Key Questions to Answer:

1. Authentication vs authorization - what's the difference?
   - **Answer:** Authentication verifies identity (who you are), authorization checks permissions (what you can do)

2. Session-based vs token-based auth - when to use each?
   - **Answer:** Session for traditional web (easy revocation), token for mobile/microservices (scalable, stateless)

3. How does JWT work and what's in it?
   - **Answer:** Three parts: header (algorithm), payload (claims/data), signature (prevents tampering); base64-encoded, NOT encrypted

4. What is OAuth 2.0 and when to use it?
   - **Answer:** Authorization protocol for "Login with Google/Facebook"; delegate authentication to trusted provider

5. How to protect against SQL injection?
   - **Answer:** Use parameterized queries/prepared statements, never concatenate SQL strings with user input

6. What's the difference between hashing and encryption?
   - **Answer:** Hashing is one-way (can't decrypt, for passwords), encryption is two-way (can decrypt, for sensitive data)

7. Why use HTTPS? What does TLS provide?
   - **Answer:** Encrypts data in transit (privacy), prevents tampering (integrity), verifies server identity (authentication)

8. How to store passwords securely?
   - **Answer:** Hash with slow algorithm (bcrypt, scrypt, Argon2), use unique salt per user, never store plaintext

---

## Day 14: Week 2 Review & Mini Project

### 🎯 Week 2 Review Checklist:

#### Load Balancing (Day 8):
- ✅ Can explain different load balancing algorithms?
- ✅ Know when to use Round Robin vs Least Connections?
- ✅ Understand Layer 4 vs Layer 7 load balancing?
- ✅ Know how to implement health checks?
- ✅ Understand consistent hashing?
- ✅ Can design session persistence strategy?

#### API Gateway (Day 9):
- ✅ Can explain API Gateway responsibilities?
- ✅ Understand reverse proxy vs forward proxy?
- ✅ Know when to use BFF pattern?
- ✅ Can explain circuit breaker pattern?
- ✅ Understand request aggregation?
- ✅ Know challenges of API Gateway (SPOF, bottleneck)?

#### Rate Limiting (Day 10):
- ✅ Can compare different rate limiting algorithms?
- ✅ Understand token bucket vs leaky bucket?
- ✅ Know how to implement distributed rate limiting?
- ✅ Understand rate limit headers?
- ✅ Can handle boundary problem in fixed window?
- ✅ Know different throttling strategies?

#### Message Queues (Day 11):
- ✅ Understand message queue vs pub/sub?
- ✅ Know different delivery guarantees?
- ✅ Understand idempotency?
- ✅ Can explain dead letter queue?
- ✅ Know how to handle backpressure?
- ✅ Understand message ordering challenges?

#### CDN (Day 12):
- ✅ Can explain how CDN works?
- ✅ Understand cache invalidation strategies?
- ✅ Know push vs pull CDN?
- ✅ Understand versioned URLs?
- ✅ Know when to use CDN and when not?
- ✅ Can calculate bandwidth savings?

#### Security (Day 13):
- ✅ Understand authentication vs authorization?
- ✅ Know session-based vs token-based auth?
- ✅ Can explain JWT and OAuth 2.0?
- ✅ Know common security vulnerabilities?
- ✅ Understand encryption basics?
- ✅ Can design secure API?

### 💻 Mini Project: Design Complete API Infrastructure

**Scenario:** Design API infrastructure for e-commerce platform

**Requirements:**
- **Expected Traffic:** 10,000 requests/second
- **Users:** 10 million registered, 1 million daily active
- **Need:** High availability (99.9%), security, scalability
- **Features:** User auth, product catalog, shopping cart, order processing

**Components to Design:**

**1. Load Balancing:**
- **Algorithm Choice:** 
  - Product browsing: Round Robin (fast, equal requests)
  - Checkout: Least Connections (variable processing time)
- **Layer:** Layer 7 (need content-based routing: /api → backend, /static → CDN)
- **Health Checks:** 
  - Check `/health` endpoint every 10 seconds
  - Mark unhealthy after 3 consecutive failures
  - Remove from rotation, check every 30 seconds for recovery
- **Deployment:** Multiple LB instances behind DNS failover

**2. API Gateway:**

**Responsibilities:**
- **Authentication:** 
  - Verify JWT tokens
  - Reject unauthorized requests (return 401)
  - Extract user_id from token, pass to backend
- **Rate Limiting:**
  - Anonymous users: 100 requests/hour
  - Free tier: 1,000 requests/hour
  - Premium tier: 10,000 requests/hour
  - Implementation: Token bucket, store counters in Redis
- **Request Routing:**
  - `/users/*` → User Service
  - `/products/*` → Product Service
  - `/cart/*` → Cart Service
  - `/orders/*` → Order Service
- **Circuit Breaker:**
  - If Product Service fails 5 times → Open circuit
  - Return cached data or friendly error
  - Test recovery after 30 seconds
- **Logging:** Centralized logging (request ID, user, endpoint, latency, status)

**3. Async Processing (Message Queue):**

**Use Cases:**
- Order placed → Queue → Process payment, update inventory, send email
- Image uploaded → Queue → Resize, generate thumbnails
- Newsletter → Queue → Send emails to 1 million users

**Design:**
- **Pattern:** Message Queue (RabbitMQ or AWS SQS)
- **Guarantee:** At-least-once delivery
- **Idempotency:** Check order_id before processing payment
- **Dead Letter Queue:** After 3 retries, move to DLQ
- **Scaling:** Multiple consumers, auto-scale based on queue depth

**Order Processing Flow:**
```
1. User places order → Order Service
2. Order Service: Save order, publish to queue
3. Queue: "OrderPlaced" message
4. Consumer:
   a. Process payment (call Payment Service)
   b. Update inventory (call Inventory Service)
   c. Send confirmation email (call Email Service)
5. If any step fails: Retry 3 times, then move to DLQ
6. Mark order as processed (prevent duplicate processing)
```

**4. CDN:**

**What to Cache:**
- Product images: TTL 1 day
- CSS/JavaScript: TTL infinite (versioned URLs: `app.v2.css`)
- Product pages: TTL 1 hour
- API responses (GET): TTL 5 minutes (only for cacheable endpoints)

**What NOT to Cache:**
- User-specific data (cart, orders)
- POST/PUT/DELETE requests
- Dynamic pricing (flash sales)

**Invalidation:**
- **CSS/JS:** No invalidation (use versioned URLs)
- **Product images:** Purge on product update
- **Product pages:** Short TTL or purge on update

**5. Security:**

**Authentication Flow:**
```
1. User logs in: POST /auth/login
   Body: {email, password}

2. Server:
   - Verify credentials (check hashed password)
   - Generate JWT (15 min expiration)
   - Generate refresh token (7 days, store in DB)
   - Return both tokens

3. Client stores tokens

4. Subsequent requests:
   - Include JWT in header: Authorization: Bearer <token>

5. Gateway:
   - Verify JWT signature
   - Check expiration
   - Extract user_id
   - Pass to backend

6. Access token expires:
   - Client uses refresh token: POST /auth/refresh
   - Server issues new access token
```

**Protection:**
- **HTTPS:** All endpoints (SSL/TLS)
- **Input Validation:** 
  - Validate email format, password strength
  - Sanitize inputs to prevent SQL injection, XSS
- **Rate Limiting:** Prevent brute-force on login (5 attempts per hour per IP)
- **CORS:** Whitelist allowed origins (not `*`)
- **Logging:** Log failed login attempts, suspicious activity

### Architecture Diagram:

```
Client
  ↓ (HTTPS)
CDN (CloudFront)
  ↓
DNS (Route 53)
  ↓
Load Balancer (Layer 7)
  ↓
API Gateway
  ├── Auth (JWT verification)
  ├── Rate Limiting (Redis)
  ├── Request Routing
  └── Circuit Breaker
  ↓
Microservices
  ├── User Service (User DB)
  ├── Product Service (Product DB)
  ├── Cart Service (Redis)
  └── Order Service (Order DB)
       ↓
     Message Queue (RabbitMQ)
       ↓
     Workers
       ├── Payment Worker
       ├── Email Worker
       └── Inventory Worker
```

### Document Trade-offs:

**1. Why Layer 7 Load Balancer?**
- **Need:** Content-based routing (/api vs /static)
- **Trade-off:** Slower than Layer 4, but flexibility needed
- **Alternative:** Could use Layer 4 for performance, but lose routing capability

**2. Why Message Queue?**
- **Need:** Decouple order processing, handle spikes
- **Trade-off:** Adds complexity, eventual consistency
- **Alternative:** Synchronous calls, but slower user experience, can't handle spikes

**3. Why JWT instead of Session?**
- **Need:** Stateless, scalable, microservices-friendly
- **Trade-off:** Hard to revoke, larger than session ID
- **Mitigation:** Short expiration (15 min), refresh tokens (can revoke)

**4. Why Redis for Rate Limiting?**
- **Need:** Distributed rate limiting across multiple gateways
- **Trade-off:** Redis is single point of failure
- **Mitigation:** Redis Cluster for high availability

**5. CDN Trade-offs:**
- **Benefit:** Reduced latency (90%), lower bandwidth costs
- **Trade-off:** Added complexity, cache invalidation challenges
- **Solution:** Use versioned URLs for static assets

### Capacity Calculations:

**QPS:**
- 10,000 requests/second average
- Peak: 30,000 requests/second (3× for traffic spikes)

**Servers:**
- Assume each server handles 1,000 QPS
- Servers needed: 30,000 / 1,000 = 30 servers
- Add 30% buffer: 40 servers total

**Database:**
- Assume each DB handles 5,000 QPS
- Read-heavy (90% reads): Need 6 read replicas
- Writes: Need 2-3 write servers (sharded)

**Cache (Redis):**
- Assume Redis handles 100,000 QPS
- Easily handles 30,000 QPS
- Use Redis Cluster for availability

**Message Queue:**
- 10,000 orders/day = 0.12 orders/second (low)
- Can handle with single queue instance
- Auto-scale workers based on queue depth

### 📖 Key Takeaways from Week 2:

**1. Load Balancers:**
- Distribute traffic, enable horizontal scaling
- Choose algorithm based on use case
- Health checks for automatic failover

**2. API Gateway:**
- Centralizes cross-cutting concerns (auth, rate limiting, routing)
- Simplifies clients, but can become bottleneck
- Keep gateway thin

**3. Rate Limiting:**
- Protects against abuse, ensures fair usage
- Token bucket allows bursts, leaky bucket enforces steady rate
- Distribute across servers using Redis

**4. Message Queues:**
- Decouple services, enable async processing
- At-least-once delivery requires idempotency
- Use DLQ for failed messages

**5. CDN:**
- Reduces latency and bandwidth costs
- Use versioned URLs for best cache behavior
- Not for dynamic, user-specific content

**6. Security:**
- Authentication (who) vs Authorization (what)
- Token-based (JWT) for scalability, session-based for control
- Always use HTTPS, validate inputs, hash passwords

**7. Always Consider Trade-offs:**
- No perfect solution
- Evaluate pros/cons for your specific use case
- Document decisions

### 🎯 Prepare for Week 3:

**Week 3 Topics:**
- CAP Theorem & Trade-off Analysis
- Distributed Transactions
- Replication & Consensus (Raft, Paxos)
- Microservices Architecture
- Event-Driven Architecture
- Observability & Monitoring

**Focus Areas:**
- Understanding trade-offs in distributed systems
- Back-of-envelope capacity estimation
- Designing for scale (millions to billions of users)

**Practice:**
- Work through capacity calculations daily
- Draw architecture diagrams
- Explain trade-offs out loud (prepare for interviews)

---

**Week 2 Complete! 🎉**

You've mastered core system components that power modern applications. These building blocks will be essential as we move into distributed systems in Week 3.

Keep practicing, and remember: System design is about trade-offs!

---

# Week 3: Distributed Systems & Advanced Patterns (Days 15-21)

### Day 15: CAP Theorem & Trade-off Analysis

#### 🎯 Core Concepts to Learn:

**CAP Theorem:**
- **Definition**: In a distributed system, you can only guarantee 2 of 3 properties:
  - **C**onsistency: All nodes see the same data at the same time
  - **A**vailability: Every request receives a response (success or failure)
  - **P**artition Tolerance: System continues despite network failures

- **The Reality**:
  - Partition tolerance is NOT optional (networks WILL fail)
  - Real choice: **CP** (Consistent + Partition Tolerant) vs **AP** (Available + Partition Tolerant)
  
- **CP Systems** (Choose Consistency):
  - When partition occurs: Reject requests to maintain consistency
  - **Examples**: 
    - Banking systems (can't show wrong balance)
    - HBase, MongoDB (with strong consistency), Redis (single master)
    - Traditional RDBMS (PostgreSQL, MySQL in single-master mode)
  - **Use cases**: Financial transactions, inventory management, booking systems
  - **Trade-off**: Sacrifice availability during partitions

- **AP Systems** (Choose Availability):
  - When partition occurs: Accept requests, allow temporary inconsistencies
  - **Examples**:
    - Cassandra, DynamoDB, Riak
    - DNS (Domain Name System)
    - Social media (likes, views, comments)
  - **Use cases**: Social media, analytics, caching, content delivery
  - **Trade-off**: Sacrifice consistency for uptime

**Consistency Models** (Spectrum):

1. **Strong Consistency (Linearizability)**:
   - Once a write completes, all subsequent reads return that value
   - Appears as if only one copy exists
   - **Implementation**: 
     - Synchronous replication
     - Wait for majority (quorum)
     - Use locks or transactions
   - **Latency**: High (must wait for confirmation)
   - **Example**: Bank account balance

2. **Sequential Consistency**:
   - Operations appear in order for each client
   - But different clients may see different orders
   - Weaker than linearizability
   - **Example**: Social media timeline

3. **Causal Consistency**:
   - Causally related operations seen in order
   - Concurrent operations can be seen in any order
   - **Example**: Comment threads (reply must come after original)

4. **Eventual Consistency**:
   - Given enough time with no updates, all replicas converge
   - No guarantee when convergence happens
   - **Implementation**: Asynchronous replication
   - **Latency**: Low (don't wait for replicas)
   - **Challenges**: 
     - Conflict resolution (what if same data updated differently?)
     - Read-your-writes guarantee (user should see their own updates)
   - **Example**: DNS, Amazon shopping cart

5. **Read-Your-Writes Consistency**:
   - User sees their own writes immediately
   - Other users might see stale data
   - **Implementation**: 
     - Read from same replica you wrote to
     - Track version numbers
   - **Use case**: User profile updates

**Trade-off Analysis Framework:**

When designing systems, always consider these trade-offs:

1. **Consistency vs Availability**:
   - **Question**: What happens during network partition?
   - **Consistent**: Reject requests (return error)
   - **Available**: Accept requests (risk stale data)
   - **Decision guide**:
     - Money involved? → Consistency
     - User experience matters more? → Availability

2. **Consistency vs Performance (Latency)**:
   - **Strong consistency** = High latency (wait for replicas)
   - **Eventual consistency** = Low latency (don't wait)
   - **Question**: Can users tolerate stale data?
   - **Examples**:
     - Stock trading: Need strong consistency
     - Twitter likes: Eventual consistency fine

3. **Latency vs Throughput**:
   - **Latency**: Time for single request
   - **Throughput**: Number of requests handled per second
   - **Trade-off**: 
     - Batch requests → Higher throughput, higher latency
     - Process individually → Lower latency, lower throughput
   - **Example**: 
     - Database batch inserts (high throughput)
     - API real-time responses (low latency)

4. **Durability vs Performance**:
   - **Durability**: Data persists after crashes
   - **Performance**: Fast writes
   - **Trade-off**:
     - Write to disk → Durable but slow
     - Write to memory → Fast but risky
   - **Solution**: Write-Ahead Log (WAL) - write to disk sequentially

5. **Cost vs Performance**:
   - More servers = Better performance but higher cost
   - Better hardware = Faster but expensive
   - **Question**: What's the SLA requirement?
   - **Example**: 99.9% uptime vs 99.99% (10x cost difference)

6. **Simplicity vs Scalability**:
   - Monolith: Simple but limited scalability
   - Microservices: Scalable but complex
   - **Start simple**, scale when needed

7. **Normalization vs Denormalization**:
   - **Normalized**: Less redundancy, slower reads
   - **Denormalized**: Faster reads, more storage
   - **Read-heavy?** → Denormalize
   - **Write-heavy?** → Normalize

8. **Strong Schema vs Flexible Schema**:
   - **SQL**: Strong schema, integrity, complex queries
   - **NoSQL**: Flexible schema, scalability
   - **Question**: Do you know data structure upfront?

**Decision Matrix for Common Scenarios:**

| Use Case | CAP Choice | Consistency Model | Why |
|----------|-----------|------------------|-----|
| Banking | CP | Strong | Money - must be accurate |
| Social Media | AP | Eventual | User experience over perfect accuracy |
| E-commerce Inventory | CP | Strong | Can't oversell products |
| E-commerce Recommendations | AP | Eventual | Stale recommendations OK |
| Collaborative Editing | CP | Strong | Users see same content |
| Analytics Dashboard | AP | Eventual | Slightly old data acceptable |
| Chat Messages | CP | Strong | Message order matters |
| Online Presence (green dot) | AP | Eventual | Approximate status OK |

#### 💻 Practice Tasks:

1. **Trade-off Analysis Exercise**:
   
   **Scenario 1: Design Twitter**
   - Analyze each component:
     - **Tweets**: AP or CP? (AP - eventual consistency OK)
     - **Follows**: AP or CP? (AP - slight delay acceptable)
     - **Direct Messages**: AP or CP? (CP - users expect consistency)
     - **Likes/Retweets**: AP or CP? (AP - counts can be approximate)
   - Document reasoning for each choice

   **Scenario 2: Design Instagram**
   - Components:
     - Photo uploads
     - Likes counter
     - Comments
     - User feed
   - For each: Choose consistency model and justify

   **Scenario 3: Design Banking System**
   - Components:
     - Account balance
     - Transaction history
     - ATM withdrawals
     - Mobile app balance display
   - For each: Choose CAP and consistency model

2. **Build Trade-off Decision Tree**:
   ```
   Question 1: Is data critical (money, security)?
   ├─ Yes → CP System
   │  └─ Strong Consistency
   └─ No → AP System
      ├─ Users expect real-time?
      │  ├─ Yes → Read-Your-Writes Consistency
      │  └─ No → Eventual Consistency
   ```

3. **Comparative Analysis**:
   Create comparison table for these scenarios:
   
   | System | Consistency | Availability | Partition Tolerance | Trade-off Choice |
   |--------|------------|--------------|-------------------|-----------------|
   | Google Docs | High | Medium | High | CP (consistency during edit) |
   | Facebook | Medium | High | High | AP (availability over consistency) |
   | Stripe Payments | High | Medium | High | CP (must be accurate) |
   | YouTube Views | Low | High | High | AP (approximate counts OK) |

4. **Cost-Performance Analysis**:
   - Given: Need to serve 10K requests/second with 100ms latency
   - Option A: 10 servers @ $100/month each = $1000/month
   - Option B: 5 high-performance servers @ $250/month = $1250/month
   - Option C: 20 smaller servers @ $50/month = $1000/month
   - Analyze: Reliability, cost, maintenance overhead, failure handling

5. **Design Decision Document**:
   - Pick a real system (e.g., Uber, Airbnb, Netflix)
   - For each major component, document:
     - CAP choice (CP or AP)
     - Consistency model
     - Why this choice?
     - What's the trade-off?
     - What could go wrong?

#### 📖 Resources & Key Questions:

**Key Concepts to Master**:
- CAP theorem is about partitions, not normal operation
- Eventual consistency requires conflict resolution strategy
- Consistency models form a spectrum
- Trade-offs are context-dependent
- Real systems often mix approaches (different consistency per component)

**Important Formulas**:
```
Availability = Uptime / (Uptime + Downtime)
99.9% = 8.76 hours downtime/year
99.99% = 52.6 minutes downtime/year

Consistency-Performance Trade-off:
Strong Consistency Latency = RTT × (Replication Factor)
Eventual Consistency Latency = RTT (single node)
```

**Resources**:
- Martin Kleppmann's "Designing Data-Intensive Applications" (Chapter 9)
- Jepsen.io - Tests consistency of databases
- CAP Theorem paper by Eric Brewer
- Kyle Kingsbury's consistency model explanations

**Key Questions to Answer**:
1. Why is partition tolerance not optional in distributed systems?
2. Can you have both strong consistency AND high availability?
3. How does DNS prioritize availability over consistency?
4. What's the difference between linearizability and serializability?
5. How would you implement read-your-writes consistency?
6. When would you choose eventual consistency for a banking feature?
7. What are the hidden costs of strong consistency?
8. How do you handle conflicts in eventual consistency systems?

**Interview Practice**:
- "Design a system that needs strong consistency - explain your choices"
- "Your system has network partition - what happens? Justify your decision"
- "When would you sacrifice consistency for availability?"
- "Explain CAP theorem to a 5-year-old"

---

### Day 16: Distributed Transactions

#### 🎯 Core Concepts to Learn:

**The Distributed Transaction Problem:**

- **Scenario**: Transfer $100 from Account A to Account B across different databases
  - Debit Account A: -$100
  - Credit Account B: +$100
  - **Challenge**: What if one succeeds and other fails?
  
- **ACID in Distributed Systems**:
  - Atomicity harder: Operations span multiple nodes
  - Consistency harder: Multiple data stores
  - Isolation harder: Distributed locks
  - Durability easier: Replicate data

**Two-Phase Commit (2PC):**

- **Purpose**: Ensure atomicity across multiple nodes
- **Participants**:
  - **Coordinator**: Orchestrates transaction
  - **Participants**: Nodes doing actual work

- **Phase 1: Prepare (Voting)**:
  1. Coordinator asks all participants: "Can you commit?"
  2. Participants check if they can complete operation
  3. Participants lock resources
  4. Participants respond: YES or NO
  5. Participants write to transaction log (prepare state)

- **Phase 2: Commit/Abort (Completion)**:
  - **If all votes YES**:
    1. Coordinator decides: COMMIT
    2. Coordinator writes decision to log
    3. Coordinator sends COMMIT to all
    4. Participants commit and release locks
    5. Participants send ACK
  - **If any votes NO**:
    1. Coordinator decides: ABORT
    2. Coordinator sends ABORT to all
    3. Participants rollback and release locks

- **Pros**:
  - Guarantees atomicity
  - Prevents inconsistent states
  - Well-understood protocol

- **Cons**:
  - **Blocking**: Participants hold locks during prepare phase
  - **Single Point of Failure**: If coordinator crashes, participants wait forever
  - **Slow**: Multiple round trips (2 phases)
  - **Not partition-tolerant**: Blocks during network splits

- **Failure Scenarios**:
  - **Participant fails during prepare**: Coordinator aborts
  - **Coordinator fails after prepare**: Participants stuck with locks
  - **Coordinator fails after commit decision**: Participants must query coordinator state on recovery
  - **Network partition**: Some participants unreachable, transaction blocks

**Three-Phase Commit (3PC):**

- **Improvement over 2PC**: Add "pre-commit" phase to reduce blocking

- **Phases**:
  1. **Can-Commit**: Ask if participants ready
  2. **Pre-Commit**: Tell participants to prepare, but don't commit yet
  3. **Do-Commit**: Actually commit

- **Benefit**: If coordinator fails, participants can timeout and decide
- **Drawback**: Still slow, still blocks, rarely used in practice

**Saga Pattern** (Preferred Modern Approach):

- **Philosophy**: Break transaction into sequence of local transactions
- Each step has compensating action (undo)
- No locks held across services

- **Two Implementation Styles**:

  **1. Choreography (Event-Based)**:
  - Each service publishes events
  - Next service listens and reacts
  - Example: Order Processing
    ```
    Order Service: Create order → Emit "OrderCreated"
    Payment Service: Charge card → Emit "PaymentCompleted"
    Inventory Service: Reserve items → Emit "ItemsReserved"
    Shipping Service: Ship order → Emit "OrderShipped"
    ```
  - If any fails: Publish "Failed" event, trigger compensations

  **2. Orchestration (Coordinator-Based)**:
  - Central coordinator calls each service
  - Coordinator tracks state
  - Example: Order Processing
    ```
    Orchestrator:
    1. Call Payment Service
    2. If success: Call Inventory Service
    3. If success: Call Shipping Service
    4. If any fails: Call compensation actions in reverse
    ```

- **Compensation Actions**:
  - Not same as rollback (can't undo external effects)
  - Examples:
    - Charge refund (compensate for charge)
    - Release inventory (compensate for reserve)
    - Cancel shipment (compensate for ship)

- **Saga Example: Flight Booking**:
  ```
  Forward Flow:
  1. Reserve seat on flight A
  2. Reserve seat on flight B  
  3. Charge customer
  4. Send confirmation
  
  Compensation Flow (if step 3 fails):
  1. Cancel flight B reservation
  2. Cancel flight A reservation
  ```

- **Pros**:
  - No locks (high performance)
  - No blocking (high availability)
  - Works across services (microservices-friendly)
  - Partition-tolerant

- **Cons**:
  - Complex error handling
  - No isolation (other transactions see intermediate states)
  - Compensations can fail
  - Eventual consistency (not immediate)

**Eventual Consistency Patterns:**

1. **Event Sourcing**:
   - Store all changes as events
   - Rebuild state by replaying events
   - Example: Bank account
     ```
     Events: 
     - AccountCreated(id: 123, balance: 0)
     - MoneyDeposited(id: 123, amount: 100)
     - MoneyWithdrawn(id: 123, amount: 30)
     Current State: balance = 70
     ```
   - Benefits: Full audit trail, can recompute state
   - Used with Saga for distributed transactions

2. **CQRS (Command Query Responsibility Segregation)**:
   - Separate write model from read model
   - Write: Handle commands, emit events
   - Read: Build optimized views from events
   - Benefits: Scale reads and writes independently

3. **Conflict-Free Replicated Data Types (CRDTs)**:
   - Data structures that automatically resolve conflicts
   - Examples: Counters, Sets, Maps
   - Used by: Riak, Cassandra
   - Benefit: No coordination needed

**Idempotency** (Critical for Distributed Transactions):

- **Definition**: Operation produces same result if done once or multiple times
- **Why important**: Network failures cause retries
- **Examples**:
  - Idempotent: PUT, DELETE (replace/remove is same if repeated)
  - Not idempotent: POST (creates new resource each time)
  
- **How to make operations idempotent**:
  - Use unique request IDs
  - Check if operation already done before executing
  - Example: Payment processing
    ```
    def process_payment(payment_id, amount):
        if payment_already_processed(payment_id):
            return existing_result
        result = charge_card(amount)
        store_result(payment_id, result)
        return result
    ```

#### 💻 Practice Tasks:

1. **Implement 2PC Protocol**:
   ```python
   # Pseudocode for 2PC Coordinator
   
   def two_phase_commit(participants, transaction):
       # Phase 1: Prepare
       votes = []
       for participant in participants:
           vote = participant.prepare(transaction)
           votes.append(vote)
           
       # Decision
       if all(votes):  # All voted YES
           decision = "COMMIT"
       else:
           decision = "ABORT"
       
       # Phase 2: Commit or Abort
       for participant in participants:
           if decision == "COMMIT":
               participant.commit(transaction)
           else:
               participant.abort(transaction)
       
       return decision
   ```
   
   Exercise:
   - Implement participant logic
   - Add timeout handling
   - Simulate coordinator failure
   - Implement recovery protocol

2. **Design Saga for Order Processing**:
   
   **Requirements**:
   - Create order
   - Validate inventory
   - Process payment
   - Update inventory
   - Ship order
   
   **Design both styles**:
   
   **Choreography**:
   ```
   Services:
   - Order Service
   - Inventory Service
   - Payment Service
   - Shipping Service
   
   Events:
   - OrderCreated
   - InventoryValidated / InventoryValidationFailed
   - PaymentProcessed / PaymentFailed
   - InventoryUpdated
   - OrderShipped
   
   Compensations:
   - CancelOrder
   - ReleaseInventory
   - RefundPayment
   ```
   
   **Orchestration**:
   ```python
   class OrderSagaOrchestrator:
       def execute_order(order):
           try:
               order_id = order_service.create_order(order)
               inventory_service.validate(order.items)
               payment_id = payment_service.charge(order.amount)
               inventory_service.update(order.items)
               shipping_service.ship(order_id)
               return "SUCCESS"
           except InventoryError:
               order_service.cancel(order_id)
           except PaymentError:
               inventory_service.release(order.items)
               order_service.cancel(order_id)
           except ShippingError:
               payment_service.refund(payment_id)
               inventory_service.release(order.items)
               order_service.cancel(order_id)
   ```

3. **Implement Idempotent API**:
   ```python
   # API endpoint for payment processing
   
   @app.post("/payments")
   def create_payment(payment_request):
       request_id = payment_request.idempotency_key
       
       # Check if already processed
       existing = db.get_payment_by_request_id(request_id)
       if existing:
           return existing  # Return cached result
       
       # Process payment
       result = payment_gateway.charge(
           amount=payment_request.amount,
           card=payment_request.card
       )
       
       # Store with request ID
       db.store_payment(request_id, result)
       
       return result
   ```
   
   Exercise:
   - Test with duplicate requests
   - Handle race conditions (what if two requests with same ID arrive simultaneously?)
   - Add expiration for request IDs

4. **Compare 2PC vs Saga**:
   
   Create comparison table:
   
   | Criteria | 2PC | Saga |
   |----------|-----|------|
   | Atomicity | Strong | Eventual |
   | Blocking | Yes (holds locks) | No |
   | Performance | Slow (2 phases) | Fast |
   | Availability | Low (coordinator failure) | High |
   | Complexity | Medium | High |
   | Isolation | Strong | Weak |
   | Partition Tolerance | Poor | Good |
   | Use Case | Monolith databases | Microservices |

5. **Design Banking Transfer with Saga**:
   
   **Requirement**: Transfer money between accounts in different banks
   
   **Steps**:
   1. Reserve amount in source account (debit hold)
   2. Reserve credit in destination account (credit hold)
   3. Commit debit
   4. Commit credit
   5. Release holds
   
   **Compensation**:
   - If step 2 fails: Release debit hold
   - If step 3 fails: Release both holds
   - If step 4 fails: ??? (money deducted but not credited - critical!)
   
   **Solution**: Add retry with exponential backoff, manual intervention if all retries fail

#### 📖 Resources & Key Questions:

**Key Terms**:
- **2PC**: Two-Phase Commit (atomic but blocking)
- **3PC**: Three-Phase Commit (less blocking, rarely used)
- **Saga**: Sequence of local transactions with compensations
- **Choreography**: Event-driven saga (decentralized)
- **Orchestration**: Coordinator-driven saga (centralized)
- **Idempotency**: Safe to retry operations

**Resources**:
- Chris Richardson's Microservices.io (Saga pattern)
- Martin Fowler's "Patterns of Enterprise Application Architecture"
- Paper: "Life Beyond Distributed Transactions" by Pat Helland
- Saga pattern examples: Uber, Netflix tech blogs

**Key Questions**:
1. Why is 2PC rarely used in microservices?
2. What happens if compensation action fails in Saga?
3. How do you ensure idempotency in distributed systems?
4. Choreography vs Orchestration - which is better? (depends!)
5. Can Saga provide ACID guarantees? (No - only eventual consistency)
6. How would you handle "lost message" in choreographed Saga?
7. What's the difference between rollback and compensation?
8. How do you test Saga failure scenarios?

**Real-World Examples**:
- **Uber**: Uses Saga for ride booking (match driver, reserve car, charge user, notify all)
- **Amazon**: Shopping cart uses eventual consistency
- **Netflix**: Service orchestration for account creation
- **Banks**: Still use 2PC internally, but Saga for cross-bank transfers

**Interview Questions**:
- "Design a flight booking system that books multiple connecting flights"
- "How would you handle distributed transactions in microservices?"
- "Explain trade-offs between 2PC and Saga"
- "What if the payment service goes down during Saga execution?"

---

### Day 17: Replication & Consensus

#### 🎯 Core Concepts to Learn:

**Why Replication?**
- **High Availability**: If one node fails, others serve requests
- **Fault Tolerance**: Survive node crashes
- **Read Scalability**: Distribute read load across replicas
- **Geographic Distribution**: Serve users from nearby locations (low latency)
- **Disaster Recovery**: Backup in different data centers

**Leader Election:**

- **Problem**: In distributed system, who decides who's in charge?
- **Need**: One node to coordinate (accept writes, manage replicas)
- **Challenges**:
  - Nodes can crash
  - Network partitions
  - Multiple leaders ("split-brain")

- **Requirements for Leader Election**:
  - **Safety**: At most one leader at a time
  - **Liveness**: System eventually elects leader
  - **Agreement**: All nodes agree on who's leader

- **Bully Algorithm** (Simple but Flawed):
  ```
  1. Each node has unique ID
  2. Node notices leader is down
  3. Node sends "election" message to nodes with higher IDs
  4. If no response from higher IDs: Declare self as leader
  5. If response from higher ID: Wait for new leader announcement
  6. Node with highest ID becomes leader
  ```
  - Problem: Doesn't handle network partitions well
  - Used in: Simple systems, Hadoop (early versions)

- **Raft Leader Election** (Modern Approach):
  ```
  1. All nodes start as followers
  2. If follower doesn't hear from leader: Become candidate
  3. Candidate votes for itself, requests votes from others
  4. Other nodes vote for first candidate that asks
  5. Candidate with majority votes becomes leader
  6. Leader sends heartbeats to maintain authority
  ```
  - Uses term numbers to detect stale leaders
  - Handles network partitions gracefully

**Paxos Consensus:**

- **The Gold Standard** (but complex)
- Developed by Leslie Lamport in 1998
- **Problem**: How do distributed nodes agree on a single value?
- **Use Case**: Choose which server is leader

- **Roles**:
  - **Proposer**: Proposes values
  - **Acceptor**: Votes on proposals
  - **Learner**: Learns chosen value

- **Two Phases**:
  1. **Prepare Phase**:
     - Proposer picks proposal number (higher than any seen)
     - Asks acceptors: "Will you accept my proposal?"
     - Acceptors respond: "Yes, if this is highest proposal number I've seen"
  
  2. **Accept Phase**:
     - If majority agrees: Proposer sends actual value
     - Acceptors accept if no higher proposal seen
     - If majority accepts: Value is chosen

- **Key Insight**: Use proposal numbers to order operations
- **Problem**: Very complex to implement correctly
- **Real Usage**: Most systems use Raft instead

**Raft Consensus** (Paxos Made Simple):

- **Goal**: Same guarantees as Paxos, but easier to understand
- **Core Idea**: Elect a leader, leader manages log replication

**Raft Components**:

1. **Leader Election** (already covered above)

2. **Log Replication**:
   - Client sends command to leader
   - Leader appends to its log
   - Leader sends log entry to followers
   - Followers append to their logs
   - Once majority confirms: Leader commits entry
   - Leader executes command and returns result
   - Leader tells followers to commit

3. **Safety**:
   - **Election Safety**: Only one leader per term
   - **Log Matching**: If two logs have same entry at same index, all preceding entries are identical
   - **Leader Completeness**: If entry committed in term, it appears in all future leaders' logs
   - **State Machine Safety**: If server executes command at index, no other server executes different command at that index

**Raft Terms**:
- **Term**: Time period with one leader (or election)
- **Term Number**: Monotonically increasing
- Each node tracks current term
- If node sees higher term: Updates its term, steps down if leader

**Raft Heartbeats**:
- Leader sends periodic AppendEntries (even if empty)
- Followers reset election timer
- No heartbeat → Follower starts election

**Raft Example** (3 nodes: A, B, C):
```
Initial State:
- A, B, C are followers

Election:
1. A's timer expires → Becomes candidate (term 1)
2. A votes for itself (1/3 votes)
3. A requests votes from B and C
4. B and C vote for A (3/3 votes - majority)
5. A becomes leader

Log Replication:
1. Client sends command to A: "Set x=5"
2. A appends to log: [term:1, index:1, cmd:"Set x=5"]
3. A sends entry to B and C
4. B and C append to their logs
5. B and C send acknowledgment to A
6. A marks entry as committed (majority confirmed)
7. A executes command: x=5
8. A sends response to client
9. A tells B and C to commit
10. B and C execute: x=5
```

**Network Partition Scenario**:
```
Partition: [A, B] | [C]

- A is leader (term 1)
- Partition occurs
- C can't reach A, starts election (term 2)
- C votes for itself, but can't get majority (needs 2/3)
- C stays candidate, keeps trying
- A continues as leader in partition [A, B]
- A can still commit entries (majority in its partition)

Partition Heals:
- C sees A's higher term (wait, no - C has term 2, A has term 1)
- Actually: C's higher term causes A to step down
- New election occurs across all three
- One node (likely C or whoever has most up-to-date log) becomes leader
```

**Quorum Reads and Writes:**

- **Quorum**: Majority of nodes (N/2 + 1)
- **Write Quorum (W)**: Must write to W nodes
- **Read Quorum (R)**: Must read from R nodes
- **Guarantee**: If R + W > N, reads always see latest write

- **Example** (5 nodes):
  - N = 5
  - W = 3 (write to 3 nodes)
  - R = 3 (read from 3 nodes)
  - R + W = 6 > 5 ✓ (guaranteed to overlap)
  
- **Configurations**:
  - **Strong consistency**: R + W > N
    - Example: W=3, R=3 (N=5)
  - **Read-optimized**: R=1, W=N
    - Fast reads, slow writes
  - **Write-optimized**: R=N, W=1
    - Fast writes, slow reads (must read all)

- **Trade-offs**:
  - Higher W: Slower writes, more durable
  - Higher R: Slower reads, more consistent
  - Lower W: Faster writes, less durable
  - Lower R: Faster reads, might be stale

**Sloppy Quorums**:
- If not enough nodes available: Write to temporary nodes
- Later transfer to primary nodes ("hinted handoff")
- Used by Dynamo, Cassandra
- Trades consistency for availability

#### 💻 Practice Tasks:

1. **Simulate Raft Leader Election**:
   ```python
   import random
   import time
   
   class RaftNode:
       def __init__(self, node_id, peers):
           self.node_id = node_id
           self.peers = peers
           self.state = "follower"  # follower, candidate, leader
           self.current_term = 0
           self.voted_for = None
           self.votes_received = 0
           self.election_timeout = random.uniform(150, 300)  # ms
           self.last_heartbeat = time.time()
       
       def start_election(self):
           self.state = "candidate"
           self.current_term += 1
           self.voted_for = self.node_id
           self.votes_received = 1
           
           for peer in self.peers:
               response = peer.request_vote(self.current_term, self.node_id)
               if response:
                   self.votes_received += 1
           
           if self.votes_received > len(self.peers) / 2:
               self.become_leader()
       
       def become_leader(self):
           self.state = "leader"
           print(f"Node {self.node_id} is now leader (term {self.current_term})")
           self.send_heartbeats()
       
       def request_vote(self, term, candidate_id):
           if term > self.current_term:
               self.current_term = term
               self.voted_for = None
               self.state = "follower"
           
           if self.voted_for is None or self.voted_for == candidate_id:
               self.voted_for = candidate_id
               return True
           return False
   ```
   
   Exercise:
   - Implement full election simulation
   - Test with 5 nodes
   - Simulate node failures
   - Simulate network partitions
   - Verify only one leader elected per term

2. **Implement Quorum Reads/Writes**:
   ```python
   class QuorumSystem:
       def __init__(self, nodes, W, R):
           self.nodes = nodes  # list of storage nodes
           self.W = W  # write quorum
           self.R = R  # read quorum
           self.N = len(nodes)
           
           assert W + R > self.N, "Invalid quorum: W + R must be > N"
       
       def write(self, key, value, version):
           responses = []
           for node in self.nodes:
               try:
                   success = node.write(key, value, version)
                   if success:
                       responses.append(node)
               except NetworkError:
                   continue
               
               if len(responses) >= self.W:
                   return True  # Write quorum reached
           
           return False  # Failed to reach write quorum
       
       def read(self, key):
           responses = []
           for node in self.nodes:
               try:
                   value, version = node.read(key)
                   responses.append((value, version, node))
               except NetworkError:
                   continue
               
               if len(responses) >= self.R:
                   # Return value with highest version
                   return max(responses, key=lambda x: x[1])[0]
           
           return None  # Failed to reach read quorum
   ```
   
   Exercise:
   - Test with N=5, W=3, R=3
   - Simulate node failures (verify still works with 2 nodes down)
   - Test with N=5, W=5, R=1 (write-all, read-one)
   - Measure latency differences

3. **Design Consensus-Based Configuration System**:
   
   **Requirements**:
   - Store configuration (key-value pairs)
   - Multiple servers need to agree on configuration
   - Handle server failures
   - Linearizable reads and writes
   
   **Using Raft**:
   ```
   Components:
   - Raft cluster (3-5 nodes)
   - Leader accepts writes
   - Log replication for all changes
   - State machine: Key-value store
   
   Operations:
   - Put(key, value): Leader appends to log, replicates, commits
   - Get(key): Read from leader (or follower with read index)
   - Delete(key): Same as Put but mark as deleted
   
   Failure Handling:
   - Leader fails: New election, new leader continues
   - Network partition: Majority partition continues
   - Split-brain prevention: Quorum ensures single source of truth
   ```

4. **Compare Consensus Algorithms**:
   
   Create comparison:
   
   | Feature | Paxos | Raft | Zab (ZooKeeper) |
   |---------|-------|------|-----------------|
   | Complexity | Very High | Medium | Medium |
   | Understandability | Low | High | High |
   | Leader Election | Yes | Yes | Yes |
   | Log Replication | Yes | Yes | Yes |
   | Used By | Chubby (Google) | etcd, Consul | ZooKeeper |
   | Partition Tolerance | Strong | Strong | Strong |
   | Performance | Fast | Fast | Fast |
   | Implementation Difficulty | Hard | Medium | Medium |

5. **Analyze Split-Brain Scenarios**:
   
   **Scenario 1**: 5 nodes, split into [3] and [2]
   - Majority partition [3]: Continues operations
   - Minority partition [2]: Cannot form quorum, read-only or reject requests
   - After heal: Minority syncs from majority
   
   **Scenario 2**: 4 nodes, split into [2] and [2]
   - No majority: Both partitions freeze
   - Requires manual intervention or wait for partition to heal
   - This is why odd numbers (3, 5, 7) preferred
   
   **Scenario 3**: 5 nodes, one node has network issues
   - 4 nodes form majority, continue
   - Isolated node cannot become leader (cannot reach quorum)
   - After heal: Isolated node syncs

#### 📖 Resources & Key Questions:

**Key Concepts**:
- **Consensus**: Agreement among distributed nodes
- **Leader Election**: Choosing coordinator
- **Quorum**: Majority agreement
- **Split-Brain**: Multiple leaders (BAD!)
- **Term/Epoch**: Logical time period

**Important Numbers**:
```
For N nodes:
- Quorum = N/2 + 1
- Can tolerate failures = N/2 - 1

Examples:
3 nodes: Quorum=2, Tolerate=0 failures (not really, actually 1)
5 nodes: Quorum=3, Tolerate=2 failures  
7 nodes: Quorum=4, Tolerate=3 failures

Why odd numbers?
4 nodes: Quorum=3, Tolerate=1 (same as 3 nodes!)
5 nodes: Quorum=3, Tolerate=2 (better)
```

**Resources**:
- Raft paper: "In Search of an Understandable Consensus Algorithm"
- Raft visualization: https://raft.github.io/
- Paxos Made Simple (still not that simple) by Lamport
- Diego Ongaro's Raft thesis
- etcd documentation (uses Raft)
- ZooKeeper documentation (uses Zab)

**Key Questions**:
1. Why do we need consensus in distributed systems?
2. What's the difference between Paxos and Raft? (Understandability!)
3. Can a 4-node cluster tolerate 2 failures? (No, needs quorum of 3)
4. Why are odd numbers of nodes preferred? (Better fault tolerance per cost)
5. How does Raft prevent split-brain? (Term numbers, majority votes)
6. What happens if leader and one follower partition from other followers? (Leader steps down, new leader elected in majority partition)
7. How do you read from Raft without going through leader? (Read Index mechanism)
8. What's the difference between quorum and consensus? (Quorum is majority, consensus is agreement protocol)

**Real-World Usage**:
- **etcd**: Uses Raft, configuration store for Kubernetes
- **Consul**: Uses Raft, service mesh and configuration
- **CockroachDB**: Uses Raft per range of data
- **TiDB**: Uses Raft for distributed transactions
- **ZooKeeper**: Uses Zab (similar to Raft)
- **Chubby** (Google): Uses Paxos

**Interview Questions**:
- "Explain how Raft leader election works"
- "Design a distributed lock service using consensus"
- "What happens if network partition occurs?"
- "How many nodes needed for fault tolerance of F failures?" (Answer: 2F + 1)
- "Explain split-brain problem and how Raft solves it"

---

### Day 18: Microservices & Capacity Planning

#### 🎯 Core Concepts to Learn:

**Microservices Architecture:**

**What are Microservices?**
- Small, independent services
- Each service owns its data
- Communicate via APIs (REST, gRPC, message queues)
- Can be deployed independently

**Monolith vs Microservices:**

**Monolithic Architecture**:
```
Single Application
├── User Interface
├── Business Logic
├── Data Access Layer
└── Database
```
- **Pros**:
  - Simple development
  - Easy testing (everything in one place)
  - Simple deployment
  - Good performance (no network calls)
- **Cons**:
  - Hard to scale (must scale everything)
  - Long build times
  - Technology lock-in
  - Hard to understand (large codebase)
  - Risky deployments (one bug takes down everything)

**Microservices Architecture**:
```
Frontend
├── User Service (User DB)
├── Product Service (Product DB)
├── Order Service (Order DB)
├── Payment Service (Payment DB)
└── Notification Service
```
- **Pros**:
  - Scalable (scale individual services)
  - Technology flexibility (different tech per service)
  - Fault isolation (one service down doesn't kill all)
  - Small teams, independent deployment
  - Better CI/CD
- **Cons**:
  - Complex (distributed system challenges)
  - Network latency
  - Data consistency issues
  - Difficult testing
  - Operational overhead (deploy/monitor many services)

**When to Use Microservices?**
- Team size > 10-15 people
- Need to scale specific features differently
- Different parts need different technologies
- Frequent deployments
- Mature DevOps practices

**When NOT to Use Microservices?**
- Small team (< 10 people)
- Early stage startup (iterate fast)
- Simple application
- Immature DevOps
- **Start with monolith, migrate to microservices when needed**

**Service Boundaries (Domain-Driven Design):**

- **Bounded Context**: Each service owns a domain
- **Example: E-commerce**
  - User Service: Authentication, profiles
  - Catalog Service: Products, categories, search
  - Cart Service: Shopping cart management
  - Order Service: Order processing, fulfillment
  - Payment Service: Payments, refunds
  - Inventory Service: Stock management
  - Notification Service: Emails, SMS, push notifications

- **How to Define Boundaries?**
  - **Business capabilities**: What does the business do?
  - **Data ownership**: One service owns one set of tables
  - **Change frequency**: Things that change together, stay together
  - **Team structure**: One team per service (Conway's Law)

**Inter-Service Communication:**

1. **Synchronous** (Request-Response):
   
   **REST APIs**:
   - HTTP-based
   - Easy to understand
   - Language-agnostic
   - Example:
     ```
     GET /users/123
     POST /orders
     PUT /products/456
     DELETE /cart/items/789
     ```
   - Pros: Simple, widely supported, human-readable
   - Cons: Slower than binary protocols, verbose

   **gRPC**:
   - Binary protocol (Protocol Buffers)
   - Fast, efficient
   - Strong typing (schema defined)
   - Example:
     ```protobuf
     service UserService {
       rpc GetUser(UserRequest) returns (UserResponse);
     }
     ```
   - Pros: Fast, type-safe, streaming support
   - Cons: Less human-readable, requires tooling

2. **Asynchronous** (Event-Driven):
   
   **Message Queue** (Point-to-Point):
   - Producer sends message to queue
   - One consumer processes message
   - Example: RabbitMQ, AWS SQS
   - Use case: Task distribution

   **Publish-Subscribe**:
   - Publisher emits event
   - Multiple subscribers receive event
   - Example: Apache Kafka, AWS SNS
   - Use case: Event notifications
   - Example:
     ```
     Event: OrderCreated
     Subscribers:
     - Inventory Service (reduce stock)
     - Email Service (send confirmation)
     - Analytics Service (track metrics)
     ```

**Service Discovery:**

- **Problem**: Services need to find each other (IP addresses change)
- **Solutions**:

  1. **Client-Side Discovery**:
     - Service registers with registry (Consul, etcd)
     - Client queries registry for service location
     - Client load balances across instances
     - Example: Netflix Eureka

  2. **Server-Side Discovery**:
     - Client requests via load balancer
     - Load balancer queries registry
     - Load balancer routes request
     - Example: AWS ELB, Kubernetes Service

  3. **DNS-Based**:
     - Each service has DNS name
     - DNS resolves to service instances
     - Simple but limited load balancing

**API Gateway Pattern:**
- Single entry point for all clients
- Routes requests to appropriate services
- **Responsibilities**:
  - Authentication & Authorization
  - Rate limiting
  - Request/Response transformation
  - Aggregation (combine multiple service calls)
  - Caching
  - Load balancing
  - Monitoring & Logging

**Challenges and Solutions:**

| Challenge | Solution |
|-----------|----------|
| Distributed transactions | Saga pattern |
| Data consistency | Eventual consistency, event sourcing |
| Cascading failures | Circuit breaker, timeouts |
| Monitoring | Distributed tracing (Jaeger), centralized logging |
| Testing | Contract testing, consumer-driven contracts |
| Security | Service mesh (Istio), mutual TLS |

---

**Back-of-Envelope Calculations:**

**Why Important?**
- Estimate system capacity in interviews
- Make design decisions (how many servers?)
- Plan costs

**Key Numbers to Remember** (Powers of 2):
```
1 KB = 1,000 bytes (actually 1,024)
1 MB = 1,000 KB = 1 million bytes
1 GB = 1,000 MB = 1 billion bytes
1 TB = 1,000 GB = 1 trillion bytes
1 PB = 1,000 TB = 1 quadrillion bytes
```

**Time Units**:
```
1 second = 1,000 milliseconds (ms)
1 ms = 1,000 microseconds (μs)
1 μs = 1,000 nanoseconds (ns)
```

**Latency Numbers** (L1 cache to Network):
```
L1 cache reference: 0.5 ns
L2 cache reference: 7 ns
Main memory reference: 100 ns
Send 1K bytes over 1 Gbps network: 10,000 ns = 10 μs
SSD random read: 150,000 ns = 150 μs
Read 1 MB sequentially from SSD: 1,000,000 ns = 1 ms
Disk seek: 10,000,000 ns = 10 ms
Read 1 MB sequentially from disk: 20,000,000 ns = 20 ms
Send packet CA -> Netherlands -> CA: 150,000,000 ns = 150 ms
```

**Takeaways**:
- Memory is fast (100 ns)
- SSD is okay (150 μs)
- Disk is slow (10 ms)
- Network is variable (10 μs to 150 ms)

**Typical System Values**:
```
QPS for single server: 1,000 - 10,000
Database queries per second: 1,000 - 5,000
Cache requests per second: 100,000 - 1,000,000
Characters per tweet: 280
Characters per SMS: 160
```

**Calculation Frameworks:**

**1. QPS (Queries Per Second)**:
```
QPS = (Daily Active Users × Actions per User) / 86400

Example: Twitter
- 300 million DAU
- Average 5 tweets/day per user
- Peak is 3x average
Average QPS = (300M × 5) / 86400 = 17,361 QPS
Peak QPS = 17,361 × 3 = 52,083 QPS
```

**2. Storage Estimation**:
```
Storage = Number of Items × Size per Item

Example: Instagram Photos
- 500 million photos/day
- Average photo size: 2 MB
Daily Storage = 500M × 2 MB = 1,000 TB = 1 PB/day
5-year Storage = 1 PB × 365 × 5 = 1,825 PB = 1.8 EB
```

**3. Bandwidth Calculation**:
```
Bandwidth = (Data Size × QPS) / 1,000,000 (for Mbps)

Example: Video Streaming
- Average video bitrate: 5 Mbps
- 1 million concurrent viewers
Total Bandwidth = 5 Mbps × 1M = 5 Tbps
```

**4. Server Estimation**:
```
Servers = (Peak QPS × Response Time) / 1 second

Example:
- Peak QPS = 50,000
- Response time = 100 ms = 0.1 second
- Each server handles: 1 / 0.1 = 10 requests simultaneously
Servers = 50,000 / 10 = 5,000 servers
Add 30% buffer: 6,500 servers
```

**5. Database Shard Calculation**:
```
Shards = Total Data / Max Shard Size

Example:
- Total data: 10 TB
- Max shard size: 1 TB (for manageability)
Shards = 10 TB / 1 TB = 10 shards

Or based on QPS:
- Total write QPS: 100,000
- Single DB handles: 10,000 QPS
Shards = 100,000 / 10,000 = 10 shards
```

**6. Cache Size Estimation**:
```
Cache Size = Hot Data Percentage × Total Data

Example:
- Total data: 1 TB
- 80-20 rule: 20% of data gets 80% of traffic
Cache Size = 0.2 × 1 TB = 200 GB
```

#### 💻 Practice Tasks:

**1. Design Microservices for E-commerce:**

Break down monolith:
```
Services:
1. User Service
   - Registration, authentication, profiles
   - Database: users table
   
2. Product Catalog Service
   - Products, categories, search
   - Database: products, categories tables
   
3. Shopping Cart Service
   - Add/remove items, calculate total
   - Database: carts, cart_items (or Redis for temp data)
   
4. Order Service
   - Create orders, order history
   - Database: orders, order_items tables
   
5. Payment Service
   - Process payments, refunds
   - Database: payments table
   - External: Stripe API
   
6. Inventory Service
   - Stock management, reservations
   - Database: inventory table
   
7. Shipping Service
   - Tracking, fulfillment
   - Database: shipments table
   - External: FedEx/UPS APIs
   
8. Notification Service
   - Emails, SMS, push notifications
   - Message queue: consume events
   - External: SendGrid, Twilio
   
9. Analytics Service
   - User behavior, sales metrics
   - Database: Events (time-series)
```

**Communication Design**:
```
Synchronous (REST):
- Frontend → API Gateway
- API Gateway → Individual services
- Cart Service → Product Service (get product details)

Asynchronous (Events):
- Order Service emits "OrderCreated" event
  → Inventory Service (reduce stock)
  → Payment Service (charge customer)
  → Notification Service (send confirmation email)
  → Analytics Service (track conversion)
```

**2. Calculate Twitter Scale**:

**Given**:
- 500 million DAU
- Average user:
  - Posts 2 tweets/day
  - Views 100 tweets/day
  - Follows 200 people
- Average tweet: 280 characters + metadata
- 10% of tweets have images (200 KB)
- 1% of tweets have videos (2 MB)

**Calculate**:

**a) QPS (Queries Per Second)**:
```
Write QPS:
- Daily tweets = 500M × 2 = 1 billion tweets/day
- Average write QPS = 1B / 86400 = 11,574 QPS
- Peak write QPS (3x) = 34,722 QPS

Read QPS:
- Daily reads = 500M × 100 = 50 billion reads/day
- Average read QPS = 50B / 86400 = 578,703 QPS
- Peak read QPS (3x) = 1,736,111 QPS
```

**b) Storage**:
```
Text:
- 1B tweets/day × 1 KB (text + metadata) = 1 TB/day

Images:
- 1B × 10% × 200 KB = 20 TB/day

Videos:
- 1B × 1% × 2 MB = 20 TB/day

Total: 1 + 20 + 20 = 41 TB/day
5-year storage: 41 TB × 365 × 5 = 74.8 PB
```

**c) Bandwidth**:
```
Upload:
- Text: 11,574 QPS × 1 KB = 11.5 MB/s
- Images: 11,574 × 10% × 200 KB = 231 MB/s
- Videos: 11,574 × 1% × 2 MB = 231 MB/s
Total upload: 474 MB/s = 3.8 Gbps

Download:
- Text: 578,703 QPS × 1 KB = 579 MB/s
- Images: 578,703 × 10% × 200 KB = 11,574 MB/s = 11.5 GB/s
- Videos: 578,703 × 1% × 2 MB = 11,574 MB/s = 11.5 GB/s
Total download: 23.5 GB/s = 188 Gbps
```

**d) Cache Size**:
```
Assume 80-20 rule: 20% of tweets get 80% of reads
Cache hot tweets: 74.8 PB × 20% = 15 PB

But cache for 1 day of data is more practical:
41 TB × 20% = 8.2 TB cache
```

**e) Number of Servers**:
```
Assume:
- Each server handles 1000 QPS
- Peak read QPS = 1,736,111

Servers for reads: 1,736,111 / 1000 = 1,737 servers
Add 30% buffer: 2,258 servers

Servers for writes: 34,722 / 1000 = 35 servers
```

**3. Calculate Storage for WhatsApp**:

**Given**:
- 2 billion users
- 50 messages per user per day
- Average message: 100 bytes
- 10% of messages have media (average 500 KB)
- 5-year retention

**Calculate**:
```
Messages per day:
2B users × 50 messages = 100 billion messages/day

Text storage:
100B × 100 bytes = 10 TB/day

Media storage:
100B × 10% × 500 KB = 5 PB/day

Total daily: 10 TB + 5 PB ≈ 5 PB/day
5-year storage: 5 PB × 365 × 5 = 9,125 PB = 9.1 EB
```

**4. Calculate Database Shards for Instagram**:

**Given**:
- 1 billion users
- Each user posts 0.5 photos/day (average)
- User data: 1 KB per user
- Photo metadata: 1 KB per photo
- Each shard max: 1 TB

**Calculate**:
```
User data:
1B users × 1 KB = 1 TB
Shards for users: 1 TB / 1 TB = 1 shard (but use 10 for distribution)

Photo metadata:
- 1B × 0.5 = 500M photos/day
- 1 year: 500M × 365 = 182.5B photos
- Storage: 182.5B × 1 KB = 182.5 TB
Shards for photos: 182.5 / 1 = 183 shards
```

**5. Server Capacity for Netflix**:

**Given**:
- 100 million concurrent viewers
- Average video bitrate: 5 Mbps
- Video stored at multiple qualities: 1 Mbps, 3 Mbps, 5 Mbps, 10 Mbps

**Calculate**:
```
Bandwidth:
100M viewers × 5 Mbps = 500 million Mbps = 500 Tbps

Origin servers (for encoding):
- 10,000 hours of content uploaded/day
- Each hour takes 10 minutes to encode
- Encoding slots: 10,000 × (10/60) / 24 = 69 servers

CDN edge servers:
- Use CDN for delivery (Cloudflare, Akamai)
- Netflix uses AWS CloudFront + own CDN (Open Connect)
```

#### 📖 Resources & Key Questions:

**Key Formulas** (Memorize These!):
```
QPS = (DAU × Actions/User) / 86,400
Storage = Num_Items × Size_Per_Item × Retention_Days
Bandwidth (Mbps) = QPS × Avg_Object_Size_KB × 8 / 1,000
Servers = Peak_QPS / QPS_Per_Server
Cache_Size = Total_Data × Hot_Data_Percentage

Conversions:
1 million ≈ 10^6 ≈ 2^20
1 billion ≈ 10^9 ≈ 2^30
1 day = 86,400 seconds ≈ 100,000 seconds
```

**Standard Assumptions for Interviews**:
```
- Single server handles: 1,000-10,000 QPS (depending on complexity)
- Database handles: 1,000-5,000 QPS
- Cache (Redis) handles: 100,000-500,000 QPS
- Peak traffic is 2-3x average
- 80-20 rule: 20% of data gets 80% of traffic
- User session: 30 minutes average
- Mobile app: Opens 5-10 times/day
- 1 char = 1 byte (approximately)
- Image: 200 KB - 1 MB
- Video (1 min): 5-10 MB
```

**Resources**:
- "System Design Interview" by Alex Xu (Chapter on Estimation)
- "Building Microservices" by Sam Newman
- Martin Fowler's blog on Microservices
- AWS Well-Architected Framework
- Google SRE Book

**Key Questions**:
1. When should you use microservices vs monolith?
2. How do you define service boundaries?
3. Synchronous (REST) vs Asynchronous (events) - when to use each?
4. How to handle distributed transactions in microservices? (Saga!)
5. How many servers for 100K QPS?
6. How much storage for 1B users, 5 years retention?
7. What's 80-20 rule and why does it matter?
8. How to estimate cache size?

**Interview Tips**:
- Always state assumptions clearly
- Round numbers for simplicity (86,400 ≈ 100,000)
- Show your work (write calculations)
- Discuss peak vs average
- Consider redundancy (3x replication = 3x storage)
- Add 20-30% buffer for safety

---

### Day 19: Event-Driven Architecture

#### 🎯 Core Concepts to Learn:

**What is Event-Driven Architecture (EDA)?**

- **Definition**: System design where components communicate through events
- **Event**: Significant change in state
  - Examples: UserRegistered, OrderPlaced, PaymentProcessed, InventoryUpdated
- **Components**:
  - **Event Producer**: Generates events
  - **Event Channel**: Message broker (Kafka, RabbitMQ, AWS SNS)
  - **Event Consumer**: Reacts to events

**Benefits of EDA:**
- **Loose Coupling**: Services don't need to know about each other
- **Scalability**: Add consumers without changing producers
- **Flexibility**: New features by adding new consumers
- **Real-time**: React to changes immediately
- **Resilience**: Async means services don't block each other

**Challenges of EDA:**
- **Complexity**: Harder to trace flow
- **Debugging**: Events spread across system
- **Eventual Consistency**: No immediate consistency
- **Duplicate Events**: Must handle retries
- **Ordering**: Events may arrive out of order

---

**Event Sourcing:**

**Core Idea**: Store all changes as sequence of events, not current state

**Traditional Approach** (State-Based):
```
User account balance: $100
UPDATE accounts SET balance = 70 WHERE user_id = 123;
Current state: $100 → $70
Lost information: How did we get here?
```

**Event Sourcing Approach**:
```
Events (append-only log):
1. AccountCreated(user_id=123, initial_balance=0)
2. MoneyDeposited(user_id=123, amount=100, timestamp=...)
3. MoneyWithdrawn(user_id=123, amount=30, timestamp=...)

Current State (derived by replaying):
balance = 0 + 100 - 30 = $70

Full history preserved!
```

**Benefits**:
- **Audit Trail**: Complete history of all changes
- **Time Travel**: Replay events to any point in time
- **Debugging**: See exactly what happened
- **Event Replay**: Fix bugs by reprocessing events
- **Multiple Views**: Build different projections from same events

**Challenges**:
- **Storage**: Events grow indefinitely (need snapshots)
- **Complexity**: More complex than CRUD
- **Schema Changes**: Old events may have different schema
- **Performance**: Replaying many events can be slow

**Event Sourcing Pattern**:
```
Command → Aggregate → Events → Event Store
                          ↓
                    Event Handlers → Read Models
```

**Example: Bank Account**
```python
class BankAccount:
    def __init__(self):
        self.balance = 0
        self.events = []
    
    def deposit(self, amount):
        # Validate
        if amount <= 0:
            raise ValueError("Amount must be positive")
        
        # Create event
        event = MoneyDeposited(amount, timestamp=now())
        
        # Apply event
        self.apply(event)
        
        # Store event
        self.events.append(event)
    
    def apply(self, event):
        if isinstance(event, AccountCreated):
            self.balance = event.initial_balance
        elif isinstance(event, MoneyDeposited):
            self.balance += event.amount
        elif isinstance(event, MoneyWithdrawn):
            self.balance -= event.amount
    
    def rebuild_from_events(self, events):
        for event in events:
            self.apply(event)
```

**Snapshots**:
- Problem: Replaying 1 million events is slow
- Solution: Periodically save snapshot of current state
- Rebuild: Load snapshot + replay events since snapshot
- Example:
  ```
  Snapshot at event 1000: balance = $5,000
  New events 1001-1050: 50 events
  Current state: snapshot + 50 events (much faster)
  ```

---

**CQRS (Command Query Responsibility Segregation):**

**Core Idea**: Separate write model from read model

**Traditional Approach** (Same Model for Reads and Writes):
```
Database (Normalized)
├── Users table
├── Orders table
├── OrderItems table
└── Products table

Read: JOIN 3 tables for order details
Write: UPDATE 3 tables for order
```

**CQRS Approach** (Separate Models):
```
Write Side (Command):
- Optimized for writes
- Normalized schema
- Enforce business rules
- Emit events

Event Store

Read Side (Query):
- Optimized for reads
- Denormalized views
- Fast queries
- Built from events
```

**Example: E-commerce Orders**

**Write Model**:
```
Commands:
- PlaceOrder(user_id, items)
- CancelOrder(order_id)
- UpdateShippingAddress(order_id, address)

Database (Normalized):
- orders (id, user_id, status, total)
- order_items (id, order_id, product_id, quantity, price)

Events Emitted:
- OrderPlaced
- OrderCancelled
- ShippingAddressUpdated
```

**Read Models** (Multiple Views):
```
1. OrderDetails View (for users):
   - Denormalized: order + items + product names
   - Fast reads: Single table query

2. OrderHistory View (for users):
   - Simple list: order_id, date, total, status

3. AdminOrders View (for admins):
   - Different columns: order_id, user, status, fulfillment_center

4. Analytics View (for business):
   - Aggregated: daily_sales, popular_products
```

**Benefits**:
- **Scalable Reads**: Read models can be replicated
- **Optimized Queries**: Each read model designed for specific use case
- **Independent Scaling**: Scale reads and writes separately
- **Multiple Representations**: Same data, different views

**Challenges**:
- **Complexity**: Maintain multiple models
- **Eventual Consistency**: Read models lag behind writes
- **Synchronization**: Keep read models updated

**CQRS + Event Sourcing**:
- Perfect combination
- Events from Event Store update Read Models
- Write side: Append events
- Read side: Project events into views

---

**Event Streaming with Kafka:**

**What is Kafka?**
- Distributed event streaming platform
- High throughput (millions of messages/second)
- Persistent storage (events stored on disk)
- Pub/Sub + Message Queue

**Core Concepts**:

1. **Topic**: Category of events
   - Example topics: "orders", "payments", "user-activity"

2. **Partition**: Shard of topic for parallelism
   - Topic split into N partitions
   - Each partition is ordered log
   - Messages with same key go to same partition
   - Example:
     ```
     Topic: orders (3 partitions)
     Partition 0: Orders from users A-F
     Partition 1: Orders from users G-M
     Partition 2: Orders from users N-Z
     ```

3. **Producer**: Publishes events to topics
   ```python
   producer.send(
       topic='orders',
       key=user_id,  # Ensures user's orders go to same partition
       value=order_data
   )
   ```

4. **Consumer**: Subscribes to topics and processes events
   ```python
   consumer.subscribe(topics=['orders'])
   for message in consumer:
       process_order(message.value)
   ```

5. **Consumer Group**: Multiple consumers working together
   - Each partition consumed by one consumer in group
   - Enables parallel processing
   - Example:
     ```
     Consumer Group: order-processors
     Consumer 1: Processes partition 0
     Consumer 2: Processes partition 1
     Consumer 3: Processes partition 2
     ```

6. **Offset**: Position in partition
   - Each message has offset (like index)
   - Consumer tracks its offset
   - Can replay by resetting offset

**Kafka Guarantees**:
- **Ordering**: Within partition, events are ordered
- **Durability**: Events persisted to disk, replicated
- **At-least-once**: Events delivered at least once (may have duplicates)
- **Exactly-once**: Can be configured (complex)

**Use Cases**:
- **Activity Tracking**: User clicks, page views
- **Metrics Collection**: Application logs, system metrics
- **Log Aggregation**: Centralize logs from multiple services
- **Stream Processing**: Real-time analytics
- **Event Sourcing**: Store events
- **Commit Log**: Replicate databases

**Kafka vs Traditional Message Queue**:

| Feature | Kafka | RabbitMQ |
|---------|-------|----------|
| Message Persistence | Long-term (days/weeks) | Short-term (until consumed) |
| Throughput | Very high (millions/sec) | High (tens of thousands/sec) |
| Message Ordering | Per partition | Per queue |
| Message Replay | Yes (rewind offset) | No (consumed = gone) |
| Use Case | Event streaming, logs | Task queues, RPC |

---

**Saga Patterns for Distributed Transactions:**
(Covered in detail on Day 16, but relevant here for event-driven context)

**Choreography** (Event-Based Saga):
- No central coordinator
- Each service publishes events
- Next service reacts to event
- Example:
  ```
  Order Service: OrderPlaced event →
  Payment Service: Listens, processes, emits PaymentCompleted →
  Inventory Service: Listens, reserves items, emits InventoryReserved →
  Shipping Service: Listens, ships, emits OrderShipped
  ```

**Orchestration** (Command-Based Saga):
- Central orchestrator directs flow
- Orchestrator commands each service
- Example:
  ```
  Saga Orchestrator:
  1. Command: Process Payment → Payment Service
  2. Wait for response
  3. Command: Reserve Inventory → Inventory Service
  4. Wait for response
  5. Command: Ship Order → Shipping Service
  ```

---

#### 💻 Practice Tasks:

**1. Implement Event Sourcing for Shopping Cart**:

```python
from datetime import datetime
from typing import List

class Event:
    def __init__(self):
        self.timestamp = datetime.now()

class CartCreated(Event):
    def __init__(self, cart_id, user_id):
        super().__init__()
        self.cart_id = cart_id
        self.user_id = user_id

class ItemAdded(Event):
    def __init__(self, cart_id, product_id, quantity, price):
        super().__init__()
        self.cart_id = cart_id
        self.product_id = product_id
        self.quantity = quantity
        self.price = price

class ItemRemoved(Event):
    def __init__(self, cart_id, product_id):
        super().__init__()
        self.cart_id = cart_id
        self.product_id = product_id

class CartCheckedOut(Event):
    def __init__(self, cart_id, total):
        super().__init__()
        self.cart_id = cart_id
        self.total = total

class ShoppingCart:
    def __init__(self, cart_id, user_id):
        self.cart_id = cart_id
        self.user_id = user_id
        self.items = {}  # product_id -> {quantity, price}
        self.checked_out = False
        self.events = []
        
        # Record creation
        self._apply_event(CartCreated(cart_id, user_id))
    
    def add_item(self, product_id, quantity, price):
        if self.checked_out:
            raise ValueError("Cannot modify checked out cart")
        
        event = ItemAdded(self.cart_id, product_id, quantity, price)
        self._apply_event(event)
    
    def remove_item(self, product_id):
        if product_id not in self.items:
            raise ValueError("Item not in cart")
        
        event = ItemRemoved(self.cart_id, product_id)
        self._apply_event(event)
    
    def checkout(self):
        if self.checked_out:
            raise ValueError("Already checked out")
        
        total = sum(item['quantity'] * item['price'] 
                   for item in self.items.values())
        
        event = CartCheckedOut(self.cart_id, total)
        self._apply_event(event)
    
    def _apply_event(self, event):
        # Apply event to state
        if isinstance(event, CartCreated):
            pass  # Already initialized
        
        elif isinstance(event, ItemAdded):
            if event.product_id in self.items:
                self.items[event.product_id]['quantity'] += event.quantity
            else:
                self.items[event.product_id] = {
                    'quantity': event.quantity,
                    'price': event.price
                }
        
        elif isinstance(event, ItemRemoved):
            del self.items[event.product_id]
        
        elif isinstance(event, CartCheckedOut):
            self.checked_out = True
        
        # Store event
        self.events.append(event)
    
    @classmethod
    def rebuild_from_events(cls, events: List[Event]):
        if not events or not isinstance(events[0], CartCreated):
            raise ValueError("First event must be CartCreated")
        
        cart = cls(events[0].cart_id, events[0].user_id)
        cart.events = []  # Clear creation event
        
        for event in events:
            cart._apply_event(event)
        
        return cart

# Usage
cart = ShoppingCart("cart-123", "user-456")
cart.add_item("product-1", 2, 29.99)
cart.add_item("product-2", 1, 49.99)
cart.remove_item("product-1")
cart.add_item("product-3", 1, 99.99)
cart.checkout()

# Replay events
events = cart.events
rebuilt_cart = ShoppingCart.rebuild_from_events(events)
print(rebuilt_cart.items)  # Same state as original cart
```

**Exercise**:
- Add snapshot functionality (save state every 10 events)
- Implement event versioning (handle schema changes)
- Add time-travel queries ("What was cart state at 2 PM?")

**2. Design CQRS for Blog Platform**:

**Write Model** (Commands):
```python
# Commands
class CreatePost:
    def __init__(self, author_id, title, content):
        self.author_id = author_id
        self.title = title
        self.content = content

class PublishPost:
    def __init__(self, post_id):
        self.post_id = post_id

class AddComment:
    def __init__(self, post_id, author_id, content):
        self.post_id = post_id
        self.author_id = author_id
        self.content = content

# Write Model (Database)
posts = {
    'id': 'uuid',
    'author_id': 'uuid',
    'title': 'string',
    'content': 'text',
    'status': 'draft|published',
    'created_at': 'timestamp'
}

comments = {
    'id': 'uuid',
    'post_id': 'uuid',
    'author_id': 'uuid',
    'content': 'text',
    'created_at': 'timestamp'
}

# Events Emitted
- PostCreated(post_id, author_id, title)
- PostPublished(post_id, published_at)
- CommentAdded(comment_id, post_id, author_id, content)
```

**Read Models**:
```python
# Read Model 1: Post List (for homepage)
post_list = {
    'post_id': 'uuid',
    'title': 'string',
    'author_name': 'string',  # Denormalized!
    'excerpt': 'string',
    'published_at': 'timestamp',
    'comment_count': 'int'  # Precomputed!
}

# Read Model 2: Post Detail (for individual post page)
post_detail = {
    'post_id': 'uuid',
    'title': 'string',
    'content': 'text',
    'author_name': 'string',
    'author_avatar': 'url',
    'published_at': 'timestamp',
    'comments': [  # Embedded!
        {
            'comment_id': 'uuid',
            'author_name': 'string',
            'content': 'text',
            'created_at': 'timestamp'
        }
    ]
}

# Read Model 3: Author Posts (for author profile)
author_posts = {
    'author_id': 'uuid',
    'author_name': 'string',
    'post_count': 'int',
    'posts': [
        {
            'post_id': 'uuid',
            'title': 'string',
            'published_at': 'timestamp',
            'comment_count': 'int'
        }
    ]
}
```

**Event Handlers** (Update Read Models):
```python
def handle_post_published(event: PostPublished):
    # Update Read Model 1: Post List
    post_data = get_post_from_write_db(event.post_id)
    author_name = get_author_name(post_data.author_id)
    
    post_list_db.insert({
        'post_id': event.post_id,
        'title': post_data.title,
        'author_name': author_name,
        'excerpt': post_data.content[:200],
        'published_at': event.published_at,
        'comment_count': 0
    })
    
    # Update Read Model 3: Author Posts
    author_posts_db.update(
        author_id=post_data.author_id,
        increment_post_count=1,
        add_post={
            'post_id': event.post_id,
            'title': post_data.title,
            'published_at': event.published_at,
            'comment_count': 0
        }
    )

def handle_comment_added(event: CommentAdded):
    # Update Read Model 1: Increment comment count
    post_list_db.update(
        post_id=event.post_id,
        increment_comment_count=1
    )
    
    # Update Read Model 2: Add comment to post detail
    author_name = get_author_name(event.author_id)
    post_detail_db.update(
        post_id=event.post_id,
        add_comment={
            'comment_id': event.comment_id,
            'author_name': author_name,
            'content': event.content,
            'created_at': event.created_at
        }
    )
```

**Exercise**:
- Implement command handlers
- Implement event handlers
- Handle eventual consistency (what if user refreshes immediately after posting?)
- Add caching layer for read models

**3. Build Event-Driven Order System with Kafka**:

```python
from kafka import KafkaProducer, KafkaConsumer
import json

# Producer: Order Service
class OrderService:
    def __init__(self):
        self.producer = KafkaProducer(
            bootstrap_servers=['localhost:9092'],
            value_serializer=lambda v: json.dumps(v).encode('utf-8')
        )
    
    def create_order(self, user_id, items, total):
        order = {
            'order_id': generate_uuid(),
            'user_id': user_id,
            'items': items,
            'total': total,
            'status': 'created',
            'timestamp': now()
        }
        
        # Publish event
        self.producer.send(
            topic='orders',
            key=user_id.encode('utf-8'),
            value=order
        )
        
        return order

# Consumer: Inventory Service
class InventoryService:
    def __init__(self):
        self.consumer = KafkaConsumer(
            'orders',
            bootstrap_servers=['localhost:9092'],
            group_id='inventory-service',
            value_deserializer=lambda m: json.loads(m.decode('utf-8'))
        )
        self.producer = KafkaProducer(
            bootstrap_servers=['localhost:9092'],
            value_serializer=lambda v: json.dumps(v).encode('utf-8')
        )
    
    def start(self):
        for message in self.consumer:
            order = message.value
            
            # Process order
            try:
                self.reserve_inventory(order['items'])
                
                # Publish success event
                self.producer.send(
                    topic='inventory-reserved',
                    value={
                        'order_id': order['order_id'],
                        'status': 'success'
                    }
                )
            except InsufficientInventoryError:
                # Publish failure event
                self.producer.send(
                    topic='inventory-failed',
                    value={
                        'order_id': order['order_id'],
                        'status': 'failed',
                        'reason': 'insufficient inventory'
                    }
                )

# Consumer: Payment Service
class PaymentService:
    def __init__(self):
        self.consumer = KafkaConsumer(
            'inventory-reserved',
            bootstrap_servers=['localhost:9092'],
            group_id='payment-service',
            value_deserializer=lambda m: json.loads(m.decode('utf-8'))
        )
        self.producer = KafkaProducer(
            bootstrap_servers=['localhost:9092'],
            value_serializer=lambda v: json.dumps(v).encode('utf-8')
        )
    
    def start(self):
        for message in self.consumer:
            event = message.value
            order_id = event['order_id']
            
            # Get order details
            order = get_order(order_id)
            
            # Process payment
            try:
                payment_id = self.charge_card(order['user_id'], order['total'])
                
                # Publish success
                self.producer.send(
                    topic='payment-completed',
                    value={
                        'order_id': order_id,
                        'payment_id': payment_id,
                        'status': 'success'
                    }
                )
            except PaymentError:
                # Publish failure (will trigger compensation)
                self.producer.send(
                    topic='payment-failed',
                    value={
                        'order_id': order_id,
                        'status': 'failed'
                    }
                )
                
                # Trigger inventory release
                self.producer.send(
                    topic='release-inventory',
                    value={'order_id': order_id}
                )
```

**Exercise**:
- Add shipping service consumer
- Implement compensation for failures
- Add dead letter queue for failed messages
- Monitor offset lag
- Implement idempotency (handle duplicate messages)

**4. Compare Saga Patterns**:

Design order processing with both patterns:

**Choreography**:
```
Services: Order, Inventory, Payment, Shipping

Events:
OrderPlaced → 
    Inventory listens, reserves → InventoryReserved →
        Payment listens, charges → PaymentCompleted →
            Shipping listens, ships → OrderShipped

Failure (Payment Fails):
PaymentFailed →
    Inventory listens → InventoryReleased →
    Order listens → OrderCancelled
```

Pros:
- No single point of failure
- Services loosely coupled
- Easy to add new services

Cons:
- Hard to understand flow
- Difficult to debug
- No central monitoring

**Orchestration**:
```
Orchestrator:
1. Call Inventory.reserve()
2. If success: Call Payment.charge()
3. If success: Call Shipping.ship()
4. If any fails: Call compensations in reverse
```

Pros:
- Clear flow
- Easy to monitor
- Centralized error handling

Cons:
- Orchestrator is single point of failure
- Orchestrator becomes complex
- Services coupled to orchestrator

**When to Use Each**:
- **Choreography**: Simple flows, few services, high autonomy
- **Orchestration**: Complex flows, many services, need visibility

**5. Design Analytics Pipeline**:

**Requirements**:
- Collect user activity events (clicks, page views, purchases)
- Real-time processing
- Multiple consumers (analytics, recommendations, fraud detection)

**Architecture**:
```
Frontend → API Gateway → Kafka Topic: user-activity

Consumers:
1. Analytics Service:
   - Consumes events
   - Aggregates metrics (DAU, page views, conversion rate)
   - Stores in time-series database (InfluxDB)
   - Updates dashboards (Grafana)

2. Recommendation Service:
   - Consumes events
   - Updates user profiles
   - Trains ML models
   - Generates recommendations

3. Fraud Detection Service:
   - Consumes events
   - Detects suspicious patterns
   - Triggers alerts
   - Blocks accounts if necessary
```

**Event Schema**:
```json
{
  "event_type": "page_view",
  "user_id": "user-123",
  "session_id": "session-456",
  "page": "/products/abc",
  "timestamp": "2025-01-15T10:30:00Z",
  "metadata": {
    "referrer": "google.com",
    "device": "mobile",
    "location": "US"
  }
}
```

**Exercise**:
- Implement event producers
- Implement multiple consumers
- Handle schema evolution
- Implement stream processing (windowed aggregations)

#### 📖 Resources & Key Questions:

**Key Concepts Summary**:
- **EDA**: Systems communicate via events
- **Event Sourcing**: Store changes as events, not state
- **CQRS**: Separate read and write models
- **Kafka**: Distributed event streaming platform
- **Saga**: Orchestrate long-running transactions with events

**Resources**:
- "Designing Data-Intensive Applications" by Martin Kleppmann (Chapter 11: Stream Processing)
- "Domain-Driven Design" by Eric Evans
- "Implementing Domain-Driven Design" by Vaughn Vernon
- Kafka documentation: https://kafka.apache.org/documentation/
- Martin Fowler's articles on Event Sourcing and CQRS

**Key Questions**:
1. What's the difference between Event Sourcing and Change Data Capture (CDC)?
2. When should you use CQRS without Event Sourcing?
3. How do you handle schema evolution in Event Sourcing?
4. Kafka vs RabbitMQ - when to use each?
5. How do you ensure ordering in Kafka?
6. What are the downsides of event-driven architecture?
7. How do you handle duplicate events (idempotency)?
8. How do you debug event-driven systems?

**Real-World Examples**:
- **Netflix**: Event-driven microservices
- **Uber**: Event sourcing for trips
- **LinkedIn**: Kafka for activity streams
- **Amazon**: Event-driven order processing
- **Twitter**: Event sourcing for tweets

**Interview Questions**:
- "Design a system using event-driven architecture"
- "How would you implement audit trail for all changes?"
- "Explain Event Sourcing and when to use it"
- "How do you handle eventual consistency in CQRS?"
- "Design real-time analytics system with Kafka"

---

### Day 20: Observability & Monitoring

#### 🎯 Core Concepts to Learn:

**Observability vs Monitoring:**

**Monitoring** (Traditional):
- Predefined metrics
- Known failure modes
- Alert when thresholds crossed
- Example: CPU > 80% → Alert

**Observability** (Modern):
- Understand system from outputs
- Discover unknown unknowns
- Answer arbitrary questions
- Example: "Why is checkout slow for users in California?"

**Three Pillars of Observability:**

**1. Metrics** (Aggregated Numbers):
- **What**: Numerical measurements over time
- **Examples**:
  - Request rate (requests/second)
  - Error rate (errors/second)
  - Latency (p50, p95, p99)
  - CPU usage (%)
  - Memory usage (MB)
  - Queue depth (messages)

- **Types**:
  - **Counter**: Only increases (total requests)
  - **Gauge**: Can go up or down (current memory)
  - **Histogram**: Distribution of values (latency distribution)

- **Storage**: Time-series databases (Prometheus, InfluxDB, Graphite)

**2. Logs** (Discrete Events):
- **What**: Text records of events
- **Examples**:
  ```
  [2025-01-15 10:30:45] INFO User 123 logged in
  [2025-01-15 10:30:46] ERROR Payment failed for order 456: Insufficient funds
  [2025-01-15 10:30:47] WARN High memory usage: 85%
  ```

- **Structured Logs** (Better):
  ```json
  {
    "timestamp": "2025-01-15T10:30:46Z",
    "level": "ERROR",
    "message": "Payment failed",
    "order_id": "456",
    "user_id": "123",
    "error": "Insufficient funds",
    "amount": 99.99
  }
  ```

- **Log Levels**:
  - DEBUG: Detailed debugging info
  - INFO: General information
  - WARN: Warning, potential issues
  - ERROR: Error occurred but service continues
  - FATAL: Critical error, service crashed

- **Storage**: Elasticsearch, Splunk, Loki

**3. Traces** (Request Journey):
- **What**: Follow single request across services
- **Example**:
  ```
  Request ID: abc123
  
  Span 1: API Gateway (20ms)
    ├─ Span 2: Auth Service (5ms)
    └─ Span 3: Order Service (100ms)
         ├─ Span 4: Inventory Service (30ms)
         ├─ Span 5: Payment Service (50ms)
         │    └─ Span 6: External Payment API (40ms)
         └─ Span 7: Database Query (15ms)
  
  Total: 120ms
  ```

- **Distributed Tracing**: Trace across microservices
- **Span**: Single operation (API call, database query)
- **Trace**: Collection of spans for one request

- **Tools**: Jaeger, Zipkin, AWS X-Ray

---

**Distributed Tracing Deep Dive:**

**Why Needed?**
- Microservices: Request touches many services
- Hard to debug: Where is the slow part?
- Distributed tracing shows full picture

**How It Works:**

1. **Generate Trace ID**:
   - First service generates unique trace ID
   - Passes to all downstream services
   - All services log with same trace ID

2. **Generate Span ID**:
   - Each service operation gets span ID
   - Parent-child relationship
   - Example:
     ```
     Trace ID: abc123
     Span 1 (API Gateway): span_id=1, parent_id=null
     Span 2 (Auth Service): span_id=2, parent_id=1
     Span 3 (Order Service): span_id=3, parent_id=1
     Span 4 (Database): span_id=4, parent_id=3
     ```

3. **Record Timing**:
   - Start time
   - End time
   - Duration = End - Start

4. **Add Context**:
   - Service name
   - Operation name
   - Tags (user_id, order_id, http_status)
   - Logs (errors, warnings)

**Example with Code**:
```python
from opentelemetry import trace
from opentelemetry.instrumentation.requests import RequestsInstrumentor

tracer = trace.get_tracer(__name__)

@app.route('/orders')
def create_order():
    # Start span
    with tracer.start_as_current_span("create_order") as span:
        span.set_attribute("user_id", user_id)
        
        # Call inventory service
        with tracer.start_as_current_span("check_inventory"):
            inventory_response = requests.get(f"{INVENTORY_URL}/check")
        
        # Call payment service
        with tracer.start_as_current_span("process_payment"):
            payment_response = requests.post(f"{PAYMENT_URL}/charge")
        
        span.set_attribute("order_id", order_id)
        return {"order_id": order_id}
```

**Trace Context Propagation**:
- HTTP Headers: `traceparent`, `tracestate`
- Example:
  ```
  GET /inventory/check
  Headers:
    traceparent: 00-abc123-def456-01
                 └─ trace_id  └─ span_id
  ```

---

**SLI / SLO / SLA:**

**SLI (Service Level Indicator)**:
- **What**: Metric that measures service health
- **Examples**:
  - Request latency (p99 < 200ms)
  - Error rate (< 0.1%)
  - Availability (uptime %)
  - Throughput (requests/second)

**SLO (Service Level Objective)**:
- **What**: Target value for SLI
- **Examples**:
  - "99.9% of requests complete in < 200ms"
  - "99.99% uptime (52 minutes downtime/year)"
  - "Error rate < 0.1%"

- **Error Budget**:
  - Allowed downtime before breaking SLO
  - Example: 99.9% uptime SLO
    - 0.1% downtime allowed = 43 minutes/month
    - If used up: Freeze feature releases, focus on stability

**SLA (Service Level Agreement)**:
- **What**: Contract with consequences
- **Examples**:
  - "99.9% uptime, or refund 10%"
  - "p99 latency < 200ms, or credit $1000"

**Relationship**:
```
SLA (Legal contract) ≤ SLO (Internal target) < SLI (Measurement)

Example:
SLA: 99.9% uptime (promise to customers)
SLO: 99.95% uptime (internal target, buffer)
SLI: Actual uptime measurement
```

**Setting SLOs**:
1. Identify user-facing metrics (latency, errors, availability)
2. Measure current performance
3. Set achievable but ambitious targets
4. Monitor and adjust

---

**Alerting Best Practices:**

**Types of Alerts:**

1. **Symptom-Based** (User-Facing):
   - Alert on user impact
   - Examples:
     - High error rate
     - Slow response time
     - Service unavailable
   - **Good**: Indicates real problem

2. **Cause-Based** (Internal):
   - Alert on internal issues
   - Examples:
     - High CPU
     - Low disk space
     - Database connection errors
   - **Problem**: May not impact users

**Alert Fatigue Prevention:**

1. **Alert Only When Action Needed**:
   - Bad: "Disk at 60%" (no action needed yet)
   - Good: "Disk at 95%" (needs immediate action)

2. **Reduce Noise**:
   - Use thresholds (not single spike)
   - Example: Alert if error rate > 5% for 5 minutes (not 1 second)

3. **Severity Levels**:
   - **P1 (Critical)**: Service down, page on-call
   - **P2 (High)**: Degraded, notify during business hours
   - **P3 (Medium)**: Track, fix in next sprint
   - **P4 (Low)**: Nice to fix eventually

4. **Actionable Alerts**:
   - Bad: "Service slow"
   - Good: "Order service p99 latency > 1s for 10 minutes. Runbook: wiki.com/latency"

**Golden Signals** (Google SRE):
1. **Latency**: How long requests take
2. **Traffic**: How many requests
3. **Errors**: Rate of failed requests
4. **Saturation**: How "full" the service is (CPU, memory)

---

**Logging Best Practices:**

1. **Structured Logging**:
   ```python
   # Bad (unstructured)
   logger.info(f"User {user_id} ordered {order_id}")
   
   # Good (structured)
   logger.info("Order created", extra={
       "user_id": user_id,
       "order_id": order_id,
       "amount": total,
       "items": item_count
   })
   ```

2. **Log Levels**:
   - Production: INFO and above
   - Development: DEBUG and above

3. **What to Log**:
   - **Always**:
     - Request ID (for tracing)
     - User ID (for debugging)
     - Errors with stack traces
     - Important business events
   - **Sometimes**:
     - Database queries (debug only)
     - External API calls
   - **Never**:
     - Passwords
     - Credit card numbers
     - PII (without hashing)

4. **Log Sampling**:
   - Problem: Too many logs (expensive)
   - Solution: Sample (log 1% of requests)
   - Always log errors (100%)

5. **Centralized Logging**:
   - Collect logs from all servers
   - Tools: ELK Stack (Elasticsearch, Logstash, Kibana), Splunk, Datadog

---

**Monitoring Stack Example:**

**Metrics**: Prometheus + Grafana
```
Application → Prometheus (scrapes metrics)
              ↓
           Grafana (visualizations)
           
Metrics exported:
- http_requests_total (counter)
- http_request_duration_seconds (histogram)
- active_users (gauge)
```

**Logs**: Elasticsearch + Kibana
```
Application → Filebeat (collect logs)
              ↓
           Logstash (parse and transform)
              ↓
           Elasticsearch (store and index)
              ↓
           Kibana (search and visualize)
```

**Traces**: Jaeger
```
Application (instrumented) → Jaeger Agent
                              ↓
                           Jaeger Collector
                              ↓
                           Jaeger Query (UI)
```

---

#### 💻 Practice Tasks:

**1. Implement Distributed Tracing**:

```python
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
from opentelemetry.exporter.jaeger.thrift import JaegerExporter
import time

# Setup tracing
trace.set_tracer_provider(TracerProvider())
tracer = trace.get_tracer(__name__)

jaeger_exporter = JaegerExporter(
    agent_host_name="localhost",
    agent_port=6831,
)

span_processor = BatchSpanProcessor(jaeger_exporter)
trace.get_tracer_provider().add_span_processor(span_processor)

# API Gateway
def api_gateway(request):
    with tracer.start_as_current_span("api_gateway") as span:
        span.set_attribute("http.method", request.method)
        span.set_attribute("http.url", request.url)
        
        # Authenticate
        with tracer.start_as_current_span("authenticate"):
            user_id = authenticate(request.token)
            span.set_attribute("user_id", user_id)
        
        # Process order
        order_id = process_order(user_id, request.items)
        
        span.set_attribute("order_id", order_id)
        return {"order_id": order_id}

# Order Service
def process_order(user_id, items):
    with tracer.start_as_current_span("process_order") as span:
        span.set_attribute("user_id", user_id)
        
        # Check inventory
        with tracer.start_as_current_span("check_inventory"):
            inventory_ok = check_inventory(items)
            span.set_attribute("inventory_ok", inventory_ok)
        
        if not inventory_ok:
            span.set_attribute("error", "insufficient_inventory")
            raise InsufficientInventoryError()
        
        # Process payment
        with tracer.start_as_current_span("process_payment"):
            time.sleep(0.05)  # Simulate payment API
            payment_id = charge_card(user_id, total)
            span.set_attribute("payment_id", payment_id)
        
        # Save order
        with tracer.start_as_current_span("save_order_db"):
            time.sleep(0.01)  # Simulate DB write
            order_id = save_to_database(user_id, items, payment_id)
        
        return order_id
```

**Exercise**:
- Run Jaeger locally (Docker)
- Generate traces for different scenarios
- Analyze slow requests (which service is bottleneck?)
- Add custom attributes (region, experiment_id)
- Implement baggage propagation (context across services)

**2. Set Up Prometheus Monitoring**:

```python
from prometheus_client import Counter, Histogram, Gauge, start_http_server
import time

# Define metrics
request_count = Counter(
    'http_requests_total',
    'Total HTTP requests',
    ['method', 'endpoint', 'status']
)

request_duration = Histogram(
    'http_request_duration_seconds',
    'HTTP request latency',
    ['method', 'endpoint']
)

active_users = Gauge(
    'active_users',
    'Number of active users'
)

# Instrument application
@app.route('/orders', methods=['POST'])
def create_order():
    # Track request
    with request_duration.labels(method='POST', endpoint='/orders').time():
        try:
            # Process order
            result = process_order(request.json)
            
            # Success
            request_count.labels(method='POST', endpoint='/orders', status=200).inc()
            return result, 200
        
        except Exception as e:
            # Error
            request_count.labels(method='POST', endpoint='/orders', status=500).inc()
            raise

# Update gauge periodically
def update_active_users():
    while True:
        count = get_active_user_count()
        active_users.set(count)
        time.sleep(60)

# Start metrics server
start_http_server(8000)  # Metrics exposed at :8000/metrics
```

**Prometheus Config** (`prometheus.yml`):
```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'my-app'
    static_configs:
      - targets: ['localhost:8000']
```

**Grafana Dashboard**:
```
Request Rate:
rate(http_requests_total[5m])

Error Rate:
rate(http_requests_total{status="500"}[5m]) / rate(http_requests_total[5m])

p99 Latency:
histogram_quantile(0.99, rate(http_request_duration_seconds_bucket[5m]))

Active Users:
active_users
```

**Exercise**:
- Set up Prometheus + Grafana
- Create dashboard with golden signals
- Set up alerts (error rate > 1%, latency > 200ms)
- Simulate load and observe metrics

**3. Design SLOs and Error Budget**:

**Scenario**: E-commerce API

**Step 1: Identify SLIs**:
```
1. Availability
   Measurement: Successful requests / Total requests
   Current: 99.95%

2. Latency
   Measurement: p99 request duration
   Current: 150ms

3. Error Rate
   Measurement: 5xx errors / Total requests
   Current: 0.01%
```

**Step 2: Set SLOs** (With Buffer):
```
1. Availability SLO: 99.9%
   (Current: 99.95%, so buffer of 0.05%)

2. Latency SLO: p99 < 200ms
   (Current: 150ms, so buffer of 50ms)

3. Error Rate SLO: < 0.1%
   (Current: 0.01%, so buffer of 0.09%)
```

**Step 3: Calculate Error Budget**:
```
Availability SLO: 99.9%
Error Budget: 100% - 99.9% = 0.1%

Time Period: 30 days = 720 hours = 43,200 minutes
Allowed Downtime: 43,200 × 0.001 = 43.2 minutes/month

If 10 minutes downtime already: 
Remaining Budget: 43.2 - 10 = 33.2 minutes
```

**Step 4: Error Budget Policy**:
```
If Error Budget > 50%:
  - Ship features aggressively
  - Take risks on releases

If Error Budget 20-50%:
  - Ship features carefully
  - Increase testing

If Error Budget < 20%:
  - Freeze feature releases
  - Focus on stability
  - Conduct postmortem

If Error Budget exhausted:
  - Emergency freeze
  - All hands on reliability
```

**Exercise**:
- Define SLIs for different services (API, database, cache)
- Set SLOs with buffer
- Calculate error budgets
- Track budget consumption
- Create policy for different budget levels

**4. Implement Structured Logging**:

```python
import logging
import json
from datetime import datetime

class JSONFormatter(logging.Formatter):
    def format(self, record):
        log_data = {
            'timestamp': datetime.utcnow().isoformat(),
            'level': record.levelname,
            'logger': record.name,
            'message': record.getMessage(),
        }
        
        # Add extra fields
        if hasattr(record, 'user_id'):
            log_data['user_id'] = record.user_id
        if hasattr(record, 'request_id'):
            log_data['request_id'] = record.request_id
        if hasattr(record, 'order_id'):
            log_data['order_id'] = record.order_id
        
        # Add exception info
        if record.exc_info:
            log_data['exception'] = self.formatException(record.exc_info)
        
        return json.dumps(log_data)

# Setup
logger = logging.getLogger(__name__)
handler = logging.StreamHandler()
handler.setFormatter(JSONFormatter())
logger.addHandler(handler)
logger.setLevel(logging.INFO)

# Usage
logger.info("Order created", extra={
    'user_id': '123',
    'request_id': 'abc',
    'order_id': '456',
    'amount': 99.99,
    'items': 3
})

# Output:
# {"timestamp": "2025-01-15T10:30:00", "level": "INFO", "logger": "__main__", 
#  "message": "Order created", "user_id": "123", "request_id": "abc", 
#  "order_id": "456", "amount": 99.99, "items": 3}
```

**Exercise**:
- Set up structured logging for all services
- Add correlation ID (request_id) to all logs
- Set up log aggregation (ELK or similar)
- Create log queries (all logs for request_id, all errors for user_id)
- Set up log-based alerts

**5. Design Monitoring for Microservices**:

**Services**: API Gateway, Auth, Order, Inventory, Payment, Shipping

**Metrics to Collect**:
```
For Each Service:
1. Golden Signals:
   - Latency (p50, p95, p99)
   - Traffic (requests/sec)
   - Errors (error rate %)
   - Saturation (CPU, memory, connections)

2. Business Metrics:
   - Orders/hour
   - Revenue/hour
   - Successful payments/failed payments ratio

3. Infrastructure Metrics:
   - CPU usage
   - Memory usage
   - Disk I/O
   - Network I/O
   - Database connections
   - Cache hit rate
```

**Dashboards**:
```
1. Overview Dashboard:
   - Total requests/sec (all services)
   - Overall error rate
   - p99 latency (all services)
   - Active alerts

2. Service-Specific Dashboards:
   - Per-service metrics
   - Dependencies (what this service calls)
   - Top endpoints by traffic/latency/errors

3. Business Dashboard:
   - Orders per hour
   - Revenue per hour
   - Conversion funnel
   - Cart abandonment rate
```

**Alerts**:
```
P1 (Page On-Call):
- Service down (availability < 99%)
- Error rate > 5%
- p99 latency > 1 second

P2 (Notify During Business Hours):
- Error rate > 1%
- p99 latency > 500ms
- CPU > 80%

P3 (Create Ticket):
- Cache hit rate < 80%
- Slow database queries
- High memory usage
```

**Exercise**:
- Design full monitoring stack
- Create dashboards for each level
- Define alerts with runbooks
- Implement on-call rotation
- Practice incident response

#### 📖 Resources & Key Questions:

**Key Concepts**:
- **Three Pillars**: Metrics, Logs, Traces
- **SLI**: What you measure
- **SLO**: Your target
- **SLA**: Your promise
- **Error Budget**: Allowed downtime
- **Distributed Tracing**: Follow requests across services
- **Golden Signals**: Latency, Traffic, Errors, Saturation

**Key Formulas**:
```
Error Budget:
Allowed Downtime = (100% - SLO) × Time Period
Example: (100% - 99.9%) × 30 days = 0.1% × 43,200 min = 43.2 min

Availability:
Availability = Uptime / (Uptime + Downtime)

Error Rate:
Error Rate = Failed Requests / Total Requests
```

**Resources**:
- "Site Reliability Engineering" (Google SRE Book) - FREE online
- "Observability Engineering" by Charity Majors
- Prometheus documentation
- OpenTelemetry documentation
- Jaeger documentation

**Key Questions**:
1. What's the difference between monitoring and observability?
2. Why use distributed tracing instead of just logs?
3. How do you set SLOs? (Based on user experience)
4. What's an error budget and why is it useful?
5. What are the four golden signals?
6. How do you prevent alert fatigue?
7. When should you page on-call vs send notification?
8. How do you monitor microservices effectively?

**Real-World Examples**:
- **Google**: Dapper (distributed tracing system that inspired Jaeger/Zipkin)
- **Netflix**: Atlas (metrics), Mantis (stream processing)
- **Uber**: Jaeger (they created it!)
- **Datadog**: Full observability platform (metrics, logs, traces)

**Interview Questions**:
- "How would you monitor a microservices system?"
- "Explain SLI, SLO, and SLA with examples"
- "How do you debug slow requests in distributed system?" (Distributed tracing!)
- "Design alerting strategy for production system"
- "What metrics would you track for e-commerce API?"

---

### Day 21: Week 3 Review & Advanced Project

#### 🎯 Week 3 Concepts Review:

**Distributed Systems (Day 15-17)**:
- [ ] Can explain CAP theorem and give real examples?
- [ ] Understand trade-offs (consistency vs availability, latency vs throughput)?
- [ ] Know different consistency models (strong, eventual, causal)?
- [ ] Can explain 2PC vs Saga?
- [ ] Understand when to use Saga orchestration vs choreography?
- [ ] Can explain Raft leader election?
- [ ] Understand quorum reads/writes?
- [ ] Know how to prevent split-brain?

**Microservices (Day 18)**:
- [ ] Can explain microservices benefits and challenges?
- [ ] Know how to define service boundaries?
- [ ] Understand inter-service communication (sync vs async)?
- [ ] Can do back-of-envelope calculations?
- [ ] Know key formulas (QPS, storage, bandwidth, servers)?
- [ ] Can estimate capacity for given requirements?

**Event-Driven Architecture (Day 19)**:
- [ ] Understand event sourcing pattern?
- [ ] Can explain CQRS and when to use it?
- [ ] Know Kafka concepts (topics, partitions, consumer groups)?
- [ ] Understand event-driven vs request-response?

**Observability (Day 20)**:
- [ ] Know three pillars (metrics, logs, traces)?
- [ ] Can explain distributed tracing?
- [ ] Understand SLI / SLO / SLA?
- [ ] Know golden signals?
- [ ] Can design alerting strategy?

---

#### 💻 Advanced Project: Distributed Chat System

**Requirements**:
- Support 100M users
- Real-time messaging (< 100ms latency)
- Message persistence
- Group chats (up to 1000 members)
- Read receipts
- Online/offline status
- Message search
- Multiple devices per user

**Part 1: Capacity Estimation**

**Given**:
- 100 million users
- 50 million daily active users (DAU)
- Average user:
  - Sends 50 messages/day
  - Receives 100 messages/day
  - Online 4 hours/day
- Average message: 200 bytes
- 10% messages have media (200 KB image)
- Retention: 5 years

**Calculate**:

**1. QPS (Messages)**:
```
Write QPS:
- Total messages/day = 50M × 50 = 2.5 billion messages/day
- Average QPS = 2.5B / 86400 = 28,935 QPS
- Peak QPS = 28,935 × 3 = 86,805 QPS

Read QPS (Delivery):
- Total deliveries/day = 50M × 100 = 5 billion/day
- Average QPS = 5B / 86400 = 57,870 QPS
- Peak QPS = 57,870 × 3 = 173,610 QPS
```

**2. Storage**:
```
Text Messages:
- 2.5B × 200 bytes = 500 GB/day

Media:
- 2.5B × 10% × 200 KB = 50 TB/day

Total Daily: 500 GB + 50 TB ≈ 50 TB/day
5-Year Storage: 50 TB × 365 × 5 = 91,250 TB = 91.25 PB
```

**3. WebSocket Connections**:
```
Concurrent Users:
- 50M DAU × (4 hours online / 24 hours) = 8.3M concurrent
- Multiple devices: 8.3M × 1.5 = 12.5M connections

Connections per Server:
- Assume 50K connections/server
- Servers needed: 12.5M / 50K = 250 servers

With redundancy (3x): 750 servers
```

**4. Bandwidth**:
```
Upload:
- Text: 28,935 QPS × 200 bytes = 5.8 MB/s
- Media: 28,935 × 10% × 200 KB = 579 MB/s
- Total: 585 MB/s = 4.68 Gbps

Download:
- Text: 57,870 QPS × 200 bytes = 11.6 MB/s
- Media: 57,870 × 10% × 200 KB = 1,158 MB/s
- Total: 1,170 MB/s = 9.36 Gbps
```

**5. Database Shards**:
```
Assumptions:
- Single shard handles 5K write QPS, 10K read QPS
- Max shard size: 1 TB

Based on QPS:
- Write shards: 86,805 / 5,000 = 18 shards
- Read shards: 173,610 / 10,000 = 18 shards

Based on storage (per shard):
- 91.25 PB / 1 TB = 91,250 shards (too many!)
- Solution: Separate message storage from metadata

Message Metadata DB (hot data):
- 30 days of metadata: 50 TB × 30 = 1,500 TB
- Shards: 1,500 / 1 = 1,500 shards

Cold Storage (old messages):
- Object storage (S3): 91.25 PB
- Partitioned by time (monthly)
```

**Part 2: High-Level Design**

**Architecture**:
```
Client (Mobile/Web)
   ↓ WebSocket
WebSocket Servers (250 servers × 3 = 750)
   ↓
API Gateway / Load Balancer
   ↓
┌────────────────┬────────────────┬────────────────┬─────────────────┐
│ Auth Service   │ Chat Service   │ User Service   │ Media Service   │
└────────────────┴────────────────┴────────────────┴─────────────────┘
         ↓               ↓                ↓                ↓
┌────────────────┬────────────────┬────────────────┬─────────────────┐
│ User DB        │ Message DB     │ Presence Cache │ Object Storage  │
│ (Sharded)      │ (Sharded)      │ (Redis)        │ (S3)            │
└────────────────┴────────────────┴────────────────┴─────────────────┘
```

**Components**:

1. **WebSocket Servers**:
   - Maintain persistent connections
   - Route messages to correct servers
   - Use consistent hashing for user → server mapping
   - Heartbeat to detect disconnects

2. **Chat Service**:
   - Send message API
   - Receive message API
   - Group chat management
   - Message persistence

3. **User Service**:
   - User profiles
   - Friends/contacts
   - Block lists

4. **Presence Service**:
   - Online/offline status
   - Last seen timestamp
   - Use Redis for fast lookups

5. **Media Service**:
   - Upload images/videos
   - Generate thumbnails
   - Serve media via CDN

6. **Search Service**:
   - Elasticsearch for message search
   - Index message text, sender, timestamp

**Part 3: Detailed Design**

**1. Real-Time Messaging Flow**:

**Send Message (User A → User B)**:
```
1. User A sends message via WebSocket
   POST /messages
   {
     "to": "user_b",
     "text": "Hello",
     "client_id": "msg-123"  // For idempotency
   }

2. WebSocket Server receives message

3. Call Chat Service
   - Validate user A is authenticated
   - Check user B exists and not blocked
   - Generate message ID (Snowflake)
   - Timestamp

4. Write to Message DB (sharded by conversation_id)
   message = {
     "id": "msg-456",
     "conversation_id": "conv-789",
     "from": "user_a",
     "to": "user_b",
     "text": "Hello",
     "timestamp": "2025-01-15T10:30:00Z",
     "status": "sent"
   }

5. Publish to Message Queue
   Topic: "messages"
   Event: MessageSent(msg-456, user_a, user_b, text, timestamp)

6. Find User B's WebSocket server
   - Check Presence Cache: Which server has user B's connection?
   - Use service discovery or consistent hashing

7. Push to User B via WebSocket
   ws.send(user_b, message)

8. User B receives message
   - Display in chat
   - Send ACK back

9. Update message status to "delivered"

10. User B reads message
    - Send read receipt
    - Update status to "read"
```

**2. Group Chat (1000 members)**:

**Challenge**: Delivering message to 1000 users

**Solution**: Fan-out on read (pull model)
```
1. User A sends message to group

2. Save message once:
   message = {
     "id": "msg-123",
     "group_id": "group-456",
     "from": "user_a",
     "text": "Hello group",
     "timestamp": "..."
   }

3. Increment group message counter:
   groups[group-456].message_count += 1

4. Push notification to online members only:
   - Check Presence Cache
   - Send to WebSocket servers of online users
   
5. Offline members:
   - When they come online, fetch new messages
   - GET /groups/{group-456}/messages?since={last_read_id}

6. Track read position per user:
   user_group_position = {
     "user_id": "user_b",
     "group_id": "group-456",
     "last_read_message_id": "msg-120"
   }
```

**3. Online/Offline Presence**:

```python
# Redis data structure
# Key: user:{user_id}:presence
# Value: {status: "online", last_seen: timestamp, server: "ws-server-5"}

def update_presence(user_id, status):
    redis.set(
        f"user:{user_id}:presence",
        {
            "status": status,  # "online" or "offline"
            "last_seen": now(),
            "server": current_server_id
        },
        ttl=300  # 5 minutes
    )

# Heartbeat (every 30 seconds)
def heartbeat(user_id):
    update_presence(user_id, "online")

# On disconnect
def on_disconnect(user_id):
    update_presence(user_id, "offline")

# Get user status
def get_user_status(user_id):
    data = redis.get(f"user:{user_id}:presence")
    if not data:
        return "offline"
    return data["status"]
```

**4. Message Search**:

```
Elasticsearch Index:
- Index: messages
- Type: message
- Schema:
  {
    "id": "msg-123",
    "conversation_id": "conv-456",
    "from": "user_a",
    "to": "user_b",
    "text": "Hello world",
    "timestamp": "2025-01-15T10:30:00Z"
  }

Search Query:
GET /messages/_search
{
  "query": {
    "bool": {
      "must": [
        {"match": {"text": "hello"}},
        {"term": {"conversation_id": "conv-456"}}
      ]
    }
  },
  "sort": [{"timestamp": "desc"}],
  "size": 20
}
```

**Part 4: Advanced Features**

**1. Read Receipts**:
```
1. User B reads message
   - Frontend sends read event
   POST /messages/{msg-123}/read

2. Update message status in DB
   UPDATE messages 
   SET status = 'read', read_at = NOW()
   WHERE id = 'msg-123'

3. Notify User A (sender)
   - Find User A's WebSocket
   - Send read receipt event
   ws.send(user_a, {
     "type": "read_receipt",
     "message_id": "msg-123",
     "read_by": "user_b",
     "read_at": "..."
   })
```

**2. Typing Indicators**:
```
1. User A starts typing
   - Send event to WebSocket server
   ws.send({
     "type": "typing_start",
     "user_id": "user_a",
     "conversation_id": "conv-456"
   })

2. WebSocket server broadcasts to conversation members
   - Don't persist (ephemeral)
   - Send to online users only

3. User A stops typing (after 5 seconds of inactivity)
   - Send typing_stop event
```

**3. Message Encryption** (End-to-End):
```
1. User A encrypts message with User B's public key
   encrypted_text = encrypt(text, user_b_public_key)

2. Send encrypted message to server

3. Server stores encrypted message (can't read it)

4. User B receives encrypted message

5. User B decrypts with private key
   text = decrypt(encrypted_text, user_b_private_key)

Key Management:
- Each user has public/private key pair
- Public keys stored on server
- Private keys stored only on user's device
```

**Part 5: Trade-off Analysis**

Document design decisions:

**1. WebSocket vs Polling**:
- **Decision**: WebSocket
- **Why**: Real-time requirements (< 100ms latency)
- **Trade-off**: More complex (need to maintain connections)
- **Alternative**: Long polling (simpler but higher latency)

**2. Fan-out on Write vs Read (for groups)**:
- **Decision**: Fan-out on read (for large groups)
- **Why**: 1000 members → 1000 writes is expensive
- **Trade-off**: Slower reads (must query for new messages)
- **For small groups** (< 10): Fan-out on write (faster reads)

**3. Strong vs Eventual Consistency**:
- **Decision**: Eventual consistency for message delivery
- **Why**: Availability > consistency for chat
- **Trade-off**: Messages might arrive out of order (use timestamps)
- **For read receipts**: Strong consistency (must be accurate)

**4. Sharding Strategy**:
- **Decision**: Shard by conversation_id
- **Why**: All messages in conversation on same shard (fast queries)
- **Trade-off**: Hot shards if one conversation very active
- **Solution**: Monitor and re-shard hot conversations

**Part 6: System Design Diagram**

```
┌─────────────────────────────────────────────────────────────────┐
│                         Client Layer                             │
│  Mobile App, Web App (WebSocket connections)                     │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│                    WebSocket Gateway (750 servers)               │
│  - Maintain connections                                          │
│  - Consistent hashing (user → server)                            │
│  - Heartbeat monitoring                                          │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│                         API Gateway                              │
│  - Authentication, Rate limiting, Routing                        │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌──────────────┬──────────────┬──────────────┬───────────────────┐
│ Auth Service │ Chat Service │ User Service │  Media Service    │
│              │              │              │                   │
│ - JWT tokens │ - Send msg   │ - Profiles   │ - Upload          │
│ - Refresh    │ - Receive    │ - Contacts   │ - Thumbnails      │
│              │ - Groups     │ - Blocks     │                   │
└──────────────┴──────────────┴──────────────┴───────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│                      Message Queue (Kafka)                       │
│  Topics: messages, read_receipts, presence_updates               │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌──────────────┬──────────────┬──────────────┬───────────────────┐
│  Message DB  │ Presence     │ Search       │  Object Storage   │
│  (Cassandra) │ (Redis)      │ (ES)         │  (S3)             │
│              │              │              │                   │
│ - Sharded    │ - user:123:  │ - Message    │ - Images          │
│ - Hot: 30d   │   presence   │   search     │ - Videos          │
│ - Cold: S3   │ - TTL: 5min  │              │ - Files           │
└──────────────┴──────────────┴──────────────┴───────────────────┘
```

#### 📖 Week 3 Review Resources:

**Key Takeaways**:
- Distributed systems require trade-offs (CAP theorem)
- Microservices add complexity but enable scalability
- Event-driven architecture enables loose coupling
- Observability is critical for debugging distributed systems
- Always do capacity calculations in interviews

**Practice Exercises**:
1. Design Twitter with full capacity calculations
2. Design Uber with real-time location tracking
3. Design Netflix with video streaming
4. Design WhatsApp with end-to-end encryption
5. For each: Document trade-offs and justify decisions

**Interview Preparation**:
- Practice explaining CAP theorem with examples
- Practice back-of-envelope calculations
- Draw architecture diagrams quickly
- Explain trade-offs clearly
- Use real examples (Twitter, Uber, Netflix)

**Next Steps**:
- Ready for Week 4: Modern Architecture Patterns
- Will cover cloud-native, APIs, search, real-time, geo, and AI/ML integration

---



# Week 4: Modern Architecture Patterns (Days 22-28)

### Day 22: Cloud-Native Architecture

#### 🎯 Core Concepts to Learn:

**12-Factor App Methodology:**
- Codebase: One codebase tracked in version control
- Dependencies: Explicitly declare dependencies
- Config: Store config in environment (not code)
- Backing services: Treat as attached resources
- Build, release, run: Strictly separate stages
- Processes: Execute as stateless processes
- Port binding: Export services via port binding
- Concurrency: Scale out via process model
- Disposability: Fast startup and graceful shutdown
- Dev/prod parity: Keep environments similar
- Logs: Treat as event streams
- Admin processes: Run as one-off processes

**Container Orchestration with Kubernetes:**
- Pods: Smallest deployable units (one or more containers)
- Deployments: Declarative updates for pods
- Services: Stable network endpoint for pods
- ConfigMaps and Secrets: Configuration management
- Ingress: External access to services
- Horizontal Pod Autoscaler: Auto-scaling based on metrics
- Namespaces: Virtual clusters for resource isolation
- StatefulSets: For stateful applications
- DaemonSets: Run pod on every node

**Service Mesh Concepts:**
- What is service mesh: Dedicated infrastructure layer for service-to-service communication
- Sidecar pattern: Proxy alongside each service
- Features: Load balancing, service discovery, failure recovery, metrics, tracing
- Traffic management: Canary deployments, A/B testing, circuit breaking
- Security: mTLS (mutual TLS) between services
- Examples: Istio, Linkerd, Consul Connect
- When to use: Many microservices (>10), need advanced traffic control

**Serverless Architecture Patterns:**
- Function as a Service (FaaS): AWS Lambda, Azure Functions, Google Cloud Functions
- Event-driven execution: Trigger functions from events
- Benefits: No server management, auto-scaling, pay-per-use
- Limitations: Cold starts, execution time limits, stateless
- Use cases: API backends, data processing, scheduled tasks, webhooks
- Serverless vs containers: When to use each

#### 💻 What to Practice:
- Deploy application on Kubernetes cluster
- Configure service mesh (Istio) for microservices
- Build serverless function (AWS Lambda) triggered by S3 upload
- Design cloud-native e-commerce platform with K8s and serverless components
- Compare deployment strategies: Blue-green, canary, rolling updates

#### 📖 Key Questions:
- What are the 12 factors and why important?
- When would you use Kubernetes vs serverless?
- What problems does service mesh solve?
- How does sidecar pattern work?
- Trade-offs of serverless (cost, cold starts, limits)?

---

### Day 23: API Design & Management

#### 🎯 Core Concepts to Learn:

**RESTful API Design Principles:**
- Resources: Everything is a resource (noun-based URLs)
- HTTP methods: GET (read), POST (create), PUT (update), PATCH (partial update), DELETE (remove)
- Statelessness: Each request independent
- URL structure: /users, /users/123, /users/123/orders
- Status codes: Proper use of 2xx, 3xx, 4xx, 5xx
- HATEOAS: Hypermedia as engine of application state
- Idempotency: GET, PUT, DELETE are idempotent
- Versioning: /v1/users, /v2/users or header-based

**GraphQL vs REST Trade-offs:**
- GraphQL benefits: Single endpoint, fetch exactly what needed, strongly typed, no over/under-fetching
- GraphQL challenges: Caching harder, monitoring/rate limiting complex, learning curve
- REST benefits: Simple, cacheable, well understood, stateless
- REST challenges: Over-fetching/under-fetching, multiple requests, versioning
- When GraphQL: Complex data requirements, mobile apps (reduce requests)
- When REST: Simple CRUD, need caching, standard operations

**API Versioning Strategies:**
- URL versioning: /v1/users, /v2/users (most common, visible)
- Header versioning: Accept: application/vnd.myapi.v2+json (cleaner URLs)
- Query parameter: /users?version=2 (simple but less standard)
- When to version: Breaking changes, backwards incompatible
- Semantic versioning: Major.Minor.Patch (2.1.3)

**Rate Limiting and Throttling:**
- Why needed: Prevent abuse, ensure fair usage, protect backend
- Algorithms: Token bucket, leaky bucket, fixed window, sliding window (covered Day 10)
- Where to implement: API gateway, application layer
- Headers: X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset
- Per-user limits: Different tiers (free, premium)
- Strategies: Return 429 (Too Many Requests), queue requests, reject

**API Gateway Pattern:**
- Single entry point for all API requests
- Responsibilities:
  - Authentication and authorization
  - Rate limiting and throttling
  - Request/response transformation
  - Protocol translation (HTTP to gRPC)
  - API composition (aggregate multiple services)
  - Caching
  - Logging and monitoring
  - Load balancing
- Examples: Kong, AWS API Gateway, Apigee, Azure API Management
- Benefits: Centralized control, reduced complexity in services
- Drawbacks: Single point of failure, can become bottleneck

#### 💻 What to Practice:
- Design RESTful API for social platform (users, posts, comments, likes)
- Design GraphQL schema for same platform
- Compare: When to use REST vs GraphQL for different features
- Implement rate limiting with token bucket algorithm
- Set up API gateway with authentication, rate limiting, and logging
- Design API versioning strategy for mobile banking app
- Design API for backward compatibility

#### 📖 Key Questions:
- What makes API RESTful?
- GraphQL vs REST - when to use each?
- How to version APIs without breaking clients?
- Where to implement rate limiting (gateway vs service)?
- How to design API for mobile apps (minimize requests)?
- How to handle API deprecation?

---

### Day 24: Search & Indexing Systems

#### 🎯 Core Concepts to Learn:

**Full-Text Search Concepts:**
- Inverted index: Maps terms to documents (like book index)
- Tokenization: Breaking text into terms
- Normalization: Lowercase, remove punctuation
- Stemming: Reduce words to root (running → run)
- Stop words: Remove common words (the, a, is)
- TF-IDF: Term frequency × inverse document frequency (relevance scoring)
- BM25: Modern ranking algorithm (better than TF-IDF)

**Elasticsearch Architecture:**
- Cluster: Collection of nodes
- Node: Single server in cluster
- Index: Collection of documents (like database)
- Document: JSON object (like row)
- Shard: Subset of index (for horizontal scaling)
- Replica: Copy of shard (for fault tolerance)
- Primary shard: Handles writes
- Replica shard: Handles reads
- Mapping: Schema definition (field types)
- Query DSL: JSON-based query language

**Search Ranking Algorithms:**
- Relevance scoring: How well document matches query
- Boosting: Increase importance of certain fields (title > body)
- Filtering: Exact match (category = "electronics")
- Fuzzy matching: Tolerate typos (ipone → iphone)
- Synonyms: Treat words as equivalent (car, automobile)
- Personalization: User history, location, preferences
- Freshness: Newer documents ranked higher
- Popularity: Click-through rate, user engagement

**Auto-complete and Suggestions:**
- Prefix matching: Match beginning of words
- Trie data structure: Efficient prefix search
- N-gram indexing: Index character sequences
- Fuzzy suggestions: Handle typos
- Popularity-based: Rank by frequency
- Personalization: Based on user history
- Real-time updates: Update suggestions as user types
- Implementation: Edge n-grams in Elasticsearch

**Inverted Index Deep Dive:**
- Forward index: Document → Terms
- Inverted index: Term → Documents
- Example:
  - Doc 1: "quick brown fox"
  - Doc 2: "brown dog"
  - Inverted: {"quick": [1], "brown": [1,2], "fox": [1], "dog": [2]}
- Posting list: List of documents for term
- Position information: Where term appears in document
- Compression: Reduce storage (delta encoding, variable byte encoding)

#### 💻 What to Practice:
- Set up Elasticsearch cluster (3 nodes)
- Index 1 million product documents
- Implement search with filters (category, price range, brand)
- Build auto-complete for product names (handle typos)
- Implement search ranking: Boost title, consider popularity
- Design search system for e-commerce with 100M products
- Calculate: How many shards needed? How much storage?
- Design search for multi-language content

#### 📖 Key Questions:
- How does inverted index work?
- What's difference between filtering and scoring?
- How to handle typos in search?
- How to scale search to billions of documents?
- How to implement real-time search (index new docs immediately)?
- How to personalize search results?
- Trade-offs: Elasticsearch vs Solr vs custom solution?

---

### Day 25: Real-Time Systems

#### 🎯 Core Concepts to Learn:

**WebSocket vs Server-Sent Events (SSE):**
- WebSocket:
  - Full-duplex: Bidirectional communication
  - Single TCP connection (persistent)
  - Use cases: Chat, gaming, collaboration, live updates
  - Pros: Low latency, efficient, bidirectional
  - Cons: More complex, needs special server support
  - Scaling: Sticky sessions or use Redis for pub/sub
- SSE:
  - One-way: Server → Client only
  - Uses regular HTTP
  - Use cases: News feeds, stock tickers, notifications
  - Pros: Simpler, automatic reconnection, works through proxies
  - Cons: One-way only, browser limits (6 connections)
- Long Polling (fallback):
  - Client requests, server holds until data available
  - Simpler than WebSocket but less efficient

**Real-Time Messaging Patterns:**
- Push-based: Server pushes to clients (WebSocket, SSE)
- Pull-based: Clients poll server (HTTP polling)
- Hybrid: Combine push and pull
- Message queue: Decouple producers and consumers
- Pub/Sub: Multiple subscribers to same messages
- Request-reply: Traditional RPC pattern

**Push Notification Systems:**
- Components:
  - Notification service: Receives requests, queues notifications
  - Worker: Processes queue, sends to providers
  - Providers: APNs (Apple), FCM (Google), Web Push
- Device tokens: Unique identifier per device
- Topics: Broadcast to subscribers
- User preferences: Opt-in/opt-out, frequency control
- Priority: High (immediate), Normal (batched)
- Analytics: Track delivery, open rate

**Challenges in Real-Time Systems:**
- Scaling connections: Millions of concurrent WebSockets
- Message ordering: Ensure messages arrive in order
- Exactly-once delivery: Prevent duplicates
- Presence management: Who's online?
- Connection recovery: Handle network issues
- Message persistence: Store for offline users
- Load balancing: Distribute connections across servers

#### 💻 What to Practice:
- Build WebSocket chat server (handle 10K connections)
- Implement push notification system (queue → workers → FCM/APNs)
- Compare polling vs WebSocket performance (latency, bandwidth)
- Design real-time collaborative editing (like Google Docs)
- Handle connection recovery and message replay
- Design real-time dashboard (stock prices, server metrics)
- Design presence system (online/offline/away status)

#### 📖 Key Questions:
- WebSocket vs SSE vs Long Polling - when to use each?
- How to scale WebSocket connections to millions?
- How to ensure message ordering in distributed system?
- How to handle offline users (store messages)?
- How to implement presence (online status)?
- What's the difference between push notification and WebSocket?
- How to load balance WebSocket connections?

---

### Day 26: Geospatial Systems & Location Services

#### 🎯 Core Concepts to Learn:

**Geospatial Data Structures:**
- Quadtree:
  - Divide space into 4 quadrants recursively
  - Good for: Dynamic data, frequent updates
  - Operations: Insert, delete, search in O(log n)
  - Use case: Find nearby points
- R-tree:
  - Rectangles organized in hierarchy
  - Good for: Spatial objects (polygons, routes)
  - Use case: Map data, geographic boundaries
- Geohash:
  - Encode lat/lon to string (base32)
  - Nearby locations have similar prefixes
  - Good for: Static data, enables range queries
  - Example: San Francisco = 9q8y (precision varies)
- H3 (Uber's hexagonal grid):
  - Divide earth into hexagons
  - Better than squares (equal distance to neighbors)
  - Hierarchical levels (0-15)
  - Use case: Uber's pricing zones, demand prediction

**Proximity Search Algorithms:**
- Bounding box: Filter by rectangle (lat1, lon1, lat2, lon2)
- Radius search: Find points within distance
- K-nearest neighbors: Find K closest points
- Optimizations:
  - Use index on location
  - Filter with bounding box first, then calculate exact distance
  - Cache popular searches

**Distance Calculations:**
- Haversine formula:
  - Calculate distance on sphere
  - Accounts for Earth's curvature
  - Good for distances < 500km
  - Formula uses lat/lon in radians
- Vincenty formula:
  - More accurate (uses ellipsoid)
  - Good for long distances
  - More complex calculation
- Simple approximation:
  - For small distances: Pythagorean (fast but inaccurate for large distances)

**Geofencing and Region Queries:**
- Geofence: Virtual perimeter around real-world area
- Point-in-polygon: Check if location inside geofence
- Use cases:
  - Notifications when entering area
  - Ride-sharing zones
  - Delivery areas
  - Location-based promotions
- Implementation: Quadtree or R-tree for efficiency

**Location-Based Indexing Strategies:**
- Geohash indexing:
  - Store geohash as string column
  - Index allows prefix search
  - Example: Find all points in 9q8y* (4-char prefix)
- Composite index:
  - (geohash, other_field) for filtered queries
- Database solutions:
  - PostgreSQL + PostGIS extension
  - MongoDB geospatial queries
  - Redis GEOADD/GEORADIUS
  - Elasticsearch geo_point type

#### 💻 What to Practice:
- Implement quadtree for storing restaurant locations
- Build proximity search: "Find restaurants within 5 km"
- Implement geohash encoding/decoding
- Calculate distances using Haversine formula
- Design "find nearby" feature (like Yelp)
- Design Uber's driver-rider matching based on location
- Design geofencing system for location-based notifications
- Calculate: How to index 1M restaurant locations for fast queries?
- Compare: Quadtree vs Geohash vs Database (PostGIS)

#### 📖 Key Questions:
- When to use Quadtree vs Geohash vs R-tree?
- How does Uber match drivers to riders?
- How to efficiently find k-nearest locations?
- What's the accuracy of Haversine formula?
- How to handle locations crossing date line or poles?
- How to update location in real-time for millions of users?
- How to partition geospatial data (shard by region)?
- Trade-offs: In-memory index vs database solution?

---

### Day 27: AI/ML Integration in System Design

#### 🎯 Core Concepts to Learn:

**ML Model Serving Architecture:**
- Model serving: Deploy trained model for predictions
- Online prediction: Real-time (< 100ms)
- Batch prediction: Process in batches (offline)
- Model server: Flask API, TensorFlow Serving, TorchServe
- Versioning: Multiple model versions, A/B testing
- Scalability: Load balancer → multiple model servers
- Caching: Cache predictions for common inputs

**Feature Stores and Pipelines:**
- Feature store: Centralized repository for ML features
- Purpose: Share features across models, ensure consistency
- Components:
  - Online store: Low-latency (Redis) for real-time predictions
  - Offline store: Batch features (S3, Hive) for training
  - Feature computation: Transform raw data to features
- Examples: Feast, Tecton, AWS SageMaker Feature Store
- Benefits: Reusability, consistency, faster development

**Online vs Offline Predictions:**
- Online (real-time):
  - Low latency required (< 100ms)
  - Examples: Recommendation on page load, fraud detection
  - Architecture: API → Model server → Prediction
  - Challenges: Latency, availability, scalability
- Batch (offline):
  - High throughput, latency not critical
  - Examples: Email recommendations, daily reports
  - Architecture: Scheduled job → Process data → Store predictions
  - Benefits: Cost-effective, can use complex models

**A/B Testing Frameworks:**
- Purpose: Compare model versions
- Components:
  - Experiment configuration: % traffic to each variant
  - Assignment: Consistent user → variant mapping
  - Metrics tracking: Conversion, engagement, revenue
  - Statistical significance: Determine winner
- Implementation:
  - Feature flags: Enable/disable features
  - Gradual rollout: 5% → 20% → 50% → 100%
  - Automated rollback: If metrics degrade

**Model Monitoring and Retraining:**
- Model drift: Performance degrades over time
- Causes: Data distribution changes, user behavior shifts
- Monitoring:
  - Prediction quality: Accuracy, precision, recall
  - Input distribution: Detect drift in features
  - Latency: Response time
  - Resource usage: CPU, memory
- Retraining:
  - Scheduled: Weekly, monthly
  - Triggered: When performance drops
  - Online learning: Update model continuously
- MLOps: CI/CD for ML models

**ML System Design Patterns:**
- Embedding-based retrieval: Convert items to vectors, find similar
- Two-stage ranking: Fast candidate generation → precise ranking
- Real-time feature computation: Stream processing (Kafka)
- Cold start: Handle new users/items (use content-based features)
- Exploration vs exploitation: Balance showing known good vs trying new
- Multi-armed bandit: Adaptive A/B testing

#### 💻 What to Practice:
- Design model serving infrastructure for recommendation system
- Build feature pipeline: Raw data → Features → Store in Redis
- Implement A/B testing framework: Route traffic, track metrics
- Design real-time fraud detection system (< 10ms latency)
- Design batch recommendation system (process overnight)
- Design cold start solution for new users
- Design monitoring dashboard for ML model (accuracy, latency, drift)
- Calculate: Capacity for serving 10K predictions/sec

#### 📖 Key Questions:
- When to use online vs batch predictions?
- What is feature store and why needed?
- How to handle model versioning and rollback?
- How to detect model drift?
- What's difference between A/B testing and multi-armed bandit?
- How to serve multiple models efficiently?
- How to handle cold start problem?
- Trade-offs: Model complexity vs latency?

---

### Day 28: Week 4 Review & Integration

#### 🎯 Week 4 Review Checklist:

**Cloud-Native (Day 22):**
- Can explain 12-factor app principles?
- Understand Kubernetes concepts (pods, deployments, services)?
- Know what service mesh does and when to use?
- Understand serverless benefits and limitations?

**APIs (Day 23):**
- Can design RESTful API following best practices?
- Understand GraphQL vs REST trade-offs?
- Know different API versioning strategies?
- Can implement rate limiting?

**Search (Day 24):**
- Understand how inverted index works?
- Know how to scale search to billions of documents?
- Can design auto-complete system?
- Understand search ranking factors?

**Real-Time (Day 25):**
- Know when to use WebSocket vs SSE vs polling?
- Can design push notification system?
- Understand challenges of scaling real-time connections?

**Geospatial (Day 26):**
- Understand different geospatial data structures?
- Can design proximity search system?
- Know how to calculate distances efficiently?
- Understand geofencing?

**AI/ML (Day 27):**
- Can design ML model serving architecture?
- Understand feature stores?
- Know online vs batch prediction trade-offs?
- Can design A/B testing framework?

#### 💻 Comprehensive Project: Food Delivery Platform

Design complete system combining all Week 4 concepts:

**Requirements:**
- 10M users, 1M restaurants
- Real-time order tracking
- Location-based restaurant search
- Personalized recommendations (ML)
- Driver-rider matching
- Push notifications
- API for mobile apps

**Design Components:**
1. API Gateway (RESTful + GraphQL)
2. Location services (Quadtree for proximity search)
3. Real-time tracking (WebSocket connections)
4. Search (Elasticsearch for restaurant search)
5. Recommendations (ML model serving)
6. Notifications (Push notification system)
7. Cloud infrastructure (Kubernetes deployment)

**Capacity Calculations:**
- QPS for search, orders, tracking
- Storage for restaurant data, orders, locations
- WebSocket connections for real-time tracking
- ML model serving capacity
- Database shards needed

**Trade-off Decisions:**
- REST vs GraphQL for mobile API
- Geohash vs Quadtree for location indexing
- Online vs batch for recommendations
- WebSocket vs SSE for tracking
- Kubernetes vs serverless for services

---

# Week 5: System Design Practice - Classic Problems (Days 29-35)

### Day 29: URL Shortener - Part 1 (Core System)

#### 🎯 Core Concepts to Learn:

**URL Shortener Requirements:**
- Functional: Shorten long URL, redirect to original, custom aliases, expiration
- Non-functional: High availability, low latency (<10ms), scalable to billions of URLs
- Scale: 100M new URLs/month, 10B redirects/month

**URL Encoding Strategies:**
- Hash-based (MD5, SHA):
  - Hash long URL → Take first 6-7 characters
  - Pros: Deterministic, easy to implement
  - Cons: Collisions (need to handle), not sequential
- Base62 encoding:
  - Use auto-increment ID → Convert to base62 (0-9, a-z, A-Z)
  - Example: ID 125 → "c1"
  - Pros: No collisions, short codes, sequential
  - Cons: Need ID generator
- Comparison: Base62 is standard approach

**Database Schema Design:**
- URLs table: id (PK), short_code (unique), original_url, created_at, expires_at, clicks
- Users table (if needed): id, email, api_key
- Analytics table: short_code, timestamp, country, device, referrer

**Short Code Generation:**
- Requirements: Unique, short (6-7 chars), random-looking
- Approaches:
  - Single database with auto-increment (simple but single point)
  - UUID (too long, 36 chars)
  - Distributed ID generator (Twitter Snowflake)
  - Pre-generated codes (reserve ranges)

**Capacity Estimation:**
- 100M new URLs/month = 40 writes/sec (average), 120 writes/sec (peak)
- 10B redirects/month = 4K reads/sec (average), 12K reads/sec (peak)
- Storage: 100M URLs × 500 bytes = 50 GB/month, 30 TB for 5 years
- Read-heavy: 100:1 read-to-write ratio

#### 💻 What to Practice:
- Design database schema with indexes
- Compare hash-based vs base62 encoding
- Calculate: Storage for 1B URLs
- Calculate: QPS for given scale
- Calculate: Cache size (80-20 rule)
- Design for 100M writes/month, 10B reads/month

#### 📖 Key Questions:
- How to generate unique short codes?
- How to handle collisions in hash-based approach?
- How to prevent abuse (spam, malicious URLs)?
- How to implement custom aliases?
- How to handle URL expiration?

---

### Day 30: URL Shortener - Part 2 (Advanced Features)

#### 🎯 Advanced Features to Learn:

**Caching Strategy:**
- What to cache: Popular URLs (80-20 rule)
- Cache layer: Redis, Memcached
- Eviction policy: LRU (Least Recently Used)
- TTL: 24 hours for URLs
- Cache invalidation: When URL deleted/updated
- Cache size: 20% of URLs for 80% traffic

**Analytics and Tracking:**
- Track: Clicks, timestamp, country, device, referrer, browser
- Real-time: Update counters asynchronously (don't block redirect)
- Batch processing: Aggregate daily/weekly stats
- Storage: Time-series database (InfluxDB) or analytics DB
- Privacy: Hash IP addresses, comply with regulations

**Rate Limiting:**
- Prevent abuse: Limit requests per IP/user
- Anonymous users: 10 URLs/hour
- Authenticated users: 100 URLs/hour
- Implementation: Token bucket algorithm
- Distributed rate limiting: Redis with sliding window

**Custom Aliases:**
- Allow users to choose short code (e.g., "mylink")
- Validation: Check if available, no profanity
- Reserved words: Prevent system URLs (/api, /admin)
- Premium feature: Custom domains (short.io/mylink)

**High Availability Design:**
- Load balancer: Distribute across multiple servers
- Database replication: Master-slave for reads
- Redis cluster: Distributed cache
- Multiple data centers: Geographic redundancy
- Failover: Automatic switching on failure

**Security Considerations:**
- Validate URLs: Check for malicious sites (phishing, malware)
- Bot detection: CAPTCHA, rate limiting
- DDoS protection: Rate limiting, Cloudflare
- Data encryption: HTTPS for all connections
- Access control: Authentication for analytics

#### 💻 What to Practice:
- Design caching strategy with eviction policy
- Implement async click counter (don't block redirect)
- Design rate limiting for abuse prevention
- Design custom alias feature (check availability)
- Design analytics dashboard (top URLs, geographic distribution)
- Design for multiple data centers (geo-distribution)

#### 📖 Key Questions:
- How to scale to billions of URLs?
- How to implement analytics without slowing redirects?
- How to prevent spam and abuse?
- How to ensure high availability (99.9%)?
- How to handle database failures?
- How to implement custom domains?

---

### Day 31: Pastebin / Code Sharing

#### 🎯 Core Concepts to Learn:

**Pastebin Requirements:**
- Functional: Paste text/code, generate link, view paste, expiration, syntax highlighting
- Non-functional: Low latency, high availability, secure (private pastes)
- Scale: 1M pastes/day, 10M views/day

**Similar to URL Shortener but Different:**
- Store content (not just redirect)
- Larger storage per item (up to 10 MB vs URL's 500 bytes)
- Syntax highlighting (detect language)
- Expiration: 10 min, 1 hour, 1 day, 1 week, never
- Access control: Public, unlisted, private

**Storage Strategy:**
- Small pastes (< 1 KB): Store in database
- Large pastes (> 1 KB): Store in object storage (S3)
- Metadata: Always in database (id, title, language, expiration, visibility)
- Hot storage: Recent pastes in cache
- Cold storage: Old pastes in S3 (cheaper)

**Content Delivery:**
- CDN: Serve static syntax highlighting assets
- Cache: Frequently viewed pastes in Redis
- Compression: Gzip text before storage
- Lazy loading: For very large pastes

**Expiration Handling:**
- Active deletion: Cron job scans for expired pastes
- Lazy deletion: Delete when accessed after expiration
- Soft delete: Mark as deleted, cleanup later
- Storage recovery: Reclaim space from expired pastes

**Security and Privacy:**
- Private pastes: Require authentication or share token
- Encryption: Encrypt private pastes at rest
- Password protection: Optional password for paste
- Burn after reading: Delete after first view
- Content moderation: Scan for illegal content

#### 💻 What to Practice:
- Design database schema (pastes, users, metadata)
- Calculate storage: 1M pastes/day, average 2 KB, 1 year retention
- Design expiration mechanism (active vs lazy deletion)
- Design access control (public, unlisted, private)
- Design for syntax highlighting (detect language, apply colors)
- Design CDN strategy for static assets

#### 📖 Key Questions:
- How to handle large pastes (10 MB)?
- How to implement expiration efficiently?
- How to ensure private pastes are secure?
- How to detect and highlight code language?
- How to prevent abuse (spam, illegal content)?
- Differences from URL shortener?

---

### Day 32: Twitter News Feed - Part 1 (Core Architecture)

#### 🎯 Core Concepts to Learn:

**Twitter Feed Requirements:**
- Functional: Post tweet, follow user, view feed (tweets from followed users), like/retweet
- Non-functional: High availability, eventual consistency, low latency feed
- Scale: 500M users, 200M DAU, 500M tweets/day

**Feed Generation Approaches:**

**1. Fan-out on Write (Push Model):**
- When user tweets: Push to all followers' feeds immediately
- Pros: Fast reads (pre-computed feed)
- Cons: Slow writes (celebrity with 100M followers), high storage
- Use for: Regular users (< 10K followers)

**2. Fan-out on Read (Pull Model):**
- When user views feed: Fetch tweets from followed users
- Pros: Fast writes, less storage
- Cons: Slow reads (must merge N users' tweets)
- Use for: Celebrities (> 1M followers)

**3. Hybrid Approach (Twitter's Solution):**
- Regular users: Fan-out on write
- Celebrities: Fan-out on read
- When user views feed: Merge pre-computed feed + celebrity tweets
- Best of both worlds

**Database Schema:**
- Users table: id, username, created_at
- Tweets table: id, user_id, text, created_at, likes_count, retweets_count
- Follows table: follower_id, followee_id, created_at
- Feed table: user_id, tweet_id, created_at (pre-computed feeds)

**Capacity Estimation:**
- 500M tweets/day = 6K writes/sec (average), 18K writes/sec (peak)
- 200M users check feed 10 times/day = 2B feed loads/day = 23K reads/sec
- Tweet storage: 500M × 140 bytes = 70 GB/day = 25 TB/year
- Feed storage: 200M users × 500 tweets = 100B entries (if materialize all)

**Timeline Pagination:**
- Cursor-based: Use tweet_id as cursor (more than, less than)
- Offset-based: Skip N tweets (inefficient for large offsets)
- Bidirectional: Load older and newer tweets

#### 💻 What to Practice:
- Design database schema with proper indexes
- Compare fan-out on write vs read vs hybrid
- Calculate storage for 500M tweets/day
- Calculate QPS for writes and reads
- Design timeline pagination (cursor-based)
- Design for celebrity problem (100M followers)

#### 📖 Key Questions:
- Fan-out on write vs read - trade-offs?
- How to handle celebrity problem?
- How to ensure tweets appear in order?
- How to paginate timeline efficiently?
- How to handle deleted tweets in pre-computed feed?

---

### Day 33: Twitter News Feed - Part 2 (Advanced Features)

#### 🎯 Advanced Features to Learn:

**Feed Ranking Algorithm:**
- Chronological: Simple, but may miss important tweets
- Relevance-based: Rank by engagement (likes, retweets, replies)
- Personalized: ML model predicts user interest
- Signals: User relationship, tweet recency, media type, engagement
- Implementation: Two-stage (candidate generation → ranking)

**Real-Time Updates:**
- WebSocket: Push new tweets to connected users
- Polling: Check for updates periodically
- Server-Sent Events: Server pushes to clients
- Notification: "5 new tweets" banner

**Caching Strategy:**
- Cache hot users' feeds (active users)
- Cache celebrity tweets separately
- Redis cluster for distributed caching
- TTL: Short (5 minutes) for fresh content
- Cache warm-up: Pre-load popular feeds

**Trending Topics:**
- Count hashtags in real-time (stream processing)
- Time-window: Last 1 hour, 24 hours
- Geographic: Trending by location
- Storage: Redis sorted set (score = tweet count)
- Update frequency: Every 5 minutes

**Media Handling:**
- Images/videos: Store in object storage (S3)
- Thumbnails: Generate multiple sizes
- CDN: Serve media from edge locations
- Lazy loading: Load media on scroll
- Compression: Optimize media size

**Mentions and Hashtags:**
- Parse tweet for @mentions and #hashtags
- Store in separate tables for fast lookup
- Notifications: Alert mentioned users
- Search: Find tweets by hashtag

#### 💻 What to Practice:
- Design feed ranking algorithm (consider multiple signals)
- Design real-time updates (WebSocket vs polling)
- Design caching strategy for 200M users
- Design trending topics (count hashtags in time window)
- Design media pipeline (upload → process → CDN)
- Calculate CDN bandwidth for media delivery

#### 📖 Key Questions:
- How to rank feed (chronological vs relevance)?
- How to implement real-time updates?
- How to calculate trending topics?
- How to handle media at scale?
- How to detect and filter spam?
- How to ensure high availability?

---

### Day 34: Instagram Feed - Differences from Twitter

#### 🎯 Core Concepts to Learn:

**Instagram vs Twitter Differences:**
- Media-first: Every post has image/video
- No character limit: Can have longer captions
- Private accounts: Not all content is public
- Stories: Ephemeral content (24 hours)
- Direct messages: Private chat feature
- Explore feed: Algorithmic discovery

**Media-Centric Design:**
- Storage: Much larger (images 1-5 MB, videos 50-500 MB)
- Processing: Resize, compress, multiple formats
- Thumbnails: Generate for feed (small), profile (medium), full (large)
- Formats: JPEG (images), MP4 (videos), WebP (modern browsers)
- Storage cost: Dominant expense

**Stories Feature:**
- Ephemeral: Auto-delete after 24 hours
- Storage: Separate from posts (temporary storage)
- Prioritized display: Show at top of feed
- View tracking: Who viewed your story
- Expiration handling: Cron job or lazy deletion

**Privacy and Access Control:**
- Public vs private accounts
- Approve followers (for private accounts)
- Feed visibility: Only show to approved followers
- Database: Check relationship before serving post

**Explore Feed (Discovery):**
- Algorithmic: Not based on follows
- Personalization: ML model predicts interest
- Signals: Similar users, engagement, content type
- Diversity: Mix popular and niche content
- Real-time: Update frequently

**Direct Messages:**
- Real-time chat (WebSocket)
- One-on-one and group chats
- Media sharing in messages
- Read receipts, typing indicators
- End-to-end encryption (optional)

#### 💻 What to Practice:
- Design media processing pipeline (upload → resize → store → CDN)
- Calculate storage for 100M photos/day, 5 MB average
- Design Stories feature (24-hour expiration)
- Design privacy controls (public vs private accounts)
- Design Explore feed (ML-based recommendations)
- Design DM system (real-time chat)

#### 📖 Key Questions:
- How to handle media storage at scale?
- How to generate thumbnails efficiently?
- How to implement 24-hour expiration for Stories?
- How to personalize Explore feed?
- How to ensure privacy for private accounts?
- Differences from Twitter architecture?

---

### Day 35: Week 5 Review & Mock Interview

#### 🎯 Week 5 Review Checklist:

**URL Shortener (Days 29-30):**
- Can design end-to-end URL shortener?
- Understand base62 encoding?
- Can calculate capacity (QPS, storage)?
- Know how to implement caching and analytics?
- Understand rate limiting and security?

**Pastebin (Day 31):**
- Understand differences from URL shortener?
- Can design expiration mechanism?
- Know how to handle large pastes?
- Understand syntax highlighting?

**Twitter Feed (Days 32-33):**
- Can explain fan-out approaches?
- Understand hybrid approach for celebrities?
- Can design feed ranking?
- Know how to implement real-time updates?
- Understand trending topics calculation?

**Instagram (Day 34):**
- Understand media-centric design?
- Can design Stories feature?
- Know how to implement Explore feed?
- Understand privacy controls?

#### 💻 Mock Interview Practice:

**Practice these in 45-minute sessions:**

1. Design URL Shortener
   - Clarify requirements (5 min)
   - Capacity estimation (5 min)
   - High-level design (10 min)
   - Deep dive (20 min): Encoding, caching, analytics
   - Trade-offs (5 min)

2. Design Twitter
   - Clarify requirements (5 min)
   - Capacity estimation (5 min)
   - High-level design (10 min)
   - Deep dive (20 min): Fan-out, ranking, real-time
   - Trade-offs (5 min)

3. Design Pastebin
   - Focus on: Storage strategy, expiration, security

4. Design Instagram
   - Focus on: Media handling, Stories, privacy

**Interview Framework:**
1. Clarify requirements: Functional and non-functional
2. Capacity estimation: QPS, storage, bandwidth
3. API design: Key endpoints
4. High-level design: Major components
5. Database schema: Tables and relationships
6. Deep dive: Pick 2-3 areas (caching, scaling, real-time)
7. Trade-offs: Justify decisions

---

# Week 6: Advanced Applications (Days 36-42)

### Day 36: Video Streaming - Part 1 (Core Infrastructure)

#### 🎯 Core Concepts to Learn:

**Video Streaming Requirements:**
- Functional: Upload video, transcode to multiple formats, stream to users, recommendations
- Non-functional: Low latency (<2s to start), high availability, scalable to billions of views
- Scale: 100M videos, 1B views/day

**Video Encoding and Transcoding:**
- Codecs: H.264 (widely supported), H.265/HEVC (better compression), VP9 (YouTube), AV1 (future)
- Container formats: MP4, WebM, HLS
- Bitrates: 144p (200 kbps), 360p (500 kbps), 720p (2.5 Mbps), 1080p (5 Mbps), 4K (20 Mbps)
- Adaptive bitrate: HLS (HTTP Live Streaming), DASH
- Transcoding: Convert to multiple resolutions and bitrates
- Processing time: 1 hour video → 10 minutes to encode

**CDN Strategy for Video:**
- Why CDN: Reduce latency, reduce origin load, save bandwidth
- Edge locations: Serve video from nearest location
- Cache videos: Popular videos cached at edge
- Origin: S3 or object storage
- Chunking: Break video into small chunks (2-10 seconds)
- Manifest file: Lists available chunks and bitrates

**Recommendation System Basics:**
- Collaborative filtering: Users who liked A also liked B
- Content-based: Recommend similar videos (tags, category)
- Hybrid: Combine both approaches
- Signals: Watch time, likes, shares, user history
- Two-stage: Candidate generation (1000s) → Ranking (top 50)
- Personalization: Per-user recommendations

**View Count Consistency:**
- Eventual consistency: OK if count slightly delayed
- Async updates: Don't block video serving
- Batch updates: Aggregate every minute
- Approximate count: HyperLogLog for distinct views
- Display: Round to nearest (1.2M instead of 1,234,567)

#### 💻 What to Practice:
- Design video upload and processing pipeline
- Calculate transcoding capacity (1M videos/day, 10 min each)
- Design CDN strategy for global users
- Calculate storage (100M videos, avg 500 MB each)
- Calculate bandwidth (1B views/day, avg 5 Mbps)
- Design recommendation system (high-level)
- Design view counter (eventual consistency)

#### 📖 Key Questions:
- How to transcode videos efficiently?
- Why use CDN for video streaming?
- What is adaptive bitrate streaming?
- How to ensure low startup latency?
- How to handle view count at scale?
- How to recommend videos to users?

---

### Day 37: Video Streaming - Part 2 (Advanced Features)

#### 🎯 Advanced Features to Learn:

**Live Streaming:**
- Ingestion: RTMP (Real-Time Messaging Protocol) from encoder
- Transcoding: Real-time encoding to multiple bitrates
- Distribution: HLS or DASH to viewers
- Latency: Traditional (10-30s), Low-latency (2-5s), Ultra-low (< 1s)
- Challenges: Scale live viewers, handle encoder failures

**Comments and Engagement:**
- Comments: Store in database, paginated, threaded
- Real-time updates: New comments via WebSocket
- Spam filtering: ML-based moderation
- Likes/dislikes: Fast increment (Redis counters)
- Notifications: Alert creator of new comments

**Creator Monetization:**
- Ad insertion: Pre-roll, mid-roll, post-roll ads
- Subscriptions: Premium content, ad-free
- Super chat: Pay to highlight comment in live stream
- Revenue share: 55% creator, 45% platform (YouTube's split)
- Analytics: Views, watch time, demographics for creators

**Content Moderation:**
- Automated: ML models detect inappropriate content
- Human review: Escalate to reviewers
- User reports: Flagging system
- Strikes: Warn creators, remove videos, ban accounts
- Age restrictions: Mark videos as 18+

**Copyright Detection:**
- Content ID: Fingerprint videos, match against database
- Manual claims: Rights holders can claim content
- Monetization: Transfer revenue to rights holder
- Blocking: Remove or mute audio

#### 💻 What to Practice:
- Design live streaming architecture (ingestion → transcoding → delivery)
- Design comment system with real-time updates
- Design monetization system (ads, subscriptions, revenue tracking)
- Design content moderation pipeline (automated + human review)
- Design copyright detection (video fingerprinting)
- Calculate costs: Storage, bandwidth, transcoding

#### 📖 Key Questions:
- How does live streaming differ from on-demand?
- How to scale live streaming to millions of viewers?
- How to insert ads without disrupting experience?
- How to detect copyrighted content?
- How to moderate content at scale?

---

### Day 38: Ride Sharing (Uber) - Part 1 (Core Matching)

#### 🎯 Core Concepts to Learn:

**Ride Sharing Requirements:**
- Functional: Request ride, match driver, track ride, calculate fare, rate ride
- Non-functional: Low latency matching (<5s), real-time tracking, high availability
- Scale: 10M riders, 1M drivers, 10M trips/day

**Driver-Rider Matching Algorithms:**
- Nearest driver: Simple but not optimal (may not be available)
- Availability-weighted: Consider driver acceptance rate
- ETA-based: Minimize rider wait time
- Load balancing: Distribute across drivers
- Batch matching: Match multiple requests together (UberPool)
- Constraints: Car type, driver rating, surge pricing

**Real-Time Location Tracking:**
- GPS updates: Driver sends location every 3-5 seconds
- Storage: Store in geospatial database (Redis GEOADD)
- Querying: Find drivers within radius
- Optimization: Only update if moved significant distance
- Battery: Reduce update frequency when idle

**ETA Calculation:**
- Simple: Straight-line distance / average speed
- Advanced: Use real-time traffic data
- APIs: Google Maps, Mapbox, HERE
- Factors: Distance, traffic, time of day, weather
- Update: Recalculate periodically during ride

**Dynamic Pricing (Surge):**
- Supply-demand: More riders than drivers → surge
- Pricing: 1.5x, 2x, 3x normal fare
- Geographic: Different areas different surge
- Time-based: Rush hour, events, weather
- Transparency: Show multiplier to users

#### 💻 What to Practice:
- Design driver-rider matching algorithm
- Implement location tracking (update every 3 seconds)
- Design ETA calculation with traffic data
- Design dynamic pricing (calculate surge multiplier)
- Calculate: How many drivers within 5 km of rider?
- Design geospatial index for 1M drivers

#### 📖 Key Questions:
- How to match driver and rider in <5 seconds?
- How to track millions of drivers in real-time?
- How to calculate ETA accurately?
- How to implement surge pricing?
- How to handle GPS accuracy issues?

---

### Day 39: Ride Sharing (Uber) - Part 2 (Operations)

#### 🎯 Advanced Features to Learn:

**Supply-Demand Balancing:**
- Prediction: Forecast demand by area and time
- Incentives: Send drivers to high-demand areas
- Pricing: Use surge to balance supply and demand
- Data: Historical patterns, events, weather

**Route Optimization:**
- Shortest path: Dijkstra, A* algorithm
- Real-time: Update route based on traffic
- Multiple stops: Optimize order (UberPool)
- Turn-by-turn: Navigation instructions

**Payment Processing:**
- Credit card: Stripe, Braintree integration
- Security: PCI compliance, tokenization
- Failed payment: Retry, notify user, suspend account
- Refunds: Handle cancellations, issues
- Split payments: UberPool cost splitting

**Surge Pricing Algorithms:**
- Zone-based: Divide city into zones (geohash)
- Calculate: (Demand - Supply) / Supply
- Thresholds: 20% imbalance → 1.5x, 50% → 2x
- Dynamic: Update every minute
- Prediction: Anticipate demand spikes

**Driver and Rider Safety:**
- Background checks: Verify driver identity
- Ratings: Two-way rating system
- Emergency button: Contact authorities
- Share trip: Send live location to friend
- Insurance: Coverage during ride
- Incident reporting: In-app reporting

#### 💻 What to Practice:
- Design supply-demand prediction model
- Implement route optimization (shortest path with traffic)
- Design payment processing (handle failures, refunds)
- Calculate surge pricing per zone
- Design safety features (emergency button, trip sharing)
- Design rating system (calculate average, detect fraud)

#### 📖 Key Questions:
- How to balance supply and demand?
- How to optimize routes for multiple stops?
- How to handle failed payments?
- How to calculate surge fairly?
- How to ensure rider and driver safety?

---

### Day 40: Search Engine - Part 1 (Crawling & Indexing)

#### 🎯 Core Concepts to Learn:

**Search Engine Requirements:**
- Functional: Crawl web, index pages, rank results, serve queries
- Non-functional: Low latency (<100ms), high relevance, scalable to billions of pages
- Scale: 10B web pages, 100K queries/second

**Web Crawling Strategies:**
- Crawler: Bot that downloads web pages
- Frontier: Queue of URLs to crawl
- Politeness: Respect robots.txt, rate limit per domain
- Freshness: Re-crawl popular sites frequently
- Depth: Limit crawl depth (avoid infinite loops)
- Distributed: Multiple crawlers working in parallel
- Deduplication: Avoid crawling same page twice (URL normalization, content hash)

**Distributed Indexing:**
- Inverted index: Term → Document list (covered Day 24)
- Partition: Shard index by term or document
- Map-Reduce: Distributed index building
- Update: Incremental updates vs full rebuild
- Storage: Billions of documents, petabytes of data

**Link Analysis (PageRank):**
- Idea: Important pages linked by important pages
- Random surfer: Model web browsing as random walk
- Formula: PR(A) = (1-d) + d * Σ(PR(B)/C(B))
  - d: Damping factor (0.85)
  - B: Pages linking to A
  - C(B): Number of outbound links from B
- Iteration: Converge to stable scores
- Modern: ML models augment PageRank

**Search Ranking Factors:**
- Relevance: TF-IDF, BM25
- Link analysis: PageRank, authority
- Freshness: Newer content ranked higher
- User behavior: Click-through rate, dwell time
- Personalization: Location, history, preferences
- Query intent: Understand what user wants

#### 💻 What to Practice:
- Design web crawler (frontier, politeness, deduplication)
- Calculate: How many crawlers for 10B pages, 1 month?
- Design distributed indexing (MapReduce)
- Implement PageRank algorithm (simplified version)
- Design ranking factors (combine multiple signals)
- Calculate storage for inverted index (10B pages)

#### 📖 Key Questions:
- How to crawl 10 billion pages efficiently?
- How to handle duplicate content?
- What is PageRank and how does it work?
- How to build inverted index at scale?
- How to rank search results?

---

### Day 41: Search Engine - Part 2 (Query Processing)

#### 🎯 Advanced Features to Learn:

**Query Understanding:**
- Spell correction: Did you mean "python"? (Levenshtein distance)
- Tokenization: Break query into terms
- Stemming: "running" → "run"
- Synonyms: "car" = "automobile"
- Stop words: Remove "the", "a", "is"
- Intent: Navigate (go to site), informational (learn), transactional (buy)

**Result Ranking and Personalization:**
- Two-stage: Retrieval (1000s of candidates) → Ranking (top results)
- ML ranking: Learn from user clicks, dwell time
- Personalization: Use user location, history, preferences
- Diversity: Don't show too many results from same site
- Freshness: Boost recent content for news queries

**Auto-complete Systems:**
- Trie data structure: Efficient prefix search
- Popularity: Rank by frequency
- Personalization: Recent searches, location
- Speed: Sub-second response (<100ms)
- Caching: Cache popular prefixes

**Snippet Generation:**
- Extract: Relevant portion of page
- Highlight: Bold query terms
- Limit: 150-200 characters
- Rich snippets: Structured data (ratings, price, date)

**Voice and Visual Search:**
- Voice: Speech-to-text → text search
- Visual: Image recognition → find similar images
- Multimodal: Combine text, image, voice

**Search Quality Metrics:**
- Relevance: Precision (relevant / returned), Recall (relevant / total)
- Ranking: NDCG (Normalized Discounted Cumulative Gain)
- User satisfaction: Click-through rate, dwell time, return rate
- A/B testing: Experiment with ranking changes

#### 💻 What to Practice:
- Design query understanding pipeline (spell check, synonyms)
- Implement auto-complete with trie
- Design ranking algorithm (ML-based)
- Design snippet generation
- Design A/B testing framework for search
- Calculate: Cache size for auto-complete

#### 📖 Key Questions:
- How to handle misspelled queries?
- How to personalize search results?
- How does auto-complete work at scale?
- How to measure search quality?
- How to serve queries in <100ms?

---

### Day 42: Week 6 Review & Integration

#### 🎯 Week 6 Review Checklist:

**Video Streaming (Days 36-37):**
- Can design video upload and transcoding pipeline?
- Understand CDN strategy for video?
- Know adaptive bitrate streaming?
- Can design live streaming?
- Understand content moderation?

**Ride Sharing (Days 38-39):**
- Can design driver-rider matching?
- Understand real-time location tracking?
- Know how to calculate ETA and surge pricing?
- Can design payment processing?

**Search Engine (Days 40-41):**
- Can design web crawler?
- Understand distributed indexing?
- Know PageRank algorithm?
- Can design query processing pipeline?
- Understand ranking factors?

#### 💻 Integration Practice:

Design these integrated systems:

1. **YouTube-like Platform:**
   - Combine: Video streaming + comments + recommendations + monetization
   - Consider: Scale, costs, trade-offs

2. **Uber-like Platform:**
   - Combine: Matching + tracking + payments + surge pricing
   - Consider: Real-time requirements, accuracy, safety

3. **Google-like Search:**
   - Combine: Crawling + indexing + ranking + query processing
   - Consider: Latency, relevance, scale

**Practice Interview Questions:**
- "Design Netflix" (video streaming focus)
- "Design Uber" (real-time systems focus)
- "Design Google Search" (distributed systems focus)

---

# Weeks 7-8: Specialized Systems & Data Processing (Days 43-56)

---

## Day 43-44: Messaging Systems (WhatsApp/Slack)

### 🎯 Core Concepts to Learn:

#### One-to-One Messaging Architecture:

**Requirements:**
- Send message from User A to User B
- Real-time delivery (< 100ms latency)
- Message persistence (store for years)
- Read receipts
- Typing indicators
- Online/offline status

**High-Level Design:**
```
User A → WebSocket → Message Server → Database
                           ↓
                      WebSocket → User B
```

**Components:**

**1. WebSocket Servers:**
- Maintain persistent connections with clients
- Each user connected to one WebSocket server
- Server holds mapping: user_id → WebSocket connection
- Send/receive messages in real-time

**2. Message Flow:**
```
1. User A sends message via WebSocket
   {
     "from": "user_a",
     "to": "user_b",
     "text": "Hello",
     "timestamp": "2025-01-15T10:30:00Z",
     "message_id": "msg-123"
   }

2. Message Server receives message
   - Save to database
   - Check if User B is online
   - If online: Find User B's WebSocket server
   - Push message to User B

3. User B receives message
   - Display in chat
   - Send acknowledgment (delivery receipt)

4. Update message status to "delivered"

5. User B reads message
   - Send read receipt
   - Update status to "read"
```

**3. Message Storage (Database):**

**Schema:**
```
messages table:
- id (UUID)
- from_user_id
- to_user_id
- text
- timestamp
- status (sent, delivered, read)
- attachment_url (for images/videos)

conversations table:
- id
- user1_id
- user2_id
- last_message_id
- last_message_timestamp
- unread_count_user1
- unread_count_user2
```

**Sharding Strategy:**
- Shard by conversation_id (all messages in conversation on same shard)
- Or shard by user_id (all user's conversations on same shard)

**4. Message Delivery Guarantees:**

**At-Least-Once Delivery:**
- Message sent to recipient
- If no acknowledgment, retry
- Recipient may receive duplicates
- Use message_id to deduplicate

**Handling Offline Users:**
- User B offline when message sent
- Store message in database
- When User B comes online:
  - Query unread messages
  - Push to User B
  - Or use push notification to wake app

#### Group Chat Architecture:

**Requirements:**
- Support groups up to 10,000 members (WhatsApp limit: 1024, Slack larger)
- Real-time delivery to all online members
- Message persistence
- Read receipts per user

**Challenge:**
- Sending message to 10,000 users = 10,000 push operations

**Solution 1: Fan-out on Write (Push Model):**
- When user sends message:
  - Save message once
  - Push to all online members immediately
- **Pros:** Fast reads (users get message immediately)
- **Cons:** 
  - Slow writes (push to 10,000 users)
  - What if 5,000 users online? Still need to push to 5,000
- **Use when:** Small groups (< 100 members)

**Solution 2: Fan-out on Read (Pull Model):**
- When user sends message:
  - Save message once in group's message log
  - Increment group message counter
  - Send notification to online members only
- When user opens group:
  - Fetch new messages from server
  - Display
- **Pros:** Fast writes (save once), scalable
- **Cons:** Not real-time (user must pull), more API calls
- **Use when:** Large groups (> 100 members)

**Hybrid Approach (Best):**
- For small groups (< 100): Fan-out on write
- For large groups (> 100): Fan-out on read with notifications

**Group Message Storage:**
```
group_messages table:
- id
- group_id
- user_id
- text
- timestamp

group_members table:
- group_id
- user_id
- last_read_message_id
- joined_at
```

**Read Receipts in Groups:**
- Don't track per-user read status (too expensive for 10,000 members)
- Track only "delivered to device" (not "read by eyes")
- Or show "Read by 245 members" (aggregate count)

#### Real-Time Presence (Online/Offline Status):

**Requirements:**
- Show if user is online, offline, or "last seen"
- Update in real-time

**Implementation:**

**1. Heartbeat Mechanism:**
```
Client sends heartbeat every 30 seconds:
POST /presence/heartbeat
{
  "user_id": "user_a",
  "status": "online"
}

Server updates Redis:
SET user:user_a:presence "online" EX 60
(expires in 60 seconds if no heartbeat)
```

**2. Status Check:**
```
When User B checks User A's status:
GET user:user_a:presence

If exists: "online"
If expired/not exists: "offline"

Last seen:
GET user:user_a:last_seen
→ "2025-01-15T10:30:00Z"
```

**3. On Disconnect:**
```
WebSocket disconnects:
- Update status to "offline"
- Set last_seen timestamp
```

**4. Optimization:**
- Don't broadcast presence changes to all contacts
- Only send when user opens chat with that person
- Batch presence updates (send every 10 seconds, not every second)

#### Read Receipts and Typing Indicators:

**Read Receipts:**
```
User B reads message:
1. Send event: POST /messages/{msg_id}/read
2. Update message status in database
3. Push notification to User A:
   {
     "type": "read_receipt",
     "message_id": "msg-123",
     "read_by": "user_b",
     "read_at": "2025-01-15T10:30:00Z"
   }
```

**Typing Indicators:**
```
User A starts typing:
1. Send event via WebSocket:
   {
     "type": "typing_start",
     "conversation_id": "conv-456"
   }

2. Server forwards to User B (if online)
   - Don't persist (ephemeral)
   - User B shows "User A is typing..."

3. User A stops typing (after 5 seconds of no activity):
   {
     "type": "typing_stop",
     "conversation_id": "conv-456"
   }
```

**Optimization:**
- Don't send typing event on every keystroke
- Throttle to once per 2-3 seconds

#### End-to-End Encryption:

**Purpose:** Only sender and recipient can read messages, not server

**How Signal Protocol Works:**

**1. Key Exchange:**
- Each user has public/private key pair
- Public keys stored on server
- Private keys NEVER leave device

**2. Sending Encrypted Message:**
```
User A sends message to User B:
1. Fetch User B's public key from server
2. Encrypt message with User B's public key
   encrypted_text = encrypt(text, user_b_public_key)
3. Send encrypted message to server
4. Server stores encrypted message (can't read it)
5. Server forwards to User B
6. User B decrypts with private key
   text = decrypt(encrypted_text, user_b_private_key)
```

**3. Group Encryption:**
- Each message encrypted with group key
- Group key encrypted separately for each member
- Complex key management

**Trade-off:**
- **Pro:** Privacy, security
- **Con:** 
  - Can't search messages on server
  - Can't show message preview in notifications
  - Complexity

#### Media Handling (Images, Videos, Files):

**Upload Flow:**
```
1. User A selects image
2. Upload to object storage (S3)
   - Generate thumbnail
   - Compress image
3. Save metadata in database:
   {
     "message_id": "msg-123",
     "media_url": "s3://bucket/images/abc.jpg",
     "thumbnail_url": "s3://bucket/thumbnails/abc.jpg",
     "media_type": "image",
     "size": 2048000
   }
4. Send message with media_url
5. User B fetches image from S3 (via CDN)
```

**Optimization:**
- CDN for fast image delivery
- Progressive loading (thumbnail first, full image later)
- Lazy loading (load images as user scrolls)

**Storage:**
- Store media in object storage (S3), not database
- Use CDN (CloudFront) for fast delivery
- Delete old media to save costs (after 1-2 years)

### 💻 Practice Tasks:

1. **Design Message Delivery:**
   - User A sends message to User B (offline)
   - Message saved in database
   - User B comes online
   - How to deliver message?
   - Options: Query on connect, push notification, WebSocket on reconnect

2. **Design Group Chat for 1,000 Members:**
   - Choose fan-out strategy (write vs read)
   - Calculate: 100 online members, user sends 1 message
   - Fan-out on write: 100 push operations
   - Fan-out on read: 1 save + 100 notifications

3. **Calculate Storage:**
   - 1 billion users
   - 50 messages per user per day
   - Average message: 200 bytes
   - Daily: 1B × 50 × 200 = 10 TB/day
   - 5 years: 10 TB × 365 × 5 = 18.25 PB

4. **Design Presence System:**
   - Heartbeat every 30 seconds
   - Store in Redis with TTL 60 seconds
   - If no heartbeat, status → offline
   - Last seen timestamp

5. **Design End-to-End Encryption:**
   - Key exchange using public/private keys
   - Encrypt message with recipient's public key
   - Server stores encrypted message
   - Recipient decrypts with private key

### 📖 Key Questions:

1. How to handle offline users in messaging?
   - **Answer:** Store messages in database, deliver when online, use push notifications

2. Fan-out on write vs read for group chat?
   - **Answer:** Write for small groups (< 100), read for large groups (> 1000)

3. How to ensure message delivery (at-least-once)?
   - **Answer:** Send message, wait for ack, retry if no ack, deduplicate using message_id

4. How to implement read receipts?
   - **Answer:** Update message status when read, notify sender via WebSocket

5. How to scale WebSocket connections to millions?
   - **Answer:** Distribute across multiple servers, use consistent hashing for user → server mapping

---

## Day 45-46: Social Network (Facebook-like)

### 🎯 Core Concepts to Learn:

#### Friend Relationships (Graph Database):

**Challenge:**
- Represent friend relationships (bidirectional)
- Efficient queries: Get friends, mutual friends, friend suggestions

**Schema (SQL):**
```
users table:
- id
- name
- email
- profile_pic_url

friendships table:
- user_id_1
- user_id_2
- status (pending, accepted, blocked)
- created_at

(user_id_1, user_id_2) unique constraint
Store both directions or ensure user_id_1 < user_id_2
```

**Queries:**

**Get User's Friends:**
```sql
SELECT u.* FROM users u
JOIN friendships f ON (
  (f.user_id_1 = ? AND f.user_id_2 = u.id) OR
  (f.user_id_2 = ? AND f.user_id_1 = u.id)
)
WHERE f.status = 'accepted'
```

**Graph Database (Neo4j):**
```
Better for friend relationships:

CREATE (alice:User {name: 'Alice'})
CREATE (bob:User {name: 'Bob'})
CREATE (alice)-[:FRIEND]->(bob)

Query friends:
MATCH (user:User {id: 123})-[:FRIEND]-(friend)
RETURN friend

Query mutual friends:
MATCH (user:User {id: 123})-[:FRIEND]-(friend)-[:FRIEND]-(mutual)
WHERE NOT (user)-[:FRIEND]-(mutual)
RETURN mutual
```

**Trade-off:**
- SQL: Easy to set up, mature, but complex queries for graph operations
- Graph DB: Natural for relationships, efficient graph queries, but less mature ecosystem

#### News Feed Generation:

**Requirements:**
- Show posts from friends (and pages user follows)
- Ranked by relevance (not just chronological)
- Real-time updates (see new posts as they appear)
- Scalable to billions of users

**Similar to Twitter Feed (Day 32), but key differences:**
- Facebook: Bidirectional friendships (mutual consent)
- Twitter: Asymmetric following (no consent needed)
- Facebook: More photos/videos, longer posts

**Feed Generation Approaches:**

**1. Fan-out on Write:**
- When User A posts:
  - Push post to all friends' feeds immediately
  - Pre-compute feeds
- **Pros:** Fast reads (feed already computed)
- **Cons:** Slow writes (if User A has 5,000 friends, 5,000 writes)

**2. Fan-out on Read:**
- When User B views feed:
  - Fetch recent posts from all friends
  - Merge and rank
- **Pros:** Fast writes
- **Cons:** Slow reads (must query many users)

**3. Hybrid (Facebook's Approach):**
- Regular users: Fan-out on write
- Celebrities: Fan-out on read
- When viewing feed: Merge pre-computed feed + celebrity posts

**Feed Ranking Algorithm:**

**Factors:**
- **Recency:** Recent posts ranked higher
- **Engagement:** Likes, comments, shares
- **Relationship:** Close friends ranked higher (based on interaction frequency)
- **Post Type:** Photos/videos ranked higher than text
- **User Behavior:** Personalized (ML model predicts interest)

**EdgeRank Formula (Simplified):**
```
Score = Affinity × Weight × Time Decay

Affinity: How close you are to poster (based on interactions)
Weight: Post type weight (photo > link > text)
Time Decay: Older posts score lower
```

#### Photo/Video Storage:

**Requirements:**
- Upload photos/videos
- Multiple sizes (thumbnail, small, medium, large)
- Fast delivery worldwide
- Tagging, comments, likes

**Architecture:**
```
User → Upload → API Server → S3 (Object Storage)
                  ↓
            Processing Queue
                  ↓
              Workers
                  ↓
        Generate Thumbnails
        Compress Images
        Extract Metadata
                  ↓
            Store in S3
                  ↓
              CDN (CloudFront)
                  ↓
              Users (Fast Delivery)
```

**Storage:**
```
photos table:
- id
- user_id
- album_id
- caption
- upload_date
- original_url (S3)
- thumbnail_url
- small_url
- medium_url
- large_url
- likes_count
- comments_count
```

**Process:**
1. User uploads photo (5 MB)
2. Save original to S3
3. Queue: "ProcessPhoto" job
4. Worker: 
   - Download from S3
   - Generate thumbnails (100×100, 300×300)
   - Compress (reduce quality for smaller sizes)
   - Upload all versions to S3
5. Update database with URLs
6. CDN caches images

**Optimization:**
- Serve via CDN for low latency
- Lazy loading (load images as user scrolls)
- Progressive JPEG (show low-quality first, then high-quality)

#### Friend Suggestions (People You May Know):

**Algorithms:**

**1. Mutual Friends:**
```
Find users who have many mutual friends with you

Example:
You: [Alice, Bob, Carol]
Dave: [Alice, Bob, Charlie]
Mutual: [Alice, Bob] (2 mutual friends)
Suggest: Dave
```

**2. Network Distance:**
- Friends of friends (2nd degree connections)
- Friends of friends of friends (3rd degree)
- Closer in network = higher score

**3. Common Interests:**
- Same school, workplace, location
- Same groups, pages liked

**4. Graph Algorithm (Collaborative Filtering):**
- Users similar to you liked this person
- Machine learning model predicts

**Implementation:**
```
Batch job runs daily:
1. For each user:
   - Calculate mutual friends with all non-friends
   - Sort by mutual friends count
   - Top 50 → friend suggestions
2. Store in cache (Redis)
3. Serve suggestions from cache
```

#### Notification System:

**Types:**
- Friend request
- Post like/comment
- Photo tag
- Event invitation
- Birthdays

**Architecture:**
```
Event occurs (e.g., Alice likes Bob's post)
  ↓
Notification Service
  ↓
Queue: "SendNotification"
  ↓
Workers:
  - In-app notification
  - Push notification (mobile)
  - Email (if user opted in)
```

**Schema:**
```
notifications table:
- id
- user_id (recipient)
- type (like, comment, friend_request)
- actor_id (who did the action)
- entity_id (post_id, photo_id, etc.)
- read (boolean)
- created_at
```

**Optimization:**
- Batch notifications (don't send email for every like)
- "Alice and 10 others liked your post"
- User preferences (opt out of certain notification types)

### 💻 Practice Tasks:

1. **Design Friend Suggestion Algorithm:**
   - Find users with most mutual friends
   - Weight by interaction frequency
   - Exclude already friends, pending requests

2. **Calculate Feed Generation:**
   - User has 500 friends
   - Average 10 posts per friend per day
   - Total: 5,000 posts/day
   - How to fetch and rank in real-time?

3. **Design Photo Upload Pipeline:**
   - Upload original to S3
   - Generate thumbnails (3 sizes)
   - Compress images
   - Store URLs in database
   - Serve via CDN

4. **Calculate Storage:**
   - 1 billion users
   - Each uploads 5 photos/month
   - Average photo: 3 MB
   - Monthly: 1B × 5 × 3 MB = 15 PB/month

5. **Design Privacy Controls:**
   - Posts: Public, Friends, Custom
   - Photos: Public, Friends, Only Me
   - Check permissions before serving content

### 📖 Key Questions:

1. Why use graph database for social networks?
   - **Answer:** Natural representation of relationships, efficient graph queries (mutual friends, shortest path)

2. How to generate news feed?
   - **Answer:** Hybrid approach - fan-out on write for regular users, fan-out on read for celebrities

3. How to suggest friends?
   - **Answer:** Mutual friends algorithm, network distance, common interests

4. How to handle photo storage at scale?
   - **Answer:** Object storage (S3), multiple sizes, CDN for delivery, async processing

---

## Day 47-48: E-Commerce Platform (Amazon-like)

### 🎯 Core Concepts to Learn:

#### Product Catalog & Search:

**Requirements:**
- 100 million products
- Search by keyword, category, brand, price range
- Filters (color, size, rating)
- Auto-complete
- Fast search (< 100ms)

**Database:**
```
products table:
- id
- name
- description
- brand
- category_id
- price
- rating
- reviews_count
- inventory_count
- images (JSON array)
```

**Search Implementation:**

**Elasticsearch Index:**
```json
{
  "product_id": "123",
  "name": "iPhone 15 Pro",
  "description": "Latest iPhone with...",
  "brand": "Apple",
  "category": "Electronics > Phones",
  "price": 999,
  "rating": 4.5,
  "reviews_count": 1523
}
```

**Search Query:**
```
GET /products/_search
{
  "query": {
    "multi_match": {
      "query": "iphone",
      "fields": ["name^3", "description", "brand^2"]
    }
  },
  "filter": {
    "range": {"price": {"gte": 500, "lte": 1500}},
    "term": {"category": "Phones"}
  },
  "sort": [
    {"_score": "desc"},
    {"rating": "desc"}
  ]
}
```

**Auto-complete:**
- Use Elasticsearch completion suggester
- Or Trie data structure
- Index: "iphone" → ["iPhone 15", "iPhone 15 Pro", "iPhone case"]

#### Shopping Cart:

**Requirements:**
- Add/remove items
- Persist across sessions
- Update quantities
- Calculate total

**Storage Options:**

**Option 1: Database:**
```
carts table:
- user_id (PK)
- created_at
- updated_at

cart_items table:
- cart_id
- product_id
- quantity
- price (snapshot at time of add)
```
- **Pros:** Persistent, durable
- **Cons:** Slower (database query), more load on DB

**Option 2: Redis (Session-based):**
```
Key: cart:{user_id}
Value: {
  "items": [
    {"product_id": "123", "quantity": 2, "price": 999},
    {"product_id": "456", "quantity": 1, "price": 499}
  ],
  "total": 2497
}
TTL: 30 days
```
- **Pros:** Fast (in-memory), low latency
- **Cons:** Less durable (if Redis fails, cart lost)

**Option 3: Hybrid:**
- Redis for active sessions (fast access)
- Database for persistence (backup)
- Sync Redis to DB periodically

#### Order Processing Pipeline:

**Steps:**
1. User clicks "Place Order"
2. Validate cart (check inventory, prices)
3. Reserve inventory
4. Process payment
5. Create order
6. Update inventory
7. Initiate shipping
8. Send confirmation email

**Challenge:** These steps must be atomic (all succeed or all fail)

**Solution: Saga Pattern (Day 16)**

**Orchestration:**
```
Order Saga:
1. Reserve Inventory
   - Success → Proceed
   - Failure → Return error

2. Process Payment
   - Success → Proceed
   - Failure → Release inventory, return error

3. Create Order
   - Success → Proceed
   - Failure → Refund payment, release inventory

4. Initiate Shipping
   - Success → Done
   - Failure → Manual intervention (order created, payment done, but shipping failed)

5. Send Email
   - Success → Done
   - Failure → Retry, log error (non-critical)
```

**Compensation:**
- Payment fails → Release inventory
- Shipping fails → Refund payment, release inventory

#### Inventory Management:

**Requirements:**
- Track stock for each product
- Prevent overselling
- Handle concurrent orders (two users buying last item)

**Schema:**
```
inventory table:
- product_id (PK)
- warehouse_id
- quantity
- reserved_quantity
- updated_at
```

**Concurrency Challenge:**
```
Product has 1 item in stock
User A and User B order simultaneously

Without lock:
1. User A reads: quantity = 1 (available)
2. User B reads: quantity = 1 (available)
3. User A places order: quantity = 0
4. User B places order: quantity = -1 (OVERSOLD!)
```

**Solution 1: Pessimistic Lock:**
```sql
BEGIN TRANSACTION;

SELECT * FROM inventory 
WHERE product_id = ? 
FOR UPDATE; -- Locks row

IF quantity >= order_quantity:
    UPDATE inventory 
    SET quantity = quantity - order_quantity
    WHERE product_id = ?;
    COMMIT;
ELSE:
    ROLLBACK;
```

**Solution 2: Optimistic Lock (Version Number):**
```sql
-- Read with version
SELECT quantity, version FROM inventory WHERE product_id = ?;

-- Update only if version hasn't changed
UPDATE inventory 
SET quantity = quantity - ?, version = version + 1
WHERE product_id = ? AND version = ?;

IF affected_rows = 0:
    -- Version changed, retry
```

**Solution 3: Reserved Quantity:**
```
Two-step process:
1. Reserve: quantity → reserved_quantity (decrease available)
2. After payment: reserved_quantity → 0 (confirm)
3. If payment fails: reserved_quantity → quantity (release)
```

#### Payment Processing:

**Requirements:**
- Support multiple payment methods (credit card, PayPal, etc.)
- Secure (PCI compliance)
- Retry on failure
- Idempotent (don't charge twice)

**Integration:**
- Use payment gateway (Stripe, Braintree, PayPal)
- Never store credit card numbers (let gateway handle)

**Flow:**
```
1. User enters payment info
2. Frontend sends to backend
3. Backend calls Stripe API:
   POST /charges
   {
     "amount": 9999,
     "currency": "usd",
     "source": "tok_visa",  // Token from Stripe.js
     "idempotency_key": "order-123"
   }
4. Stripe processes payment
5. Stripe returns charge_id
6. Store charge_id in database
7. If API fails, retry with same idempotency_key (no double charge)
```

**Handling Failures:**
- Network failure → Retry
- Insufficient funds → Return error to user
- Fraud detection → Return error, flag for review
- Success but database write fails → Reconciliation needed

**Idempotency:**
- Use `order_id` as idempotency key
- Stripe ensures same order_id = same charge (no duplicates)

#### Recommendation Engine:

**Types:**

**1. Collaborative Filtering:**
- Users who bought X also bought Y
- Based on user behavior similarity

**2. Content-Based:**
- Similar products (same category, brand, price range)

**3. Personalized:**
- Based on user's browsing history, purchases, searches

**Implementation:**

**Offline Processing:**
```
Batch job (daily):
1. Analyze purchase history
2. Calculate product similarity (cosine similarity)
3. Generate recommendations per product
4. Store in cache (Redis)

Example:
Product: iPhone 15
Recommendations: [iPhone case, AirPods, Screen protector]
```

**Real-Time:**
```
User views iPhone 15:
1. Fetch recommendations from cache
2. Personalize based on user history (viewed cases before)
3. Boost case recommendations
4. Display top 10
```

### 💻 Practice Tasks:

1. **Design Product Search:**
   - Index 100M products in Elasticsearch
   - Search query: "iphone", filter by price $500-$1500
   - Sort by relevance, then rating
   - Auto-complete for search box

2. **Design Shopping Cart:**
   - Store in Redis for speed
   - Backup to database for persistence
   - Calculate total, apply discount codes
   - Handle out-of-stock items

3. **Design Order Processing:**
   - Saga pattern: Reserve inventory → Charge payment → Create order
   - Compensation: Refund if shipping fails
   - Idempotency: Use order_id to prevent duplicate charges

4. **Handle Inventory Concurrency:**
   - Use pessimistic locks or optimistic locks
   - Test with concurrent users ordering last item
   - Ensure no overselling

5. **Calculate Capacity:**
   - 10M orders/day = 116 orders/second
   - Peak: 300 orders/second
   - Each order: Reserve inventory, charge payment, create order, send email
   - Payment API: 50ms latency
   - Servers: 300 / (1000/50) = 15 servers

### 📖 Key Questions:

1. How to prevent overselling inventory?
   - **Answer:** Pessimistic locks (row locking) or optimistic locks (version numbers)

2. How to ensure idempotent payments?
   - **Answer:** Use order_id as idempotency key with payment gateway

3. How to handle distributed transactions in order processing?
   - **Answer:** Saga pattern with compensating transactions

4. How to scale product search?
   - **Answer:** Elasticsearch cluster, sharding by product_id

---

## Days 49-50: Data Processing Pipelines

### 🎯 Core Concepts to Learn:

#### Batch Processing:

**Use Cases:**
- ETL (Extract, Transform, Load)
- Daily reports
- Data aggregation
- Log analysis

**MapReduce Concept:**
```
Map: Transform data (parallelize)
Reduce: Aggregate results (combine)

Example: Word count
Input: Large text files
Map: Each node counts words in its file
Reduce: Combine counts from all nodes
```

**Spark (Modern Batch Processing):**
- Faster than MapReduce (in-memory)
- Unified API for batch and streaming
- Example:
  ```
  Read logs from S3
  Filter by error level
  Count errors per service
  Write results to database
  ```

#### Stream Processing:

**Use Cases:**
- Real-time analytics
- Fraud detection
- Live dashboards
- Event processing

**Kafka Streams:**
```
Input: Kafka topic "user-events"
Processing:
- Count events per user (windowed aggregation)
- Detect anomalies (unusual patterns)
Output: Kafka topic "aggregated-events"
```

**Apache Flink:**
- Stateful stream processing
- Exactly-once semantics
- Event time processing

#### Lambda vs Kappa Architecture:

**Lambda:**
```
Batch Layer → Historical data → Batch views
Speed Layer → Real-time data → Real-time views
Merge → Unified view
```
- **Pros:** Accurate (batch) + fast (streaming)
- **Cons:** Two codebases (batch and stream)

**Kappa:**
```
Everything is streaming
Process events in real-time
Reprocess if needed (replay from Kafka)
```
- **Pros:** Single codebase
- **Cons:** Complex reprocessing

### 💻 Practice Tasks:

1. **Design ETL Pipeline:**
   - Extract: Pull data from multiple databases
   - Transform: Clean, aggregate, enrich
   - Load: Write to data warehouse (Redshift, BigQuery)

2. **Design Real-Time Analytics:**
   - Kafka ingests user events
   - Flink processes stream (windowed aggregations)
   - Output to dashboard (Grafana)

### 📖 Key Questions:

1. Batch vs stream processing?
   - **Answer:** Batch for historical data, stream for real-time

2. Lambda vs Kappa architecture?
   - **Answer:** Lambda has separate batch/stream, Kappa is stream-only

---

## Days 51-52: Notification System (Multi-Channel)

### 🎯 Core Concepts to Learn:

#### Multi-Channel Notifications:

**Channels:**
1. Push notifications (mobile)
2. Email
3. SMS
4. In-app notifications

**Architecture:**
```
Event occurs (e.g., order shipped)
  ↓
Notification Service
  ↓
Determine channels (user preferences)
  ↓
Queue per channel:
- Push queue
- Email queue
- SMS queue
  ↓
Workers:
- Push worker → APNs (iOS), FCM (Android)
- Email worker → SendGrid
- SMS worker → Twilio
```

**Priority:**
- High: Payment failure (all channels)
- Medium: Order shipped (push + email)
- Low: Marketing (email only, respect opt-out)

#### Rate Limiting Per Channel:

**Why:** Providers have limits
- SendGrid: 10,000 emails/day (free tier)
- Twilio: Rate limits per account

**Implementation:**
- Track sending rate per channel
- Queue if exceeding limit
- Backoff and retry

#### User Preferences:

**Schema:**
```
notification_preferences table:
- user_id
- push_enabled
- email_enabled
- sms_enabled
- marketing_enabled
```

**Respect opt-outs:**
- Don't send marketing if opted out
- Always send critical (payment, security)

### 💻 Practice Tasks:

1. **Design Notification System:**
   - Support push, email, SMS, in-app
   - User preferences (opt in/out per channel)
   - Priority levels
   - Rate limiting per channel

2. **Calculate Throughput:**
   - 10M users
   - 10 notifications per user per day
   - Total: 100M notifications/day
   - QPS: 100M / 86,400 = 1,157 notifications/second
   - Peak: 3,000/second

### 📖 Key Questions:

1. How to handle user preferences?
   - **Answer:** Store preferences per channel, check before sending

2. How to prioritize notifications?
   - **Answer:** High (critical), Medium (important), Low (marketing); separate queues

---

## Days 53-54: Payment System

### 🎯 Core Concepts to Learn:

#### Payment Gateway Integration:

**Flow:**
```
1. User initiates payment
2. Frontend collects payment info
3. Backend calls payment gateway (Stripe)
4. Gateway returns result
5. Store transaction in database
```

#### Idempotency:

**Critical:** Never charge user twice

**Implementation:**
```
Use unique request_id:
- Generate: request_id = order_id + timestamp
- Send to gateway with idempotency_key
- If retry, same idempotency_key = same charge
```

#### Failure Handling:

**Scenarios:**
- Network timeout → Retry
- Insufficient funds → Return error to user
- Gateway down → Queue, process later

#### Reconciliation:

**Purpose:** Ensure internal records match gateway records

**Process:**
```
Daily job:
1. Fetch transactions from gateway
2. Compare with internal database
3. Flag discrepancies
4. Manual review
```

### 💻 Practice Tasks:

1. **Design Payment Processing:**
   - Integration with Stripe
   - Retry logic with exponential backoff
   - Idempotency using order_id
   - Store transaction records

2. **Handle Payment Failures:**
   - Retry on network error
   - Notify user on insufficient funds
   - Fraud detection → Manual review

### 📖 Key Questions:

1. How to ensure idempotent payments?
   - **Answer:** Use unique idempotency_key (order_id) with payment gateway

2. How to handle failed payments?
   - **Answer:** Retry network errors, notify user on validation errors, queue for manual review on fraud

---

## Days 55-56: Gaming Backend & IoT Platform

### 🎯 Gaming Backend Concepts:

**Real-Time Multiplayer:**
- WebSocket for low latency
- Authoritative server (prevent cheating)
- State synchronization

**Matchmaking:**
- Skill-based (MMR - Matchmaking Rating)
- Queue players
- Match similar skill levels

**Leaderboards:**
- Redis sorted sets
- Update scores in real-time
- Query top N players

### 🎯 IoT Platform Concepts:

**Device Management:**
- Register devices
- Authentication (certificates)
- Device shadow (last known state)

**Telemetry:**
- Time-series data (InfluxDB)
- Millions of data points per second
- Aggregate and visualize

**OTA Updates:**
- Over-the-air firmware updates
- Staged rollout (1% → 10% → 100%)
- Rollback if issues

### 💻 Practice Tasks:

1. **Design Gaming Leaderboard:**
   - Redis sorted set
   - Update score: ZADD leaderboard {score} {player_id}
   - Get top 10: ZREVRANGE leaderboard 0 9

2. **Design IoT Data Ingestion:**
   - MQTT for device communication
   - Kafka for data pipeline
   - InfluxDB for storage
   - Grafana for visualization

### 📖 Key Questions:

1. How to prevent cheating in multiplayer games?
   - **Answer:** Authoritative server validates all actions, don't trust client

2. How to handle millions of IoT devices?
   - **Answer:** Scalable ingestion (Kafka), time-series database (InfluxDB), device shadow for state

---

**Weeks 7-8 Complete! 🎉**

You've covered specialized systems used in real-world applications. These concepts are frequently asked in system design interviews.


# Weeks 9-12: Interview Mastery & Final Preparation (Days 57-90)

---

## Week 9: Interview Framework & Communication (Days 57-63)

### 🎯 Master the Interview Framework

The interview framework is your systematic approach to solving any system design problem in 45 minutes. This is the most important skill for passing interviews.

---

### The 6-Step Interview Framework:

#### **Step 1: Clarify Requirements (5 minutes)**

**Purpose:** Understand what to build and scope the problem

**What to Ask:**

**Functional Requirements:**
- What are the core features?
- What should the system do?
- What are the use cases?

**Non-Functional Requirements:**
- How many users (DAU, MAU)?
- What scale (QPS, storage)?
- What's the read/write ratio?
- What are the latency requirements?
- What are the availability requirements (99.9%, 99.99%)?

**Out of Scope:**
- What NOT to design?
- What features can we skip?

**Example - Design Twitter:**
```
Clarifying Questions:
Q: Should we support posting tweets?
A: Yes

Q: Should we support following users?
A: Yes

Q: Should we support direct messages?
A: No, out of scope for this interview

Q: How many users?
A: 300 million DAU

Q: How many tweets per day?
A: 200 million tweets/day

Q: What's the read/write ratio?
A: 100:1 (mostly reads)

Q: Latency requirement?
A: Feed loads in < 1 second
```

**Red Flags (Don't Do This):**
❌ Jump straight to design without asking questions
❌ Assume too much
❌ Ask yes/no questions without exploring
❌ Spend 15 minutes on requirements (too long)

---

#### **Step 2: Back-of-Envelope Capacity Estimation (5 minutes)**

**Purpose:** Understand scale and make informed architecture decisions

**Key Calculations:**

**1. QPS (Queries Per Second):**
```
Formula: (DAU × Actions_Per_User) / 86,400

Example - Twitter:
- 300M DAU
- Each user views feed 5 times/day, posts 0.1 tweets/day
- Read QPS: (300M × 5) / 86,400 = 17,361 reads/second
- Write QPS: (300M × 0.1) / 86,400 = 347 writes/second
- Peak QPS: 17,361 × 3 = 52,083 reads/second (assume 3× for peak)
```

**2. Storage Estimation:**
```
Formula: Items × Size_Per_Item × Retention_Period

Example - Twitter:
- 200M tweets/day
- Each tweet: 140 chars × 2 bytes = 280 bytes (text)
- Media: 20% have media, average 200 KB
- Text storage: 200M × 280 bytes = 56 GB/day
- Media storage: 200M × 0.2 × 200 KB = 8 TB/day
- 5 years: (56 GB + 8 TB) × 365 × 5 ≈ 15 PB
```

**3. Bandwidth:**
```
Formula: QPS × Average_Size × 8 / 1,000,000 (for Mbps)

Example - Twitter:
- Read QPS: 17,361
- Average tweet with media: 100 KB
- Bandwidth: 17,361 × 100 KB × 8 / 1,000,000 = 13,889 Mbps ≈ 14 Gbps
```

**4. Servers Needed:**
```
Formula: Peak_QPS / QPS_Per_Server

Example:
- Peak: 52,083 QPS
- Each server: 1,000 QPS
- Servers: 52,083 / 1,000 = 52 servers
- Add 30% buffer: 68 servers
```

**5. Cache Size:**
```
Formula: Total_Data × Cache_Ratio (usually 20% for 80-20 rule)

Example:
- 15 PB total
- Cache 20%: 3 PB
- Or cache just today's tweets: 8 TB
```

**Quick Reference Numbers:**
```
Time:
- 1 day = 86,400 seconds
- 1 month = 2.5M seconds
- 1 year = 31.5M seconds

Availability:
- 99.9% = 43.2 min downtime/month
- 99.99% = 4.32 min downtime/month
- 99.999% = 26 seconds downtime/month

Powers of 2:
- 2^10 = 1 KB (1,024)
- 2^20 = 1 MB (1 million)
- 2^30 = 1 GB (1 billion)
- 2^40 = 1 TB (1 trillion)
```

**Red Flags:**
❌ Skip calculations entirely
❌ Spend 10+ minutes on math
❌ Get stuck on exact numbers (estimates are fine)

---

#### **Step 3: Define API or System Interface (5 minutes)**

**Purpose:** Clarify how clients interact with the system

**REST API Design:**

**Example - Twitter API:**
```
POST /tweets
Request:
{
  "user_id": "123",
  "text": "Hello world",
  "media_urls": ["url1", "url2"]
}
Response:
{
  "tweet_id": "789",
  "created_at": "2025-01-15T10:30:00Z",
  "status": "success"
}

GET /feed?user_id={user_id}&page={page}&size={size}
Response:
{
  "tweets": [
    {
      "tweet_id": "789",
      "user_id": "123",
      "text": "Hello world",
      "created_at": "2025-01-15T10:30:00Z",
      "likes_count": 10,
      "retweets_count": 5
    },
    ...
  ],
  "next_page": "cursor-abc"
}

POST /follow
Request:
{
  "follower_id": "123",
  "followee_id": "456"
}

POST /like
Request:
{
  "user_id": "123",
  "tweet_id": "789"
}
```

**Best Practices:**
- Use RESTful conventions (POST for create, GET for read)
- Include pagination (cursor or offset)
- Return relevant fields only
- Use consistent naming

**Red Flags:**
❌ Skip API design
❌ Include implementation details in API
❌ Overly complex APIs

---

#### **Step 4: High-Level Design (10 minutes)**

**Purpose:** Draw the big picture architecture

**What to Include:**
- **Client:** Web, mobile, desktop
- **Load Balancer:** Distribute traffic
- **API Gateway:** Auth, rate limiting, routing
- **Application Servers:** Business logic
- **Databases:** User data, tweets, etc.
- **Caches:** Redis for hot data
- **Message Queues:** Async processing
- **Object Storage:** Images, videos
- **CDN:** Static content delivery

**Example - Twitter High-Level Design:**
```
┌─────────┐
│ Clients │ (Web, iOS, Android)
└────┬────┘
     │ HTTPS
     ▼
┌─────────────┐
│     CDN     │ (Static content: images, JS, CSS)
└─────────────┘
     │
     ▼
┌─────────────┐
│Load Balancer│
└──────┬──────┘
       │
       ▼
┌──────────────┐
│ API Gateway  │ (Auth, Rate Limiting, Routing)
└──────┬───────┘
       │
       ▼
┌──────────────────────────────────┐
│   Application Servers (Stateless) │
└─────┬────────────────────────┬────┘
      │                        │
      ▼                        ▼
┌─────────────┐          ┌──────────────┐
│   Cache     │          │ Message Queue│
│  (Redis)    │          │  (Kafka)     │
└─────────────┘          └──────┬───────┘
      │                         │
      ▼                         ▼
┌──────────────┐          ┌──────────────┐
│  Databases   │          │   Workers    │
│  (Sharded)   │          │ (Fan-out,    │
│              │          │  Analytics)  │
│ - Users DB   │          └──────────────┘
│ - Tweets DB  │
│ - Graph DB   │
└──────────────┘
      │
      ▼
┌──────────────┐
│Object Storage│
│    (S3)      │
└──────────────┘
```

**Data Flow:**

**Post Tweet:**
```
1. Client → Load Balancer → API Gateway
2. API Gateway: Verify auth, check rate limit
3. API Server: 
   - Generate tweet_id
   - Save to Tweets DB
   - Publish to Kafka (for fan-out)
4. Return success to client
5. Workers: Fan out to followers' feeds (async)
```

**View Feed:**
```
1. Client → Load Balancer → API Gateway
2. API Gateway: Verify auth
3. API Server:
   - Check cache for user's feed
   - If cache miss: Query Feed DB
   - Merge with celebrity tweets (fan-out on read)
4. Return tweets to client
```

**Best Practices:**
- Keep it simple initially
- Show data flow with arrows
- Label components clearly
- Explain briefly as you draw

**Red Flags:**
❌ Too detailed too early
❌ Draw without explaining
❌ Messy, unclear diagrams

---

#### **Step 5: Deep Dive (15 minutes)**

**Purpose:** Dive deep into 2-3 critical components

**Interviewer will guide:** "Can you explain how feed generation works in detail?"

**Example - Twitter Feed Generation Deep Dive:**

**Challenge:**
- User has 1,000 followers
- When user posts, need to update 1,000 feeds
- Celebrities have millions of followers
- Can't update millions of feeds on every post

**Solution: Hybrid Fan-out**

**Fan-out on Write (Regular Users):**
```
When User A posts:
1. Generate tweet_id
2. Save tweet to Tweets DB
3. Publish to Kafka: "NewTweet" event
4. Workers consume event:
   - Fetch User A's followers (1,000 users)
   - For each follower:
     - Insert tweet_id into their feed (Redis)
     - Feed stored as sorted set (by timestamp)
     - Keep only recent N tweets (e.g., 1,000)
5. Next time follower views feed:
   - Read from Redis (pre-computed, fast!)
   - Fetch tweet details from Tweets DB
```

**Fan-out on Read (Celebrities):**
```
When Celebrity posts:
1. Save tweet to Tweets DB
2. Don't fan out (too expensive)
3. When follower views feed:
   - Fetch pre-computed feed from Redis
   - Merge with recent celebrity tweets (query Tweets DB)
   - Sort by timestamp
   - Return combined feed
```

**Optimization:**
```
Feed Structure (Redis Sorted Set):
Key: feed:{user_id}
Value: tweet_id
Score: timestamp

Example:
ZADD feed:123 1610000000 tweet_789
ZADD feed:123 1610000100 tweet_790

Fetch feed:
ZREVRANGE feed:123 0 99 (get 100 most recent)
```

**Trade-offs:**
- **Fan-out on Write:** Fast reads, slow writes, good for regular users
- **Fan-out on Read:** Fast writes, slow reads, good for celebrities
- **Hybrid:** Balance both, best of both worlds

**Other Topics to Deep Dive:**

**1. Database Sharding:**
- How to shard Tweets DB?
  - Shard by user_id: All user's tweets on same shard
  - Shard by tweet_id: Distribute evenly
  - Trade-off: user_id keeps user data together, tweet_id better distribution

**2. Ranking Algorithm:**
- How to rank feed?
  - Chronological (simple)
  - Engagement-based (likes, retweets)
  - Personalized (ML model)
  - EdgeRank: Affinity × Weight × Time Decay

**3. Caching Strategy:**
- What to cache?
  - User feeds (hot data)
  - Popular tweets (trending)
  - User profiles
- Cache invalidation?
  - TTL (time-based)
  - LRU (least recently used)
  - Write-through vs write-back

**Best Practices:**
- Pick 2-3 components to deep dive
- Explain algorithms clearly
- Discuss trade-offs
- Show how it scales

**Red Flags:**
❌ Surface-level explanations
❌ Can't explain how components work
❌ No trade-off discussion

---

#### **Step 6: Identify Bottlenecks & Discuss Trade-offs (5 minutes)**

**Purpose:** Show you understand limitations and can optimize

**Example - Twitter Bottlenecks:**

**1. Database Bottleneck:**
- **Problem:** Single database can't handle 50,000 QPS
- **Solution:** 
  - Read replicas (distribute reads)
  - Sharding (distribute writes)
  - NoSQL for better scalability
- **Trade-off:** Complexity vs performance

**2. Fan-out Bottleneck:**
- **Problem:** Celebrity with 100M followers, fan-out takes too long
- **Solution:** Hybrid approach (fan-out on read for celebrities)
- **Trade-off:** Slower reads for celebrity followers vs faster writes

**3. Hot Key Problem (Cache):**
- **Problem:** Trending tweet gets millions of requests, overloads cache
- **Solution:** 
  - Distribute hot keys across multiple cache nodes
  - CDN for very hot content
- **Trade-off:** More infrastructure vs availability

**4. Single Point of Failure:**
- **Problem:** Load balancer fails, entire system down
- **Solution:** Multiple load balancers, health checks, failover
- **Trade-off:** Cost vs availability

**Common Trade-offs to Discuss:**

**Consistency vs Availability (CAP Theorem):**
- Twitter: Choose availability (eventual consistency OK)
- Feed may be slightly stale (acceptable)
- Critical data (user auth) needs consistency

**Latency vs Consistency:**
- Strong consistency: Slower (wait for all replicas)
- Eventual consistency: Faster (return immediately)
- Twitter: Choose speed (eventual consistency)

**Cost vs Performance:**
- More servers: Better performance, higher cost
- Find balance based on requirements

**Complexity vs Simplicity:**
- Complex solution: Better performance, harder to maintain
- Simple solution: Easier to maintain, may not scale as well

**Best Practices:**
- Proactively mention bottlenecks
- Suggest solutions
- Discuss trade-offs
- Show you're thinking about production

**Red Flags:**
❌ Claim design is perfect
❌ Can't identify any bottlenecks
❌ No trade-off discussion

---

### 💬 Communication Best Practices

#### **Think Out Loud:**
- Share your reasoning process
- "I'm thinking we should use Redis here because..."
- "The trade-off is... vs..."
- Don't go silent for 5 minutes

#### **Ask Clarifying Questions:**
- Don't make assumptions
- "Should we optimize for read or write?"
- "What's more important: latency or consistency?"
- "Are we building this for global or regional scale?"

#### **Draw Diagrams:**
- Visual communication is powerful
- Draw as you explain
- Keep it neat and organized
- Use arrows to show data flow

#### **Discuss Trade-offs:**
- Every decision has pros/cons
- "We're choosing X over Y because..."
- "The downside is..., but the benefit is..."
- Shows depth of understanding

#### **Time Management:**
- Don't spend 20 minutes on one component
- Keep track of time (45-minute interview)
- If running out of time, summarize quickly
- "I'd also consider X, Y, Z but we can discuss if needed"

#### **Be Receptive to Hints:**
- Interviewer may guide you
- "Have you considered caching?"
- Don't be defensive, incorporate feedback
- "Good point, let's add caching here"

#### **Stay Calm:**
- Don't panic if stuck
- "Let me think through this..."
- It's OK to pause and think
- Interview is about process, not just final answer

---

### 🎯 Interview Dos and Don'ts

**DO:**
✅ Clarify requirements before designing
✅ Calculate capacity estimates (show you understand scale)
✅ Draw clear diagrams
✅ Explain your reasoning
✅ Discuss trade-offs
✅ Identify bottlenecks and suggest improvements
✅ Ask questions throughout
✅ Manage your time
✅ Be collaborative (it's a discussion, not a test)

**DON'T:**
❌ Jump straight to solution without clarifying
❌ Over-design (keep it simple first)
❌ Focus on one component too long
❌ Stay silent (think out loud)
❌ Be rigid (adapt based on feedback)
❌ Claim your design is perfect
❌ Get defensive when questioned
❌ Run out of time (watch the clock)
❌ Focus only on happy path (discuss failures)

---

### 📝 Practice Exercise (Day 57):

**Problem:** Design Instagram

**Practice with Timer (45 minutes):**

**Minutes 0-5: Requirements**
- Functional: Post photos, follow users, view feed
- Non-functional: 500M DAU, 100M photos/day, 100:1 read/write ratio
- Out of scope: Stories, direct messages, video

**Minutes 5-10: Capacity**
- QPS: Calculate read/write
- Storage: Photos for 5 years
- Bandwidth: Peak traffic

**Minutes 10-15: API**
- POST /photos (upload)
- GET /feed (view feed)
- POST /follow

**Minutes 15-25: High-Level Design**
- Draw architecture diagram
- Client → CDN → LB → API Gateway → App Servers → DB/Cache/S3

**Minutes 25-40: Deep Dive**
- Pick 2: Feed generation, photo storage
- Explain algorithms
- Discuss trade-offs

**Minutes 40-45: Bottlenecks**
- Identify issues
- Suggest improvements

**Record yourself or practice with partner!**

---

## Week 10: Practice Common Interview Questions (Days 64-70)

### 🎯 Goal: Master the Most Frequently Asked Problems

This week, you'll practice 7 of the most common system design interview questions. Spend 1 day per problem, following the 6-step framework.

---

### Day 64: Design YouTube

**Requirements:**
- Upload videos
- Watch videos
- Search videos
- Recommendations
- 1B users, 500M DAU
- 1M videos uploaded per day
- 100:1 view/upload ratio

**Key Components:**
1. **Video Upload Pipeline:**
   - Upload to object storage (S3)
   - Transcode to multiple formats (1080p, 720p, 480p)
   - Generate thumbnails
   - Extract metadata
   - Update database

2. **Video Streaming:**
   - CDN for global distribution
   - Adaptive bitrate streaming (HLS, DASH)
   - Pre-signed URLs for security

3. **Video Storage:**
   - Object storage (S3) for videos
   - Metadata in database (title, description, views)
   - Sharding by video_id

4. **Recommendations:**
   - Collaborative filtering (users who watched X also watched Y)
   - Content-based (similar videos)
   - ML model for personalization

**Capacity Estimation:**
```
Storage:
- 1M videos/day × 500 MB average = 500 TB/day
- 5 years: 500 TB × 365 × 5 = 912 PB

Bandwidth:
- 100M video views/day
- Average video: 50 MB
- Daily: 100M × 50 MB = 5 PB/day
- Bandwidth: 5 PB / 86,400 sec = 58 GB/sec
```

**Deep Dive Topics:**
- Video transcoding pipeline (async processing)
- CDN strategy (cache popular videos)
- Recommendation algorithm
- View count accuracy (eventual consistency OK)

**Trade-offs:**
- Live transcoding vs pre-transcoding (cost vs latency)
- Strong consistency vs eventual consistency for views
- Cost of storage (compress older videos)

---

### Day 65: Design Uber

**Requirements:**
- Match riders with drivers
- Real-time location tracking
- ETA calculation
- Surge pricing
- 50M riders, 5M drivers
- 10M rides per day

**Key Components:**
1. **Location Service:**
   - Drivers send location every 5 seconds (WebSocket)
   - Store in QuadTree or Geohash
   - Find nearby drivers quickly

2. **Matching Algorithm:**
   - Rider requests ride
   - Find drivers within radius (1-2 km)
   - Score based on: distance, rating, car type
   - Send request to best driver
   - If declined, try next driver

3. **ETA Calculation:**
   - Use maps API (Google Maps)
   - Consider traffic
   - Update every minute during ride

4. **Surge Pricing:**
   - Monitor supply/demand ratio per area
   - If demand > supply: Increase price multiplier
   - Dynamic pricing algorithm

**Capacity Estimation:**
```
Location Updates:
- 5M drivers × 1 update/5 sec = 1M updates/sec

Storage:
- 10M rides/day × 5 KB per ride = 50 GB/day
- 5 years: 50 GB × 365 × 5 = 91 TB
```

**Deep Dive Topics:**
- Geospatial indexing (QuadTree vs Geohash)
- WebSocket scaling (millions of connections)
- Matching algorithm (optimization)
- Surge pricing (supply/demand monitoring)

**Trade-offs:**
- GPS accuracy vs battery life
- Real-time updates vs bandwidth
- Optimal match vs fast match

---

### Day 66: Design WhatsApp

**Requirements:**
- One-to-one messaging
- Group chat
- Read receipts
- Typing indicators
- Online/offline status
- End-to-end encryption
- 2B users, 100B messages/day

**Key Components:**
1. **Message Delivery:**
   - WebSocket connections
   - At-least-once delivery
   - Message queue for offline users

2. **Message Storage:**
   - Sharded by conversation_id
   - Store messages for years
   - Compress old messages

3. **Group Chat:**
   - Fan-out on write for small groups (< 100)
   - Fan-out on read for large groups (> 1000)

4. **Presence:**
   - Heartbeat every 30 seconds
   - Store in Redis with TTL

**Capacity Estimation:**
```
Storage:
- 100B messages/day × 200 bytes = 20 TB/day
- 5 years: 20 TB × 365 × 5 = 36.5 PB

QPS:
- 100B messages/day / 86,400 = 1.15M messages/second
```

**Deep Dive Topics:**
- Message delivery guarantees
- End-to-end encryption (Signal Protocol)
- Group chat scaling (fan-out strategies)
- Media storage (S3 + CDN)

**Trade-offs:**
- At-least-once vs exactly-once
- Fan-out on write vs read for groups
- E2E encryption vs server-side features (search)

---

### Day 67: Design Netflix

**Requirements:**
- Video streaming
- Recommendations
- User profiles
- Resume watching
- 200M users, 100M DAU
- 1M hours watched per day

**Key Components:**
1. **Video Encoding:**
   - Transcode to multiple bitrates
   - Store in object storage (S3)
   - Generate thumbnails

2. **Content Delivery:**
   - CDN with edge servers worldwide
   - Adaptive bitrate streaming
   - Pre-fetch next episode

3. **Recommendations:**
   - Collaborative filtering
   - Watch history analysis
   - A/B testing for algorithms

4. **User State:**
   - Resume position
   - Watch history
   - Preferences

**Capacity Estimation:**
```
Storage:
- 10,000 movies/shows
- Average: 2 hours × 5 GB/hour = 10 GB per title
- Multiple bitrates: 10 GB × 5 = 50 GB per title
- Total: 10,000 × 50 GB = 500 TB

Bandwidth:
- 1M hours/day = 41,667 hours/hour = 11.6 hours/sec
- Average bitrate: 5 Mbps
- Bandwidth: 11.6 × 5 Mbps = 58 Mbps
```

**Deep Dive Topics:**
- Video encoding (formats, bitrates)
- CDN strategy (pre-populate edge servers)
- Recommendation algorithm (ML model)
- A/B testing infrastructure

**Trade-offs:**
- Encoding cost vs quality
- CDN cost vs user experience
- Personalization accuracy vs latency

---

### Day 68: Design Google Drive

**Requirements:**
- Upload/download files
- Sync across devices
- Share files/folders
- Version history
- 1B users, 10M active
- 100 PB total storage

**Key Components:**
1. **File Upload:**
   - Chunking (split large files)
   - Upload chunks in parallel
   - Resume on failure

2. **File Storage:**
   - Object storage (S3)
   - Metadata in database
   - Deduplication (hash-based)

3. **Sync:**
   - WebSocket for real-time updates
   - Long polling as fallback
   - Conflict resolution (last-write-wins or manual merge)

4. **Sharing:**
   - Permission model (owner, editor, viewer)
   - Signed URLs for public sharing

**Capacity Estimation:**
```
Storage:
- 100 PB total
- Average user: 100 GB
- 1B users × 100 GB = 100,000 PB (need deduplication!)

Bandwidth:
- Upload: 10M files/day × 1 MB = 10 TB/day
- Download: 100M files/day × 1 MB = 100 TB/day
```

**Deep Dive Topics:**
- File chunking (variable-size blocks for deduplication)
- Sync algorithm (detect changes, propagate)
- Conflict resolution
- Deduplication (reduce storage 10×)

**Trade-offs:**
- Chunking size (small = better dedup, large = less overhead)
- Real-time sync vs battery/bandwidth
- Version history storage (keep all versions? limited time?)

---

### Day 69: Design Yelp (Location-Based Service)

**Requirements:**
- Search nearby restaurants
- Add/view reviews and ratings
- Business listings
- 100M businesses, 500M users
- 50M daily searches

**Key Components:**
1. **Geospatial Index:**
   - QuadTree or Geohash
   - Index businesses by location
   - Find within radius quickly

2. **Search:**
   - Elasticsearch for text search
   - Filter by rating, price, category
   - Combine geo + text search

3. **Reviews:**
   - Store in database
   - Calculate aggregate rating
   - Sort by helpfulness

4. **Cache:**
   - Cache popular searches
   - Cache business details
   - Cache aggregated ratings

**Capacity Estimation:**
```
QPS:
- 50M searches/day / 86,400 = 579 searches/sec
- Peak: 1,737 searches/sec

Storage:
- 100M businesses × 1 KB = 100 GB
- Reviews: 500M reviews × 500 bytes = 250 GB
```

**Deep Dive Topics:**
- QuadTree vs Geohash (geospatial indexing)
- Search ranking (distance + rating + popularity)
- Aggregating ratings (real-time vs batch)
- Caching strategy

**Trade-offs:**
- QuadTree (flexible boundaries) vs Geohash (fixed grid)
- Real-time rating updates vs eventual consistency
- Search accuracy vs latency

---

### Day 70: Design Ticketmaster (Event Ticketing)

**Requirements:**
- Browse events
- Book tickets
- Prevent overbooking
- Handle high traffic (Taylor Swift tickets!)
- Fair allocation (no bots)
- 100M users, 10K events/day, 1M bookings/day

**Key Components:**
1. **Ticket Inventory:**
   - Track available seats
   - Lock seats during booking
   - Release after timeout (5 minutes)

2. **Booking Flow:**
   - Select event → Reserve seat → Payment → Confirm
   - Use distributed lock (Redis)
   - Saga pattern for atomicity

3. **Queue System:**
   - Virtual waiting room for high-demand events
   - FIFO queue
   - Rate limiting per user

4. **Bot Prevention:**
   - CAPTCHA
   - Rate limiting per IP
   - Behavior analysis (ML)

**Capacity Estimation:**
```
Peak Traffic (Taylor Swift concert):
- 1M users trying to buy 50K tickets
- 1M requests in 1 minute = 16,667 QPS
- Need queue system to handle spike

Storage:
- 10K events/day × 365 = 3.65M events/year
- 1M bookings/day × 365 = 365M bookings/year
- Small storage (metadata only)
```

**Deep Dive Topics:**
- Distributed locking (prevent double booking)
- Queue system (virtual waiting room)
- Seat reservation timeout
- Bot detection

**Trade-offs:**
- Strong consistency (no overbooking) vs availability
- Fair queue vs highest price (auction model)
- User experience (fast) vs fairness (prevent bots)

---

## Week 11: Mock Interviews & Review (Days 71-77)

### 🎯 Goal: Simulate Real Interview Conditions

This week is crucial. You'll do 3 mock interviews with peers or platforms, get feedback, and improve.

---

### Day 71-72: Mock Interview #1 - Design Twitter

**Setup:**
1. Find interview partner:
   - Use Pramp (free peer interviews)
   - interviewing.io (paid, with pros)
   - LeetCode discussions (find partner)
   - Friend or colleague

2. Set 45-minute timer

3. Record session (Zoom, Loom)

**Interview Process:**

**As Interviewee (45 min):**
- Follow 6-step framework
- Clarify requirements
- Calculate capacity
- Design API
- Draw high-level architecture
- Deep dive on feed generation
- Discuss trade-offs

**As Interviewer (45 min):**
- Give problem: "Design Twitter"
- Don't give all requirements upfront (make them ask)
- Guide them if stuck: "Have you considered caching?"
- Take notes on strengths/weaknesses
- Give feedback after

**After Interview:**

**Self-Review Questions:**
1. Did I clarify requirements thoroughly?
2. Did I do capacity estimation?
3. Was my high-level design clear?
4. Did I deep dive on important components?
5. Did I discuss trade-offs?
6. Did I manage time well (not too long on one part)?
7. Did I communicate clearly (think out loud)?
8. Was I receptive to hints?

**Partner Feedback:**
- What went well?
- What needs improvement?
- Did I explain clearly?
- Any confusion?

**Areas for Improvement:**
- If rushed: Practice time management
- If shallow: Go deeper on key components
- If unclear: Practice explaining out loud
- If no trade-offs: Always discuss pros/cons

**Action Items:**
- Write down top 3 things to improve
- Practice those specific areas
- Review concepts that were unclear

---

### Day 73-74: Mock Interview #2 - Design Instagram

**Goal:** Improve based on Mock #1 feedback

**Focus Areas from Mock #1:**
- If time management was issue: Use timer for each step
- If communication was issue: Practice explaining to someone
- If depth was issue: Prepare deep dives beforehand

**New Problem: Design Instagram**

**Requirements to Clarify:**
- Post photos
- Follow users
- View feed
- Like and comment
- 500M DAU
- 100M photos/day

**Follow Same Process:**
1. Requirements (5 min)
2. Capacity (5 min)
3. API (5 min)
4. High-Level Design (10 min)
5. Deep Dive (15 min) - Focus on:
   - Feed generation (fan-out strategies)
   - Photo storage (S3 + CDN)
6. Trade-offs (5 min)

**After Interview:**
- Compare to Mock #1
- Did you improve in weak areas?
- What's still challenging?
- Get feedback from partner

**Measure Progress:**
✅ Better time management?
✅ Clearer communication?
✅ Deeper technical discussion?
✅ More trade-off analysis?

---

### Day 75-76: Mock Interview #3 - Design Uber

**Goal:** Polish your interview skills

**Problem: Design Uber**

**Key Focus:**
- Smooth flow through all 6 steps
- Confident communication
- Deep technical knowledge
- Thoughtful trade-offs

**Common Mistakes to Avoid:**
❌ Jumping to solution without clarifying
❌ Getting stuck on one component too long
❌ Not discussing trade-offs
❌ Being too vague or too detailed

**What Great Candidates Do:**
✅ Ask insightful questions
✅ Think out loud
✅ Draw clear diagrams
✅ Explain reasoning for decisions
✅ Proactively identify issues
✅ Suggest improvements
✅ Discuss real-world considerations (cost, operations)

**After Interview:**
- Review recording
- Identify patterns (recurring mistakes)
- Practice weak areas
- Celebrate improvements!

---

### Day 77: Review All Mock Interviews

**Retrospective:**

**Watch All Recordings:**
- Take notes on common themes
- What consistently went well?
- What consistently needs work?

**Common Patterns:**

**If Time Management is Issue:**
- Practice with strict timer
- Allocate time: 5-5-5-10-15-5
- Don't get lost in one component

**If Communication is Issue:**
- Practice explaining to rubber duck
- Record yourself explaining concepts
- Slow down, structure your thoughts

**If Depth is Issue:**
- Go deeper on 2-3 systems
- Study implementation details
- Practice explaining algorithms

**If Trade-offs Missing:**
- For every decision, think: "What's the downside?"
- Practice: "We're choosing X over Y because..."
- Always have pros/cons

**Create Improvement Plan:**
1. Top 3 weaknesses identified
2. Specific action for each
3. Practice daily for remaining weeks

**Celebrate Wins:**
- Acknowledge what improved
- Confidence matters in interviews!

---

## Week 12: Company-Specific Preparation & Final Polish (Days 78-84)

### 🎯 Goal: Tailor Prep to Target Companies

---

### Day 78-79: FAANG Deep Dive

#### **Meta (Facebook):**

**Common Questions:**
- Design Facebook News Feed
- Design Instagram Stories
- Design Facebook Messenger
- Design Facebook Ads system

**What Meta Values:**
- Scale (billions of users)
- Real-time systems (messaging, live updates)
- Social graph (friend relationships)
- Personalization (ML models)
- Mobile-first design

**Study Focus:**
- News feed ranking algorithms
- Fan-out strategies (write vs read)
- Graph databases (friend relationships)
- Real-time messaging (WebSocket)
- ML for recommendations

**Interview Tips:**
- Emphasize scale (billions)
- Discuss A/B testing
- Mobile bandwidth considerations
- Tradeoff: Engagement vs privacy

---

#### **Amazon:**

**Common Questions:**
- Design Amazon product search
- Design order management system
- Design inventory management
- Design Amazon Prime Video
- Design recommendation engine

**What Amazon Values:**
- Customer obsession (user experience first)
- Operational excellence (metrics, monitoring)
- Frugality (cost-effective solutions)
- Ownership (production-ready designs)
- Bias for action (practical over theoretical)

**Study Focus:**
- E-commerce fundamentals (cart, checkout, inventory)
- Search and ranking (Elasticsearch)
- Distributed transactions (Saga pattern)
- Microservices (Amazon pioneered this)
- Operational metrics (CloudWatch, alarms)

**Interview Tips:**
- Mention cost optimization
- Discuss monitoring and alerting
- Think about failure scenarios
- Consider operational burden

---

#### **Apple:**

**Common Questions:**
- Design iCloud
- Design Apple Music
- Design App Store
- Design iMessage
- Design Apple Pay

**What Apple Values:**
- Privacy (end-to-end encryption)
- User experience (seamless, intuitive)
- Performance (smooth, fast)
- Ecosystem integration (iPhone, iPad, Mac sync)
- Security (no compromise)

**Study Focus:**
- End-to-end encryption
- Cross-device sync (iCloud)
- Offline-first design
- Privacy-preserving systems
- Secure payment processing

**Interview Tips:**
- Always mention privacy
- Discuss encryption
- Consider battery life (mobile)
- Seamless user experience

---

#### **Netflix:**

**Common Questions:**
- Design video streaming platform
- Design recommendation system
- Design content encoding pipeline
- Design A/B testing platform

**What Netflix Values:**
- Streaming quality (no buffering)
- Personalization (ML recommendations)
- A/B testing culture (data-driven)
- Microservices (freedom & responsibility)
- Chaos engineering (resilience)

**Study Focus:**
- Video encoding and transcoding
- CDN and edge caching
- Adaptive bitrate streaming
- Recommendation algorithms (collaborative filtering)
- A/B testing infrastructure

**Interview Tips:**
- Discuss encoding formats
- CDN strategy (Open Connect)
- Recommendation accuracy
- Handle failures gracefully

---

#### **Google:**

**Common Questions:**
- Design Google Search
- Design Google Maps
- Design Gmail
- Design YouTube
- Design Google Drive

**What Google Values:**
- Scale (billions of users, petabytes of data)
- Performance (speed matters)
- Innovation (cutting-edge solutions)
- Data-driven decisions
- Distributed systems expertise

**Study Focus:**
- Search indexing (inverted index)
- MapReduce and BigTable
- Geospatial systems (Google Maps)
- Distributed storage (GFS, Colossus)
- Machine learning at scale

**Interview Tips:**
- Emphasize massive scale
- Discuss distributed systems
- Performance optimization
- Data structures and algorithms

---

### Day 80-81: Unicorns & Startups

#### **Uber:**

**Focus:** Real-time location, matching algorithms, surge pricing

**Key Systems:**
- Geospatial indexing (QuadTree, Geohash)
- Real-time tracking (WebSocket, GPS)
- Matching algorithm (supply/demand)
- Surge pricing (dynamic pricing)
- ETA calculation

**Interview Tips:**
- Discuss real-time constraints
- GPS accuracy vs battery
- Fairness in matching
- Handling peak demand

---

#### **Airbnb:**

**Focus:** Search, booking, reviews, payments

**Key Systems:**
- Geospatial search
- Availability calendar
- Booking workflow (prevent double booking)
- Review and rating system
- Payment processing

**Interview Tips:**
- Search ranking (price, location, rating)
- Prevent overbooking (distributed locks)
- Trust and safety (reviews, verification)

---

#### **Stripe:**

**Focus:** Payment processing, API design, reliability

**Key Systems:**
- Payment gateway integration
- Idempotency (critical!)
- Retry logic and failure handling
- Webhook delivery
- Fraud detection

**Interview Tips:**
- Financial transactions (no errors!)
- Idempotency keys
- Retry with exponential backoff
- Audit logging

---

#### **Spotify:**

**Focus:** Music streaming, recommendations, social features

**Key Systems:**
- Audio streaming (different from video)
- Playlist management
- Recommendation engine
- Social features (follow, share)
- Offline mode

**Interview Tips:**
- Audio codec efficiency
- Pre-caching for offline
- Collaborative playlists
- Real-time sync across devices

---

### Day 82-83: Final Mock Interviews (Company-Specific)

**Day 82: Mock Interview with Target Company Problem**

**If interviewing with Meta:**
- Problem: Design Instagram Stories
- Focus: Real-time, mobile-first, high engagement

**If interviewing with Amazon:**
- Problem: Design order management system
- Focus: Reliability, cost-effectiveness, operational excellence

**If interviewing with Google:**
- Problem: Design Google Maps
- Focus: Scale, performance, geospatial algorithms

**Simulate Real Interview:**
- 45-minute timer
- Same company interviewer style (research on Glassdoor)
- Record session
- Get feedback

---

### Day 84: Final Review & Confidence Building

**Morning: Comprehensive Review**

**Review All Key Concepts:**
- ✅ Load balancing algorithms
- ✅ Database sharding strategies
- ✅ Caching strategies (write-through, write-back, cache-aside)
- ✅ Consistency models (strong, eventual, causal)
- ✅ Replication strategies (leader-follower, multi-leader, leaderless)
- ✅ Partitioning strategies (hash, range, consistent hashing)
- ✅ Message queues (Kafka, RabbitMQ)
- ✅ CDN strategies
- ✅ Rate limiting algorithms
- ✅ Consensus algorithms (Raft, Paxos - high level)

**Review Key Formulas:**
```
QPS = (DAU × Actions/User) / 86,400
Storage = Items × Size × Retention
Bandwidth = QPS × Avg_Size × 8 / 1M (Mbps)
Servers = Peak_QPS / QPS_Per_Server
Cache = Total_Data × 0.2 (80-20 rule)
```

**Review Common Trade-offs:**
- Consistency vs Availability (CAP)
- Latency vs Consistency
- SQL vs NoSQL
- Vertical vs Horizontal scaling
- Strong consistency vs Eventual consistency
- Pull vs Push (CDN, news feed)
- Fan-out on write vs Fan-out on read

**Afternoon: Confidence Boosting**

**What You've Accomplished:**
- ✅ 12 weeks of intense study
- ✅ Mastered 50+ system design topics
- ✅ Practiced 30+ full system designs
- ✅ Completed multiple mock interviews
- ✅ Learned from feedback and improved

**You're Ready Because:**
- You understand the framework (6 steps)
- You can calculate capacity quickly
- You know common architectures
- You can discuss trade-offs intelligently
- You've practiced communicating clearly

**Mental Preparation:**
- System design is about process, not perfect solution
- No one right answer
- Communication is as important as technical knowledge
- It's OK to not know everything - show how you'd figure it out
- Interviewers want to work with you - be collaborative

**Evening: Relaxation**
- Light review only (don't cram)
- Get good sleep
- Exercise or meditate
- Build confidence: "I've prepared well, I'm ready"

---

## Days 85-90: Final Week - Practice & Polish

### Day 85: Design Dropbox

**Practice the full framework:**
- File upload/download
- Sync across devices
- Conflict resolution
- Version history
- Sharing

**Focus:** File chunking, deduplication, sync algorithm

**Time yourself: 45 minutes**

**Self-evaluate:**
- Did you follow framework?
- Clear communication?
- Technical depth?
- Trade-off discussion?

---

### Day 86: Design Zoom

**Practice the full framework:**
- Video conferencing
- Screen sharing
- Recording
- Chat
- Scalability for 10,000 participants

**Focus:** WebRTC, media servers, bandwidth optimization

**Time yourself: 45 minutes**

---

### Day 87: Design Tinder

**Practice the full framework:**
- Profile browsing
- Swiping mechanism
- Matching algorithm
- Chat

**Focus:** Geospatial search, matching algorithm, real-time chat

**Time yourself: 45 minutes**

---

### Day 88: Design API Rate Limiter

**Practice the full framework:**
- Distributed rate limiting
- Multiple algorithms
- Per-user, per-IP, per-API
- Sliding window

**Focus:** Algorithms (token bucket, leaky bucket), distributed coordination (Redis)

**Time yourself: 45 minutes**

---

### Day 89: Final Mock Interview

**Full Simulation:**
- Random problem (have friend pick)
- 45-minute timer
- Record session
- Get feedback

**Treat as Real Interview:**
- Professional setup
- Dress professionally
- Take it seriously

**After Interview:**
- Quick review only
- Don't stress over mistakes
- Focus on what went well

---

### Day 90: Rest & Final Prep

**Morning: Light Review**
- Skim through your notes
- Review key formulas (QPS, storage)
- Review common trade-offs
- Don't learn anything new!

**Afternoon: Logistics**
- Check internet connection
- Test video/audio
- Prepare whiteboard or paper
- Have water nearby

**Evening: Mental Preparation**

**Affirmations:**
- "I've prepared thoroughly"
- "I understand the concepts"
- "I can communicate clearly"
- "I'll do my best"

**Visualization:**
- Imagine successful interview
- See yourself drawing clear diagrams
- See yourself explaining confidently
- Feel the satisfaction of doing well

**Get Good Sleep:**
- No late-night cramming
- Relax, trust your preparation
- Sleep at least 7-8 hours

---

## Interview Day Checklist

### Before Interview:

**30 Minutes Before:**
- ✅ Use bathroom
- ✅ Have water nearby
- ✅ Test video/audio
- ✅ Close unnecessary apps
- ✅ Have paper/whiteboard ready
- ✅ Review key formulas (QPS, storage)
- ✅ Deep breath, relax

**5 Minutes Before:**
- ✅ Join meeting early
- ✅ Smile, be friendly
- ✅ Positive mindset

### During Interview:

**Remember:**
- ✅ Follow 6-step framework
- ✅ Think out loud
- ✅ Ask clarifying questions
- ✅ Draw clear diagrams
- ✅ Discuss trade-offs
- ✅ Manage time (don't spend too long on one part)
- ✅ Be collaborative (not defensive)
- ✅ Stay calm, it's OK to pause and think

**If Stuck:**
- "Let me think through this..."
- "Can you clarify...?"
- "I'm considering two approaches..."
- It's OK to ask for hints!

### After Interview:

**Immediate:**
- Thank interviewer
- Ask about next steps
- Stay professional

**Later:**
- Write down what you remember
- What went well?
- What could improve?
- Don't overthink mistakes

**Regardless of Outcome:**
- Every interview is practice
- You learn and improve
- Be proud of your preparation
- Keep applying and interviewing

---

## Final Words of Encouragement

**You've Done the Work:**
- 90 days of dedicated study
- Dozens of practice problems
- Multiple mock interviews
- Continuous improvement

**You're Not Expected to Know Everything:**
- No one designs perfect systems in 45 minutes
- Interviewers understand constraints
- Process matters more than perfection

**You've Got This:**
- Trust your preparation
- Trust your knowledge
- Trust yourself

**Remember:**
- System design is about making thoughtful decisions
- It's about trade-offs, not right/wrong
- Communication and reasoning matter as much as technical knowledge
- You're interviewing them too - it's a conversation

---

## 🎉 Congratulations!

You've completed the 90-day journey. You've mastered:
- ✅ Foundational concepts
- ✅ Core system components
- ✅ Distributed systems
- ✅ Modern architecture
- ✅ Classic problems
- ✅ Advanced applications
- ✅ Specialized systems
- ✅ Interview framework
- ✅ Communication skills

**You're ready to ace system design interviews!**

**Go out there and get that offer! 💪🚀**

---

## Quick Reference: The 6-Step Framework

**Step 1: Requirements (5 min)**
- Functional: What features?
- Non-functional: Scale, latency, availability?
- Out of scope: What to exclude?

**Step 2: Capacity (5 min)**
- QPS (read/write)
- Storage (5 years)
- Bandwidth (peak)
- Servers needed

**Step 3: API (5 min)**
- Core endpoints
- Request/response format
- REST conventions

**Step 4: High-Level Design (10 min)**
- Draw architecture
- Show data flow
- Label components

**Step 5: Deep Dive (15 min)**
- Pick 2-3 components
- Explain algorithms
- Discuss trade-offs
- Show how it scales

**Step 6: Bottlenecks (5 min)**
- Identify issues
- Suggest solutions
- Discuss trade-offs

**Remember: Communicate clearly, think out loud, be collaborative!**

---

**Best of luck with your interviews! 🍀**
