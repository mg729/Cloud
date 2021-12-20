# AWS Database
> [RDS](#RDS)  
> [DynamoDB](#DynamoDB)  
> [Aurora](#Aurora)  
> [Database Types](#types)  


## RDS
- [RDS snapshot](https://aws.amazon.com/ko/premiumsupport/knowledge-center/encrypt-rds-snapshots/)
    - **You can't take an encrypted snapshot of an unencrypted DB instance.** However, you can perform a workaround that achieves the same results. The following steps are applicable to Amazon RDS for MySQL, Oracle, SQL Server, PostgreSQL, or MariaDB.

    - Important: If you use Amazon Aurora, you can restore an unencrypted Aurora DB cluster snapshot to an encrypted Aurora DB cluster. However, you must specify an AWS Key Management Service (AWS KMS) encryption key when you restore from the unencrypted DB cluster snapshot. 
        1.    Open the Amazon RDS console, and then choose Snapshots from the navigation pane.
        2.    Select the snapshot that you want to encrypt.
        3.    Under Snapshot Actions, choose Copy Snapshot.
        4.    Choose your Destination Region, and then enter your New DB Snapshot Identifier.
        5.    Change Enable Encryption to Yes.
        6.    Select your AWS KMS Key from the list.
        7.    Choose Copy Snapshot.

- [RDS Read Replica](https://aws.amazon.com/rds/features/read-replicas)
    - You can reduce the load on your source DB instance by routing read queries from your applications to the read replica. Read replicas allow you to elastically scale out beyond the capacity constraints of a single DB instance for read-heavy database workloads. Because read replicas can be promoted to master status, they are useful as part of a sharding implementation.
    - To further maximize read performance, Amazon RDS for MySQL allows you to add table indexes directly to Read Replicas, without those indexes being present on the master.
### RDS Security - Encryption
> At rest encryption  


-  Possibility to encrypt the master & read replicas with AWS KMS - AES-256 encryption
- Encryption has to be defined at launch time
- If the master is not encrypted, the read replicas cannot be encrypted
- Transparent Data Encryption (TDE) available for Oracle and SQL Server
> In-flight encryption  


- SSL certificates to encrypt data to RDS in flight
- Provide SSL options with trust certificate when connecting to database
- To enforce SSL:
    - PostgreSQL: rds.force_ssl=1 in the AWS RDS Console (Parameter Groups)
    - MySQL: Within the DB: GRANT USAGE ON *.* TO 'mysqluser'@'%' REQUIRE SSL;


## DynamoDB
- Dynamo DB does not perform joins
- ~JSON
### DynamoDB – Time To Live (TTL)
- Automatically delete items after an expiry timestamp


## Aurora
- **Aurora Serverless** – for unpredictable / intermittent workloads
- **Aurora Multi-Master** – for continuous writes failover


## types
- **RDBMS (= SQL / OLTP)**: RDS, Aurora – great for joins
- **NoSQL database**: DynamoDB (~JSON), ElastiCache (key / value pairs), Neptune (graphs) – no joins, no SQL
- **Object Store**: S3 (for big objects) / Glacier (for backups / archives)
- **Data Warehouse (= SQL Analytics / BI)**: Redshift (OLAP), Athena
- **Search**: ElasticSearch (JSON) – free text, unstructured searches
- **Graphs**: Neptune – displays relationships between data