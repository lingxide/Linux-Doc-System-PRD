# How To Obtain File Creation Date with debugfs

## Get file inode

`ls -id <filename>`

take inode `2345` for example.

## Get LV for this file

`df -hPT` to check mount point.

take mount point `/dev/mapper/vg_vg01-lv01` for example.

## Get Creating Date

```
debugfs
open /dev/mapper/vg_vg01-lv01
logdump -i <2345>
```

### Creating Date in Different FS

- ext4 ->  crtime
- ufs2 -> st_birthtime
- zfs   -> crtime
- btrfs -> otime
- jfs    -> di_otime
