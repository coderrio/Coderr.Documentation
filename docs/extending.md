Extending
=====================

Run this script after creating an application. It will set the same appKey/SharedSecret as in all demo projects in all client library projects.


```sql
UPDATE Applications 
SET 
  AppKey = '13d82df603a845c7a27164c4fec19dd6',
  SharedSecret = '6f0a0a7fac6d42caa7cc47bb34a6520b'
WHERE 
  Id = 1;
```
