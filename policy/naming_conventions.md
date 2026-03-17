# Data Engineering Naming Conventions

## Overview
These naming conventions apply to all objects created in the Databricks Lakehouse,
including catalogs, schemas, tables, columns, and indexes. All engineers must follow
these standards when creating new objects or modifying existing ones.

## Scope
These standards apply to all newly created objects.
Existing objects are subject to a separate remediation process.

## Catalogs
- Use lowercase, snake_case
- Example: `my_catalog`, `data_platform`

## Schemas
- Use lowercase, snake_case
- Example: `ai_project`, `raw_ingestion`

## Tables
- Use lowercase, snake_case
- Prefix with the domain or subject area
- Example: `ai_project.doc_chunks`, `hr_employees`, `finance_transactions`

## Columns
- Use lowercase, snake_case
- Example: `chunk_id`, `source_type`, `processed_at`

## Primary Key Columns
- Named using the pattern `{entity}_id`
- Example: `chunk_id`, `doc_id`, `log_id`

## Timestamp Columns
- Suffix with `_at` or `_timestamp`
- Example: `processed_at`, `fetch_timestamp`, `created_at`

## Boolean Columns
- Prefix with `is_` or `has_`
- Example: `is_active`, `has_error`

## Vector Search Indexes
- Suffix with `_vector_index`
- Example: `doc_vector_index`, `book_vector_index`, `policy_vector_index`

## General Rules
- The only acceptable special character in any object name is an underscore (_). Spaces, hyphens, periods, and all other special characters are not permitted.
- Never use reserved SQL keywords as object names
- Abbreviations should be avoided unless universally understood
