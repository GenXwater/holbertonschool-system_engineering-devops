# Distributed Web Infrastructure

We are designing a **three-server distributed web infrastructure** to host the website `www.foobar.com`. This setup improves scalability, availability, and reliability compared to a single-server infrastructure. Below are the components and their purposes.

---

## Components of the Infrastructure

### 1. **3 Servers**
   - **1 Load Balancer (HAProxy):**
     - Distributes incoming traffic among multiple servers to balance the load and prevent any single server from being overwhelmed.
     - Improves reliability by providing redundancy.
   - **1 Web Server (Nginx):**
     - Handles HTTP/HTTPS requests, serves static files (images, CSS, JavaScript), and forwards dynamic requests to the application server.
   - **1 Application Server:**
     - Processes application logic and interacts with the database to generate dynamic responses for user requests.

### 2. **1 Code Base (Application Files)**
   - Shared across all servers, this contains the application's logic and functionality.

### 3. **1 Database (MySQL)**
   - A **Primary-Replica (Master-Slave)** cluster is used to distribute database read and write operations for better performance and redundancy.

---

## Why Add These Components?

1. **Load Balancer (HAProxy):**
   - Ensures high availability and scalability by distributing traffic.
   - Handles failover in case one server becomes unavailable.

2. **Web Server and Application Server Separation:**
   - Improves performance and scalability by separating the concerns of serving static files and processing application logic.

3. **Primary-Replica Database Cluster:**
   - Enhances data availability and performance.
   - The **Primary node** handles all write operations, while **Replica nodes** handle read operations, reducing the load on the Primary database.

---

## Load Balancer Configuration

### Distribution Algorithm
- **Round Robin:**
  - The load balancer forwards each incoming request to the next server in a cyclical manner.
  - Ensures an even distribution of traffic across all servers.

### Active-Active vs. Active-Passive Setup
- **Active-Active:**  
  - All servers are operational and handle traffic simultaneously.
  - Provides better performance as traffic is distributed across all servers.
- **Active-Passive:**  
  - One server is active and handles all traffic, while the other(s) remain idle until a failover is triggered.
  - Provides redundancy but may waste resources compared to Active-Active.

---

## Primary-Replica Database Cluster

### How It Works:
- **Primary Node (Master):**
  - Handles all write operations and propagates changes to the Replica(s) through replication.
- **Replica Node(s) (Slave):**
  - Handle read operations to reduce the load on the Primary.
  - Replica nodes are kept in sync with the Primary through periodic updates.

### Difference Between Primary and Replica:
- The **Primary** is writable, meaning it handles data insertion, deletion, and updates.
- The **Replica** is read-only, ensuring data consistency and reducing the load on the Primary node.

---

## Issues with the Infrastructure

### 1. **SPOF (Single Point of Failure)**
   - The load balancer is a single point of failure. If it fails, the entire infrastructure becomes inaccessible.

### 2. **Security Issues**
   - No firewall: The servers are vulnerable to unauthorized access and attacks.
   - No HTTPS: Communication between the user and servers is not encrypted, exposing sensitive data to potential interception.

### 3. **No Monitoring**
   - Without monitoring, issues such as server overload, downtime, or database replication lag cannot be detected or addressed proactively.
