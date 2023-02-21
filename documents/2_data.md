# Importing/Exporting Data
## Supported File Formats:
- Avro
- Delimited (CSV, DSV, TSV)
- JSON
- ORC
- Parquet
- XML

## Options:
- Compression
    - Files can be either automatically or manually compressed to Snowflake
- Encryption
    - Snowflake can automatically encrypt files with a managed key
    - Files can also be encrypted with your own key **(Business Critical Feature)**

## Best Practices
- Have a dedicated loading virtual warehouse
    - Ensures resources for loading files do not compete with resources used to query data
    - XS - M sized warehouses are usually large enough
- Seperate files by folders with source/application name along with relevent date information
    - Files should be around 10MB to 100MB compressed, it is recommended to aggregate or split data to fit within this range
        - Aggregate if you don't have enough data
        - Split if you have too much data

## Available Tools
- Web portal
    - Wizard driven
    - Not recommended for large files
    - GUI driven, not recommended for large *quantities* of files
- COPY command
    - Built-in with Snowflake implementation
    - Can use when batch loading files
- Snowpipe
    - Used for continuous loading of files

> **Note**  
> There are many third-party ETL tools, a list of tools can be found on [their website](https://docs.snowflake.com/en/user-guide/ecosystem-etl).

## Data Stage
- Virtual file system location
- Used for:
    - Loading data from files into Snowflake
    - Unloading data into files out of Snowflake

- Types:
    - Internal
        - Storaged managed directly by Snowflake
        - User stage
            - Space inside Snowflake to stage personal files
            - Can only be used by the one who staged the file
        - Table stage
            - Space inside Snowflake to load data into specific tables 
            - Can be used by multiple users
            - Exclusive to its table
        - Named stage
            - Available to all users
            - Can load data into any table

    - External
        - Storage managed by an external cloud provider such as:
            - AWS s3
            - Azure blob storage or data lake
            - Google cloud storage
    
> **Note**  
> The contents of internal stages are considered active data, meaning they will have a direct impact on storage billing

## Import Process
1. Select a stage to copy the file(s) into
2. Put the file(s) into the selected stage
    - If you are using an internal stage managed by Snowflake, best way to do this would be to run a put command with SnowSQL
    - If you are using an external stage, you must rely on tools from your cloud provider to upload files
3. Use the `COPY` command to put data into tables
4. Purge the copied file (can be done either automatically or manually)