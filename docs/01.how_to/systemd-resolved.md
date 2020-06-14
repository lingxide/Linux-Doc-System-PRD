# How To Update DNS by systemd-resolved

## How To Modify

Modify `/etc/systemd/resolved.conf`

Set `DNS=YOUR_IP_ADDRESS` in `[Resolve]` block

## How To Apply

Restart Service:

`systemctl restart systemd-resolved`
