# Additional element:
1. Three Firewalls
  - Firewall 1 (Load Balancer): Protects the entry point, only allows HTTPS (443) and SSH (22)
  - Firewall 2 (Web Tier): Controls traffic between load balancer and web servers, restricts to HTTP (80)
  - Firewall 3 (Database): Protects database layer, only allows MySQL (3306) from web servers
  - Benefit: Defense in depth, minimizes attack surface

2. SSL Certificate for HTTPS
  - Purpose: Encrypts all communication between users and the website
  - Benefit: Protects sensitive data, prevents eavesdropping, required for modern web standards
  - Implementation: SSL termination at load balancer with wildcard certificate (*.foobar.com)

3. Three Monitoring Clients
  Purpose: Collect metrics from all infrastructure components
  Benefit: Real-time visibility into performance, errors, and health status
  Implementation: Agents on each server sending data to external monitoring service

## What are firewalls for?
## Why is the traffic served over HTTPS?
## What monitoring is used for?
## How the monitoring tool is collecting data?
## Explain what to do if you want to monitor your web server QPS
# issues are with this infrastructure:
## Why terminating SSL at the load balancer level is an issue?
## Why having only one MySQL server capable of accepting writes is an issue?
## Why having servers with all the same components (database, web server and application server) might be a problem?
