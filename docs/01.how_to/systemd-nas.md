# How To Mount a NAS Server by systemd

## Create a systemd mount unit file

This unit file **MUST** contain the path within the name using hyphens(-) instead of slashes(/). In my case, I will be mounting the NFS export at `/mnt/things` so my file name will be mnt-things.mount. The mount file itself will be stored at `/etc/systemd/system/` here's the full path to the file `/etc/systemd/system/mnt-things.mount`.


/etc/systemd/system/mnt-things.mount
```
[Unit]
Description=Things devices
After=network.target

[Mount]
What=172.16.1.1:/mnt/things
Where=/mnt/things
Type=nfs
Options=_netdev,auto

[Install]
WantedBy=multi-user.target
```

## Start a mount

Reload the daemon:
`systemctl daemon-reload`

Start the mount:
`systemctl start mnt-things.mount`

## Validate that it all works

If everything is working you should be able to begin using the mount at `/mnt/things` and browsing the filesystem. You can also check the status of the mount using the following:
`systemctl status mnt-things.mount `
```
> systemctl status mnt-things.mount 
● mnt-things.mount - /mnt/things
   Loaded: loaded
   Active: active (mounted) since Sun 2017-05-21 20:56:44 CDT; 22h ago
    Where: /mnt/things
     What: 172.16.1.1:/mnt/things

May 21 20:56:44 carterhousekodi systemd[1]: Mounting Things devices...
```

You'll notice that I **omitted** the directory creation command (`mkdir -p /mnt/things`) for the mount point on the client node, this was intentional. There's **no need** to create the path when mounting filesystems using systemd, if the `Where` path defined in the mount unit file does not exist systemd will create it Automagically.



