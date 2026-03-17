# Table Creation Standards

## Overview
These standards apply to all Delta tables created in the Databricks Lakehouse.
All CREATE TABLE statements must comply with these requirements before execution.

## Scope
These standards apply to all newly created objects.
Existing objects are subject to a separate remediation process.

## Fully Qualified Names
- All tables must be created using a three-part fully qualified name
- Format: `catalog.schema.table`
- Example: `workspace.ai_project.doc_chunks`
- Never create tables without specifying catalog and schema explicitly

## Primary Keys
- All Delta tables must define a primary key constraint
- Example: `CONSTRAINT pk_doc_chunks PRIMARY KEY (chunk_id)`

## Change Data Feed (CDF)
- CDF must be enabled on all tables that feed downstream vector search indexes
- Enable with: `TBLPROPERTIES (delta.enableChangeDataFeed = true)`

## Timestamps
- All tables must include a created_at or equivalent timestamp column
- Timestamp columns must default to `current_timestamp()`
- Example: `created_at TIMESTAMP DEFAULT current_timestamp()`

## Partitioning
- Partitioning is required on tables expected to exceed 1TB
- Partition columns should align with common query filter patterns
- Example: `PARTITIONED BY (date_partition)`

## External Tables
- External tables must specify a LOCATION explicitly
- Example: `LOCATION 'abfss://container@storage.dfs.core.windows.net/path'`

## Example Compliant CREATE TABLE Statement
    # Table Creation Standards

## Overview
These standards apply to all Delta tables created in the Databricks Lakehouse.
All CREATE TABLE statements must comply with these requirements before execution.

## Scope
These standards apply to all newly created objects.
Existing objects are subject to a separate remediation process.

## Fully Qualified Names
- All tables must be created using a three-part fully qualified name
- Format: `catalog.schema.table`
- Example: `workspace.ai_project.doc_chunks`
- Never create tables without specifying catalog and schema explicitly

## Primary Keys
- All Delta tables must define a primary key constraint
- Example: `CONSTRAINT pk_doc_chunks PRIMARY KEY (chunk_id)`

## Change Data Feed (CDF)
- CDF must be enabled on tables that feed downstream vector search indexes or streaming pipelines
- CDF should not be enabled on audit/log tables, staging tables, or read-only serving tables
- Enable with: `TBLPROPERTIES (delta.enableChangeDataFeed = true)`
  
## Timestamps
- Tables are recommened to include a created_at or equivalent timestamp column
- Timestamp columns must default to `current_timestamp()`
- Example: `created_at TIMESTAMP DEFAULT current_timestamp()`

## Partitioning
- Partitioning is required on tables expected to exceed 1TB
- Partition columns should align with common query filter patterns
- Example: `PARTITIONED BY (date_partition)`

## External Tables
- External tables must specify a LOCATION explicitly
- Example: `LOCATION 'abfss://container@storage.dfs.core.windows.net/path'`

## Example Compliant CREATE TABLE Statement
    CREATE TABLE workspace.ai_project.example_table (
        example_id STRING NOT NULL COMMENT 'Primary key identifier',
        content STRING COMMENT 'Main content field',
        created_at TIMESTAMP DEFAULT current_timestamp(),
        CONSTRAINT pk_example PRIMARY KEY (example_id)
    )
    TBLPROPERTIES (delta.enableChangeDataFeed = true);
