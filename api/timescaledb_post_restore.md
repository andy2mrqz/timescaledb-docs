---
api_name: timescaledb_post_restore()
excerpt: Resume normal operations after restoring a database
license: apache
topic: administration
tags: [administration, restore, backup, background workers]
---

## timescaledb_post_restore() 
Perform the proper operations after restoring the database has completed.
Specifically this resets the `timescaledb.restoring` GUC and restarts any
background workers. See [backup/restore docs][backup-restore] for more information.

### Sample usage  

```sql
SELECT timescaledb_post_restore();
```

[backup-restore]: timescaledb/:currentVersion:/how-to-guides/backup-and-restore/pg-dump-and-restore/
