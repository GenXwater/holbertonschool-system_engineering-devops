# Secure and Monitored Three-Server Web Infrastructure

We are designing a **three-server secure web infrastructure** to host the website `www.foobar.com`. This setup ensures encrypted traffic, adds monitoring capabilities, and improves overall security. Below are the components and their purposes.

---

## Components of the Infrastructure

### 1. **3 Firewalls**
   - Protect the servers by filtering and blocking unauthorized traffic.

### 2. **1 SSL Certificate**
   - Ensures secure communication between the user's browser and the web server by encrypting traffic over HTTPS.

### 3. **3 Monitoring Clients**
   - Installed on each server to collect and send performance and operational data to a monitoring service like Sumologic or similar.

### 4. **3 Servers**
   - **Load Balancer:** Distributes traffic among servers and terminates SSL.
   - **Web Server (Nginx):** Handles static content and forwards dynamic requests to the application server.
   - **Application Server:** Processes business logic and interacts with the database.

### 5. **Database (MySQL):**
   - Stores and organizes the data required by the application.

---

## Why Add These Components?

1. **Firewalls:**
   - Protect the servers by filtering out malicious traffic, preventing unauthorized access, and allowing only legitimate traffic.

2. **SSL Certificate:**
   - Encrypts data exchanged between the user and the server, ensuring privacy and protection from eavesdropping or man-in-the-middle attacks.
   - Necessary for serving `www.foobar.com` over HTTPS.

3. **Monitoring Clients:**
   - Provide visibility into server health, performance, and traffic.
   - Allow proactive issue detection, such as high CPU usage, disk space shortage, or increased error rates.

---

## Specifics of the Infrastructure

### Firewalls
- **Purpose:**  
  - Filter incoming and outgoing traffic to ensure only trusted sources can access the servers.
  - Block malicious traffic like DDoS attacks or unauthorized IPs.

### HTTPS Traffic
- **Why HTTPS:**  
  - Encrypts communication, ensuring user privacy and data integrity.
  - Prevents sensitive information (e.g., passwords) from being intercepted.

### Monitoring
- **Purpose:**  
  - Tracks performance metrics like CPU usage, memory, disk space, and request rates.
  - Detects failures or potential issues early to ensure quick resolution.
- **How It Works:**  
  - Monitoring clients collect data (logs, metrics) from the servers.
  - The data is sent to a central service (e.g., Sumologic) for analysis and visualization.

### Monitoring Web Server QPS
- **Steps:**
  1. Install a monitoring client on the web server.
  2. Configure the monitoring tool to track request logs or metrics.
  3. Set up a dashboard or alerting system to visualize the Queries Per Second (QPS) and detect spikes or anomalies.

---

## Issues with the Infrastructure

### 1. **Terminating SSL at the Load Balancer**
   - Problem: The traffic between the load balancer and backend servers is unencrypted, creating a potential vulnerability if this segment is compromised.
   - Solution: Use end-to-end encryption by encrypting traffic between the load balancer and servers.

### 2. **Single MySQL Server for Writes**
   - Problem: The write workload is concentrated on one server, which could lead to performance bottlenecks or downtime if the server fails.
   - Solution: Implement a **Primary-Replica** setup with failover or consider a distributed database system to handle write scalability.

### 3. **Servers with All Components**
   - Problem: Each server has the same components (database, web server, and application server), leading to resource competition and inefficiency.
   - Solution: Separate concerns by dedicating specific servers for each role (e.g., web server, application server, database server) to improve performance and scalability.
