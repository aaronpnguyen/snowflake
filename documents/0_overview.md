# Overview
## Introduction
- Fully managed cloud platform
- No need for ongoing component adminstration
- Able to be implemented in AWS, Azure, and Google Cloud
- Deployed by vendor
    - No additional setup other than infrastructure needed
- No access to underlying OS or hardware
    - No need to maintain underlying components
- Data platform
    - Includes a data warehouse, lake, processing, and sharing

## Core Services
- Virtual Warehouses
    - Anytime you are interacting with the data, you need a virtual warehouse setup
- Snowpipe

## Tools
- Web Portal
- SnowSQL
- Connectors/Drivers

# Billing Model
- Storage
    - Pay for data you are storing
    - Flat rate per terabyte, depends on:
        - Region
        - Payment plan
    - Snowflake time travel
        - Enables access to data that has been changed or deleted at any point within a defined period
    - Snowflake fail-safe
        - Recovery from a catastrophic incident like storage failure, corruption, or security breach (last resort measure)
        - The only team that has access to this is Snowflake support, we no longer have access to data here.
    - Countinous data protection
        - Active Data -> Time Travel -> Fail-Safe

- Compute
    - Number and size of virtual warehouses
    - Serverless features
        - Background table maintenance
        - Database replication
        - Snowpipe
    - Cloud (core) services
        - Authentication and authorization
        - Infrastructure management
        - Query parsing and optimization
        - Only charged if usage exceeds 10% of your daily compute consumption
    - Snowflake credit
        - Depends on account edition, region, and payment plan
        - Credits are billed per second, with a **1 minute minimum**.

- Data Transfer
    - Data transfer egress is a chargeback from the cloud provider (AWS, Azure, GCP). Usually only charged when the data leaves the cloud region
    - This is charged when you take data out from the region it was stored from

- Please refer to Snowflake's official [price guide](https://www.snowflake.com/pricing/pricing-guide/) for more information

# Editions
- Standard
    - SQL data warehouse engine
    - Encryption in transit and at rest
    - All system tools available
    - 1 day of time travel

- Enterprise
    - Standard +
    - Materialized views, data masking, point-lookup optimization
    - Multi-cluster warehouses
    - Periodic rekey of encryption
    - *Up to* 90 days of time travel

- Business Critical
    - Enterprise +
    - HIPAA and PCI support (shared responsibility model)
    - Customer-managed keys
    - AWS and Azure private links (publishes private endpoints into VPC/VN)
    - Disaster recovery failover and failback between regions and cloud providers

- Virtual Private Snowflake
    - Business Critical +
    - Dedicated metadata store and pool of virtual servers
    - Isolated environment from all other Snowflake accounts

# Definitions:
- Active Data: Data that is active until it is changed
- Fail-Safe: A Snowflake feature, wheere expired data from time-travel is automatically moved to after expiration. The only way to access data within fail-safe is by contacting Snowflake support
- Snowpipe: Enables data loading as soon as they're available
- Time Travel: A Snowflake feature that stores expired data in 1-90 day periods (depending on Snowflake edition)
- Virtual Warehouse: Cluster of compute resources that executes database queries and commands