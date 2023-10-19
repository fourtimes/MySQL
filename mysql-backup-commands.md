## Backup for the specified table
```sql
sudo mysqldump -u username -p dbname daily_collection_multi > daily_collection_multi.sql
```
## Backup for last 2 months data to the specified table

```sql
# count the last 2 months data
select count(*) from daily_transcoll_verified where CreatedDate >= now()-interval 2 month;

# last 2 months data 
sudo mysqldump -u username -p dbname table_name --where="created_at >= DATE(NOW()) - INTERVAL 2 MONTH" > backup.sql
```

