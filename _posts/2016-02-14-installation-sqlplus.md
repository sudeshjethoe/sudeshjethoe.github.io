---
title: Installation SQLplus
date: 2016-02-14
category:
- articles
tags:
- linux
- oracle
- sqlplus

---

For a customer I was required to extract and report data from an Oracle database.
Ofcourse I want to automate this task to the full extent.
Normally I would use a scripting language like bash/perl/python for this task.
Unfortunately, the environment did not allow for "easy" retrieval of external modules to interface with an Oracle database.\
However, the environment did allow access tot the Oracle SQLplus instantclient.
The instantclient allows running SQL-queries directly against Oracle databases,
much like running "mysql -u root -p$password $mydatabase" in a MySQL environment.\
By piping or redirecting commands to such a "connection" we are able to extract the required information from the database.

Below I will outline the required steps and after I will show you snippets of the code I used for the reporting mechanism.

### Install oracle client
```bash
yum install oracle-instantclient11.2-sqlplus-11.2.0.3.0-1.i386
```
### Create oracle user
```bash
useradd oracle
```

### Edit database configuration
```bash
# /usr/lib/oracle/12.1/client64/network/admin/tnsnames.ora
TDIGJ =
(DESCRIPTION =
  (ADDRESS_LIST =
    (ADDRESS = (PROTOCOL = TCP)(HOST = ${IPADDRESS})(PORT = ${PORT:1521}))
  )
  (CONNECT_DATA =
    (SID = ${SID})
  )
)
```

### Test
```bash
echo "SELECT table_name FROM DICTIONARY ORDER BY table_name;" | \
  sqlplus ${USER}@${DBNAME}/${DBPASSWD}
```
