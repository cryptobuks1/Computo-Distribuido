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
