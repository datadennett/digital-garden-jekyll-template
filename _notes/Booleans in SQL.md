---
title: Booleans in SQL
---

> [!info] false is less than true
> At least in Redshift, `false` is considered to be less than `true`, so you can use `least` on two values to make it pick `false` if one of them is false.
> 
```sql
select least(false,true)
```
<br>

>[!info] The `least` and `greatest` operators are a very convenient way to compare two or more values, picking the lowest or highest value.
> Syntax: `least(value_1, value_2...,)`. This will even skip over null values. So the statement below will return -3.
```sql
select least(null::int, 8, -3)
```
<br>

>[!info] Converting text into a boolean
> Another thing I learned recently, is that in the context of comparison expressions, Redshift SQL at least will natively convert text that looks like a Boolean into a boolean. For example, if you ask Redshift if `false` the Boolean, is equal to `'False'` the text value, it will find that they are equal.
```sql
select false = 'False'
```
