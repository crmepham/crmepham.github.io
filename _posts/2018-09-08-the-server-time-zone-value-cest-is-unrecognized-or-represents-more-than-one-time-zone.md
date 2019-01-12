---
classes: wide
tags: [mysql]
---
This was a particularly challenging issue that I came up against recently. I'm still not entirely sure of the exact cause, other than many people have already suggested that it is a bug with certain versions of the mysql-connector library. Although I did try using many different versions of it and the error didn't go away.

The temporary solution, at least, is to update the timezone values within Mysql. Run the following commands:

```
MariaDB [server]&gt; SELECT @@global.time_zone, @@session.time_zone;
+--------------------+---------------------+
| @@global.time_zone | @@session.time_zone |
+--------------------+---------------------+
| SYSTEM             | SYSTEM              |
+--------------------+---------------------+
1 row in set (0.01 sec)

MariaDB [server]&gt; SET @@global.time_zone = '+00:00';
Query OK, 0 rows affected (0.00 sec)

MariaDB [server]&gt;
MariaDB [server]&gt; SET @@session.time_zone = '+00:00';
Query OK, 0 rows affected (0.00 sec)

MariaDB [server]&gt; SELECT @@global.time_zone, @@session.time_zone;
+--------------------+---------------------+
| @@global.time_zone | @@session.time_zone |
+--------------------+---------------------+
| +00:00             | +00:00              |
+--------------------+---------------------+
1 row in set (0.00 sec)
```

For a more permanent solution you could set the values in the Mysql configuration file.
