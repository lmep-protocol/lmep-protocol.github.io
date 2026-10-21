# Analysis and Product Identification

## Statement of the Problem

Cloudrain is a cloud storage provider. The CEO of Cloudrain, Marcus Church, and I had a meeting about the issue of communication between different departments, and he believes that the throughput of his company has been hindered by the labyrinth of different messaging protocols and platforms being used by different departments.
He thinks this is because different departments have varying degrees of technical proficiency and use a variety of different hardware.
Some departments rely on older messaging platforms because they use legacy hardware.
Other departments, such as finance, which use modern messaging platforms only within their own departments, still must use older instant messaging protocols to communicate with other departments. Church has asked me to develop an instant messaging protocol for them, which is able to run on older hardware and simultaneously facilitate the needs of modern instant messaging. After meeting with him, these are the main points I have taken away:

* Current protocols which run on legacy hardware do not facilitate modern instant messaging needs, such as pinned messages and replies
* The new instant messaging protocol needs features which would facilitate these needs but needs to be minimal enough to run on legacy hardware. Features would include: replies, permissions management, statuses and presence tracking, and pinned messages.
* The administrator would need a way to create text channels and have permissions to manage them, whilst ordinary employees do not have these permissions.

### Why not upgrade legacy hardware?

Church has pinned down his hesitation to upgrade legacy hardware to four main reasons:

* High replacement costs: Replacing computers across entire departments is expensive, considering that not only workstations have to be replaced but also entire programs and suites of software. This could mean that upgrading hardware might require purchasing new software licences, migrating data and re-training employees.
* Legacy software dependencies: The records and archives department maintains its own in-house archival database software. Upgrading hardware would mean employees within that department would have to spend more time refactoring their code to work on modern hardware instead of archiving company data.
* Operational disruption: Cloudrain performs backups and archives data daily. Upgrading hardware would introduce downtime, which would increase complexity regarding archiving recent data.

## My solution

I will create an instant messaging protocol, which I will name “LMEP” (Lightweight Message Exchange Protocol), where clients can log in with their credentials.
This protocol must be implementable on text-only environments.
If they do not have credentials, they can issue requests to the server to create them. Once they log in, they will be able to access different chatrooms under a single space (named the “chathome”).
They can message others using the chatrooms they have the permissions to access.
There will also be an option to enable and disable TLS (Transport Layer Security) encryption for the server administrator, which can secure messages and data from potential malicious attackers (as plaintext communication is never inherently secure).
Alongside this will also exist the ability to create multiple chathomes under one server, so the heads of different departments can manage their own department’s chathome without managing the chathomes of other departments.  
This protocol will be decentralised. By decentralised, I mean that each server manages their own database of credentials without interaction between servers (known as federation. Federation is not supported by the submitted version of LMEP). This improves the security of the model, since if one LMEP server is compromised, fewer users are affected because credentials are not synchronised between servers.
To accompany a specification for this protocol, I will write a reference implementation so that it is evident that such a protocol works and to assist those who may be interested in implementing LMEP.

## Stakeholders

The stakeholders of LMEP are important because they are the people that are affected by, or have an interest in, it.

### My client

Church is the main stakeholder of the LMEP protocol.
He will be using an LMEP client to communicate with department managers through company-wide or executive chathomes.This is because one aim of the system is to have multiple chathomes under one server, meaning that departments do not interfere with each other when connected to the same server, each department will have its own chathome, and each chathome will be managed by its respective manager of said department (see below under Heads of Departments).
Since he requires a system to ensure that employees can easily access announcements and other important information, I will need to implement a pinned messages feature, where such pinned messages are stored separately from regular messages, so that other LMEP clients can retrieve them by issuing commands (see below under LMEP Model) to the LMEP server. 
Church will also need a way of organising messages and business decisions. For this reason, I will also implement a replies feature, where messages can directly reply to other messages so it is clear who is talking to whom.

### Heads of departments

The department managers at Cloudrain are also a stakeholder for this protocol.
They will be using the reference implementation of LMEP to centrally manage the chathome for their department, whilst making sure that only they have the ability to manage chathomes.
Because of this, LMEP will have permissions tracking, where each member of a chathome will be assigned a database entry which manages what they can and cannot do on a chathome, such as deleting messages and renaming chatrooms.
If an LMEP client requests administrative operations from a server, the server will check the client has the sufficient permissions for it, only performing the action if so.
Since there will almost certainly be people with similar names in the same department, a manager of a department will need to distinguish between the two when managing users on a chathome.
For this reason, LMEP will require that each server issue each user within a chathome a Universally Unique Identifier (UUID). A UUID will only be used to identify users globally across a server, it cannot be used as an authentication mechanism, as clients still must authenticate with servers through password. UUIDs are mandated so that even when two or more people have the same name on a server, they show up on the database as distinct entries, rather than the same entry. This will therefore simplify chathome administration.

### Employees

The employees of Cloudrain are a stakeholder for this protocol. They will be using the reference implementation of LMEP to exchange messages. This will especially benefit the Records and Archives department because it means that employees of that department do not have to upgrade their hardware in order to communicate with other departments.
They will be using the reference client implementation of LMEP to organise their messages into different chatrooms to modularise information.
To facilitate this, the reference implementation will have chatroom IDs to identify a chatroom inside of a chathome. This is so that LMEP clients can send messages in a chatroom without messages in one chatroom appearing inside another.
One problem I may run into is the level of technical literacy that employees in different departments may have. For example, employees in the sales department may be less technically inclined than their IT department counterparts. My solution to this is creating an implementation of the LMEP protocol with a simple frontend which abstracts the details of the LMEP protocol from clients so they can focus on sending messages on others. 
To make sure that the employees have the necessary skills to navigate using an LMEP client, I will create comprehensive documentation which will be made available on this website. This will go into details about how to set up an LMEP client, but also the more technical details of LMEP for the more technically proficient. 
Additionally, the reference client implementation will have an intuitive interface tested with representative users.
