# How To Restore Deleted files on Linux

Take LV `/dev/mapper/vg_01-lv01` for example

## Steps

`debugfs -w /dev/mapper/vg_01-lv01` to enter debugfs.

`lsdel` to list deleted files.

`echo lsdel | debugfs /dev/mapper/vg_01-lv01 > lsdel.out` to output deleted file list.

Find out the inode of deleted file.

`dump <inode> /tmp/file.bak` to recover file.



