# How To resolve High CPU occupation from kswapd0

## Why?

kswapd0, manages **virtual memory** and may be having issues due to moving processes to SWAP too frequently, causing cpu spikes and decreased system performance.

High CPU Usage of kswapd0 indicates insufficient memory and memory swapping is in progress.

## Checking

### Swappiness

`cat /proc/sys/vm/swappiness`

```
This control is used to define how aggressive the kernel will swap
memory pages.  Higher values will increase aggressiveness, lower values
decrease the amount of swap.  A value of 0 instructs the kernel not to
initiate swap until the amount of free and file-backed pages is less
than the high water mark in a zone.

The default value is 60.
```

Set to 0 can prevent swap activity in unnecessary.

### vfs_cache_pressure

`cat /proc/sys/vm/vfs_cache_pressure`

default value is 100, when set to 0, it will never reclaim dentries and inodes due to memory pressure and this can easily
lead to out-of-memory conditions.
With vfs_cache_pressure=1000, it will look for ten times more freeable objects than there are.

### transparent_hugepage

`cat /sys/kernel/mm/transparent_hugepage/enabled`

In short it should be set to `always`

## Fixing

### Prevent swappiness

`echo vm.swappiness=0 | tee -a /etc/sysctl.conf`

### Clear Cache

`echo 1 > /proc/sys/vm/drop_caches`

## Reference

[Documentation for /proc/sys/vm/*](https://www.kernel.org/doc/Documentation/sysctl/vm.txt)
