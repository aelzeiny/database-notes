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

In other words, always start with a bread-first look at any problem; including databases.

https://db-engines.com/en/ranking_categories
## Step 1 - Understanding the Categories
In order of popularity, here are the different types of databases **CATEGORIES**:
1) Relational DBMS
2) Document Stores
3) Key-Value Stores
4) Search Engines
5) Wide Column Stores
6) Graph DBMS
7) Time Series DBMS
8) RDF Stores
9) Native XML DBMS
10) Multivalue DBMS
11) Object-Oriented DBMS
12) Content Stores
13) Navigational DBMS
14) Event Stores

Generally speaking, technologies hire on this list overlap with use-cases than technologies lower on the list. For example, Document Stores can store Object-Oriented meta-data rather quite nicely, but the later also exist for their own reason.

###  NoSQL vs SQL
Let's keep this relatively simple. SQL is one of the oldest technologies that we have in CS, and I mean that as a generally positive thing. When I think of relational schemas, I think of inituive and easy-to-deploy technologies that have been optimized to the nth degree, and are the defacto standard for 90% of use cases. I should note that there's an old-school mentality that argues that SQL can do it all, and it's mostly rooted in truth. Generally the strategy is to start here, and move to other alternatives based on necessity.

NoSQL is a general bucket that denotes practically everything else on this list that doesn't fit in the category of Relational DBMS. Perhaps the data you're looking at is too large, decentralized, unstructured, timely, or relationship-centric for SQL to be your #1 choice. So keep an open mind and step forward into the world of DBs.



## Step 2 - Understanding Technologies
