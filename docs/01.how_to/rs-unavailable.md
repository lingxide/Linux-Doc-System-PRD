# How To Fix fork failed: Resource temporarily unavailable

## Root Cause

- There is a misbehaving service or process running, consuming more resources than expected.
- The system was not able to create new processes, because of the limits set for **nproc** in /etc/security/limits.conf.
- The system **ran out of memory** and new processes were unable to start because they could not allocate memory.
- There is not an available ID to assign to the new process. A unique value less than **kernel.pid_max** must be available.

## Troubleshooting

You can run the below command to find the number of processes opened for every user:

`ps --no-headers auxwwwm | cut -f1 -d' ' | sort | uniq -c | sort -n`

Compare to `/etc/security/limits.conf` or `/etc/security/limits.d/*`

Check the total number of threads and processes running on the server:

`ps -eLf | wc -l`

Compare to kernel.pid_max:

`sysctl kernel.pid_max`

## Fixing

### nproc

Refer to [Amending Maximum Number of Processes in RHEL](01.how_to/nproc.md)

Set `/etc/security/limits.conf`
```
* soft nproc 65535
* hard nproc 65535
```
`*` should be `username`

### Memory

`sar -r 1 10`

Check commit%

### kernel.pid_max

`echo 65535 > /proc/sys/kernel/pid_max`

## Check for File Descriptors

### System Limit

`sysctl fs.file-nr`

Explain:

`<in_use> <unused_but_allocated> <maximum>`

### User Limit

```
su - <username>
ulimit -Hn
```

### User Used

`lsof -u <username> 2>/dev/null | wc -l`

### Rewrite for system level

`/etc/sysctl.conf `:

```
fs.file-max = 204708
```
