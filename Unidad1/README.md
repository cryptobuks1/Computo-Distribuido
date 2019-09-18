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

The service of the suppliers is not 100% reliable so that if an incident occurs they will ignore it and will pretend that nothing happens in their SLA, so that when monitoring it is possible to have a plan regarding failures.

Establishing an SLO implies that you know what you really want and it involves estimating the construction time of the software that you are going to do, so that when implementing it there are no errors. This way your SLA will be less complicated to solve.

## Video 8

**Class Project: Distributed Chat**

It presents a project that consists of a chat, so that if you use it at the same time as another person on the same server, you can see the messages he sends, these messages are saved and you can search with keywords in the search engine of the chat and related messages will appear.

How does it work?
The infrastructure of the engine and the Google application do a lot of work, the pieces that really had to be created are: an application that runs on users, contains HTML and JavaScript that periodically consults the App Engine infrastructure and asks if there are messages new, and if so, retrieves them and rewrites the HTML to include the messages of that part. The complicated part is the Python application, which is what makes all the server-side logic run and is executed by the Google App Engine infrastructure, this means that when a user requests to send or receive chat messages, he distributes those messages to the user, the messages themselves are stored in the database of the App Engine data store.

Why is this system so good?
First of all, the data warehouse database is highly reliable for our messages, replicates on several hard drives and many machines and has fault tolerance. On the other hand the code is executed in a scalable and fault-tolerant manner of the application, the engine infrastructure works by making copies on multiple machines, rotates more copies if the server load demands it.
The infrastructure also provides a channel termination mechanism that allows each browser to open the connection back to App Engine and receive chat messages as they enter.

Google provides us with several tools that make the job easier, but there is a disadvantage to the cost of App Engine. In this way we have a distributed system, but Google did a lot of work, so if you want to see how a system of this type works and learn, we must build it ourselves.

## Video 9

**Paxos Simplified**


Paxos is a complicated study topic, so a fairly simple example would be to eat in a group, make the decision of what to eat, if some want pizza or hamburgers we must have a solution for this problem, in the same way it happens in a system you have to prevent this type of failures if you have a product sale and two of your computers fail there is no problem if one is still working.
To solve this type of problem, the paxos algorithm is used, with this you can build a multipax that is a record that helps you solve your problems through records of what you do.
In the 1980s Leslie Lamport came up with Paxos and although he saw that he had successfully built a reliable distributed system he did not have a mathematical proof that his system was good.
If you want to build a distributed system there are three options:
Byzantine fault tolerant
Paxos
Database Replication
How does Paxos work?
Suppose we have 3 computers and one of these fails, it will no longer participate in sending messages to the other computers until it is well again, for this it is necessary that you have a memory so that when you join the cluster again, remember where It was that he stayed. It is necessary that the system is adequate to tolerate this type of failure.

What can go wrong?

if a proponent fails, the others continue working normally because each of the phases only awaits the response of some of their peers and not of all,

Another thing that can happen is that if a proponent fails to complete the phase, another proponent will take over once they realize that there is no one progressing anywhere, the protocol will end and it will only do so.

The third case of failure is a proponent that could fail to accept the phase, there are actually two cases to consider. The first case is that the proponent who takes the part above does not realize that the first ever existed and did not receives promising responses, which contains data from a previous one, then it simply runs normally and ends the protocol

## Video 10

**How does Counterstrike work?**

Start with a very simple model Client-Server model each player sits on a computer and that computer records the keystrokes and movements of the player's mouse and sends as a series of keystrokes to a server where the engine of the engine runs game, where it takes all the keystrokes of all the players and simulates the next step in time for the next tic of the game, in this way calculates where the players are now and who shot who and any relevant information, and sends that information back to customers as an instant consequence of the client, in this way the screens are updated to show what happened in the game. It is quite simple as well as the real-time strategy, but this type of system is bad, the information has to be sent to the server and receive the response, but what happens if it is very far from the server, this causes the LAG, this type of systems worked well with the classic games since it was played from a local server, but now the games have become international competitions so that the systems must have a network delay tolerance of up to 200 milliseconds round trip, That is a long time if you are waiting to take the next step.
A more effective way would be through speculation, so that a local server stores the player's keystrokes and compares them to the server on which the game is run, if they are correct, it changes the player's screen to the next step, it is something that often used in distributed systems to improve game performance. But the game is still not perfect, since there is a delay for example if on your screen you are moving and you shoot the other player in which the signal is sent and the response returns, the other player may have moved on his screen and you will not hit the target, you would have to guess where his other movement would be, he would have to have a delay compensation to calculate the movement.

Predict the future?

There are many ways to predict future movements although an important one would be that an AI (artificial intelligence) will take care of that, one of the big problems is the latency of the players since communication goes through the process of going to the server and of back to the players, and if the middleman was eliminated? (the server) this would reduce the lag by half but it generates other problems since it would be easier for hackers to hack their game version.
There are several factors that must be taken into account when pressing the keys to be able to predict the movement of the players, one of them is that if the pulsation is fresh, this is what we mean if that press is useful or not to detect the position of the player.
One thing that can be done is to measure the pulsations by the time, that is to say to each pulsation an hour of the day is assigned to it so it tells us when that happened, we could think that these pulsations can be compared with other pulsations that we keep to see if they are similar, if so we keep them and if not, we throw them, but it is not so since we are not interested in what time the keystrokes that we save in the snapshot are assigned, we are only interested in the time of the last press in that snapshot so we have to attach only the last hit of the keyboard perceived by the server.

Time is hard
To be able to compare the previous point, we should assume that our clocks are paired by milliseconds and that means that our two clocks (those of the keystrokes and the one of the snapshot) must be quite precise this means that we should configure ntp to avoid jumps in the time and to adjust the time automatically or to try to solve synchronization errors.
The synchronization of the clocks is very complicated since the ntp works sending packages in network so the time that it takes of round trip can be prolonged by failures in the network or other common problems. So a simpler way would be to eliminate the clock and only assign numbers to the pulsations in this way if a signal of 9 pressed keys is received, they could be compared with those of another player and thus be able to predict the movement of the players.
