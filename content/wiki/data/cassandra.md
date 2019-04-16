---
title: Cassandra Database
description: Getting started with the Cassandra NoSQL database
---

Concepts
--------

| Cassandra      | SQL
|----------------|-------------
| Keyspace       | Database
| Column Family  | Table
| Row            | Partition
| Column         | Cell

| Data Types     |
|----------------|
| text / varchar |

Querying across partitions can be slow.

TTL


# Cassandra Query Language (CQL)

* Primary key determines the partition
* Primary key can be composite, in which case, first part of the primary key determines the partition.

## PRIMARY KEY

| Fields                    | Key type                                                               |
|---------------------------|------------------------------------------------------------------------|
| Id                        |  Id = Partition Key                                                    |
| (Id, Name)                | Id = Partition Key, Name = Clustering column                           |
| ((Id, Name), Description) | Id + Name = Partition Key (Composite), Description = Clustering column |

## INSERT & UPDATE

* Functionally equivalent.
* Updates do not overwrite, deletes do not remove.

Lightweight transaction, using Paxos protocol:

```cql
INSERT INTO users (username, email) VALUES ('jane', 'jane@doe.com') IF NOT EXISTS;
```

Filtering / Querying
--------------------

Can query on partition key, clustering columns and indexed columns.

You can't filter by columns that aren't part of the keys, and they must be in order.

e.g. if your key is like so:

PRIMARY KEY (Id, Timestamp, IsDisabled)

Then querying just on "Id" and "IsDisabled" will give you the error:

PRIMARY KEY column \"isdisabled\" cannot be restricted (preceding column "timestamp" is not restricted)

You can query on:

Id
Id / Timestamp
Id / Timestamp / IsDisabled

Error:

"Cannot execute this query as it might involve data filtering and thus may have unpredictable performance. If you want to execute this query despite the performance unpredictability, use ALLOW FILTERING"

This happens when you query on a field but you're not filtering on the primary key; it may mean a scan across all nodes.

Ordering
--------

Partition keys are not ordered.
Clustering columns are ordered
Can order query by clustering columns
Default order on schema ``WITH CLUSTERING ORDER``

Pagination
----------

Default limit is 10k

Performance
-----------

| Fast                               |  Slow                           |
|------------------------------------|---------------------------------|
| Query over single partition        |  Query over multiple partitions |
| Range query over clustered columns | Secondary indexes?              |

Recipes
=======

Count
-----

``nodetool --host <hostname> cfstats``

or

```cql
SELECT COUNT(*) FROM columnfamily (slow)
```

Troubleshooting
---------------

Enable tracing with ``TRACING ON``

Example
-------

```cql
INSERT INTO users (username, email) VALUES ('jane', 'jane@doe.com') IF NOT EXISTS;
```

Another:

```cql
    CREATE TABLE IF NOT EXISTS Items
    (
        Id uuid,
        FeedId uuid,
        Timestamp timeuuid,
        Name text,
        Guid text,
        DatePublished timestamp,
        DateModified timestamp,
        Content text,
        SanitizedContent text,
        Uri text,
        Author text,
        Enclosure text,
        EnclosureType text,
        EnclosureMimeType text,
        EnclosureLength bigint,
        PRIMARY KEY (Id, FeedId)
    );
```