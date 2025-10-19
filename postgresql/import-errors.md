# Import Errors

Recreate the database from the scratch (clean import)

If your goal is to replace everything with what's in `dump.sql`:

```sh
psql -U postgres -h 172.21.96.1 -c "DROP DATABASE IF EXISTS \"your-table\";"
psql -U postgres -h 172.21.96.1 -c "CREATE DATABASE \"your-table\";"

psql "postgresql://postgres:root@172.21.96.1:5432/your-table" < dump.sql
```

**Note**: change the ip address to localhost.
