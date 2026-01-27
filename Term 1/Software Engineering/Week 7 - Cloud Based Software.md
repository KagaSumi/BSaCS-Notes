# Cloud
Remote Virtual servers that can be rented
- Rent as many as you need
- Servers an be start-up and shut down as demand changes
- Rent to install your own software or use the products available on the cloud
## Cloud-based Software Characteristics
![[Pasted image 20251021081644.png]]
## Benefits of cloud for software development
### Cost 
You avoid the initial capital costs of hardware procurement
### Startup time
You don't have to wait for hardware to be delivered before you can start work. Using the cloud, you can have servers up and running in few minutes.
### Server Choice
If you find that the servers you are renting are not powerful enough, you can upgrade to more powerful systems. You can add servers for short-term requirements, such as load testing.
### Distributed development
If you have a distributed development team, working from different locations, all team members have the same development environment and can seamlessly share all information
## Implementing a virtual server as a virtual machine
![[Pasted image 20251021081830.png]]
# Container-based virtualization
When running a system with many instances of the same application or services.
>Containers are light weight VMs
## Using Containers to provide isolated service
![[Pasted image 20251021081946.png]]
## Why Containers
![[Pasted image 20251021082017.png]]
### Everything as a service
The idea of a service that is rented rather than owned is fundamental to cloud computing.
#### IaaS
Cloud providers offer different kinds of infrastructure service such as **compute** service, a **network** service and a **storage** service that you can use to implement virutal
#### PasS
This is an intermediate level where you use libraries and frameworks provided by the cloud provider to implement your software. These provide access to a range of functions, including SQL and NoSQL databases.
#### Saas
Your software product runs on the cloud and is accessed by users through a web browser or mobile app.
### Everything is a service
![[Pasted image 20251021082447.png]]
### Management responsibilities for Saas, Iaas, and PaaS
![[Pasted image 20251021082257.png]]
# Saas
![[Pasted image 20251021082503.png]]
![[Pasted image 20251021082532.png]]
## Benefits
### Cash Flow
Customers either pay a regular subscription or pay as they use the software. This means you have a regular cash flow, with payments throughout the year. You don't have a situation where you have a large cash injection when products are purchased but very little income between product releases.
### Update Management
You are in control of updates to your product, and all customers receive the update at the same time. You avoid the issue of several versions being simultaneously used and maintained. this reduces your costs and makes it easier to maintain a consistent software code base.
### Continuous deployment
You can deploy new versions of your software as soon as changes have been made and tested. This means you can fix bugs quickly so that your software reliability can continuously improve.
### Payment Flexibility
You can have several different payment options so that you can attract a wider range of customers. Small companies or individuals need not to be discouraged by having to pay large upfront software costs.
### Try before you buy
You can make early free or low-cost version of the software available quickly with the aim of getting customer feedback on bugs and how the product could be approved
### Data collection
You can easily collect data on how the product is used so identify areas for improvement. You may also be able to collect customer data that allow you to market other products to these customers
## Advantages and Disadvantages for customers
![[Pasted image 20251021084227.png]]
## Data Storage and management Issues for SaaS
### Regulation
Some countries, such as EU countries, have strict laws on the storage of personal information . These may be incompatible with the laws and regulations of the country where the SaaS providers i based. If an SaaS provider cannot guarantee that their storage locations conform with the laws of the customer's country, business may be reluctant to use their product.
### Data Transfer
If software use involves a lot of data transfer, the software response time may be limited by the network speed. This is a problem for individuals and smaller companies who can't afford to pay for very high speed network connections.
### Data Security
Companies dealing with sensitive information may be unwilling to hand over the control of their data to an external software provider. As we have seen from a number of high-profile cases, even large cloud providers have had security breaches. You can't assume that they always provide better security than the customer's own servers.
### Data Exchange
If you need to exchange data between a cloud service and other services or local software applications, this can be difficult unless the cloud service provides an API that is accessible for external use.
## Design Issues for Saas
![[Pasted image 20251021084250.png]]
# Multi-tenant Systems
A multi-tenant database is partitioned so that customer companies have their own space and can store and access their own data

- There is a single database schema, defined by the SaaS provider, that is shared by all of the system's users.
- Items in the database are tagged wit ha tenant identifier, representing a company that has stored data in the system. The database access software uses this tenant identifier to provide 'logical isolation', which means that users seem to be working with their own database.

## Advantages and Disadvantages for multi-tenant databases
### Advantages
#### Resource Utilization
The SaaS provider has control of all the resources used by the software and can optimize the software to make effective use of these resources
#### Security
Multi-tenant databases have to be designed for security because the data for all customers are held in the same database. They are, therefore, likely to have fewer security vulnerabilities than standard database products. Security management is also simplified as there is only a single copy of a the database software to be patched if a security vulnerability is discovered
#### Update Management
It is easier to update a single instance of software rather than multiple instances. Updates are delivered to all customers at the same time so all use the latest version of the software.
### Disadvantages
#### Inflexibility
Customers must all use the same database schema with limited scope for adapting this schema to individual needs. I explain possible database adaptations later in this section.
#### Security
As data for all customers are maintained in the same database, there is a theoretical possibility that data will leak from one customer to another. In fact, there are very few instances of this happening . More seriously, perhaps if there is a database security breach, then it affects all customers.
#### Complexity
Multi-tenant systems are usually more complex than multi-instance systems because of the need to manage any users. There is therefore an increased likelihood of bugs in the database software.
## Multi-Instanced Database
Two Types of multi-instance systems
**Vm-based** multi-instanced systems or **Container-based**
	