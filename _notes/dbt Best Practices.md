---
title: dbt Best Practices
---

> [!question] Can you add indexes to data models using DBT?
> Yes, we use unique fields like `occupancy_monthly_id`, but does that optimize the queries on that table? I tried but didn't quite complete the experiment of adding indices to `fact_occupancy_monthly`. Here's the [link](https://docs.getdbt.com/reference/resource-configs/postgres-configs#indexes) to the dbt documentation that's related to that topic.

```sql
{{ config(
    materialized = 'table',
    indexes=[
      {'columns': ['column_a'], 'type': 'hash'},
      {'columns': ['column_a', 'column_b'], 'unique': True},
    ]
)}}

select ...
```

> [!info] Update: Redshift doesn't use indices, but dist and sort keys
> I'm going to need to figure out [how dist and sort keys work](https://popsql.com/learn-sql/redshift/how-to-use-distkey-sortkey-and-define-column-compression-encoding-in-redshift) in order to better optimize the performance of our models. This is [DBT documentation](https://docs.getdbt.com/reference/resource-configs/redshift-configs) on the topic.

```sql
-- Example with one sort key
{{ config(materialized='table', sort='id', dist='received_at') }}

select ...


-- Example with multiple sort keys
{{ config(materialized='table', sort=['id', 'category'], dist='received_at') }}

select ...


-- Example with interleaved sort keys
{{ config(materialized='table',
          sort_type='interleaved'
          sort=['id', 'category'],
          dist='received_at')
}}

select ...
```
