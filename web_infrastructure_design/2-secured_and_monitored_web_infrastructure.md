# Additional element:
1. Three Firewalls
  - Firewall 1 (Load Balancer): Protects the entry point, only allows HTTPS (443) and SSH (22)
  - Firewall 2 (Web Tier): Controls traffic between load balancer and web servers, restricts to HTTP (80)
  - Firewall 3 (Database): Protects database layer, only allows MySQL (3306) from web servers
  - Benefit: Defense in depth, minimizes attack surface

3. SSL Certificate for HTTPS
- Purpose: Encrypts all communication between users and the website
- Benefit: Protects sensitive data, prevents eavesdropping, required for modern web standards
- Implementation: SSL termination at load balancer with wildcard certificate (*.foobar.com)

3. Three Monitoring Clients
- Purpose: Collect metrics from all infrastructure components
- Benefit: Real-time visibility into performance, errors, and health status
- Implementation: Agents on each server sending data to external monitoring service

## What are firewalls for?
Firewalls are network security systems that control incoming and outgoing traffic based on predetermined security rules. They:
- Block unauthorized access to servers
- Limit exposure by closing unused ports
- Prevent horizontal movement if one server is compromised
- Create security zones (DMZ, internal network, database layer)

## Why is the traffic served over HTTPS?
HTTPS provides:
- Encryption: Prevents eavesdropping on sensitive data (passwords, personal information)
- Data Integrity: Prevents tampering during transmission
- Authentication: Verifies the server identity to prevent impersonation
- SEO Benefits: Google ranks HTTPS sites higher
- Browser Requirements: Modern browsers flag HTTP sites as "Not Secure"

## What monitoring is used for?
- Performance Tracking: CPU, memory, disk usage, response times
- Error Detection: Application errors, failed requests, database issues
- Capacity Planning: Identify when to scale based on trends
- Alerting: Immediate notification of critical issues
- Troubleshooting: Historical data for debugging problems

## How the monitoring tool is collecting data?
1. Agents/Collectors: Monitoring clients installed on each server
2. Data Collection:
  - System metrics (CPU, memory, disk I/O)
  - Application metrics (response times, error rates)
  - Web server logs (Nginx access/error logs)
  - Database metrics (queries, connections, replication status)
3. Transport: Secure connection to external monitoring service (Sumo Logic)
4. Analysis: Data aggregated, visualized, and alerted on in dashboard

## Explain what to do if you want to monitor your web server QPS
# Steps to monitor QPS:
1. Configure web server to log request timestamps
2. Monitoring agent parses access logs
3. Calculate: Total Requests / Time Interval
4. Set up real-time dashboard with QPS graph
5. Configure alerts for abnormal QPS spikes/drops

# Example Nginx log format:
log_format qps '$remote_addr - $remote_user [$time_local] "$request" '
               '$status $body_bytes_sent "$http_referer" "$http_user_agent"';

# Monitoring query (pseudo):
SELECT COUNT(*) FROM nginx_logs 
WHERE timestamp >= NOW() - INTERVAL 1 SECOND
GROUP BY FLOOR(UNIX_TIMESTAMP(timestamp))
# issues are with this infrastructure:

## Why terminating SSL at the load balancer level is an issue?

## Why having only one MySQL server capable of accepting writes is an issue?

## Why having servers with all the same components (database, web server and application server) might be a problem?
