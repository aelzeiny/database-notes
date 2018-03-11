# Database Research

## Ranting my Frustrations as an Engineer

It is this developer's personal opinion that we're at the point that these labels have such far-reaching implications that the zeitgeist has stripped the definitions from all meaning.

Eventual Consistency, High Avalibility, Physical Partioning, Hadoop, Hive, Pig, Sharding, **BIG DATA**. We once lived in a world where SQL was the only palletable flavor for data storage. In the past few years the volume of vocabulary in Computer Science has finally started to match the implications of a world interconnected by technology.

Here's some statements that I have heard in my short time in tech:
 * NoSQL is just a meme at this point
 * DynamoDB is objectively the best NoSQL solution
 * CouchDB is better than MongoDB

## Engineering Philosophy

Solid engineering fundamentals tells us that is more important to understand the pros-and-cons for every technology than it is to know one standard really well. Keep in mind that engineering always starts as the problem; you don't really need to know how every technology works in depth in order to understand when to apply it.

This is a controversial statement for a lot of academics, but most folks that use hash-maps every day have little understanding of the underlying nuances this data-structure in [a typed vs a dynamic language](https://developers.redhat.com/blog/2017/02/27/towards-faster-ruby-hash-tables/). O(1) Lookup and unique elements is all you *really* need to know about a hash in any language; the rest will rarely ever come in handy.

In other words, start with a bread-first look at any problem; including databases.

https://db-engines.com/en/ranking_categories
## Step 1 - Understanding Vocabulary

###  NoSQL vs SQL
Let's keep this relatively simple. SQL is one of the oldest technologies that we have in CS, and I mean that as a generally positive thing. When I think of relational schemas, I think of inituive and easy-to-deploy technologies that have been optimized to the nth degree, and are the defacto standard for 90% of use cases. I should note that there's an old-school mentality that argues that SQL can do it all, and it's mostly rooted in truth. Generally the strategy is to start here, and move to other alternatives based on necessity.

NoSQL is a general bucket that denotes practically everything else on this list that doesn't fit in the category of Relational DBMS. Perhaps the data you're looking at is too large, decentralized, unstructured, timely, or relationship-centric for SQL to be your #1 choice. So keep an open mind and step forward into the world of DBs.

### ACID-ity
Oh boy, more acronyoms. These 4 letters denote the properties that are so coveted about databases, and what makes them different from reading/writing to a CSV on your HDFS. Keep in mind that Data is precious, and thus the technologies we entrust to carry them must have certain protections.

**Atomicity** - "All or nothing" transactions. If the 99th mutable query fails in a series of 100, then I'd rather "rollback" the effects of the previous 99 queries than to encounter a half-completed state.

**Consistency** - Databases transition from one valid state to another; always respecting its own rules and constraints. No such "half-true" states.

**Isolation** - A database is allowed (and should be) multithreaded, but transactions should be executed as if encountered one-by-one. This means that 'conflicting' queries must be either resolved or terminated.

**Durable** - Once a transaction is commited, it will be stored perminantly. Whether in the case of power loss or errors, my data remains safely and durably stored.

### Brief and shallow look into SQL Scaling
"Scalability" is another one of those words that has lost all meaning because it just means everything. I'll try to skim the surface here, as to not drown this entire article with caveats, exceptions, and expectations. Suppose that my current database is starting to reach the extents of its tolerance. I can choose to react in one of two ways.

(A) If my problem is a memory problem then maybe I buy bigger and/or better RAM. Say I have a reading or writing problem, then maybe I buy bigger and/or better harddrives and implement RAID 0 on my servers. If I'm using a cloud-service with Azure/AWS/Google then maybe I give them money for a bigger and/or better server. This is what we call **Vertical Scaling**, because I'm throwing money at my one server, thus dodging the issue entirely. If done well, this can get you a lot of milage.

(B) If I'm using a traditional SQL solution, the absolute last thing I want to do is **Horizontal Scaling**. At best this means that I implement a leader-follower replication system on my servers to prospone the issue. At worst this means that we have to go full-blown denormalization and sharding; which (while entirely possible) SQL does not handle gracefully. Quite arguably, this is one of the biggest arguments against SQL in the modern 'web-scale' era.

## Step 2 - **C**onsistency, **A**valiability and **P**artition Tolerance

**Consistency** - A read executed on any node will return the same result. Not to be confused with ACID's consistency.

**Availability** - Every request gets a response from the client despite success or failure in a reasonable amount of time.

**Partition Tolerance** - Horizontal scaling, by adding or subtracting more physical partitions, does not cripple the system. This is what people talk about most when they bring up 'web-scale' and 'sharding'.


Once upon a time the CAP theorem was proposed as a standard for choosing databases. The basic premise was that you can only pick two from the three 
DB properties, and there was no such thing as a perfect solution. SQL traded 'P' for 'C' and 'A', and NoSQL technologies were each either trading 'C' or 'A' to get 'P' back.

Such a theory was relevant back then, but now we like to say that the tradeoffs between 'CAP' are technology-specific. Sorry, but choosing a database just became a lot less binary.

One such reason why such a theorem was considered popular was because of the assumptions we placed on distributed computing and networking back then, and another attributes the change to revolution beyond SQL. In any case, you should still prioritize. Try to rank the three properties in order of importance to your needs. This will certainly come in handy down the line.

## Step 3 - Start with Categories, not Models
In order of popularity, here are the different types of databases **CATEGORIES**:
1) **Relational DBMS** - We all know and love RDBMS's; perhabs a bit too much
2) **Document Stores** - Specifically intented to solve the problem of storing and querying unstructured data. It doesn't really make sense to have a column with 1 million nulls and 1 value, because relational databases are optimized to read from left-to-right, and top-to-bottom. Document stores are often denormalized by design, and thus are argued to scale better than SQL systems (I'm oversimplfying a bit here). 
3) **Key-Value Stores** - Really good if the primary index for quering is, and will only be, based on a primary key. These stores don't need a large query interpreter, and are great for storing and scanning large structured/unstructured data quickly in real-time with great simplicity. 
4) **Search Engines** - Support for complex search expressions through full-texts grouped, filtered, and ranked results with high scalability.
5) **Wide Column Stores** - Columnar databases work really well for scans or really-large data sizes. The large amount of columns means that all joins must be done post-query.
6) **Graph DBMS** - Graph Databases are relation-ship driven databases that use a hybrid of database models to accomplish a graph-like association. LeanTaas, the company I work for, uses Graph databases to model the complex administrative hierarchies that are commonly found within hospitals. I have to say, this sure beats the hell out of having hundreds of SQL junction tables for sparse relationships.
7) **Time Series DBMS** - If the primary of all incoming information is a datetime object such that newer infromation is prioritized over older entries.
8) **RDF Stores** - Stores tuplets (AKA semantic graph databases) use a subject-predicate-object definition to define relationships. The best way I can describe the power of modeling data via human language is by example: "Bob is Joe" or "Joe likes John". The subject is the starting node, the predicate is the edge, and the object is the ending node. Unlike Graphs, Verticies and Edges here have no internal structure, and are thus really efficient to query and traverse based purely on relationships.
9) **Native XML DBMS** - I'm choosing to ignore this
10) **Multivalue DBMS** - I'm choosing to ignore this
11) **Object-Oriented DBMS** - Meant to store/load object-oriented models directly to/from a database. I'm choosing to ignore this
12) **Content Stores** - I'm choosing to ignore this
13) **Navigational DBMS** - I'm choosing to ignore this
14) **Event Stores** - I'm choosing to ignore this

Generally speaking, technologies hire on this list overlap with use-cases than technologies lower on the list. For example, it is possible for SQL technologies to store a lot of the relationships that Graph DBs and RDF stores are adept at, and Document Stores can persist object-oriented meta-data rather quite nicely. However, that the later also exist for their own reason. *The Principle of Sufficient Reason* argues that if it exist, then there must be a reason. Applied to Databases, this can be interpretted as "if it exists, then it must do something that standard SQL does not do well". 
Alright, do you have an idea of what you want now? Let's start by figuring out what people have been talking about. I once again remind the reader of the principal *The Principle of Sufficient Reason* for databases; if it exists then it does something that standard SQL doesn't do well.

### Visualizing the Zeitguist as of 2018

[INSERT VISUALIZATION #1]

Some Observations:
Understandably, with the increasing popularity of IOT, Time Series DBMS's are becoming a bit more popular. This type of database allows for high throughput of time-indexed data such that older data is less prioritized than newer data.

Columnar (Wide-Column) Databases, Key-Value stores, and Document stores are the epitome of what people mean when they talk about "NoSQL" solutions, because none of these technologies need or use joins. Key-Value stores are great if you only query based on one primary key, and nothing else. Document stores are fantastic for unstructured data. Columnar databases are well designed to scan large  data-sets of data from top-to-bottom rather than from left-to-right.

## Step 4 - Technologies and Models

[INSERT VISUALIZATION #2]