---
title: MSRP - MongoDB Storage Resource Provider
seo-title: MSRP - MongoDB Storage Resource Provider
description: Set up AEM Communities to use a relational database as its common store
seo-description: Set up AEM Communities to use a relational database as its common store
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
---

# MSRP - MongoDB Storage Resource Provider{#msrp-mongodb-storage-resource-provider}

## About MSRP {#about-msrp}

When AEM Communities is configured to use MSRP as its common store, user generated content (UGC) is accessible from all author and publish instances without the need for synchronization nor replication.

See also [Characteristics of SRP Options](/help/communities/working-with-srp.md#characteristics-of-srp-options) and [Recommended Topologies](/help/communities/topologies.md).

## Requirements {#requirements}

* [MongoDB](https://www.mongodb.org/):

    * version 2.6 or greater
    * no need to configure mongos or sharding
    * strongly recommend use of a [replica set](#mongoreplicaset)
    * may run on same host as AEM or run remotely

* [Apache Solr](https://lucene.apache.org/solr/):

    * version 4.10 or version 5
    * Solr requires Java 1.7 or greater
    * no service is needed
    * choice of run modes:

        * standalone mode
        * [SolrCloud mode](/help/communities/solr.md#solrcloud-mode) (recommended for production environments)

    * choice of Multilingual Search (MLS)

        * [Installing Standard MLS](/help/communities/solr.md#installing-standard-mls)
        * [Installing Advanced MLS](/help/communities/solr.md#installing-advanced-mls)

## MongoDB Configuration {#mongodb-configuration}

### Select MSRP {#select-msrp}

The [Storage Configuration console](/help/communities/srp-config.md) allows for the selection of the default storage configuration, which identifies which implementation of SRP to use.

On author, to access the Storage Configuration console:

* from global navigation: **Tools, Communities, Storage Configuration**

![](assets/chlimage_1-28.png)

* select **MongoDB Storage Resource Provider (MSRP)**
* **mongoDB Configuration**

    * **mongoDB URI** 
      *default*: mongodb://localhost/?maxPoolSize=10&waitQueueMultiple=5&readPreference=secondaryPreferred
    
    * **mongoDB Database** 
      *default*: communities
    
    * **mongoDB UGC Collection** 
      *default*: content
    
    * **mongoDB Attachment Collection** 
      *default*: attachments

* **SolrConfiguration**

    * ** [Zookeeper](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files) Host** 
      When running in [SolrCloud mode](/help/communities/solr.md#solrcloud-mode) with an external ZooKeeper, set this value to the `HOST:PORT` for the ZooKeeper, such as *my.server.com:2181* 
      For a ZooKeeper Ensemble, enter comma-separated `HOST:PORT` values, such as *host1:2181,host2:2181* 
      Leave blank if running Solr in standalone mode using the internal ZooKeeper.  
      *default*: * &lt;blank&gt;*
    
    * **Solr URL** 
      The URL used to communicate with Solr in standalone mode.  
      Leave blank if running in SolrCloud mode.  
      *default*: https://127.0.0.1:8983/solr/
    
    * **Solr Collection** 
      The Solr collection name.  
      *default*: collection1

* select **Submit**

>[!NOTE]
>
>The mongoDB database, which defaults to the name `communities`, should not be set to the name of a database being used for [node stores or data (binary) stores](/help/sites-deploying/data-store-config.md). See also [Storage Elements in AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md).

### MongoDB Replica Set {#mongodb-replica-set}

For the production environment, it is strongly recommended to setup a replica set, a cluster of MongoDB servers that implements master-slave replication and automated failover.

To learn more about replica sets, visit MongoDB's [Replication](https://docs.mongodb.org/manual/replication/) documentation.

To work with replica sets and learn how to define connections between applications and MongoDB instances, visit MongoDB's [Connection String URI Format](https://docs.mongodb.org/manual/reference/connection-string/) documentation.

#### Example Url for Connecting to a Replica Set  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
#     servers "mongoserver1", "mongoserver2", "mongoserver3" 
#     replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr Configuration {#solr-configuration}

A Solr installation may be shared between the node store (Oak) and common store (MSRP) by using different collections.

If both the Oak and MSRP collections are used intensively, a second Solr may be installed for performance reasons.

For production environments, [SolrCloud mode](/help/communities/solr.md#solrcloud-mode) provides improved performance over standalone mode (a single, local Solr setup).

For configuration details, see [Solr Configuration for SRP](/help/communities/solr.md).

### Upgrading {#upgrading}

If upgrading from an earlier version configured with MSRP, it will be necessary to

1. perform the [upgrade to AEM Communities](/help/communities/upgrade.md)
1. install new Solr configuration files

    * for [standard MLS](/help/communities/solr.md#installing-standard-mls)
    * for [advanced MLS](/help/communities/solr.md#installing-advanced-mls)

1. reindex MSRP  
   see section [MSRP Reindex Tool](#msrp-reindex-tool)

## Publishing the Configuration {#publishing-the-configuration}

MSRP must be identified as the common store on all author and publish instances.

To make the identical configuration available in the publish environment:

* on author:

    * navigate from main menu to `Tools > Operations > Replication`
    * select **Activate Tree**
    * **Start Path:**

        * browse to `/etc/socialconfig/srpc/`

    * select **Activate**

## Managing User Data {#managing-user-data}

For information regarding *users*, *user profiles* and *user groups*, often entered in the publish environment, visit

* [User Synchronization](/help/communities/sync.md)
* [Managing Users and User Groups](/help/communities/users.md)

## MSRP Reindex Tool {#msrp-reindex-tool}

There is an HTTP endpoint for reindexing Solr for MSRP when installing new configuration files or repairing a damaged Solr index.

With this tool, MongoDB is the source of *truth* for MSRP; backups need only be taken of MongoDB.

The entire UGC tree may be reindexed, or only a specifc subtree, as specified by the *path *data parameter.

This tool may be run from the command line using cURL or any other HTTP tool.

When reindexing, there is a tradeoff between memory and performance controlled by the *batchSize *data parameter, which specifies how many UGC records are reindexed per batch.

A reasonable default is 5000:

* if memory is an issue, specify a a smaller number 
* if speed is an issue, specify a larger number to increase speed

### Running MSRP Reindex Tool Using cURL Command {#running-msrp-reindex-tool-using-curl-command}

The following cURL command shows what is necessary for an HTTP request to reindex UGC stored in MSRP.

The basic format is:

cURL -u *signin * -d *data * *reindex-url*

*signin* = administrator-id:password  
for example: admin:admin

*data *= "batchSize=*size*&path=*path"*

*size* = how many UGC entries to reindex per operation  
`/content/usergenerated/asi/mongo/`

*path* = the root location of the tree of UGC to reindex  

* to reindex all UGC, specify the value of the `asipath`property of  
`/etc/socialconfig/srpc/defaultconfiguration`  
* to limit the index to some UGC, specify a subtree of `asipath`

*reindex-url* = the endpoint for reindexing of SRP  
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>If you are [reindexing DSRP Solr](/help/communities/dsrp.md), the URL is **/services/social/datastore/rdb/reindex**

### MSRP Reindex Example {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex

```

## How To Demo MSRP {#how-to-demo-msrp}

To setup MSRP for a demonstration or development environment, see [HowTo Setup MongoDB for Demo](/help/communities/demo-mongo.md).

## Troubleshooting {#troubleshooting}

### UGC Not Visible in MongoDB {#ugc-not-visible-in-mongodb}

Make sure MSRP has been configured to be the default provider by checking the configuration of the storage option. By default, the storage resource provider is JSRP.

On all author and publish AEM instances, revisit the [Storage Configuration console](/help/communities/srp-config.md) or check the AEM repository:

* in JCR, if [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

    * does not contain an [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) node, it means the storage provider is JSRP
    * if the srpc node exists and contains node [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), the defaultconfiguration's properties should define MSRP to be the default provider

### UGC Disappears after Upgrade {#ugc-disappears-after-upgrade}

If upgrading from an exisitng AEM Communities 6.0 site, any pre-existing UGC must be converted to conform to the structure required for the [SRP](/help/communities/srp.md) API after upgrading to AEM Communities 6.3.

There is an open source tool available on GitHub for this purpose:

* [AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

The migration tool can be customized to export UGC from earlier versions of AEM social communities for import into AEM Communities 6.1 or later.

### Error - undefined field provider_id {#error-undefined-field-provider-id}

If the following error is seen in the logs, it indicates the Solr schema file is not properly configured.

#### JsonMappingException: undefined field provider_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

To resolve the error, when following the instructions for [Installing Standard MLS](/help/communities/solr.md#installing-standard-mls), ensure

* the XML configuration files were copied to the correct Solr location
* Solr was restarted after the new configuration files replaced the existing ones

### Secure Connection to MongoDB Fails {#secure-connection-to-mongodb-fails}

If an attempt to make a secured connection to the MongoDB server fails due to a missing class definition, it is necessary to update the MongoDB driver bundle, `mongo-java-driver`, available from the public maven repository.

1. download the driver from  
   [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar)  
   (version 2.13.2 or later)

1. copy the bundle into the "crx-quickstart/install" folder for an AEM instance
1. restart the AEM instance

## Resources {#resources}

* [AEM with MongoDB](/help/sites-deploying/aem-with-mongodb.md)
* [MongoDB Documentation](https://docs.mongodb.org/)
