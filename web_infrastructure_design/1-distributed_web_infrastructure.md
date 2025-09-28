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
-- Advantages: Maximizes resource utilization, better performance
-- Disadvantages: Requires session management for stateful applications

- Active-Passive Alternative:
-- Active-Passive: Only one server handles traffic while the other sits idle as a standby
-- Advantages: Simpler configuration, automatic failover

Disadvantages: Wasted resources, lower capacity utilization
### How a database Primary-Replica (Master-Slave) cluster works?
### What is the difference between the Primary node and the Replica node in regard to the application?
### Where are SPOF
### Security issues (no firewall, no HTTPS)
### No monitoring
