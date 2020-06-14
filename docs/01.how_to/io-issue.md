# How To Identify IO Issue in Linux

## Check by disk
`iostat -xdm 1`

`argrq-sz` -> large for sequence, small for random IO.

`svctm` -> time for per IO. should <=10ms

## Check by process
`iotop`

`pidstat -drut 1`

`t` -> `thread`

`1` -> `1 sec`
