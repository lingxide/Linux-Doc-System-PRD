# How To Check Linux Memory Usage in Multiple Ways

## Free
```
[root@ServerX ~]# free -h
              total        used        free      shared  buff/cache   available
Mem:           1.8G        1.3G         91M        664K        414M        329M
Swap:            0B          0B          0B
[root@ServerX ~]# 
```

## /proc/meminfo
```
$ cat /proc/meminfo
MemTotal:        8167848 kB
MemFree:         1409696 kB
Buffers:          961452 kB
Cached:          2347236 kB
SwapCached:            0 kB
Active:          3124752 kB
Inactive:        2781308 kB
Active(anon):    2603376 kB
Inactive(anon):   309056 kB
Active(file):     521376 kB
Inactive(file):  2472252 kB
Unevictable:        5864 kB
Mlocked:            5880 kB
SwapTotal:       1998844 kB
SwapFree:        1998844 kB
Dirty:              7180 kB
Writeback:             0 kB
AnonPages:       2603272 kB
Mapped:           788380 kB
Shmem:            311596 kB
Slab:             200468 kB
SReclaimable:     151760 kB
SUnreclaim:        48708 kB
KernelStack:        6488 kB
PageTables:        78592 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     6082768 kB
Committed_AS:    9397536 kB
VmallocTotal:   34359738367 kB
VmallocUsed:      420204 kB
VmallocChunk:   34359311104 kB
HardwareCorrupted:     0 kB
AnonHugePages:         0 kB                                                                                                                           
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:       62464 kB
DirectMap2M:     8316928 kB
```

#### Comments
- `SwapTotal`: Total swap space available
- `SwapFree`: The remaining swap space available
- `Dirty`: Memory waiting to be written back to disk
- `Writeback`: Memory which is actively being written back to disk
- `AnonPages`: Non-file backed pages mapped into userspace page tables
- `Mapped`: Files which have been mmaped, such as libraries
- `Slab`: In-kernel data structures cache
- `PageTables`: Amount of memory dedicated to the lowest level of page tables. This can increase to a high value if a lot of processes are attached to the same shared memory segment.
- `NFS_Unstable`: NFS pages sent to the server, but not yet commited to the storage
- `Bounce`: Memory used for block device bounce buffers
- `CommitLimit`: Based on the overcommit ratio (vm.overcommit_ratio), this is the total amount of memory currently available to be allocated on the system. This limit is only adhered to if strict overcommit accounting is enabled (mode 2 in vm.overcommit_memory).
- `Committed_AS`: The amount of memory presently allocated on the system. The committed memory is a sum of all of the memory which has been allocated by processes, even if it has not been "used" by them as of yet.
- `VmallocTotal`: total size of vmalloc memory area
- `VmallocUsed`: amount of vmalloc area which is used
- `VmallocChunk`: largest contiguous block of vmalloc area which is free
- `HugePages_Total`: Number of hugepages being allocated by the kernel (Defined with vm.nr_hugepages)
- `HugePages_Free`: The number of hugepages not being allocated by a process
- `HugePages_Rsvd`: The number of hugepages for which a commitment to allocate from the pool has been made, but no allocation has yet been made.
- `Hugepagesize`: The size of a hugepage (usually 2MB on an Intel based system)
>RHEL 6/7 only in below:
- `Shmem`: Total used shared memory (shared between several processes, thus including RAM disks, SYS-V-IPC and BSD like SHMEM)
- `SReclaimable`: The part of the Slab that might be reclaimed (such as caches)
- `SUnreclaim`: The part of the Slab that can't be reclaimed under memory pressure
- `KernelStack`: The memory the kernel stack uses. This is not reclaimable.
- `WritebackTmp`: Memory used by FUSE for temporary writeback buffers
- `HardwareCorrupted`: The amount of RAM the kernel identified as corrupted / not working
- `AnonHugePages`: Non-file backed huge pages mapped into userspace page tables
- `HugePages_Surp`: The number of hugepages in the pool above the value in vm.nr_hugepages. The maximum number of surplus hugepages is controlled by vm.nr_overcommit_hugepages.
- `DirectMap4k`: The amount of memory being mapped to standard 4k pages
- `DirectMap2M`: The amount of memory being mapped to hugepages (usually 2MB in size)

## vmstat
```
$ vmstat -s
      8167848 K total memory
      7449376 K used memory
      3423872 K active memory
      3140312 K inactive memory
       718472 K free memory
      1154464 K buffer memory
      2422876 K swap cache
      1998844 K total swap
            0 K used swap
      1998844 K free swap
       392650 non-nice user cpu ticks
         8073 nice user cpu ticks
        83959 system cpu ticks
     10448341 idle cpu ticks
        91904 IO-wait cpu ticks
            0 IRQ cpu ticks
         2189 softirq cpu ticks
            0 stolen cpu ticks
      2042603 pages paged in
      2614057 pages paged out
            0 pages swapped in
            0 pages swapped out
     42301605 interrupts
     94581566 CPU context switches
   1382755972 boot time
         8567 forks
```
```
[root@ServerX ~]# vmstat -s | grep -E 'memory|swap'
      1882236 K total memory
      1363952 K used memory
      1507204 K active memory
       155164 K inactive memory
        94368 K free memory
        39048 K buffer memory
       384868 K swap cache
            0 K total swap
            0 K used swap
            0 K free swap
            0 pages swapped in
            0 pages swapped out
[root@ServerX ~]#

```

## Top
Press `f`, press `a` to switch to MEM view, and press `q`


```
top - 23:42:13 up 6 days, 22:38,  2 users,  load average: 0.52, 0.52, 0.33
Tasks: 103 total,   3 running, 100 sleeping,   0 stopped,   0 zombie
%Cpu(s):  4.2 us,  0.7 sy,  0.0 ni, 95.1 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  1882236 total,    73904 free,  1369288 used,   439044 buff/cache
KiB Swap:        0 total,        0 free,        0 used.   332512 avail Mem

  PID %MEM    VIRT    RES   CODE    DATA    SHR nMaj nDRT %CPU COMMAND
14030  5.7 1195376 107332  16776 1118088   5248   78    0  0.1 mysqld
14068  3.4  409044  64584   8276  130288   7340    3    0  0.7 php-fpm
14093  3.4  408324  63892   8276  129568   7372   18    0  0.0 php-fpm
14075  3.4  408008  63580   8276  129252   7368    4    0  0.8 php-fpm
14074  3.4  408276  63280   8276  129520   7444   12    0  0.7 php-fpm

 ```
 
 #### Comments
 
 `%MEM` is directly related to RES, it’s the percentage use of total physical memory by the process.
`VIRT` is the total memory that this process has access to shared memory, mapped pages, swapped out pages, etc.
`RES` is the total physical memory used shared or private that the process has access to.
`SHR` is the total physical shared memory that the process has access to.
`DATA` is the total private memory mapped to process physical or not.
`CODE` also known as “text resident set” is total physical memory used to load application code.

## SAR
```
[root@ServerX run]# sar -r 1
Linux 3.10.0-957.5.1.el7.x86_64 (ServerX)        03/25/2019      _x86_64_        (1 CPU)

11:52:09 PM kbmemfree kbmemused  %memused kbbuffers  kbcached  kbcommit   %commit  kbactive   kbinact   kbdirty
11:52:10 PM     80776   1801460     95.71     47084    310348   2815880    149.60   1522432    154576        44
11:52:11 PM     80776   1801460     95.71     47084    310348   2815880    149.60   1522480    154576        44
11:52:12 PM     80776   1801460     95.71     47084    310348   2815880    149.60   1522484    154576        44
11:52:13 PM     80776   1801460     95.71     47084    310348   2815880    149.60   1522508    154576        44
11:52:14 PM     80776   1801460     95.71     47084    310348   2815880    149.60   1522528    154576         8
```
`kbcommit` & `%commit` is the overall memory used including RAM & Swap
