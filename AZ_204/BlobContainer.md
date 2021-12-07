# Blob Storage
* Move items betweens accounts or containers
* set and retrive properties and / or metadata
* Interact with data using the SDK
* implement data archiing and retention
* Hot, cool and Archive storage

## Storage Types 
* **Container**
* **Table** 
  Azure Table storage stores large amounts of structured data. The service is a NoSQL datastore which accepts authenticated calls from inside and outside the Azure cloud. Azure tables are ideal for storing structured, non-relational data. Common uses of Table storage include:
* **File**
    Azure Files enables you to set up highly available network file shares that can be accessed by using the standard Server Message Block (SMB) protocol. That means that multiple VMs can share the same files with both read and write access. You can also read the files using the REST interface or the storage client libraries.

    One thing that distinguishes Azure Files from files on a corporate file share is that you can access the files from anywhere in the world using a URL that points to the file and includes a shared access signature (SAS) token. You can generate SAS tokens; they allow specific access to a private asset for a specific amount of time.
* **Queue**
The Azure Queue service is used to store and retrieve messages. Queue messages can be up to 64 KB in size, and a queue can contain millions of messages. Queues are generally used to store lists of messages to be processed asynchronously.

## Plan
* **General Purpose**
Standard storage account type for blobs, file shares, queues, and tables. Recommended for most scenarios using Azure Storage. Note that if you want support for NFS file shares in Azure Files, use the premium file shares account type.
* **Block Blob**
Premium storage account type for block blobs and append blobs. Recommended for scenarios with high transactions rates, or scenarios that use smaller objects or require consistently low storage latency. Learn more about example workloads.
* **File Storage**
Premium storage account type for file shares only. Recommended for enterprise or high-performance scale applications. Use this account type if you want a storage account that supports both SMB and NFS file shares.
* **Blob Storage**
Azure Blob storage is Microsoft's object storage solution for the cloud. Blob storage is optimized for storing massive amounts of unstructured data. Unstructured data is data that doesn't adhere to a particular data model or definition, such as text or binary data.

## Redundancy
* **Locally Redundant Storage ( LRS )**
    copies your data synchronously three times within a single physical location in the primary region. LRS is the least expensive replication option, but is not recommended for applications requiring high availability or durability. 
* **Zone Redundant Storage ( ZRS )**
    copies your data synchronously across three Azure availability zones in the primary region. For applications requiring high availability, Microsoft recommends using ZRS in the primary region, and also replicating to a secondary region.
* **Geo Redundant Storage ( GRS )**
    Geo-redundant storage (GRS) copies your data synchronously three times within a single physical location in the primary region using LRS. It then copies your data asynchronously to a single physical location in a secondary region that is hundreds of miles away from the primary region. GRS offers durability for Azure Storage data objects of at least 99.99999999999999% (16 9's) over a given year.

    A write operation is first committed to the primary location and replicated using LRS. The update is then replicated asynchronously to the secondary region. When data is written to the secondary location, it's also replicated within that location using LRS.
* **Read Access Geo Redundant ( RA-GRS )**
    Geo-redundant storage (with GRS or GZRS) replicates your data to another physical location in the secondary region to protect against regional outages. However, that data is available to be read only if the customer or Microsoft initiates a failover from the primary to secondary region. When you enable read access to the secondary region, your data is available to be read at all times, including in a situation where the primary region becomes unavailable. For read access to the secondary region, enable read-access geo-redundant storage (RA-GRS) or read-access geo-zone-redundant storage (RA-GZRS).
* **Geo-zone Redundant Storage ( GZRS )**
    Geo-zone-redundant storage (GZRS) combines the high availability provided by redundancy across availability zones with protection from regional outages provided by geo-replication. Data in a GZRS storage account is copied across three Azure availability zones in the primary region and is also replicated to a secondary geographic region for protection from regional disasters. Microsoft recommends using GZRS for applications requiring maximum consistency, durability, and availability, excellent performance, and resilience for disaster recovery.

    With a GZRS storage account, you can continue to read and write data if an availability zone becomes unavailable or is unrecoverable. Additionally, your data is also durable in the case of a complete regional outage or a disaster in which the primary region isn't recoverable. GZRS is designed to provide at least 99.99999999999999% (16 9's) durability of objects over a given year.
* **Read Acess geo-zone Redundant Storage (RA-GZRS )**
    Geo-redundant storage (with GRS or GZRS) replicates your data to another physical location in the secondary region to protect against regional outages. However, that data is available to be read only if the customer or Microsoft initiates a failover from the primary to secondary region. When you enable read access to the secondary region, your data is available to be read at all times, including in a situation where the primary region becomes unavailable. For read access to the secondary region, enable read-access geo-redundant storage (RA-GRS) or read-access geo-zone-redundant storage (RA-GZRS).
* SLA's Tiers
  * Hot ( 99.9 )
  * Cool 99 GRS 99.99 RA-GRS

## Durability and availability by outage scenario
The following table indicates whether your data is durable and available in a given scenario, depending on which type of redundancy is in effect for your storage account:

| Outage  scenario | 	LRS |	ZRS |	GRS/RA-GRS | 	GZRS/RA-GZRS |
|------------------|-------|-------|--------------|-----------------|
|A node within a data center becomes unavailable|	Yes |	Yes  |	Yes |	Yes|    
|An entire data center (zonal or non-zonal) becomes unavailable|	No |	Yes |	Yes1 |	Yes|
|A region-wide outage occurs in the primary region|	No	| No |	Yes1|	Yes1|
|Read access to the secondary region is available if the primary region becomes unavailable|	No|	No|	Yes (with RA-GRS)|	Yes (with RA-GZRS)|

1 Account failover is required to restore write availability if the primary region becomes unavailable. For more information, see<a href="https://docs.microsoft.com/en-us/azure/storage/common/storage-disaster-recovery-guidance"> Disaster recovery and storage account failover.</a>

## storage account support a range of redundany options
See <a href="https://docs.microsoft.com/en-us/azure/storage/common/storage-redundancy#supported-storage-account-types">Supported Azure Storage services</a>

## Storage account types are only supported by specific account types
See <a href="https://docs.microsoft.com/en-us/azure/storage/common/storage-redundancy#supported-azure-storage-services">Supported storage account types</a>

## how to acces storage account from code 
1 You need an account ( connection string to the storage account) ( Acces client)

2 You need a Container ( Container client )

3 You need a Blob Client

```
var serviceclient = new BlobServiceClient(connectionString);
var containerName = 'MyUniqueContainerName'
var containerClient = await serviceClient.CreateBlobContainerAsync(containerName);
var blobClient = containerClient.GetBlobClient("myFileName");
using FileStream stream = File.OpenRead(localPath);
await blobClient.UploadAsync(stream, true);
stream.close();
```

SAS Token ?
CLI / PS COmmand to create BlobContainer
AzureSQL Vs NoSql