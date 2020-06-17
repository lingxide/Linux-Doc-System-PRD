# How To Rebuild RPM Database

## Matched Error

```
[root@ServerX ~]# yum
error: rpmdb: BDB0113 Thread/process 47262/140593139758912 failed: BDB1507 Thread died in Berkeley DB library
error: db5 error(-30973) from dbenv->failchk: BDB0087 DB_RUNRECOVERY: Fatal error, run database recovery
error: cannot open Packages index using db5 -  (-30973)
error: cannot open Packages database in /var/lib/rpm
CRITICAL:yum.main:

Error: rpmdb open failed
[root@ServerX ~]#
```

## Fixing procedure

```
mv /var/lib/rpm/__db* /tmp/
rpm --rebuilddb
yum clean all
```

Do verification and `rm -f /tmp/__db*`
