# How To Fix Linux Wireless 54Mbps issue in 802.11ac Wireless Card

## Steps

### One
/etc/modprobe.d/iwlwifi.conf

```
options iwlwifi 11n_disable=8
options iwlwifi power_save=0
```
### Two
/etc/modprobe.d/iwldvm.conf

```
options iwldvm power_scheme=1
```
### Three
/etc/modprobe.d/iwlmvm.conf

```
options iwlmvm power_scheme=1
```
