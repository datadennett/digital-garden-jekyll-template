---
title: Advanced Filtering in SQL
---

> [!warning] Using the LIKE and IN keywords can filter out nulls 
> We had an issue a while back with oddly-formatted values in a column designed to capture the duration of an agreement. Typically it was in the format "1-Month" or "2 Year", but after we changed the business rules to allow for custom term lengths, we saw fractional months come through. So we had values like `1.5-Month` Until we had it fixed upstream, the solution the data engineer and I adopted was to add a filter to remove any records that were in decimal format. In other words, we added a filter like so:
> `where agreement_terms__c not like '%.%'`
> But the unexpected impact of that was to remove all the records in the opportunity table where that field was null altogether: in particular, all the pipeline opportunities were getting filtered out.
> This also applies to the `in` keyword. If you're applying a filter that says `not in ('A', 'B', 'C')` but you want it to count blanks or null values, then you can't write it that way. You have to say: `field is null or not field = 'A'` for example.


>[!info] IN keyword with a tuple
> Something I saw in our interview with our current data engineer is that certain dialects of SQL in certain contexts allow you to use the IN keyword with a tuple, like below.
> I don't know if this is truly recommended though. I think it might be computationally intensive, and it doesn't result in particularly clear code.
```sql
select product_id from dim_products
where (product_group, product_family) in (select distinct product_group, product_family from fact_reservations)
```
