---
title: Updating Data Models Directly
---

> [!info] Update and join simultaneously
> You can update from a join if you use syntax like the below:

```sql
update layer_0.financial_data full_history 
set jul_23 = july_data.jul_23  
from (select * from layer_0.july_23_financial_data  
         where column_name in ('unit_ebitda',  
'total_unit_operating_costs',  
'system_wide_revenue',  
'net_revenue')  
) july_data
where full_history.subsidiary_name = jul_pbcs.subsidiary_name and lower(full_history.column_name) = lower(july_data.column_name)
```


> [!info] Some SQL editors make it easy to update individual cells in a table
> We built a matching table `layer_0_redshift.coupa_gm_user_matching`. It all worked fine except for one person's name who didn't match perfectly. In DataGrip I could just edit the cell and submit the changes directly. It's better if there's a unique ID of course.
![[Screenshot 2024-03-02 at 08.45.19.png]]
