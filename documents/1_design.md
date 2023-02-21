# Design
## Architecture
- Massively parallel processing (MPP) database engine
    - Uses multiple nodes to scale query execution
- Decoupled compute and storage
    - Can scale one without affecting the other
- Tight integration with cloud storage
    - Can move Snowflake integration from one provider to another by changing cloud storage address

## Virtual Warehouse
- Automatic Operation
    - Turn off when inactive
    - Turn on when requireds
- Operations:
    - SELECT
    - INSERT/UPDATE/DELETE/MERGE
    - COPY
- Flexibility and Elasticity
    - Increase compute capacity
    - Increase number of virtual warehouses
- Warehouse sizes
    - Ranges from 1 server/cluster to 256 servers/clusters
    - 1:1 ratio of credit/hour consumed to server/cluster
- Executing DDL does not always require an active virtual warehouse (if it does, Snowflake will start it automatically)
- View table of credits on Snowflake's [price guide](https://www.snowflake.com/pricing/pricing-guide/) documentation

> **Note**  
> Actual monetary cost of a credit depends on the edition of account

## Multiple Virtual Warehouses
- Warehouses do not compete for resources, and have access to all available databases
- In a multi-clustered (enabled) warehouse, Snowflake automatically provisions new clusters to the same warehouse
    - New warehouses do not increase in size or compute power (essentials)
    - Increases concurrecy, not performance

# Tables

## Types:
- Permanent
    - Goes through time travel lifecycle
- Temporary
    - Only goes through time travel lifecycle if sessions remains online
- Transient
    - Behaves like permanent tables, but does have fail safe
- External
    - Metadata only table where the files/records are in the cloud storage

## Table Storage
- Micro-partitions
    - Automatically partitions scheme
    - Data is consumed then split up into chunks of 50MB - 500MB
    - Applies columnar compression
        - Retrieves specific columns when a query is being executed
    - Pruned during query execution based on metadata Snowflake keeps on the values in the micro-partitions

- Clustering Key
    - Orders micro-partition records based on the key
    - Order is maintained by Snowflake
        - Snowflake will automatically monitor and apply reordering to records

> **Note**  
> Clustering keys should be implemented for tables greater than 1TB+  
> The process of monitoring and keeping these keys in order could turn out to be more expensive than the actual benefits of smaller tables

## Lookup Indexes
- Search optimization service **(Enterprise Feature)**
    - Serverless feature
    - Only benefits queries that are using equality predicates
    - Table-level property
        - Useful for finding one to small subsets of records out of millions

- Constraints:
    - Primary Key
    - Unique Key
    - Foreign Key
    - Not Null

> **Warning**  
> The only contraint that is enforced is `Not Null`  
> The other constraints allow you to document your schema in the way it is supposed to be interpreted, but will not be enforced by Snowflake

## Supported Date Types:
- Numeric:
    - Number
    - Integer
    - Float
- String & Binary:
    - Char
    - Varchar
    - Binary
    - Varbinary
- Date & Time:
    - Date
    - Time
    - Datetime
    - Timestamp
- Semi-structured:
    - Variant
    - Array
    - Object
- Spatial:
    - Geography
- Logical:
    - Boolean

## Views
- Normal
    - Similar to traditional relational databases where you specify view code, create it, and on query execution, the view is expanded into the query that is being executed, and the results are returned
- Secure
    - Allows the view you are using to be protected and the data returned will not be leaked to the person querying the data
    - Snowflake will not expand the top query, but will instead get the results and then apply the top query
- Materialized **(Enterprise Feature)**
    - Snowflake saves results permanently and keeps records updated if the underlying data changes

# Code Module Support
- [User-defined functions](https://docs.snowflake.com/en/sql-reference/user-defined-functions)
- [External functions](https://docs.snowflake.com/en/sql-reference/external-functions)
- [Stored procedures](https://docs.snowflake.com/en/sql-reference/stored-procedures)

> **Note**  
> Modules can be coded in SQL or JavaScript

# Definitions:
- Predicate: Expression that evaluates to true, false, or unknown
- Views: A query generated table, that is also queryable