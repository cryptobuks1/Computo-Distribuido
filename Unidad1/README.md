**DOCUMENTATION VIDEOS**

## Video 1

**What is a distributed system?**
A system that is divided into several computers in such a way that it is not a centralized system, since its processes run on different computers.
example: save a file to your computer, if it fails your file will be lost unless the hard drive is not damaged and can be recovered in some way.
In a distributed system your document would be stored in the cloud, so that if your computer will stop serving, you will still have access to your files from any other computer.

## Video 2

**Why build a distributed system?**
Your job manager asked you: it's a duty you have at work.
You think it is fun to learn to create one: you feel interest in learning something new.
You need a server: you also need a server for the system
 Legal or privacy reasons: reliable information
Align user incentive costs: monetary interests.
Activity Time Requirements
Performance (latency and bandwidth).
You are building only part of a system you trust in the cloud.
Reliability
Scalability

## Video 3

**How to learn distributed systems?**

How systems fail: Systems that use only one computer fail, so you need to build a system tolerant to these failures in such a way that using a well-built distributed system you can get to tolerate these failures.

## Video 4

**What could go wrong?**
It is explained that it could go wrong in a distributed system.
All of the following errors can occur in a distributed system but they are very rare to happen.

-  Crash - Or Crash Loop
- Server down
- Query of death
- Data corruption
- Broken dependency
- Two attack
- Cascading failure
- Data loss
- Certificate Expires
- Runaway automation
- Natural Disaster
- Time travel
- Police raid
- Very Important User data loss.

## Video 5

**Different types of failures**

Some of the different faults can be divided into the following two groups.
Network failures and node failures, it is convenient to divide the failures into these two groups because you can hire network engineers and software engineers to solve these failures.

- Network failures:
There are a large number of ways in which the network can fail and lose large numbers of packets, you can have routing problems, network congestion and cause network collapse, there are countless things that can fail in the network, the number of failures can increase if you have a very large distributed system that connects in several countries,

--How a loss of connection to the distributed system affects.
The network consists of interconnected nodes which communicate with each other if some of the nodes fail can lose communication with other nodes and affect the entire network, due to partitions in the nodes.

--A distributed system minimizes the failure of network falls, separating the connection into several groups of nodes in which if any failure can be connected to other nodes of the group or to another group while trying to recover the defective node.

##  Video 6
**Tolerance to Byzantine faults**

The system must be built in such a way that it will tolerate failures, to provide security in the data that is handled, that when someone tries to do something malicious inside the system, they will realize what happened.
Within this type of common failures in this type of systems we find the failures in some node in such a way that you have to look for the way that does not affect the communication between the other nodes

## Video 7

**SLIs SLOs and SLAs**

These systems are used to measure the performance and reliability of your distributed system, if you do not measure the performance of your distributed system in future updates you will not know how to improve it and therefore end up improving unnecessary parts of the system so it is advisable to analyze its performance, functionality and reliability.

SLI: It is a service level indicator thanks to this we can measure for example if the user is having an excellent service based on the objectives of our system, we can also measure how long it takes a response from our system to the user.

SLO: It is a service level objective, how well we want to improve the service level, it is used to set objectives at the service level.
Example; 99% of the times a user requests a service to the system we want the response to be less than 500 milliseconds.

SLA: An SLA (Service Level Agreement) is an SLO + Consequences, what would happen if we lost our objective, how it would affect the user, the system should work as described, if you do not comply with the SLO you could pay all the problems that arise for the user based on the objective defined in the system

Why study SLIs, SLOs, SLAs?
The first point is because if we can measure it, it can be improved and if you do not measure it is really difficult to improve, we will not know if we are improving, in second if you do not know what part of the system to improve then you could be wasting your time in improving parts of the system that they don't improve at all, or you could end up making a more robust system than is needed.

To make use of the correct implementation of SLA, it is necessary to have personnel in charge of monitoring the possible failures of different suppliers to solve them as quickly and effectively, which requires a lot of investment to obtain a high level of reliability.
