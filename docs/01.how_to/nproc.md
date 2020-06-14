# How To Amend Maximum Number of Processes in RHEL

## Files

`/etc/security/limits.conf`

`/etc/security/limits.d`

`/etc/security/limits.d` **rewrites** `/etc/security/limits.conf`

## How To

### Limits.conf File

```
* soft nproc 65535
* hard nproc 65535
```

`*` should be `username`

### Amending Maximum Kernel Limits

#### Check

```
# sysctl kernel.pid_max
kernel.pid_max = 32768
```

OR

```
# cat /proc/sys/kernel/pid_max
32768
```

#### Amend

`echo 65535 > /proc/sys/kernel/pid_max`

## Related Issues

`Failed to execute /bin/bash: Resource temporarily unavailable`

## Other Related Inventories

- fsize - maximum filesize (KB)
- cpu - max CPU time (MIN)
- maxlogins - max number of logins for this user

