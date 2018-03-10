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
## Step 1 - Understanding the Dimensions
In order of popularity, here are the different types of databases **CATEGORIES**:
1) Relational DBMS (77.5%)
2) Document Stores ()
3) Key Value Stores
3) Wide Column Stores

In order of popularity (as of March 2018), here are the different types of database **MODELS**:
Relational DBMS", y: 137, color: charts_color["Relational DBMS"]},
Key-value stores", y: 65, color: charts_color["Key-value stores"]},
Document stores", y: 44, color: charts_color["Document stores"]},
Graph DBMS", y: 29, color: charts_color["Graph DBMS"]},
Time Series DBMS", y: 23, color: charts_color["Time Series DBMS"]},
RDF stores", y: 19, color: charts_color["RDF stores"]},
Object oriented DBMS", y: 17, color: charts_color["Object oriented DBMS"]},
Search engines", y: 17, color: charts_color["Search engines"]},
Wide column stores", y: 11, color: charts_color["Wide column stores"]}  ]};
Multivalue DBMS", y: 10, color: charts_color["Multivalue DBMS"]},
Native XML DBMS", y: 8, color: charts_color["Native XML DBMS"]},
Navigational DBMS", y: 2, color: charts_color["Navigational DBMS"]},
Content stores", y: 2, color: charts_color["Content stores"]},
Event Stores", y: 2, color: charts_color["Event Stores"]},


SQL vs NoSQL


## Step 2 - Understanding Technologies
