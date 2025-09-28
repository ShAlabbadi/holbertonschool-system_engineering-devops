# What is a server?
A server is a dedicated computer or system that provides resources, data, services, or programs to other computers (called clients) over a network. In this infrastructure, it's a single physical or virtual machine that hosts the entire web application stack - including the web server, application server, application code, and database.

# What is the role of the domain name?
The domain name foobar.com serves as a human-readable address that maps to the server's numerical IP address (8.8.8.8). It functions like a contact name in your phonebook - instead of memorizing the technical IP address, users can remember the simple domain name to access the website.

# What type of DNS record www is in www.foobar.com?
The www in www.foobar.com is configured using an A Record (Address Record). An A record is a DNS record that directly maps a hostname to an IPv4 address. In this case, the www A record points to the server IP 8.8.8.8.

# What is the role of the web server?
The web server has three primary roles:
1. Static Content Handler - Serves static files directly (HTML, CSS, JavaScript, images)
2. Reverse Proxy - Receives incoming HTTP requests and forwards dynamic content requests to the application server
3. Request Router - Manages and directs incoming traffic to the appropriate backend services

# What is the role of the application server?
The application server executes the business logic of your web application. It:
- Processes dynamic content generation
- Handles user authentication and authorization
- Manages application workflow and business rules
- Processes form submissions and user interactions
- Communicates with the database to retrieve or store data

# What is the role of the database?
The database (MySQL) serves as the persistent data storage layer that:
- Stores all application data (user accounts, content, transactions)
- Provides structured data organization and relationships
- Ensures data integrity and security
- Enables efficient data retrieval and manipulation through SQL queries

# What is the server using to communicate with the computer of the user requesting the website?
The server communicates using the TCP/IP protocol suite over the internet. Specifically:
1. HTTP/HTTPS protocols for web traffic (application layer)
2. TCP (Transmission Control Protocol) for reliable, ordered data delivery
3. IP (Internet Protocol) for addressing and routing packets between networks

# Issues with This Infrastructure :
## 1. SPOF (Single Point of Failure)
This infrastructure has a critical Single Point of Failure because all components run on one server:
- Server Failure: If the physical server hardware fails, the entire website goes offline
- Network Failure: If the server's network connection fails, the site becomes inaccessible
- Power Outage: A single power source means no redundancy
- No Backup Systems: There are no failover servers to handle traffic if the main server fails

## 2. Downtime when maintenance needed (like deploying new code web server needs to be restarted)
Any maintenance activity requires taking the entire system offline:
- Code Deployments: Deploying new application code requires restarting the application server, causing service interruption
- Database Maintenance: Schema changes or database updates require stopping the database service
- Security Patches: Applying OS or software security patches often requires server reboots
- Web Server Updates: Updating Nginx configuration or version requires service restarts
- Zero Recovery Time: No ability to perform blue-green deployments or rolling updates

## 3. Cannot scale if too much incoming traffic
The single-server architecture cannot handle traffic growth:
- Vertical Scaling Limits: You can only upgrade the server hardware (CPU, RAM, storage) so much before hitting physical and cost limits
- No Horizontal Scaling: Cannot add additional servers to distribute the load
- Resource Contention: All services (web server, application server, database) compete for the same finite resources (CPU, memory, I/O)
- Traffic Spike Vulnerability: Sudden traffic increases can overwhelm the server, causing slow performance or complete crashes
- Database Bottleneck: The single database instance becomes a performance choke point under heavy load

This infrastructure represents a basic starting point but lacks the reliability, maintainability, and scalability needed for production applications with any significant traffic or availability requirements.
