# How To Set Attributes by chattr 

## Setting attributes by chattr

### Read-only

By using `chattr +i` you can prevent critical files being amended without authorization.

`chattr +i /etc/resolv.conf`

After that all accounts(include root) will be only have read-only access.

### Append

By using `chattr +a` files can only be appended.

`chattr +a /var/log/messages`

## Checking attributes by lsattr

`lsattr` checking attributes:

```
root@SmartHomeCore:/home# chattr +i test/
root@SmartHomeCore:/home# lsattr 
-------------e-- ./homeassistant
----i--------e-- ./test
-------------e-- ./pi
root@SmartHomeCore:/home# cd test/
root@SmartHomeCore:/home/test# lsattr 
-------------e-- ./2222
-------------e-- ./1111
root@SmartHomeCore:/home/test#
```
