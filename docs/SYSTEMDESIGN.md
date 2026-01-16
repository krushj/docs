# System Design Concepts

## Table of Contents

### Core Concepts
- [Performance vs Scalability](#performance-vs-scalability)
- [Latency vs Throughput](#latency-vs-throughput)
- [Availability vs Consistency](#availability-vs-consistency)
- [CAP Theorem](#cap-theorem)
- [Consistency Patterns](#consistency-patterns)
- [Availability Patterns](#availability-patterns)

### Networking & Infrastructure
- [Domain Name System (DNS)](#domain-name-system-dns)
- [DNS Caching](#dns-caching)
- [Content Delivery Network (CDN)](#content-delivery-network-cdn)
- [Load Balancer](#load-balancer)
- [Load Balancer Advanced Concepts](#load-balancer-advanced-concepts)
- [Reverse Proxy](#reverse-proxy)

### API & Security
- [API Gateway](#api-gateway)
- [API Gateway Authentication](#api-gateway-authentication)
- [Microservices Trust & Service Mesh](#microservices-trust--service-mesh)
- [Mutual TLS (mTLS)](#mutual-tls-mtls)

### Architecture & Services
- [Application Layer & Microservices](#application-layer--microservices)
- [Database](#database)

### Data Management
- [SQL vs NoSQL](#sql-vs-nosql)
- [Sharding Strategies](#sharding-strategies)
- [Caching](#caching)

### Communication & Patterns
- [Asynchronism & Message Queues](#asynchronism--message-queues)
- [Communication Protocols](#communication-protocols)

### Practical Applications
- [System Design Examples](#system-design-examples)
- [System Design Interview Tips](#system-design-interview-tips)
- [RAID Levels](#raid-levels)
- [Additional Important Concepts](#additional-important-concepts)

---

## Performance vs Scalability

### 🏎️ Performance = How fast it runs
Performance is about **speed**.

It answers the question:
> "How quickly can the system do a task right now?"

**Examples:**
- A website loads in 0.5 seconds → good performance
- A database returns a query in 10 ms → good performance

**Key idea:**
> Performance measures how fast a system works with a given amount of work.

### 📈 Scalability = How well it handles more work
Scalability is about **growth**.

It answers the question:
> "What happens when the workload increases? Can the system keep up?"

**Examples:**
- A website works fine for 100 users, but crashes at 10,000 → poor scalability
- You add more servers, and the system handles more load → good scalability

**Key idea:**
> Scalability measures how well a system can grow without breaking or slowing down too much.

### 🍔 Simple Analogy
Imagine a small restaurant:

**Performance:**
- How fast they make one burger
- If they make a burger in 2 minutes → high performance

**Scalability:**
- What happens when 100 customers arrive at once?
- Can they:
  - Hire more cooks?
  - Add more grills?
  - Keep making burgers fast?
- If yes → scalable
- If no → not scalable

### 🎯 Summary

| Concept | Meaning | Question |
|---------|---------|----------|
| **Performance** | Speed now | "How fast is it?" |
| **Scalability** | Ability to grow | "Can it stay fast as load increases?" |

You can have:
- **Great performance but terrible scalability** (Fast for 10 users, crashes at 1000)
- **Great scalability but mediocre performance** (Can handle growth, but each task is slow)

---

## Latency vs Throughput

### ⏱️ Latency = How long one thing takes
Latency is the **delay**.

> "How much time does one request take from start to finish?"

**Examples:**
- A message takes 50 ms to reach a server
- A web page takes 200 ms to load
- A database query takes 5 ms to return

**Think:** Latency = time per request

### 🚚 Throughput = How many things per second
Throughput is the **amount of work done per unit of time**.

> "How many requests can we handle per second/minute?"

**Examples:**
- A server processes 5,000 requests per second
- A network transfers 1 GB per second
- A database handles 200 queries per second

**Think:** Throughput = requests per second

### 🍦 Simple Analogy
Imagine an ice-cream shop:

**Latency:**
- How long it takes to serve one customer
- If it takes 10 seconds → latency = 10 seconds

**Throughput:**
- How many customers per minute the shop can serve
- If they can serve 20 customers/min → throughput = 20 customers/min

### 🎯 Summary

| Concept | Meaning | Question |
|---------|---------|----------|
| **Latency** | Time to complete one operation | "How long does one request take?" |
| **Throughput** | Number of operations per time unit | "How many requests can we handle?" |

### 🧠 Key Relationship
- **Low latency** → fast individual responses
- **High throughput** → can handle lots of requests at once

They're related but not the same.

You can have:
- **Low latency but low throughput** (fast but handles few requests)
- **High throughput but high latency** (handles many requests but each is slow)

---

## Availability vs Consistency

### 🟢 Availability = The system is always up and responding
**Availability means:**
> "Can the system respond, even if something goes wrong?"

A system is available if:
- It always gives a response
- Even when some servers or networks fail

**But:**
- To stay available, it might return older or not perfectly up-to-date data

**Example:**
You request your profile. Even if one server is down, another one gives you some answer.

### 🟡 Consistency = Everyone sees the same data at the same time
**Consistency means:**
> "No matter which server you read from, the data is correct and up-to-date."

A system is consistent if:
- All users see the same value
- No outdated or conflicting data

**But:**
- To stay consistent, it may need to wait for all servers to sync → which can make the system temporarily unavailable

**Example:**
You update your profile, and the system waits for all servers to save it before letting anyone read it.

### 🍕 Simple Analogy
Imagine three friends sharing the same pizza tracker app.

**Consistency:**
- They all must see the same status
- If one sees "Out for delivery," everyone sees it
- The app may pause for a moment to sync before showing anything

**Availability:**
- Everyone can always access the tracker, even if syncing is delayed
- Maybe one friend sees "Being prepared" and another sees "Baking"
- Not perfect, but the app never fails to respond

### 🎯 Summary

| Concept | Meaning | Trade-off |
|---------|---------|-----------|
| **Availability** | System always responds | May serve outdated data |
| **Consistency** | System always returns the latest correct data | May pause or reject requests |

### 🏗️ Why do they conflict?
In distributed systems, when there's a network failure, the system must choose:

**👉 Stay consistent:**
- Stop answering until all servers agree → lower availability

**👉 Stay available:**
- Answer with the data it has, even if some servers disagree → lower consistency

This is the idea behind the **CAP theorem**.

---

## CAP Theorem

### 🧩 CAP Theorem (in simple terms)
A distributed system **CANNOT** have all 3 of these at the same time when a network problem (partition) occurs:

- **C – Consistency:** Everyone sees the same, most up-to-date data
- **A – Availability:** The system always responds (no errors)
- **P – Partition Tolerance:** The system keeps working even if network connections between nodes fail

> In a real distributed system, **P is required** (because network failures happen).
> So the real choice is between **C and A** during a partition.

### ⚖️ When a network partition happens, the system must choose:

#### CP → Consistency + Partition Tolerance
The system prefers **correct data** over being responsive.

**What happens?**
- If nodes cannot talk to each other, the system refuses some requests to avoid returning stale or conflicting data
- It may return an error or timeout instead of giving bad data

**In plain words:**
> CP systems keep data correct, even if they must stop responding.

**Examples:**
- HBase
- MongoDB (in certain configurations)
- Zookeeper
- Etcd

#### AP → Availability + Partition Tolerance
The system prefers being **responsive** over perfect correctness.

**What happens?**
- If nodes cannot communicate, each node still accepts reads/writes
- Responses are always given, but data may be temporarily inconsistent
- The system reconciles the differences later (eventual consistency)

**In plain words:**
> AP systems stay up, even if they return slightly outdated data.

**Examples:**
- Cassandra
- DynamoDB
- CouchDB
- Riak

### 🔑 Summary Table

| Mode | Guarantees | Sacrifices | Behavior during partition |
|------|------------|------------|---------------------------|
| **CP** | Consistency + Partition Tolerance | Availability | Returns errors/timeouts to avoid incorrect data |
| **AP** | Availability + Partition Tolerance | Consistency | Always responds, but data may be stale or conflicting |

### 🧠 The key idea to remember
- CAP is only about behavior during a **network partition**
- When the network is healthy, you can have both high availability and consistency
- But when things break, you must choose:
  - **CP:** "Don't answer unless the data is correct."
  - **AP:** "Always answer, even if the data isn't perfect."

---

## Consistency Patterns

### 🔵 1. Weak Consistency

**Definition:**
The system does not guarantee that you will read the latest data immediately after a write.
- You might get old (stale) data
- The system makes no promise about when the update will become visible

**Simple example:**
You post a photo → your friend may not see it right away.

**Where it's used:**
- Caches (e.g., CDN edge caches)
- Some distributed file systems
- High-performance systems that prefer speed over accuracy

**Goal:**
> Maximum performance and availability, accuracy is not guaranteed.

### 🟡 2. Eventual Consistency

**Definition:**
The system may return stale data now, but if no new updates happen, all copies will eventually become consistent.

> "You might not see the newest update right away, but eventually everyone will see the same data."

**Simple example:**
You send a message in a chat app → Your friend may see it 1–2 seconds later, but eventually they will.

**Where it's used:**
- DynamoDB
- Cassandra
- DNS
- S3
- Many AP systems

**Goal:**
> High availability while still ensuring data catches up over time.

### 🟢 3. Strong Consistency

**Definition:**
After you write data, every read returns the latest value immediately, no matter which server you read from.

> "Once the update succeeds, everyone sees it right away."

**Simple example:**
You transfer money in your bank account → As soon as the transfer is complete, the new balance is visible everywhere.

**Where it's used:**
- Traditional SQL databases
- Spanner
- Etcd
- Zookeeper
- CP systems

**Goal:**
> Accuracy first, even if speed or availability must be sacrificed.

### 🧠 Summary Table

| Consistency type | What you get | What you sacrifice | Easy analogy |
|------------------|--------------|-------------------|--------------|
| **Weak** | Fast responses, no guarantees | Freshness of data | A friend who might reply with old info |
| **Eventual** | Data becomes correct over time | Immediate accuracy | A friend who replies accurately but with delay |
| **Strong** | Always up-to-date data | Availability & sometimes speed | A friend who refuses to answer until they are 100% sure |

### 🎯 Quick Takeaway
- **Weak consistency** → No guarantee
- **Eventual consistency** → Will become correct, but not now
- **Strong consistency** → Always correct immediately

---

## Availability Patterns

### 🟢 1. Fail-over
Fail-over means automatically switching to a backup system when the primary one fails.

**How it works:**
- A primary server handles all traffic
- A backup server sits idle or partially active
- If the primary fails → traffic is switched to the backup

**Two types of fail-over:**

**➡️ Active–Passive**
- Only the primary is active
- Backup turns on only when needed
- Slight downtime during switch

**➡️ Active–Active**
- Multiple nodes are all active at the same time
- If one fails, others already share the load
- Faster and more reliable, but more expensive

**Benefit:**
- ✔️ Simple and effective
- ✔️ Keeps systems available during failures

**Trade-off:**
- ❌ Fail-over detection and switching may cause small downtime
- ❌ More infrastructure cost

### 🟡 2. Replication
Replication means having multiple copies of data or services so that if one fails, others can continue serving requests.

**Types of replication:**

**➡️ Synchronous replication**
- All replicas update at the same time
- Ensures strong consistency
- Slower writes, but safer

**➡️ Asynchronous replication**
- Primary writes first → replicas update later
- Ensures high availability
- May return slightly outdated data

**Where replication is used:**
- Database clusters
- Distributed file systems
- Microservice deployments
- Cloud storage (AWS S3, GCP storage)

**Benefit:**
- ✔️ Prevents single points of failure
- ✔️ Supports scaling and geographic distribution

**Trade-off:**
- ❌ More replicas = more network coordination
- ❌ May reduce consistency (depending on mode)

### 🔵 3. Availability in Numbers (Nines of Availability)
Availability is often measured in percentages, known as "nines".

| Availability | Downtime per year | Description |
|--------------|-------------------|-------------|
| 99% | ~3.65 days | High availability? Not really |
| 99.9% (3 nines) | ~8.76 hours | Good for many apps |
| 99.99% (4 nines) | ~52 minutes | Used by critical services |
| 99.999% (5 nines) | ~5 minutes | Telecom-grade; extremely hard to achieve |

**Why this matters:**

The more "nines" you want:
- The more redundancy you need
- The more automation you need
- The more expensive your system becomes

**Example:**
A service with 99.99% availability can only be down for <1 hour per year, so fail-over and replication must be fast and automatic.

### 🎯 Summary

| Pattern | Purpose | How it improves availability |
|---------|---------|------------------------------|
| **Fail-over** | Switch to backup when primary fails | Removes single-point-of-failure for compute |
| **Replication** | Keep multiple copies of services/data | Reduces failure risk & allows load sharing |
| **Availability numbers** | Measure uptime performance | Defines how reliable your system must be |

---

## Domain Name System (DNS)

### 🌐 What is DNS?
DNS is the **phonebook of the internet**.

It translates human-friendly names like:
```
www.google.com
```

into machine-friendly IP addresses like:
```
142.250.190.206
```

Because computers talk using IP addresses, but people don't want to memorize numbers.

### 🏗️ How DNS Works (Simple Steps)
When you type a website URL into your browser:

**1️⃣ Browser checks local cache**
- Your computer first checks:
  - Have I visited this site before?
  - Do I already know its IP?
- If yes → uses cached IP (fastest)

**2️⃣ Ask the Recursive DNS Resolver**
- If not cached, your computer asks a recursive resolver, usually provided by:
  - Your ISP
  - Google DNS (8.8.8.8)
  - Cloudflare DNS (1.1.1.1)
- This resolver finds the IP on your behalf

**3️⃣ Resolver checks the Root Servers**
- If the resolver doesn't know the IP, it asks a Root DNS server:
  - "Where can I find .com domains?"
- Root servers don't know exact IPs; they just point to Top-Level Domain (TLD) servers

**4️⃣ Ask the TLD Server**
- TLD servers store information for domain endings like:
  - .com, .org, .net, .edu
- They reply: "For google.com, ask the Authoritative DNS server."

**5️⃣ Ask the Authoritative DNS Server**
- This server owns the DNS records for the domain
- It returns the actual IP address:
  ```
  google.com → 142.250.190.206
  ```

**6️⃣ Resolver returns the IP to your browser**
- Now your browser knows where to connect
- It caches the result for a period called TTL (Time-To-Live) so next time it's faster

### 📦 Important DNS Record Types

| Type | Purpose | Example |
|------|---------|---------|
| **A** | Maps domain → IPv4 address | google.com → 142.250.x.x |
| **AAAA** | Maps domain → IPv6 address | |
| **CNAME** | Alias for another domain | www → example.com |
| **MX** | Mail server for the domain | example.com mail handled by Gmail |
| **TXT** | Verification / metadata | SPF, DKIM, etc. |
| **NS** | Points to authoritative DNS servers | |

### 🔁 DNS Caching
DNS is heavily cached at many levels:
- Browser cache
- OS cache
- Resolver cache
- CDN cache

Caching makes DNS fast, but can delay propagation when records change.

### 🧠 Why DNS Matters
- Allows easy-to-remember website names
- Enables global load balancing
- Provides resilience & fail-over
- Critical for email (via MX records)
- Helps defend against attacks (DNSSEC)

### 🛡️ DNS Weakness and Security
DNS was originally not secure.

**Common issues:**
- DNS spoofing
- Cache poisoning
- DDoS attacks (e.g., Dyn attack in 2016)

**Solutions:**
- DNSSEC (signed responses)
- Anycast DNS (global redundancy)

### 🎯 Summary
> DNS = Internet's address book.
> It converts names → IP addresses using a distributed, cached hierarchy.

---

## DNS Caching

### ⭐ What Is DNS Caching?
DNS caching means storing DNS lookup results temporarily so that future requests for the same domain can be answered faster without repeating the entire DNS lookup process.

**Example:**
1. You look up youtube.com
2. DNS finds the IP (e.g., 142.250.xxx.xxx)
3. That result gets cached at multiple places
4. Next time, DNS doesn't repeat the whole process — it uses the cached result
5. → Much faster response

### 🧩 Where DNS Caching Happens (4 Layers)
DNS caching doesn't happen in just one place — it happens everywhere to speed up browsing.

Let's go through the 4 layers, from closest to farthest.

#### 1️⃣ Browser Cache
Every browser (Chrome, Firefox, Safari) keeps a small DNS cache.
- Fastest lookup
- Stored only for a short period
- Cleared when you restart the browser (not always)

**Example:**
If you visited facebook.com a minute ago, the browser won't ask any DNS server again.

#### 2️⃣ OS Cache (Local Resolver)
Your operating system also has a DNS cache:
- Windows: `ipconfig /displaydns`
- macOS: `sudo killall -INFO mDNSResponder` (to view stats)
- Linux: systemd-resolved, nscd, etc.

The OS cache is used if the browser doesn't have the record.

**Why OS cache?**
Because different apps on your computer might request the same domain.

#### 3️⃣ Recursive Resolver Cache
This is usually the largest and most important cache.

Your recursive resolver is usually provided by:
- Your ISP
- Google DNS (8.8.8.8)
- Cloudflare DNS (1.1.1.1)
- OpenDNS (208.67.222.222)

Resolvers keep DNS results cached for millions of users and dramatically reduce DNS traffic.

**This is why:**
- DNS lookups are usually fast
- CDNs (Cloudflare, Akamai) can control latency globally via DNS TTL

#### 4️⃣ Authoritative DNS Server Cache
Authoritative servers usually don't cache other people's records.

But they may:
- Cache negative responses (e.g., "domain does not exist" using NXDOMAIN caching)
- Use internal caching for performance optimization

### ⏱️ TTL — The Key to DNS Caching
TTL (Time To Live) is the number (in seconds) that tells caches how long a DNS record should be stored.

**Example:**
```
A record TTL = 3600
```

**Means:**
- → Cache this DNS response for 1 hour
- → Don't ask the authoritative DNS server again during this time

**Common TTL values:**

| TTL | Meaning |
|-----|---------|
| 30 seconds | Very dynamic systems (load balancing) |
| 300 seconds (5 min) | CDNs, frequently updated domains |
| 3600 seconds (1 hour) | Typical websites |
| 86400 seconds (1 day) | Stable domains |

### 🔄 DNS Cache Invalidation & Problems

**1. Stale records**
- If a DNS record changes, but caches still hold the old value until TTL expires → users may reach the wrong server

**2. Propagation delay**
- DNS doesn't truly "propagate"
- It just waits for old TTL values to expire across all caches
- This is why DNS changes may take minutes or hours

**3. Negative caching**
- If a domain lookup fails (NXDOMAIN), resolvers cache that too
- Example: `Negative TTL = 300 seconds`
- Means the resolver won't retry for 5 minutes

### 🛡️ DNS Cache Security Issues
DNS caching can be exploited:

**1. DNS Cache Poisoning**
- Attacker tricks a resolver into caching a fake IP
- Example: `google.com → attacker's IP`

**Mitigations:**
- DNSSEC
- Randomized source ports
- Short TTLs

**2. Spoofing**
- Injecting false records into a poorly secured cache

### 📦 How DNS Caching Improves Performance

**Caching reduces:**
- Network latency
- Load on DNS servers
- Load on authoritative servers

**Caching increases:**
- Website speed
- Reliability
- Efficiency

### 🔥 Quick Summary

| Layer | Purpose | Speed |
|-------|---------|-------|
| **Browser cache** | Fastest access | ⚡ Fast |
| **OS cache** | Shared by apps | ⚡ Fast |
| **Recursive resolver cache** | Large-scale caching | ⚡⚡ Very fast |
| **Authoritative server** | No caching of others' data | – |

- TTL controls how long cached data stays valid
- Caching makes DNS fast, but causes propagation delays when records change

---

## Content Delivery Network (CDN)

### 🌍 What Is a CDN (Content Delivery Network)?
A CDN is a network of servers distributed around the world that deliver content (images, videos, HTML, CSS, JS) from locations close to the user.

Instead of your users loading content from your origin server (e.g., in the US), they load it from a CDN server near them (e.g., India, UK, Japan).

> **Result:** Faster loading, reduced bandwidth, higher availability.

### 🧠 Why CDNs Exist

**Without a CDN:**
- User in Asia → must fetch content from server in the US → slow

**With CDN:**
- User in Asia → fetches from a CDN server in Asia → fast

**CDNs reduce:**
- Latency
- Load on your servers
- Bandwidth costs

### 🔵 Push CDN
You upload or push your content manually to CDN servers.

**How Push CDNs work:**
1. You upload files (e.g., images, videos) to the CDN
2. CDN stores them permanently at all edge locations
3. Users request the content directly from CDN

**Best for:**
- Static content that rarely changes
- (e.g., game assets, videos, app binaries)

**Pros:**
- ✔️ CDN always has the latest files
- ✔️ No delay on first request
- ✔️ Good for large static files

**Cons:**
- ❌ You must manage uploads
- ❌ More work when updating files

**Example use case:**
- A static website with fixed assets
- Software downloads
- Video libraries

### 🟡 Pull CDN (Most common)
You do nothing — the CDN automatically fetches content from your origin server when needed.

**How Pull CDNs work:**
1. A user requests a file from CDN (e.g., `/image.png`)
2. CDN checks if it has the file in cache:
   - If yes: serve immediately
   - If no: fetch from your origin → store (cache) → serve
3. Future users get it from cache until TTL expires

**Best for:**
- Websites with changing content
- Blogs, web apps, SaaS
- Any app where assets are updated regularly

**Pros:**
- ✔️ Minimal setup
- ✔️ Automatically handles updates
- ✔️ No need to push files manually

**Cons:**
- ❌ First user to request the file gets a cache miss (slower)
- ❌ If origin server is slow, first response is slow

**Example use case:**
- E-commerce websites
- Media-heavy web apps
- Dynamic websites with static assets

### 🧭 Push vs Pull CDN (Quick Comparison)

| Feature | Push CDN | Pull CDN |
|---------|----------|----------|
| **How content gets on CDN** | You upload it | CDN fetches it on demand |
| **Best for** | Large static files, rarely changing | General websites, changing content |
| **First request** | Always fast | Slow if cache miss |
| **Maintenance** | Manual uploads | Automatic |
| **Storage costs** | Higher (content stored long-term) | Lower (cached until TTL expires) |

### 🎯 Simple Analogy
- **Pull CDN** = On-demand delivery
  - The CDN only stores the pizza after someone orders it
- **Push CDN** = Pre-stocking inventory
  - You fill all pizza shops with pizza before customers arrive

---

## Load Balancer

### ⚖️ What Is a Load Balancer?
A load balancer distributes incoming traffic across multiple servers so no single server gets overloaded.

Think of it like a traffic officer directing cars to different open lanes.

**Benefits:**
- Better performance
- Less downtime
- Ability to scale horizontally
- Handles failures automatically

### 🟢 1. Active–Passive Load Balancing

**In an active-passive setup:**
- Active server(s) handle all incoming traffic
- Passive server is on standby (not serving requests)
- If the active server fails → passive server takes over

**Pros:**
- ✔️ Simple
- ✔️ Good for small systems
- ✔️ Standby node increases reliability

**Cons:**
- ❌ Passive server sits idle
- ❌ Failover may take a few seconds

**Analogy:**
One cashier working, another sitting in the back waiting. If the first gets sick, the backup takes over.

### 🟡 2. Active–Active Load Balancing

**In an active-active setup:**
- All servers are active and share traffic
- If one fails, others keep handling traffic without delay
- Provides better throughput and higher availability

**Pros:**
- ✔️ Maximizes resource use
- ✔️ Failover is instant
- ✔️ Can handle more traffic (scalable)

**Cons:**
- ❌ More complex
- ❌ Requires good session management (sticky sessions, distributed cache)

**Analogy:**
All cashiers are open and taking customers at the same time.

### 🌐 3. Layer 4 Load Balancing (Transport Layer)

**L4 Load Balancing uses:**
- TCP
- UDP
- Ports and IP addresses

It forwards packets without looking inside (no understanding of HTTP/URL).

**Features:**
- ✔️ Very fast
- ✔️ Low overhead
- ✔️ Works for any protocol (not just web)

**Examples:**
- AWS NLB (Network Load Balancer)
- HAProxy in L4 mode
- LVS (Linux Virtual Server)

**When to use:**
- High-performance, low-latency traffic
- Database or game servers
- Streaming traffic

### 🕸️ 4. Layer 7 Load Balancing (Application Layer)

L7 Load Balancing understands HTTP, HTTPS, gRPC and can inspect content.

**It can route traffic based on:**
- URL path (`/api`, `/images`)
- Hostname (multi-domain)
- Cookies
- Headers
- Query parameters

**Features:**
- ✔️ Smart routing
- ✔️ Supports caching/compression
- ✔️ Can enforce authentication or rate limiting

**Examples:**
- AWS ALB
- Nginx
- Envoy
- Traefik

**When to use:**
- Web applications
- Microservices
- API gateways

### 🤝 L4 vs L7 Load Balancing (Quick Comparison)

| Feature | L4 | L7 |
|---------|----|----|
| **Works at** | TCP/UDP | HTTP/HTTPS (application) |
| **Routing** | IP + Port | URL, cookies, headers |
| **Performance** | Higher | Lower (more logic) |
| **Features** | Basic forwarding | Smart routing & filters |
| **Use cases** | Databases, games | Web apps, APIs |

### 📈 5. Horizontal Scaling
Horizontal scaling means adding more servers to handle more load.

**Example:**
- If 1 server can handle 1,000 requests/sec
- You add more servers → 5 servers = 5,000 requests/sec

**Why it works well with load balancers:**
- Load balancer spreads traffic across servers
- If one dies, others continue
- Easy to scale up or down

**Pros:**
- ✔️ Infinite scaling (theoretically)
- ✔️ Fault tolerance
- ✔️ Works well in cloud environments

**Cons:**
- ❌ Harder to manage state
- ❌ Needs distributed caching or shared storage (Redis, Memcached)

**Analogy:**
Opening more checkout counters in a supermarket when the line gets long.

### 🎯 Summary

| Concept | Meaning |
|---------|---------|
| **Load balancer** | Distributes traffic across servers |
| **Active-Passive** | One active server, one standby |
| **Active-Active** | All servers active and sharing load |
| **Layer 4 LB** | Routes by IP+Port, very fast |
| **Layer 7 LB** | Routes by URL/headers, very flexible |
| **Horizontal scaling** | Add more servers to increase capacity |

---

## Load Balancer Advanced Concepts

### 🍪 1. Sticky Sessions (Session Affinity)
Sticky sessions mean that a user is always routed to the same backend server during their session.

**Why this is needed:**
- Some applications store user session data locally on one server (in memory)
- If a user switches servers mid-session, they might:
  - get logged out
  - lose their cart
  - break their workflow

Sticky sessions fix this by keeping a user tied to one server.

#### 🔧 How sticky sessions work

**Option A: LB inserts a cookie**
- The load balancer adds its own cookie like:
  ```
  LBSESSIONID=server2
  ```
- So every future request from that browser goes to server2

**Option B: Use application cookies**
- Load balancer reads your session cookie (e.g., `PHPSESSID`)
- and uses it to route to the correct server

**Option C: IP-based stickiness**
- User IP → mapped to a specific server
- (Simplest but not very accurate due to NAT, shared networks, etc.)

#### 👍 Pros
- ✔️ No need to share session data across servers
- ✔️ Easy to set up
- ✔️ Works well for small systems

#### 👎 Cons
- ❌ One server may get overloaded
- ❌ Not suitable for high-scale apps
- ❌ Failover breaks sessions unless shared storage exists
- ❌ Harder to scale horizontally

**Modern alternative:**
Store session data in a shared store like:
- Redis
- Memcached

Then stickiness is no longer needed.

### 🩺 2. Health Checks in Load Balancers
Load balancers continuously test backend servers to make sure they are healthy.

**If a server fails a health check:**
- It is removed from the pool
- No traffic is sent to it

**If it recovers:**
- It is added back automatically

This keeps your system highly available.

#### ⚙️ How health checks work
A load balancer pings each server at intervals to verify:

**1️⃣ Is the server alive?**
- (Low-level check: TCP connect)

**2️⃣ Is the application responding correctly?**
- Application-level checks:
  - HTTP GET `/health`
  - Expecting `200 OK`
  - JSON response like: `{ "status": "UP" }`

**3️⃣ Is latency acceptable?**
- If a server becomes slow, LB may mark it "unhealthy"

**4️⃣ Is it passing N consecutive checks?**
- Servers aren't marked unhealthy after 1 failure — usually require:
  - **Fail:** 3 consecutive failures
  - **Pass:** 2 consecutive successes

#### 🏥 Common health check types

**🔹 TCP health check**
- Checks if server accepts TCP connections

**🔹 HTTP health check**
- Hits a URL like `/health` expecting:
  - status code = 200
  - maybe content in the body

**🔹 HTTPS health check**
- Like HTTP but encrypted

**🔹 Command/script health check**
- Used by Kubernetes, Docker, etc.
- Runs a probe script inside container

#### 👍 Benefits of health checks
- ✔️ Prevents sending traffic to dead servers
- ✔️ Automatic failover
- ✔️ Improves availability
- ✔️ Detects degraded servers (slow or partial failures)

### 🎯 Summary

| Concept | Meaning |
|---------|---------|
| **Sticky sessions** | Keep a user tied to the same server |
| **Methods** | LB cookie, app cookie, IP affinity |
| **Why used** | Servers holding local session state |
| **Best alternative** | Use distributed session store (Redis) |
| **Health checks** | LB tests servers for availability |
| **Types** | TCP, HTTP, HTTPS, Command |
| **Purpose** | Remove unhealthy servers, auto failover |

---

## Reverse Proxy

### 🌐 Reverse Proxy (Web Server)
A reverse proxy is a server placed in front of backend servers that receives client requests and forwards them to internal servers.

**Think of it as:**
- A gatekeeper between users and your servers

```
Users → Reverse Proxy → Application servers
```

### 🔧 What a Reverse Proxy Does

#### 1️⃣ Hides internal servers
- Users never talk directly to backend servers — only to the proxy
- This improves:
  - Security
  - Privacy
  - Architecture flexibility

#### 2️⃣ SSL termination
- TLS/HTTPS decryption happens at the reverse proxy
- Backend servers receive plain HTTP
- ✔️ Reduces CPU load on app servers
- ✔️ Centralizes certificate management

#### 3️⃣ Caching
- Reverse proxy can cache static content like:
  - Images
  - JS/CSS
  - Videos
- → Faster responses, less backend load

#### 4️⃣ Compression
- Proxy compresses responses (gzip, brotli) before sending to clients
- → Smaller payloads, faster downloads

#### 5️⃣ Routing
- Routes traffic to different backend apps based on:
  - Path (`/api`, `/static`)
  - Hostname (`api.example.com`, `app.example.com`)

#### 6️⃣ Security filtering
- Protects against:
  - DDoS
  - IP blocking
  - Request filtering
  - Rate limiting

### 🛠️ Common Reverse Proxies
- Nginx
- Apache
- HAProxy
- Envoy
- Traefik
- Cloudflare (as a reverse proxy CDN)

### ⚖️ Load Balancer vs Reverse Proxy
Many people confuse these, but here's the simplest explanation:

#### 🎯 Load Balancer
A load balancer distributes traffic across multiple servers to:
- Increase capacity
- Prevent overload
- Improve availability

**Key purpose:**
> Balance load and keep the system up.

**Example:**
You have 5 servers. LB ensures all get equal traffic.

#### 🎯 Reverse Proxy
A reverse proxy sits in front of one or many servers and performs:
- Caching
- Security
- Routing
- SSL termination

**Key purpose:**
> Optimize and secure the connection between clients and servers.

### 🧠 Easy Way to Remember
- **Load balancer** = Traffic distributor
- **Reverse proxy** = Traffic manager

### 🧩 How They Overlap
- A reverse proxy can load balance
- A load balancer can act like a reverse proxy
- Modern tools (Nginx, HAProxy, Envoy) often do both

But their primary goals differ.

### 📊 Side-by-Side Comparison

| Feature | Reverse Proxy | Load Balancer |
|---------|---------------|---------------|
| **Main job** | Manage/optimize traffic | Distribute traffic |
| **Number of backend servers** | 1 or many | Many |
| **Caching** | Yes | Rarely |
| **SSL termination** | Yes | Yes |
| **Routing logic** | Path/host-based (L7) | L4 or L7 distribution |
| **Security features** | Strong | Moderate |
| **Failover** | Optional | Core function |
| **Required for scaling** | Not necessarily | Yes |

### 🏗️ Architecture Examples

**Reverse Proxy only:**
```
Users → Nginx → Single backend server
```
(useful for caching, SSL termination, security)

**Load Balancer + Reverse Proxy:**
```
Users → Load Balancer → Reverse Proxy → Backend servers
```
(enterprise setup)

**Reverse Proxy doing load balancing:**
```
Users → Nginx/HAProxy → Multiple backend servers
```
(all-in-one solution)

### 🎯 Summary

| Concept | Short Definition |
|---------|------------------|
| **Reverse Proxy** | A server that manages, secures, and optimizes traffic before it reaches backend servers |
| **Load Balancer** | A system that spreads requests across multiple servers to improve scaling and reliability |
| **Difference** | Reverse proxy focuses on management/security/caching; load balancer focuses on distribution |

---

## API Gateway

### 🚪 What Is an API Gateway?
An API Gateway is a server that sits at the front door of your microservices system.

All clients (web apps, mobile apps, IoT devices) send their requests to the API Gateway instead of calling backend services directly.

**The gateway then:**
- Routes the request to the correct service
- Applies security
- Aggregates responses
- Enforces policies

**In short:**
> The API Gateway is the single entry point for all client requests.

### 🧠 Why do we need an API Gateway?

**Without a gateway:**
- Clients must call multiple microservices directly and handle:
  - Auth
  - Logging
  - Failures
  - Versioning
  - Serialization
- This becomes messy and inefficient

**With a gateway:**
```
Clients → 1 unified API → Microservices
```
Much simpler and more secure.

### 🛠️ What an API Gateway Does (Key Responsibilities)

#### 1️⃣ Request Routing
Forwards the request to the correct microservice based on:
- URL path
- Method
- Headers
- Version

**Example:**
```
/users   → User Service
/orders  → Order Service
/payments → Payment Service
```

#### 2️⃣ Authentication & Authorization
Gateway handles:
- API keys
- OAuth2 / JWT tokens
- Rate limits per user
- Access control

Microservices no longer need to repeat auth logic.

#### 3️⃣ Rate Limiting & Throttling
Prevents abuse by limiting:
- Requests per second
- Requests per IP/user/api key

Protects backend services from overload.

#### 4️⃣ Caching
Stores common responses so they don't hit backend services repeatedly.

**Example:**
```
GET /products
```
Cached at the gateway → faster + less load on backend.

#### 5️⃣ Request/Response Transformation
Gateway can modify:
- Headers
- Response formats (XML ↔ JSON)
- Field filtering
- Versioning logic

**Example:**
- Client uses: `v1/users`
- Gateway internally rewrites: `v2/users-service`

#### 6️⃣ Load Balancing
Some gateways (like Kong, Envoy, Nginx) can also distribute traffic across multiple service instances.

#### 7️⃣ Logging & Monitoring
Central place to log:
- API usage
- Errors
- Latency
- Traffic patterns

This makes system observability much easier.

#### 8️⃣ Failover & Circuit Breaking
If a service is down:
- Gateway returns fallback responses
- Or reroutes traffic
- Or blocks requests to prevent overload

Often implemented with tools like Hystrix or Envoy.

### 📦 Examples of API Gateways

**Open Source:**
- Kong
- Nginx / Nginx Plus
- Tyk
- KrakenD
- Envoy

**Cloud:**
- AWS API Gateway
- Azure API Management
- Google Cloud Endpoints
- Apigee

### 🧩 API Gateway vs Reverse Proxy vs Load Balancer

| Feature | API Gateway | Reverse Proxy | Load Balancer |
|---------|-------------|---------------|---------------|
| **Main job** | Manage APIs | Control traffic | Distribute traffic |
| **Level** | Layer 7 (HTTP) | Layer 7 | Layer 4/7 |
| **Routing** | Smart (service-level) | Path/host | LB algorithms |
| **Auth** | Yes | Optional | Rare |
| **Rate limiting** | Yes | No | No |
| **Transformations** | Yes | Minimal | No |
| **Aggregation** | Yes | No | No |

**Simplest explanation:**
- **Load balancer:** spreads traffic
- **Reverse proxy:** manages traffic
- **API Gateway:** controls, secures, and shapes API traffic

### 🏗️ Where API Gateway Fits in Microservices Architecture

```
Clients → API Gateway → Microservices
```

**The gateway becomes:**
- Policy enforcer
- Traffic controller
- Security gate
- Entry point
- Translator

**Microservices become:**
- Simpler
- More focused
- Easier to maintain

### 🎯 Summary

| Concept | Meaning |
|---------|---------|
| **API Gateway** | Single entry point for APIs in a distributed system |
| **Core functions** | Routing, auth, rate limiting, caching, monitoring, transformations |
| **Why needed** | Simplifies clients, centralizes control, secures APIs |
| **Best for** | Microservices architectures |

---

## API Gateway Authentication

### 🔐 Why Gateways Handle Authentication
In a microservices system, you don't want every service to implement:
- Login logic
- Token validation
- Permissions
- Rate limiting

**Instead:**
> The API Gateway handles authentication and authorization
> Microservices trust the gateway

This makes each service simpler and reduces duplicated code.

### 🟢 1. How OAuth 2.0 Works in an API Gateway

OAuth 2.0 is an authorization framework used to grant users or apps access to resources.

**The flow (simplified for gateways):**

**Step 1: Client wants to access data**
- User tries to call an API, e.g.:
  ```
  GET /orders
  ```

**Step 2: Client is redirected to Authorization Server**
- Authorization server examples:
  - Auth0
  - AWS Cognito
  - Okta
  - Keycloak
  - Google / Facebook login
- User logs in

**Step 3: Authorization Server issues an access token**
- The token is usually a JWT (JSON Web Token)
- This token contains:
  - User ID
  - Expiration time
  - Permissions/roles
  - Issuer info

**Step 4: Client sends token to the API Gateway**
- The client includes the token in the request:
  ```
  Authorization: Bearer <access_token>
  ```

**Step 5: API Gateway validates the token**
- Gateway checks:
  - Is the token well-formed?
  - Has it expired?
  - Is it issued by trusted provider?
  - Is the signature valid?
  - Does the user have access to this resource?
- The gateway uses:
  - Public keys (JWKS endpoint)
  - OAuth config (issuer, audience, scopes)

**Step 6: Gateway forwards request to the microservice**
- If token is valid:
  - Gateway → forwards request
  - Microservice → trusts the gateway
- The microservice does NOT do authentication

**Optional:** The gateway may inject headers like:
```
X-User-Id: 1234
X-User-Roles: admin
```

**Step 7: Microservice responds**
- Microservice sends the response to the gateway → then gateway returns to client

### 🔵 2. How JWT Works in an API Gateway

JWT (JSON Web Token) is just a signed JSON object used for authentication.

**It has:**
- Header
- Payload
- Signature

**Why Gateways love JWT:**
- Self-contained (holds user info, roles, expiry)
- Easy to validate (public key)
- No need for database lookup
- Fast and stateless

#### 🎯 How the gateway validates a JWT

**Step A: Read the header + payload**
- Extract claims like:
  - `sub` (user ID)
  - `exp` (expiration)
  - `scope`
  - `role`

**Step B: Verify the signature**
- The gateway uses the authorization server's public key (JWKS endpoint):
  - Example JWKS URL:
    ```
    https://auth.mycompany.com/.well-known/jwks.json
    ```
- If signature matches → token is authentic

**Step C: Check expiry**
- If `exp` is in the past → token is rejected

**Step D: Check authorization**
- Gateway compares:
  - Token scopes
  - API permissions

**Example:**
- User token: `scope: "read:orders"`
- User tries to call: `POST /orders`
- ❌ Gateway blocks it (no write permission)

### 🟨 What Gateway Does After Validation

**If token is valid:**
- Gateway forwards the request to backend
- Optionally adds user info headers
- Optionally strips sensitive token data

**If invalid:**
- Returns `401 Unauthorized`
- Or `403 Forbidden` for insufficient permissions

### 🚦 Flow Summary: JWT/OAuth in Gateway

```
Client → Login (OAuth) → Authorization Server → token issued (JWT)
Client → sends JWT → Gateway → validates token → routes to service
Microservice → trusts gateway → responds
```

This is the standard security model for microservices.

### 🧩 Why Use OAuth/JWT at the Gateway?

**✔ Centralized authentication**
- Microservices stay simple

**✔ Performance**
- JWT is stateless — no DB checks required

**✔ Scalability**
- Multiple gateway instances can validate tokens independently

**✔ Security**
- Gateway filters out unauthorized requests before they reach services

**✔ Clean separation of responsibilities**
- Identity system handles login
- Gateway handles token validation
- Services handle business logic

### 🏗️ Technologies That Support This

**API Gateways:**
- Kong
- Nginx + JWT module
- Traefik
- KrakenD
- AWS API Gateway
- Azure API Management
- GCP API Gateway

**OAuth Providers:**
- Auth0
- Okta
- Keycloak
- AWS Cognito
- Google Identity

### 🎯 Final Summary

| Concept | What it does | Who handles it |
|---------|--------------|----------------|
| **OAuth** | Defines how users/apps obtain access tokens | Authorization Server |
| **JWT** | Self-contained token used for API calls | API Gateway validates it |
| **API Gateway** | Validates tokens, checks permissions, forwards requests | Sits between client & microservices |

---

## Microservices Trust & Service Mesh

### 🔐 1. How Microservices Trust the API Gateway

In a secure microservices architecture:
> Clients never talk directly to microservices
> All requests must go through the API Gateway

**To make this work safely, microservices must trust that:**
- The gateway has already authenticated the user
- The gateway has validated the JWT/OAuth token
- The gateway enforces authorization policies

So microservices do NOT validate tokens themselves — they trust the gateway.

#### 🧩 How does this trust actually work?

**🟢 Method 1: Network Isolation (Private Network / VPC)**
- Microservices are placed in a private network where only the gateway can reach them
- Gateway = public
- Services = private (no public IPs)
- Clients CANNOT bypass the gateway

```
Client → Gateway → Services
```

This gives a trusted path.

**🟡 Method 2: Shared Secrets / Signing**
- The API Gateway adds trusted headers, such as:
  ```
  X-User-ID: 123
  X-User-Roles: admin
  ```
- Then microservices trust these headers because:
  - Only the gateway knows a secret key
  - Only the gateway can generate a signed header or token
  - Internal network blocks requests not coming from gateway

Sometimes this looks like:
```
X-Internal-Signature: <HMAC signature>
```
Microservices verify the signature with a shared secret.

**🔵 Method 3: Mutual TLS (mTLS)**
- Gateway and microservices authenticate each other using TLS certificates
- Gateway has a certificate
- Microservices have certificates
- Both sides validate each other

**This ensures:**
- ✔ Only the gateway can call services
- ✔ Only legitimate services can respond

This approach is common in service mesh (Envoy, Istio, Linkerd).

**🟣 Method 4: Internal JWT (Gateway → Service)**
- The gateway can issue a new internal token for microservices, like:
  - "User ID"
  - "Roles"
  - "Tenant ID"
  - "Permissions"

**Example flow:**
1. User sends a JWT to the gateway
2. Gateway validates it
3. Gateway issues an internal service token (short-lived)
4. Microservices verify the internal token

This keeps user tokens out of internal services.

#### 💡 Summary: How services trust the gateway

| Method | How it works |
|--------|--------------|
| **Network isolation** | Services only accept traffic from gateway IPs |
| **Signed internal headers** | Gateway signs headers; services verify signature |
| **mTLS** | Certificates prove identity of gateway + services |
| **Internal JWT** | Gateway issues new trusted JWT for service-to-service calls |

### 🕸️ 2. How Service Mesh Extends This Trust Model

A Service Mesh (like Istio, Linkerd, Consul Connect) adds a sidecar proxy next to every microservice.

**Each proxy handles:**
- mTLS
- Authorization
- Encryption
- Observability
- Traffic policies

Instead of trusting the gateway alone, every service now authenticates every call using mTLS.

#### 🧠 What changes with a service mesh?

**✔ Microservices don't trust the network — they trust certificates**
- Every service gets a unique identity:
  ```
  serviceA.mynamespace.cluster.local
  serviceB.mynamespace.cluster.local
  ```
- Communication is authenticated and encrypted automatically

**✔ Gateway to service traffic also goes through mesh**
- The gateway itself becomes part of the mesh

**Flow:**
```
Client → Gateway → Sidecar → Microservice
```

Sidecars enforce:
- "Is this really the gateway calling?"
- "Is this service allowed to call this endpoint?"

**✔ Zero Trust Architecture**
- Service mesh makes your system zero trust:
  - No trust based on IP
  - No trust based on network location
  - All trust based on identity + certificates

#### 🔄 Flow with API Gateway + Service Mesh

**Step-by-step:**
1. Client authenticates with OAuth → gets JWT
2. Gateway validates the JWT (auth + rate limit)
3. Gateway forwards the request through its sidecar
4. Sidecar establishes mTLS connection with service's sidecar
5. Service reads trusted identity from mTLS metadata
6. Service performs business logic
7. Response flows back through sidecars → gateway → client

Every hop is authenticated and encrypted.

#### 🏗️ Gateway vs Service Mesh Trust Responsibilities

| Responsibility | Gateway | Service Mesh |
|----------------|---------|--------------|
| **User auth (OAuth, JWT)** | ✔ Yes | ❌ No |
| **Rate limiting** | ✔ Yes | ❌ No |
| **API routing** | ✔ Yes | ❌ No |
| **Service identity** | ❌ No | ✔ Yes |
| **mTLS between services** | ❌ No | ✔ Yes |
| **Internal authorization** | ❌ No | ✔ Yes |
| **Traffic retries, circuit breaking** | Optional | ✔ Yes |

They work together, not as replacements.

### 🎯 Final Summary

**💡 API Gateway handles:**
- User authentication (JWT/OAuth)
- API routing
- Rate limiting
- External security

**💡 Microservices trust the gateway using:**
- Private networking
- Signed internal headers
- mTLS
- Internal JWT

**💡 Service Mesh enhances trust by:**
- Enforcing mTLS on every internal call
- Providing service identity and authorization
- Making the system "zero trust" internally

---

## Mutual TLS (mTLS)

### 🔐 What Is mTLS? (Mutual TLS)
mTLS = Mutual Transport Layer Security.

It is the same protocol used for HTTPS BUT with one key difference:
> Both the client AND the server verify each other's identity using certificates.

**Normal TLS:**
- Server proves who it is
- Client remains anonymous

**mTLS:**
- Server proves identity
- Client proves identity
- ➡️ Mutual trust

### 🧩 Why mTLS?

**🟢 1. Prevents unauthorized clients from accessing services**
- A service cannot call another service unless it presents a valid certificate

**🔵 2. Prevents impersonation**
- A compromised service cannot pretend to be another service

**🟡 3. Encrypts communication end-to-end**
- Data is encrypted in transit

**🟠 4. Provides identity for Zero-Trust Architecture**
- "No service trusts another by default."
- This is critical in microservices and service meshes

### 🔑 How TLS Works (Quick Refresher)

**Normal TLS handshake:**
1. Client → Server: Hello
2. Server → Client: certificate + key info
3. Client validates server certificate
4. They negotiate encryption keys
5. Encrypted communication begins

That's HTTPS.

### 🔄 How mTLS Works (Step-by-Step)

**Step 1: Client says "Hello"**
- Client → Server:
  - Sends its supported TLS versions, ciphers, etc.

**Step 2: Server sends certificate**
- Server → Client:
  - Server certificate
  - Certificate chain (signed by CA)

**Step 3: Client validates server certificate**
- Client checks:
  - Is it signed by a trusted CA?
  - Is it expired?
  - Is hostname correct?
- If valid → continue

**Step 4: Server requests client's certificate**
- This is where mTLS adds something extra:
  - Server → Client: "Please send your certificate."

**Step 5: Client sends its certificate**
- Client → Server:
  - Its certificate
  - Signature proving ownership of private key

**Step 6: Server validates client certificate**
- Server checks:
  - Signed by trusted CA?
  - Not expired?
  - Revoked?
  - Matches expected service identity?
- If valid → continue

**Step 7: Both sides negotiate encryption keys**
- Shared symmetric key is created

**Step 8: Secure, authenticated communication begins**
- Now:
  - Both sides know exactly who the other party is
  - Traffic is encrypted end-to-end
  - Impersonation becomes nearly impossible

### 🏢 Where Do Certificates Come From? (CA & PKI)

mTLS requires a Public Key Infrastructure (PKI).

**Components:**
- Root CA (trusted anchor)
- Intermediate CAs
- Certificate Authority (CA) signs service certificates
- Certificate Revocation List / OCSP for invalid certificates

### ⚙️ How Microservices Use mTLS

**Each microservice gets:**
- A private key
- A certificate signed by the CA

**Certificates usually contain the service identity:**
```
CN=serviceA.default.svc.cluster.local
```

**When service A calls service B:**
- A verifies B's certificate → B is legit
- B verifies A's certificate → A is legit
- → Strong trust boundary

### 🕸️ mTLS in Service Mesh (Istio, Linkerd, Consul)

In service mesh architectures:
- Sidecar proxies (Envoy) handle mTLS automatically:
  - Application code never touches certificates
  - Certificates rotate automatically (e.g., every 24 hours)
  - Identity is enforced at proxy level
  - Policies control which service can talk to which service

**Flow:**
```
serviceA → sidecarA → mTLS → sidecarB → serviceB
```

**The proxies do:**
- ✔ Certificate validation
- ✔ Identity check
- ✔ Encryption
- ✔ Authorization

### 🔁 Certificate Rotation

To minimize security risk:
- Certificates are rotated frequently (hours or days)
- Old certificates are removed
- Mesh control plane (e.g., Istio Citadel) automates this
- No downtime for apps

### 🛡️ Benefits of mTLS

| Benefit | Explanation |
|---------|-------------|
| **Mutual authentication** | Both sides must prove who they are |
| **Zero-trust networking** | No trust based on IP or network zone |
| **Prevents man-in-the-middle attacks** | Attackers cannot impersonate services |
| **Encryption in transit** | Protects sensitive data |
| **Service identity** | Certificates include service identities |
| **Automated in service mesh** | No app code change needed |

### ⚠️ Challenges (without a Service Mesh)

Implementing mTLS manually is hard:
- Certificate generation
- Certificate rotation
- Secure key storage
- CA infrastructure management
- Configuring each microservice
- Complex failures when certs expire

**This is why most modern systems use:**
- Istio
- Linkerd
- Envoy
- Consul Connect

to automate mTLS.

### 🎯 Final Summary

**mTLS = TLS + mutual authentication**

**mTLS provides:**
- 💡 Strong identity
- 🔐 Encrypted transport
- 🚫 Protection from impersonation
- 🛡 Zero-trust networking

**Used heavily in:**
- Microservices
- Service meshes
- API gateway to backend communication

Modern service meshes automate all of mTLS making secure comms simple and consistent.

---

## Application Layer & Microservices

### 🌐 1. Application Layer (Layer 7)

The application layer is the top layer in the OSI model (Layer 7).

It is where apps interact with the network.

**It deals with application-level protocols such as:**
- HTTP/HTTPS → web traffic
- gRPC → microservice communication
- DNS → domain name resolution
- SMTP → email
- FTP → file transfer

**What it handles:**
- Request formatting (HTTP requests)
- Response formatting (JSON, HTML)
- Authentication/Authorization
- Caching, compression
- Routing logic (URLs, headers)

**Why it's important:**
This is the layer where microservices, APIs, gateways, browsers, and apps talk to each other.

### 🧩 2. Microservices

Microservices is an architecture where an application is broken into small, independent services.

**Each service:**
- Runs independently
- Has its own code, database, deployment
- Owns a single business capability (e.g., Payments, Orders, Users)
- Communicates over the network (HTTP, gRPC, messaging)

**Example of microservices in an e-commerce app:**
- **User Service** → authentication, profiles
- **Order Service** → order creation and history
- **Cart Service** → shopping cart management
- **Payment Service** → billing, invoices
- **Inventory Service** → stock management

#### Benefits:
- ✔ Scales independently
- ✔ Faster deployments
- ✔ Technology flexibility (each service can use its own language/framework)
- ✔ Better fault isolation

#### Challenges:
- ❌ Network complexity
- ❌ Service discovery needed
- ❌ Distributed transactions are hard
- ❌ Need for gateways, meshes, monitoring, logs, tracing

### 🔍 3. Service Discovery

In microservices, services need to find each other's network locations (IP + port).

**But microservices:**
- Scale up/down dynamically
- Restart frequently
- Run in containers
- Change IPs constantly

So you cannot hardcode addresses like:
```
order-service = 10.0.3.14
```
This will break.

**Service discovery solves this.**

#### 🟦 How Service Discovery Works

**Two main patterns:**

**🔹 A. Client-Side Service Discovery**
- Client chooses the service instance

**Flow:**
1. Client queries a service registry
2. Registry returns a list of healthy instances
3. Client load-balances between them

**Examples:**
- Eureka (Netflix OSS)
- Consul
- etcd (used by Kubernetes components)

Used a lot in older microservice systems with Netflix stack.

**🔹 B. Server-Side Service Discovery (Recommended / Most modern)**
- Load balancer or API Gateway chooses the instance

**Flow:**
1. Client sends request to LB / gateway
2. LB queries service registry
3. LB selects a healthy instance and forwards the request

**Examples:**
- Kubernetes Services
- Envoy
- Istio
- AWS Cloud Map
- NGINX / HAProxy

Clients don't need to know anything about service locations.

#### 🔧 Service Registry

A service registry is a distributed database that stores:
- Service names
- Instance IPs
- Ports
- Health status
- Metadata

**Common registries:**
- Consul
- Etcd
- Zookeeper
- Eureka
- Kubernetes API Server (built-in registry)

**The registry updates every time:**
- A service starts
- A service scales
- A service dies
- A service fails health checks

### 🏗️ How These Concepts Connect

**Application Layer (L7):**
- Handles HTTP, gRPC, routing, security

**Microservices:**
- Use L7 protocols to communicate (HTTP, gRPC)

**Service Discovery:**
- Ensures microservices can find each other reliably

**Together:**
```
Client → API Gateway (L7) → Service Discovery → Load Balancer → Microservices
```

This is the foundation of a modern distributed system.

---

## Database

### 🗄️ Database (DB)
A database is a system that stores, organizes, and retrieves data.

**Two major families:**
- **Relational (SQL)** → structured tables
- **Non-relational (NoSQL)** → flexible schemas, distributed

### 🧱 Relational Database Management System (RDBMS)

An RDBMS stores data in tables with rows and columns.

**Examples:**
- MySQL
- PostgreSQL
- Oracle
- SQL Server

**Key features:**
- SQL queries
- ACID transactions (strong consistency)
- Joins across tables
- Structured schema

### 🔁 Master–Slave Replication (Primary–Replica)

One database server is master and handles writes.

One or more slaves replicate from it and handle reads.

**Benefits:**
- ✔ Load balances read traffic
- ✔ Backup for failover

**Downsides:**
- ❌ Writes still bottleneck at master
- ❌ Replication lag → eventual consistency for reads

### 🔁 Master–Master Replication

Two or more DB nodes accept writes and replicate to each other.

**Benefits:**
- ✔ High availability
- ✔ More write capacity

**Downsides:**
- ❌ Conflict resolution needed (same row updated at same time)
- ❌ More complex

Used by systems like: CouchDB, Cassandra (in a more advanced form).

### 🌐 Federation

You split your database by features/functions.

**Example:**
- User DB
- Order DB
- Billing DB

Each subsystem has its own database.

**Benefits:**
- ✔ Teams work independently
- ✔ Smaller DBs → easier scaling

**Downsides:**
- ❌ Joins across DBs impossible
- ❌ Must manage cross-DB transactions

Used in large enterprise systems and microservices.

### 🧩 Sharding

You split a SINGLE database table horizontally across multiple machines.

**Example:**
```
Users A–M → Shard 1
Users N–Z → Shard 2
```

**Benefits:**
- ✔ Increases total capacity and performance
- ✔ Avoids single-database bottleneck

**Downsides:**
- ❌ Hard to change shard keys later
- ❌ Cross-shard queries are complex
- ❌ Requires app logic to route queries to the right shard

Used by: Twitter, MongoDB, Cassandra, Elasticsearch.

### 📉 Denormalization

The opposite of normalization.

You duplicate data or merge tables to make reads faster.

**Benefits:**
- ✔ Fewer joins
- ✔ Faster queries
- ✔ Perfect for high-read workloads

**Downsides:**
- ❌ Data inconsistency risk
- ❌ Harder to update duplicated data

**Used heavily in:**
- NoSQL databases
- Analytics systems
- Caches

### ⚙️ SQL Tuning

Improving SQL query performance by:
- Adding indexes
- Avoiding unnecessary joins
- Optimizing WHERE clauses
- Using proper schema design
- Analyzing query plans
- Partitioning tables

**Goal** → faster queries, less load.

### 🧰 NoSQL (Not Only SQL)

NoSQL databases are designed for:
- Horizontal scaling
- High availability
- Schemaless or flexible schema
- High read/write throughput

**Four major types:**
1. Key-Value Store
2. Document Store
3. Wide-Column Store
4. Graph Database

Used in large distributed systems.

### 🔑 Key-Value Store

Stores data as:
```
key → value
```

**Examples:**
- Redis
- DynamoDB
- Riak

**Use cases:**
- Caching
- Session storage
- Real-time counters

Fastest type of NoSQL because lookup is O(1).

### 📄 Document Store

Data stored as JSON-like documents.

**Examples:**
- MongoDB
- CouchDB
- Firebase Firestore

**Benefits:**
- ✔ Dynamic schema
- ✔ Nested structures
- ✔ Great for APIs and web apps

### 🧱 Wide Column Store

Stores data in column families, optimized for huge amounts of data across distributed nodes.

**Examples:**
- Cassandra
- HBase
- Bigtable

**Benefits:**
- ✔ Massive scalability
- ✔ High write throughput
- ✔ Tunable consistency

Used by: Instagram, Netflix, Uber, Spotify.

### 🔗 Graph Database

Stores data as nodes and relationships (edges).

**Examples:**
- Neo4j
- Amazon Neptune
- JanusGraph

**Best for:**
- Social networks
- Recommendation engines
- Fraud detection
- Network graphs

Relationships are first-class citizens → very fast graph queries.

### 🎯 One-Sentence Summary for Each

| Concept | Simple Meaning |
|---------|----------------|
| **Database** | System storing data |
| **RDBMS** | SQL-based structured database |
| **Master–Slave** | 1 write node, many read nodes |
| **Master–Master** | Many write nodes, syncing with each other |
| **Federation** | Different DBs for different features |
| **Sharding** | Split one database across multiple servers |
| **Denormalization** | Duplicate data for faster reads |
| **SQL Tuning** | Make SQL queries fast |
| **NoSQL** | Scalable, flexible non-relational DB family |
| **Key-Value** | Key → value lookups (fastest) |
| **Document Store** | JSON-like flexible documents |
| **Wide Column** | Distributed column-family storage |
| **Graph Database** | Data with rich relationships |

---

## SQL vs NoSQL

### 🧱 SQL (Relational Databases)

**Examples:**
- MySQL
- PostgreSQL
- Oracle
- SQL Server

SQL databases store data in:
- Tables
- Rows
- Columns

With a fixed schema and relationships (foreign keys).

#### ✔ Best for:
- Structured data
- Complex queries
- Transactions
- Data integrity
- Analytics

#### ✔ Key strengths:
- ACID guarantees (strong consistency)
- Joins and relational modeling
- Mature tooling
- Great for business apps

#### ❌ Weaknesses:
- Scaling writes is hard
- Vertical scaling (scaling up) is expensive
- Schema changes can be slow

### 📦 NoSQL (Non-Relational Databases)

**Examples:**
- MongoDB (document)
- Cassandra (wide column)
- Redis (key-value)
- Neo4j (graph)

NoSQL databases provide:
- Flexible schema
- Horizontal scaling
- Distributed storage

#### ✔ Best for:
- High-speed writes
- Massive scale
- Semi-structured/unstructured data
- Microservices
- Real-time applications

#### ✔ Key strengths:
- Scale out across many servers
- Flexible schemas → easy to evolve
- High availability
- Fast writes & distributed by design

#### ❌ Weaknesses:
- Weaker consistency (often eventual)
- No (or limited) joins
- Complex transactions are hard
- Some lack standard query languages

### 🧠 Core Differences (Simple Table)

| Feature | SQL | NoSQL |
|---------|-----|-------|
| **Data model** | Tables, rows, columns | Key-value, document, column-family, graph |
| **Schema** | Fixed | Flexible |
| **Scaling** | Vertical (scale up) | Horizontal (scale out) |
| **Consistency** | Strong (ACID) | Tunable / eventual (BASE) |
| **Transactions** | Strong & reliable | Limited / custom |
| **Query language** | SQL (standard) | Varies |
| **Best for** | Complex queries, integrity | High scale, high throughput |

### 🗂️ When to Use SQL

Choose SQL when your application needs:

**✔ Strong consistency**
- Balances, inventory, financial data

**✔ Complex queries**
- Reporting, analytics, dashboards

**✔ Structured, predictable data**
- User accounts, product catalogs

**✔ Multi-row transactions**
- Order creation, payments, shipping updates

**Typical apps:**
E-commerce, banking, ERP systems, CRMs.

### 📡 When to Use NoSQL

Choose NoSQL when your application needs:

**✔ Massive scale or high throughput**
- Millions of users, global traffic

**✔ Flexible schema**
- Storing JSON documents, logs, events

**✔ High availability**
- Distributed systems with minimal downtime

**✔ Specialized data models**
- Graph relationships
- Time-series
- Cache storage

**Typical apps:**
Social networks, IoT platforms, messaging apps, recommendation systems.

### 🧩 Real-World Examples

**Facebook:**
- Uses MySQL for core data (SQL)
- Cassandra for chat and messaging (NoSQL)

**Netflix:**
- Cassandra for high availability
- MySQL + Postgres for billing, transactions

**Amazon:**
- DynamoDB (NoSQL) for scaling
- Aurora (SQL) for relational data

**Banking systems:**
- Almost always SQL due to consistency needs

### 🎯 Final Rule of Thumb

**Choose SQL when:**
- You need correctness
- You need complex queries
- You have structured data

**Choose NoSQL when:**
- You need scale
- You need speed
- You have flexible or large data

### 💬 Simple Analogy
- **SQL** = Office spreadsheet
  - Organized, structured, perfect for accuracy
- **NoSQL** = Filing cabinet of folders
  - Flexible, messy but scalable and fast

---

## Sharding Strategies

### 🧩 What Is Sharding? (Quick refresher)

**Sharding** = splitting one logical database table into multiple physical databases called shards.

**Goal:**
- ✔ Handle more data
- ✔ Handle more traffic
- ✔ Reduce load on a single database

### 🧭 Sharding Strategies

Below are the most common sharding strategies, with their pros/cons and where they fit.

#### 1️⃣ Range-Based Sharding

Data is partitioned by a continuous range.

**Example (User IDs):**
```
Shard 1: 1–1,000,000  
Shard 2: 1,000,001–2,000,000  
Shard 3: 2,000,001–3,000,000
```

**✔ Pros:**
- Simple
- Efficient for range queries (e.g., date-based queries)
- Easy to understand

**❌ Cons:**
- Hotspots (all new users might go to the last shard)
- Uneven data distribution
- Some shards get overloaded while others stay idle

**Best for:**
- Time-series data
- Sequential IDs

#### 2️⃣ Hash-Based Sharding (Most Popular)

A hash function decides which shard stores the data.

**Example:**
```
shard = hash(user_id) % number_of_shards
```

**✔ Pros:**
- Very even distribution
- Prevents hotspots
- Good for random-access workloads

**❌ Cons:**
- Hard to add/remove shards (requires rehashing and data migration)
- Harder to run range queries ("get users with ID between 100–200")

**Best for:**
- Large-scale microservices
- Highly parallel workloads
- Systems like DynamoDB / Cassandra distribute data this way

#### 3️⃣ Directory-Based Sharding (Lookup Table)

A routing service or lookup table maps keys → shards.

**Example:**
```
UserID 1–1M → Shard A  
UserID 1M–2M → Shard B  
VIP Users → Shard C
```

**✔ Pros:**
- Very flexible
- Can rebalance shards easily
- Can shard by custom rules

**❌ Cons:**
- Single point of failure if directory goes down
- Must keep directory consistent
- More complexity

**Best for:**
- Complex enterprise systems
- When you want fine-grained control
- When hashing or ranges don't fit well

#### 4️⃣ Geo-Based Sharding

Shards based on region:

**Example:**
```
US users → US shard  
EU users → EU shard  
Asia users → APAC shard  
```

**✔ Pros:**
- Reduced latency
- Local data residency
- Regional outage containment

**❌ Cons:**
- Hard cross-region queries
- Uneven distribution (some regions heavier)

**Used by:**
Facebook, Instagram, Google, TikTok

#### 5️⃣ Entity-Based / Functional Sharding

Shard by business domain, not by ID.

**Example:**
```
Users → User DB  
Orders → Order DB  
Inventory → Inventory DB
```

This is also called **federation**.

**✔ Pros:**
- Independent scaling
- Teams own their own DB
- No cross-entity sharding issues

**❌ Cons:**
- Hard joins across entities
- Possible duplication of data
- Must handle distributed transactions

Used heavily in microservices architectures.

### 🧨 Sharding Pitfalls (VERY IMPORTANT)

These are the classic mistakes that cause outages or slow disaster recoveries.

#### ❌ 1. Hotspot Shards (Uneven Data Distribution)

If one shard gets too much traffic or data, it becomes a bottleneck.

**Common causes:**
- Sequential IDs with range sharding
- One country has many more users
- VIP users all placed in the same shard

**Fixes:**
- Use hashing
- Pre-split ranges
- Add dynamic balancing

#### ❌ 2. Hard to Add or Remove Shards

Traditional hashing:
```
shard = hash(key) % 4
```

Adding a 5th shard forces re-hashing EVERYTHING, causing major downtime.

**Fix:**
Use **consistent hashing** (used by DynamoDB, Cassandra).

#### ❌ 3. Cross-Shard Queries Are Expensive

If you need to query multiple shards:
- High latency
- Complex logic
- Hard to guarantee consistency

**Example:**
```sql
SELECT SUM(order_amount) FROM Orders;
```

You must query ALL shards → merge results.

**Fixes:**
- Pre-aggregation
- Secondary index shards
- Use analytical DB (Snowflake, BigQuery)

#### ❌ 4. Cross-Shard Joins Don't Work

SQL joins across shards are slow or impossible.

**Example:**
Joining Users ↔ Orders across shards can break.

**Fixes:**
- Denormalize data
- Use application-level joins
- Design shard keys so related data stays together

#### ❌ 5. Wrong Shard Key Choice

Choosing a bad shard key leads to:
- Imbalanced data
- Poor performance
- Painful re-sharding

**Bad shard keys:**
- Country (one country dominates traffic)
- Time (causes hotspots)
- Email prefix (poor distribution)

**Good shard keys:**
- UUID
- Hash of user ID
- Something evenly distributed

#### ❌ 6. Re-Sharding Is Extremely Hard

Once you shard, changing the strategy later requires:
- Migrating millions/billions of rows
- Coordinated downtime
- Dual-writes
- Complex routing logic

**Plan shard key very carefully.**

#### ❌ 7. Complex Transactions (ACID becomes hard)

Distributed transactions across shards are:
- Slow
- Error-prone
- Often avoided

**Fixes:**
- Use the Saga pattern
- Avoid multi-shard writes when possible

#### ❌ 8. Operational Complexity

Sharding adds layers of complexity:
- Monitoring each shard
- Scaling each shard
- Backups per shard
- Failover per shard

Prepare for operational challenges.

### 🧠 Quick Summary Table

| Strategy | Pros | Cons | Best For |
|----------|------|------|----------|
| **Range** | Simple, good for ranges | Hotspots | Time-series |
| **Hash** | Even distribution | Hard to scale | High traffic |
| **Directory** | Flexible | Complex, central dependency | Large enterprises |
| **Geo** | Low latency | Skewed regions | Global apps |
| **Entity-based** | Independent scaling | Cross-entity joins | Microservices |

### 🎯 Final Takeaways
- **Hash sharding** is the most common for large systems
- **Re-sharding is painful** → choose shard key wisely
- **Cross-shard queries/joins are expensive** → avoid them
- **Shard early only if needed** → don't overengineer
- **Combine strategies** in mature systems (e.g., entity + hash inside each entity)

---

## Caching

### 📝 Note on Caching Demo
The original document contains a comprehensive Java caching demo with code examples. For brevity and proper markdown formatting, the conceptual explanations are provided here. The full Java code examples demonstrate:

- **Simple Cache Class** - Basic HashMap-based cache
- **Simulated Slow Database** - Demonstrates the need for caching
- **Cache-Aside Pattern** - Lazy loading strategy
- **Write-Through Cache** - Synchronous cache updates
- **Write-Behind Cache** - Asynchronous cache updates
- **Refresh-Ahead Cache** - Proactive cache refreshing

### 🎯 Caching Concepts Covered

| Concept | Demonstrated |
|---------|--------------|
| **Cache** | ✔ Simple cache class |
| **Client caching** | Behavior simulated through local cache |
| **CDN caching** | Same logic as edge caching (cache-aside style) |
| **Web server caching** | Cache at HTTP layer works same as app caching |
| **Database caching** | Cache layer sits above DB |
| **Application caching** | Yes (HashMap-based cache) |
| **Query-level caching** | Cache stores DB query results |
| **Object-level caching** | Entire objects stored in cache |
| **Cache-aside** | ✔ Implemented |
| **Write-through** | ✔ Implemented |
| **Write-behind** | ✔ Implemented |
| **Refresh-ahead** | ✔ Implemented |

---

## Asynchronism & Message Queues

### ⚡ 1. Asynchronism (Asynchronous Processing)

Asynchronism means tasks run without blocking the main flow.

The caller does not wait for the task to finish.

**Example:**
- You upload a photo
- The app immediately shows "Upload complete"
- In the background: thumbnail creation, virus scan, compression

**Why async?**
- ✔ Faster user experience
- ✔ Prevents blocking threads
- ✔ Handles long-running operations efficiently
- ✔ Improves scalability

**Real-life analogy:**
You order pizza → go watch TV → pizza arrives later.
You don't stand in the kitchen waiting.

### 📩 2. Message Queues

A message queue is a buffer that stores messages sent between services.

**Examples:**
- RabbitMQ
- Kafka
- ActiveMQ
- SQS (AWS)

**How it works:**
1. Producer sends a message (e.g., "send email")
2. Queue stores it
3. Consumer processes messages at its own speed

**Why use queues?**
- ✔ Decouple services
- ✔ Smooth out bursts of traffic
- ✔ Improve reliability (messages persist even if services crash)
- ✔ Allow asynchronous workflows

**Example:**
User signs up → app sends "welcome email" message to queue → email service sends the actual email later.

### 🧵 3. Task Queues

A task queue is a special type of message queue that stores work to be executed, not just messages.

**Examples:**
- Celery
- Sidekiq
- Resque
- RQ
- BullMQ
- AWS SQS + Lambda

**How task queues work:**
1. Producer pushes a "task" (e.g., "resize image")
2. Queue stores it
3. Worker processes it asynchronously
4. Task completes in background

**Task queues often include:**
- ✔ Retries
- ✔ Delayed tasks
- ✔ Scheduling
- ✔ Error handling

**Example:**
Generate PDF, resize images, run ML inference, send SMS, clean logs, etc.

### 🌀 4. Back Pressure

Back pressure happens when consumers cannot keep up with producers.

This prevents systems from being overwhelmed.

**Think of it like:**
Consumers say:
> ❌ "Stop sending! I'm full."

**When does back pressure happen?**
- Too many messages in queue
- Slow consumer
- Limited CPU or memory
- Traffic spikes

**Back pressure strategies:**

**A. Slow down producer**
- Producer reduces rate of sending

**B. Reject new requests**
- Return errors like `429 Too Many Requests`

**C. Drop messages (in lossy systems like telemetry)**

**D. Auto-scale consumers**
- Add more workers to catch up

**E. Queue grows temporarily**
- But only up to a safe limit

**Real-life analogy:**
Grocery checkout line:
- If the line gets too long → store slows entry, opens new counters, or directs people elsewhere

### 🧠 Putting it All Together (Real System Example)

Imagine a large e-commerce site:

**When a user places an order:**
1. Request saved to database → synchronous
2. Queue sends tasks for:
   - Payment processing
   - Inventory update
   - Email confirmation
   - Fraud detection
3. These run asynchronously via message/task queues

**If traffic spikes:**
- Payment service slows
- Queue fills with messages
- Back pressure kicks in
- System auto-scales workers
- Gateway may reject some requests

This prevents the system from crashing.

### 🎯 Summary Table

| Concept | Simple Meaning |
|---------|----------------|
| **Asynchronism** | Do work in the background without blocking |
| **Message Queue** | Stores messages between services |
| **Task Queue** | Stores tasks to be executed by workers |
| **Back Pressure** | Mechanism to prevent overload when consumers can't keep up |

---

## Communication Protocols

### 📡 1. Communication (in distributed systems)

Communication means how two systems talk to each other over a network.

**Two main models:**

**A. Connection-oriented (steady connection)**
- Uses a stable connection
- Reliable
- Example: TCP

**B. Connectionless (no handshake)**
- Sends packets without establishing a connection
- Fast but less reliable
- Example: UDP

Microservices, browsers, servers, IoT — all depend on these communication models.

### 🌐 2. Transmission Control Protocol (TCP)

TCP is a reliable, connection-oriented protocol.

**Key features:**
- ✔ 3-way handshake (connect before sending data)
- ✔ Guarantees delivery
- ✔ Guarantees order
- ✔ Retries lost packets
- ✔ Flow control & congestion control

**Used for:**
- Web browsing (HTTP/HTTPS)
- Email
- File transfer
- Database connections

**Analogy:**
Sending a registered letter — tracking, confirmation, no loss.

### 🚀 3. User Datagram Protocol (UDP)

UDP is a fast, connectionless, unreliable protocol.

**Key features:**
- ✔ No connection setup
- ✔ No order guarantee
- ✔ No delivery guarantee
- ✔ Very low latency

**Used for:**
- Real-time applications
- Video streaming
- Online gaming
- VoIP calls
- DNS

**Analogy:**
Throwing postcards — fast but some may be lost.

### 🔧 4. Remote Procedure Call (RPC)

RPC makes a network call feel like a local function call.

**How it works:**
1. Client calls a function
2. RPC framework sends request over network
3. Server executes function
4. Returns result

**Features:**
- ✔ Strong typing
- ✔ Fast binary protocols (e.g., gRPC)
- ✔ Uses HTTP/2 or TCP underneath
- ✔ Great for microservice-to-microservice communication

**Common RPC frameworks:**
- gRPC (Google)
- Thrift (Facebook)
- JSON-RPC
- XML-RPC

**Analogy:**
You call a function — but it actually runs on another machine.

### 🌍 5. Representational State Transfer (REST)

REST is an architectural style for designing web APIs.

**It uses:**
- HTTP verbs (GET, POST, PUT, DELETE)
- Resources identified by URLs
- Stateless communication

**Example:**
```
GET /users/123
POST /orders
DELETE /products/45
```

**Features:**
- ✔ Easy to use
- ✔ Works anywhere (browser-friendly)
- ✔ JSON-based
- ✔ Stateless → scalable
- ✔ Simpler than RPC

### REST vs RPC

| Factor | REST | RPC |
|--------|------|-----|
| **Style** | Resource-oriented | Function-oriented |
| **Format** | JSON over HTTP | Binary (gRPC), JSON |
| **Best for** | Public APIs | Microservices internal calls |
| **Speed** | Medium | Very fast |
| **Ease** | Very easy | More setup |

### 🧠 How They Fit Together

| Layer | What it handles |
|-------|-----------------|
| **TCP/UDP** | Low-level transport (packets) |
| **RPC / REST** | High-level communication (APIs) |
| **Application** | Business logic |

**Flow visualization:**
```
Application → REST/RPC → TCP → Network → Server
```

REST and RPC sit on top of TCP (or sometimes UDP).

### 🎯 Summary Table

| Concept | Simple meaning |
|---------|----------------|
| **Communication** | How systems talk over a network |
| **TCP** | Reliable, ordered, connection-oriented |
| **UDP** | Fast, connectionless, best-effort |
| **RPC** | Call remote functions like local functions |
| **REST** | Web-style APIs using HTTP verbs |

---

## System Design Examples

### 📝 Note on System Design Examples

The original document contains 5 comprehensive system design examples with detailed High-Level Design (HLD), Low-Level Design (LLD), component logic, trade-offs, and Java code samples. Below is a summary of these examples:

### ⭐ EXAMPLE 1 — E-Commerce Product Catalog System

**Demonstrates:** CDN, load balancer, microservices, sharding, caching, NoSQL, eventual consistency

**Architecture:**
```
Clients → CDN → API Gateway → Load Balancer → Product Service → NoSQL DB (Sharded)
                                  ↑
                                  | 
                             Redis Cache
```

**Key Components:**
- CDN for product images
- API Gateway for auth, rate limiting, routing
- Load Balancer for traffic distribution
- Product Service with cache-aside pattern
- Sharded NoSQL DB (MongoDB/Cassandra)

**Trade-offs:**
- NoSQL for scalability vs eventual consistency
- Sharding for massive scale vs complex cross-shard queries
- Cache-aside for simplicity vs slower first request

### ⭐ EXAMPLE 2 — Social Media News Feed

**Demonstrates:** MQ, async tasks, write-behind caching, eventual consistency, NoSQL wide column store

**Architecture:**
```
User Action → Feed Service → Message Queue → Fanout Workers → Feed DB (Cassandra)
                                                   ↓
                                              Cache Refresh
```

**Key Components:**
- Feed Service with async message publishing
- Message Queue for buffering
- Fanout Workers for feed generation
- Cassandra for high write throughput
- Write-behind caching

**Trade-offs:**
- MQ for traffic smoothing vs increased complexity
- Write-behind for fast writes vs potential data loss
- Cassandra for throughput vs eventual consistency

### ⭐ EXAMPLE 3 — Ride-Sharing App (Uber-like)

**Demonstrates:** RPC, service discovery, microservices, mTLS, geospatial DB

**Architecture:**
```
Client App → API Gateway → Load Balancer → Matching Service → Driver Location Service  
                                                        ↑
                                            Service Discovery + mTLS
```

**Key Components:**
- API Gateway with OAuth/JWT
- Service Discovery for dynamic service location
- gRPC for fast inter-service communication
- mTLS for zero-trust security
- Geospatial DB (Redis Geo/MongoDB GeoJSON)

**Trade-offs:**
- gRPC for low latency vs harder browser support
- mTLS for security vs certificate management complexity
- Geospatial DB for fast queries vs limited complex operations

### ⭐ EXAMPLE 4 — Video Streaming Platform (YouTube-like)

**Demonstrates:** CDN, chunking, async processing, object storage, REST APIs

**Architecture:**
```
Upload → API Gateway → Video Service → Storage (S3)  
                             ↓
                     MQ → Transcoding Workers → CDN
```

**Key Components:**
- Video Service for upload handling
- S3 for raw file storage
- Message Queue for async transcoding
- Transcoding Workers for multiple resolutions
- CDN for global content delivery

**Trade-offs:**
- CDN for low latency vs higher cost
- MQ for async processing vs increased complexity
- S3 for scalability vs not suitable for real-time ops

### ⭐ EXAMPLE 5 — Online Payment System

**Demonstrates:** SQL RDBMS, ACID, strong consistency, master-slave, L4 load balancer

**Architecture:**
```
Client → API Gateway → Payment Service → SQL DB (Master) → Slave DB (Read replicas)
```

**Key Components:**
- Payment Service with ACID transactions
- SQL DB Master for strongly consistent writes
- Slave DB for analytics and dashboards
- L4 Load Balancer for SQL read routing

**Trade-offs:**
- SQL for perfect consistency vs hard to scale writes
- Master-Slave for availability vs replication lag
- ACID for no double-charging vs slower performance

### 🎯 Summary of All System Design Concepts Used

| Concept | Where It Appeared |
|---------|-------------------|
| **CDN** | E-commerce, Video platform |
| **Load balancer** | Catalog, Payments |
| **Cache** | Redis in catalog system |
| **Sharding** | Product catalog DB |
| **Replication** | Payment SQL DB |
| **NoSQL** | Feed system, catalog |
| **SQL** | Payments |
| **Asynchronous processing** | Feed fanout, video transcoding |
| **Message queues** | Feed, video processing |
| **RPC** | Ride-sharing |
| **REST** | Catalog, video |
| **API Gateway** | All services |
| **Service Discovery** | Ride-sharing |
| **mTLS** | Ride-sharing |
| **Back pressure** | Feed system |
| **Cache-aside** | Catalog |
| **Write-through** | Payments (indirect) |
| **Write-behind** | Feed updates |

---

## System Design Interview Tips

### ⭐ 1. Knowledge You Already Have

You're very strong in these building blocks for almost every system design interview:

**✔ Databases & storage**
- SQL / NoSQL
- Sharding
- Replication
- Consistency models
- CAP theorem
- ACID vs BASE
- Caching patterns

**✔ Distributed systems**
- Load balancers (L4/L7)
- Reverse proxies
- Service discovery
- Microservices & API gateway
- mTLS, zero trust
- Message queues, event-driven systems
- Asynchronous processing
- Back pressure
- Rate limiting

**✔ Communication**
- TCP vs UDP
- REST vs RPC (gRPC)

**✔ Scaling**
- Horizontal vs vertical scaling
- CDN
- CQRS
- Partitioning
- Consistent hashing

**✔ Reliability**
- Failover (active-active / active-passive)
- Health checks
- Leader election
- Distributed locks

**✔ Architecture patterns**
- Write-behind
- Event sourcing
- Sagas
- Circuit breakers
- Load shedding

**This is already enough to design:**
- Instagram-level feed
- Twitter timeline
- WhatsApp chat system
- Uber ride-matching
- Netflix video streaming
- Amazon shopping cart
- Payment system
- URL shortener
- Notification system

### ⭐ 2. What System Design Interviews Actually Test

System design interviews test **application**, not memorization.

**They check if you can:**

**1️⃣ Clarify requirements**
- "What scale?"
- "What features are required?"
- "What consistency do we need?"

**2️⃣ Propose a high-level architecture**
- Simple boxes + arrows diagram

**3️⃣ Justify your choices**
- "Why NoSQL instead of SQL?"
- "Why use cache-aside?"
- "Why use event-driven architecture?"

**4️⃣ Make trade-offs**
- No design is perfect
- You must say:
  - "If we choose AP, we lose C."
  - "If we choose write-through, writes slow down."
  - "If we shard by userId, cross-user queries become expensive."

**5️⃣ Identify bottlenecks**
- Scaling: DB? Cache? Queue? Network?

**6️⃣ Talk through failure scenarios**
- "What if Redis fails?"
- "What if the DB master dies?"
- "What if the queue becomes full?"

**7️⃣ Explain how to scale over time**
- V1 → V2 → V3 roadmap

> Most candidates fail because they cannot walk through the design in a structured way, even though they know many concepts.

### ⭐ 3. What You Still Need to Practice

**✔ Practice real interview problems**

Start designing systems like:
- TikTok
- WhatsApp
- Google Drive
- Payment System
- Food Delivery (Zomato/Doordash)
- Youtube-like system
- Twitter trending service

**✔ Practice communicating your design**

Talk out loud for 30–45 minutes.

**Be structured:**
1. Requirements  
2. High-level architecture  
3. Database schema  
4. API design  
5. Scaling  
6. Bottlenecks  
7. Deep dive  
8. Failure handling  

**✔ Practice drawing diagrams**

Simple ASCII diagrams are enough:
```
Client → API Gateway → LB → Service → DB
             ↑
           Cache
```

**✔ Practice trade-offs**

Every choice comes with a cost.

Interviews LOVE trade-offs.

---

## RAID Levels

### What is RAID? (Definition)

**RAID** is a way of using multiple hard drives together to improve:
- Speed
- Data safety
- or both

> **Real-world idea:**
> Hard drives are like notebooks where you write important information.

### RAID 0 — Striping

**Definition:**
Data is split across multiple disks so they work at the same time.

**Real-World Example:**
You split your notes between two notebooks so two people can write at once.
- Notebook 1 → first half
- Notebook 2 → second half

**Result:**
- Writing is very fast
- If one notebook is lost, everything becomes useless

**Key Point:**
❌ No backup at all

### RAID 1 — Mirroring

**Definition:**
The same data is written exactly the same on two disks.

**Real-World Example:**
You write identical notes in two notebooks.
- Notebook 1 → original
- Notebook 2 → copy

**Result:**
- Lose one notebook → data is still safe
- But you waste space (two notebooks, same content)

**Key Point:**
- ✅ Very safe
- ❌ Storage inefficient

### RAID 5 — Parity

**Definition:**
Data is spread across disks, plus extra recovery information (parity) is stored.

**Real-World Example:**
Three people take notes:
- Two write different parts
- One writes a summary that can recreate missing notes
- If one notebook is lost, the others can rebuild it

**Result:**
- Good speed
- Good safety
- Efficient storage

**Key Point:**
⚖️ Balance of speed and safety

### RAID 6 — Double Parity

**Definition:**
Same as RAID 5, but with two sets of recovery information.

**Real-World Example:**
Three people write notes, and two people write summaries.
- Even if two notebooks are lost, notes can still be recovered

**Result:**
- Very safe
- Slightly slower than RAID 5

**Key Point:**
🧯 Extra protection

### RAID 10 — Mirror + Stripe

**Definition:**
A combination of RAID 1 (mirroring) and RAID 0 (striping).

**Real-World Example:**
- First, you create two identical copies of your notes
- Then, multiple people write different parts at the same time

**Result:**
- Very fast
- Very safe
- Needs many notebooks

**Key Point:**
🚀 Best performance, high cost

### Comparison Table (Easy to Remember)

| RAID | Definition (Short) | Real-World Idea | Speed | Safety | Storage Use |
|------|-------------------|-----------------|-------|--------|-------------|
| **RAID 0** | Split data | Split notes | ⭐⭐⭐⭐ | ❌ | ⭐⭐⭐⭐ |
| **RAID 1** | Copy data | Duplicate notes | ⭐⭐ | ⭐⭐⭐⭐ | ❌ |
| **RAID 5** | Parity | Summary notes | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| **RAID 6** | Double parity | Extra summaries | ⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ |
| **RAID 10** | Mirror + Stripe | Copy + teamwork | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ❌ |

---

## Additional Important Concepts

### ⭐ 1. Partitioning (besides Sharding)

You already know sharding, but partitioning is the more general idea.

**👉 What is partitioning?**
Splitting data or workloads into smaller chunks to improve performance and isolation.

**Types:**
- **Horizontal partitioning** → sharding
- **Vertical partitioning** → splitting data by columns
  - Example: User basic info table, User analytics table
- **Functional partitioning** → different features use different DBs (similar to federation)

**Why it matters:**
- ✔ Speeds up queries
- ✔ Reduces DB load
- ✔ Helps with scaling

**Trade-off:**
- ❌ Harder joins
- ❌ More complexity

### ⭐ 2. Rate Limiting

Used to protect your system from overload and prevent abuse.

**👉 What is it?**
Controlling how many requests a user or IP can make per second/minute.

**Examples:**
- 100 requests/minute → normal user
- 1000 requests/minute → rate limit → 429 error

**Why?**
- ✔ Prevent DDoS
- ✔ Prevent API abuse
- ✔ Prevent system overload
- ✔ Improve fairness

**Common algorithms:**
- Token bucket
- Leaky bucket
- Fixed window counter
- Sliding window

### ⭐ 3. Circuit Breakers

Prevents cascading failures in microservices.

**👉 What it does:**
If Service A calls Service B and B is failing, the circuit breaker opens and stops requests temporarily.

**Why?**
- ✔ Prevents server overload
- ✔ Helps graceful degradation
- ✔ Faster recovery

**Trade-off:**
- ❌ Sometimes blocks too aggressively
- ❌ Needs careful tuning

### ⭐ 4. Load Shedding

When system is under heavy load, you reject excess requests early instead of slow failures.

**Example:**
If your server can process 1000 req/sec but gets 5000:
- → Shed 4000 quickly with 503 or 429
- → Process 1000 successfully

**Why?**
- ✔ Keeps the system stable
- ✔ Keeps latency predictable

### ⭐ 5. Distributed Transactions

When a write needs to happen across multiple services/databases.

**Two main patterns:**

**1️⃣ Two-Phase Commit (2PC)**
- Strong consistency → slower

**2️⃣ Saga Pattern**
- Better for microservices → compensating actions

**Why important?**
Modern microservices rarely use 2PC → Sagas are preferred.

### ⭐ 6. Idempotency

Ensures retrying a request doesn't create duplicates.

**Example:**
- User hits "Pay" twice →
  - Without idempotency → 2 charges
  - With idempotency → only 1 charge

**How?**
- Use request IDs
- Token-based operations
- Upsert semantics

Max important in payment systems and distributed systems.

### ⭐ 7. Distributed Locks

Guarantees only one service can modify a resource at a time.

**Examples:**
- Redis Redlock
- Zookeeper
- Etcd locking

**Why?**
- ✔ Prevent inconsistent writes
- ✔ Prevent race conditions

**Trade-off:**
- ❌ Locks slow down distributed writes

### ⭐ 8. Quorum

Used in distributed databases (Cassandra, DynamoDB, CockroachDB).

**Example:**
- Read = 2 nodes
- Write = 2 nodes
- Total nodes = 3

**Quorum rule:**
```
R + W > N
```

Guarantees consistency without full synchronization.

### ⭐ 9. Event Sourcing

Instead of storing current state, you store all events that happened and rebuild state when needed.

**Example:**
- Balance = sum of all transactions
- Not just a single column

**Why?**
- ✔ Full audit history
- ✔ Easy debugging
- ✔ Easy replication

**Trade-off:**
- ❌ Complex to implement
- ❌ Handling large event logs

### ⭐ 10. CQRS (Command Query Responsibility Segregation)

Separate:
- **Command model** (writes → validation)
- **Query model** (reads → optimized)

**Why?**
- ✔ Read side can scale independently
- ✔ Write side stays simple
- ✔ Useful in event-driven systems

**Trade-off:**
- ❌ Eventual consistency
- ❌ More components

### ⭐ Summary of Missing Must-Know System Design Concepts

| Concept | Why Important |
|---------|---------------|
| **Rate limiting** | Prevent overload & abuse |
| **Circuit breaker** | Prevent cascading failures |
| **Load shedding** | Save system under high load |
| **Distributed locks** | Avoid race conditions |
| **Idempotency** | Safe retries |
| **Distributed transactions** | Multi-service consistency |
| **Leader election** | Choose a coordinator node |
| **Event sourcing** | Log everything, replay state |
| **CQRS** | Scale reads/writes separately |
| **Quorum** | Consistency in distributed DBs |
| **Consistent hashing** | Stable partitioning |
| **Bloom filters** | Fast existence checks |
| **Time synchronization** | Order events correctly |
| **Storage engines** | DB internals → performance impact |

---

## Conclusion

This comprehensive guide covers all the essential system design concepts you need to know for interviews and real-world architecture. Remember:

1. **Understand the fundamentals** - Performance, scalability, availability, consistency
2. **Know your trade-offs** - Every design decision has pros and cons
3. **Practice communication** - Being able to explain your design is as important as the design itself
4. **Think about failure scenarios** - How does your system handle failures?
5. **Consider scaling** - How will your design evolve as the system grows?

Good luck with your system design interviews and real-world projects!

