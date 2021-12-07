# CosmosDB
* Select the appropiate API
* Implement Pariotioning schemes
* interact with data using the SDK
* choose and use the correct consistency level
* scaling
* Stored Procedures, trigger
  
<br>

* NoSql database implementation
* Understanding replication and data distribution
* consistency levels
  * **Strong** ( Everyone has to have commit before any can see it ( regions wide ) )
    Strong consistency offers a linearizability guarantee. Linearizability refers to serving requests concurrently. The reads are guaranteed to return the most recent committed version of an item. A client never sees an uncommitted or partial write. Users are always guaranteed to read the latest committed write.
  * **Bounded** staleness ( Strong but do the stuff after x periode)
    Bounded staleness offers total global order outside of the "staleness window." When a client performs read operations within a region that accepts writes, the guarantees provided by bounded staleness consistency are identical to those guarantees by the strong consistency. As the staleness window approaches for either time or updates, whichever is closer, the service will throttle new writes to allow replication to catch up and honor the consistency guarantee
  * **Session**
    consistency is the most widely used consistency level for both single region as well as globally distributed applications. It provides write latencies, availability, and read throughput comparable to that of eventual consistency but also provides the consistency guarantees that suit the needs of applications written to operate in the context of a user
  * **Consistent** Prefix
    In consistent prefix option, updates that are returned contain some prefix of all the updates, with no gaps. Consistent prefix consistency level guarantees that reads never see out-of-order writes.
    If writes were performed in the order A, B, C, then a client sees either A, A,B, or A,B,C, but never out-of-order permutations like A,C or B,A,C. Consistent Prefix provides write latencies, availability, and read throughput comparable to that of eventual consistency, but also provides the order guarantees that suit the needs of scenarios where order is important.
  * **Eventual** ( Everyone is up to date eventually )
    In eventual consistency, there's no ordering guarantee for reads. In the absence of any further writes, the replicas eventually converge.
    
<br>

* Choosing the right API 
  * **SQL** ( Core )
  If you expect the schema to change a lot, you may want to leverage a document database, making Core (SQL) a good choice (although the MongoDB API should also be considered).
  * **Cassandra**
  This API stores data in **column-oriented schema.** If your application needs to handle high volume, real-time data, Apache Cassandra is an ideal choice. With Azure Cosmos DB Cassandra API, you can use existing Apache drivers compliant with CQLv4, and in most cases, you should be able to switch from using Apache Cassandra to using Azure Cosmos DB’s Cassandra API, by just changing a connection string. You can also continue to use Cassandra-based tools such as cqlsh.
  * **MongoDb**
  This API stores data in a document structure, via BSON format. It is compatible with MongoDB wire protocol; however, it does not use any native MongoDB related code. This API is a great choice if you want to use the broader MongoDB ecosystem and skills, without compromising on using Azure Cosmos DB’s features such as scaling, high availability, geo-replication, multiple write locations, automatic and transparent shard management, transparent replication between operational and analytical stores, and more
  * **Table API**
  This API stores data in key/value format. If you are currently using Azure Table storage, you may see some limitations in latency, scaling, throughput, global distribution, index management, low query performance. Table API overcomes these limitations and it’s recommended to migrate your app if you want to use the benefits of Azure Cosmos DB. Table API only supports OLTP scenarios.
  * **Gremlin**
  If your data model consists of relationships between entities with associated metadata, you’re better off using the graph support in Azure Cosmos DB Gremlin API.
* Troughput with request Units ( 400 default ) RU 1 KB of data

<br>

* Partioning 
  * **Logical**
    A logical partition consists of a set of items that have the same partition key. For example, in a container that contains data about food nutrition, all items contain a `foodGroup` property. You can use `foodGroup` as the partition key for the container. Groups of items that have specific values for `foodGroup`, such as `Beef Products`, `Baked Products`, and `Sausages` and `Luncheon Meats`, form distinct logical partitions.
    There is **no limit** to the number of logical **partitions** in your container. Each logical partition can **store up to 20GB** of data
  * Pysical
    A container is scaled by distributing data and throughput across physical partitions. Internally, one or more logical partitions are mapped to a single physical partition. Typically smaller containers have many logical partitions but they only require a single physical partition. Unlike logical partitions, physical partitions are an internal implementation of the system and they are entirely managed by Azure Cosmos DB.
    * The number of throughput provisioned (each individual physical partition can provide a throughput of up to 10,000 request units per second). The 10,000 RU/s limit for physical partitions implies that logical partitions also have a 10,000 RU/s limit, as each logical partition is only mapped to one physical partition.

    * The total data storage (each individual physical partition can store up to 50GB data).




 