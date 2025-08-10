
# Web infrastructure design
# TASK 0: Simple web stack
![Simple web stack diagram](https://imgur.com/gallery/simple-web-stack-qZEKJzL  "Simple web stack architecture")


## What is a server: 
### A hardware computer systems that manages requests and response from and to the web server respectively, they can only be access via network protocols e.g TCP/IP

## What is the role of the domain name: 
### A domain name is the human-readable name of a website, like foobar.com. Its role is to provide a simple way for people to access a website without having to remember the server's specific IP address.

## What type of DNS record www is in www.foobar.com: 
### The www part in www.foobar.com is typically a CNAME (Canonical Name) record. This record acts as an alias, pointing the www subdomain to the primary domain's A (Address) record.

## What is the role of the web server: 
### The webserver is a software that creates an interface between the users or stakeholder of an application by accepting requests from the users, establish communication with the server, and return server response to the user using the communication protocols, e.g of web servers are browsers.

### What is the role of the application server: application server is the core of an application, its basic role is to process application logic and return the response that is sent to the web server.

### What is the role of the database: the storage unit that stores, retrieve application data, its the application's memory.

### What is the server using to communicate with the computer of the user requesting the website: The server uses a network protocol called TCP/IP (Transmission Control Protocol/Internet Protocol) to communicate with the user's computer. 

## POTENTIAL ISSUES
### SPOF - single point of failure, if the application server or database fails the server won't be able to reach or return user required response.
### Downtime when maintenance needed (like deploying new code web server needs to be restarted): Server downtime due to system upgrade would affect application uptime.
### Cannot scale if too much incoming traffic: the application only has one application server which could create overload during high traffic or potential server downtimes

# Task 1: Distributed web infrastructure
![Distributed web infrastructure diagram](https://imgur.com/gallery/distributed-web-infrastructure-RDlh7iv "Distributed web infrastructure")

## What distribution algorithm your load balancer is configured with and how it works; 
### Active-Active vs. Active-Passive: This setup is an Active-Active cluster. In this configuration, both servers are online and actively serving traffic simultaneously.

## Is your load-balancer enabling an Active-Active or Active-Passive setup, explain the difference between both
### Active Active: This setup is an Active-Active cluster. In this configuration, both servers are online and actively serving traffic simultaneously. This contrasts with an Active-Passive setup, where one server is active while the other is on standby, only taking over if the active server fails. The active-active approach improves performance and resource utilization.


## How a database Primary-Replica (Master-Slave) cluster works
### The database needs to be more resilient than a single server. A Primary-Replica (Master-Slave) cluster solves this. In this model, the primary node handles all write operations (e.g., adding a new user), while one or more replica nodes are created to handle all read operations (e.g., displaying a user profile).

### The issues are with this infrastructure:

## Where are SPOF
### Single Points of Failure (SPOFs): The most critical SPOF in this design is the single MySQL database. If it fails, the entire application will go down.
## Security issues (no firewall, no HTTPS)
### No Firewall: Without a firewall, the servers are directly exposed to the internet, making them vulnerable to unauthorized access and various attacks.
### No HTTPS: Traffic between users and the servers is unencrypted (HTTP). This means sensitive data, like login credentials, can be intercepted and read. An

## No monitoring
### No Monitoring: The lack of monitoring is a significant issue. Without monitoring, there's no way to track server health, performance, or traffic spikes

## TASK 2: Secured and monitored web infrastructure

![Secured and monitored web infrastructure Design](https://imgur.com/gallery/secured-monitored-web-infrastructure-KJqa4YI "Secured and monitored web infrastructure")


## Firewalls:
### Firewalls act like security guards, examining all incoming and outgoing network traffic. They block anything that doesn't match a predefined set of security rules, preventing unauthorized access.


## HTTPS: 
### Traffic is served over HTTPS to ensure that communication between the user's browser and your server is encrypted. This is essential for protecting sensitive data like login credentials and credit card information.

## Monitoring: 
### Monitoring is used to maintain a reliable web infrastructure. By tracking metrics, you can identify performance bottlenecks, troubleshoot issues, and predict potential failures, allowing you to address problems proactively.


## Monitoring Data Collection: 
### A small software agent, or monitoring client, is installed on each server. It collects performance data (e.g., CPU usage, memory, disk I/O) and sends it to a central monitoring service for analysis.

## Monitoring Web Server QPS: 
### To monitor QPS (Queries Per Second), you would configure the monitoring client on each of your web servers to specifically track the number of requests they handle per second. This data is then sent to the central monitoring service for display on a dashboard, allowing you to visualize traffic load and set up alerts.

## Issues with this Infrastructure
## SSL Termination at the Load Balancer: 
### Terminating SSL at the load balancer means that traffic is encrypted from the user to the load balancer, but it is unencrypted between the load balancer and your web servers. This is an issue because the data is vulnerable to interception within your internal network. The best practice is to terminate SSL as close to the application as possible.

## Single MySQL Server: 
### The single MySQL server is a Single Point of Failure (SPOF). If it fails, the entire website goes down because the application servers have no data source. To solve this, you would use a primary-replica database cluster.

## Servers with all the same components: 
### Having a single server that hosts the database, web server, and application server is a problem because it creates a tightly coupled system. It's difficult to scale individual components independently. For example, if you need to handle more web traffic, you can't just add another web server; you would need to duplicate the entire server, including the database, which is inefficient. It also creates security risks by exposing the database to the public-facing components.

# Task 3: Scale Up

# External URL
![Scale up Design](https://imgur.com/gallery/scale-up-oHhlQ1h "Scale up")


## Split Components: 
### Split components (web server, application server, and database) onto their own dedicated servers for several key reasons:

## Improved Performance: 
### Each server can be optimized for its specific task without competing for resources with other services.

## Enhanced Scalability: 
### You can now scale each layer independently. For instance, if your web server becomes a bottleneck, you can add another web server without needing to add a new application server or database.

## Better Security: 
### A dedicated database server can be placed in a private network segment, isolated from the public-facing web servers. This significantly reduces its exposure to external threats.








