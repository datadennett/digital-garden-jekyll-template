---
title: Intermediate Unions in SQL
---

> [!info] In union statements, the order of columns is super important.
> I created a big union of two tables, but I switched the order of two columns between the two tables. In one, I put `contact_id` first, then `contact_name`, and in the second one it was the opposite. That caused us to have `contact_id` values showing up under the `contact_name` field and vice-versa. So where it was expecting an Id, it was getting a name, and vice-versa.
> This is why I much prefer to rely on dbt's `dbt-utils` functions for this kind of code writing: their `union_relations` macro is one of the most useful in the entire package!

```sql
select 
	contact_id,
	contact_name,
	wifi_attendance
from wifi_data_from_legacy_provider

union all

select
	contact_name,
	contact_id,
	wifi_attendance
from wifi_data_from_new_provider
```
