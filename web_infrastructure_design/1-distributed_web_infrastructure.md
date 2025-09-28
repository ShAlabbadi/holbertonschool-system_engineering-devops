# Specifics About This Infrastructure
### Additional Element
1. Load Balancer (HAProxy)
  - Purpose: Distributes incoming traffic across multiple web servers
  - Benefit: Prevents overloading a single server and provides high availability
  - Result: If one web server fails, traffic automatically routes to the healthy server

2. Second Web/Application Server
  - Purpose: Provides redundancy and increases capacity
  - Benefit: Handles more concurrent users and provides failover capability
  - Result: Eliminates the web/application tier as a single point of failure

3. Database Primary-Replica Cluster
- Purpose: Provides database redundancy and improves read performance
- Benefit: Read queries can be distributed to replica, writes go to primary
- Result: Database is no longer a single point of failure

### What distribution algorithm your load balancer is configured with and how it works?
Algorithm Used: Round Robin
- How it works: HAProxy distributes incoming requests sequentially to each server in rotation
- Example: Request 1 → Server 1, Request 2 → Server 2, Request 3 → Server 1, Request 4 → Server 2, etc.
- Advantages: Simple, predictable, and ensures equal distribution of requests
- Alternative algorithms: Least Connections, IP Hash, Weighted Round Robin

### Is your load-balancer enabling an Active-Active or Active-Passive setup, explain the difference between both
This Infrastructure: Active-Active

- Active-Active: Both web servers are actively handling traffic simultaneously
  - Advantages: Maximizes resource utilization, better performance
  - Disadvantages: Requires session management for stateful applications

- Active-Passive: Only one server handles traffic while the other sits idle as a standby
  - Advantages: Simpler configuration, automatic failover
  - Disadvantages: Wasted resources, lower capacity utilization
    
### How a database Primary-Replica (Master-Slave) cluster works?
1. Primary Node (Master): Handles all write operations (INSERT, UPDATE, DELETE)
2. Replica Node (Slave): Continuously copies data changes from the Primary
3. Replication Process:
  - Primary writes changes to its binary log
  - Replica reads the binary log and applies the same changes
- Process happens asynchronously in near real-time

### What is the difference between the Primary node and the Replica node in regard to the application?
- Primary Node:
  - Handles ALL write operations
  - Source of truth for data changes
  - Only one primary in the cluster
  - Application sends INSERT/UPDATE/DELETE queries here

- Replica Node:
  - Handles ONLY read operations (SELECT queries)
  - Data is read-only (cannot accept writes)
  - Used to offload read traffic from primary
  - Application can send read queries here to reduce load on primary

### Where are SPOF
1. Load Balancer SPOF
- Only one HAProxy instance
- If it fails, no traffic reaches any web servers
- Solution: Add redundant load balancers with floating IP
2. Database Primary SPOF
- Only one primary database node
- If primary fails, write operations become impossible
- Solution: Implement primary-primary replication or automatic failover
3. Single Network Connection
- Only one internet connection to load balancer
- Network outage makes entire infrastructure unavailable

### Security issues (no firewall, no HTTPS)
1. No Firewall
- No network-level protection between servers
- Database exposed directly to application servers
- Risk: Unauthorized access, SQL injection attacks
- Solution: Implement network security groups and firewalls
2. No HTTPS/SSL
- All communication happens over plain HTTP
- Risks: Data interception, man-in-the-middle attacks
- Solution: Implement SSL termination at load balancer

### No monitoring
1.No Performance Monitoring
- Cannot track server CPU, memory, disk usage
- Risk: Cannot anticipate scaling needs or detect performance degradation

2. No Application Monitoring
- No error tracking or application performance monitoring
- Risk: Bugs and issues go undetected

3. No Health Checks
- Load balancer cannot detect if a server is malfunctioning but still running
- Risk: Traffic may be sent to unhealthy servers
- Solution: Implement health checks and automated alerts
