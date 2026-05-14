# Linux Debugging Commands

## CPU Analysis

```bash
top
htop
mpstat -P ALL 1
pidstat 1
```

## Memory Analysis

```bash
free -m
vmstat 1
sar -B 1
```

## Disk IO Analysis

```bash
iostat -x 1
iotop
sar -d 1
```

## Network Analysis

```bash
ss -s
netstat -an
sar -n TCP,DEV 1
```

## Kernel & System Logs

```bash
dmesg
journalctl -xe
```

## Process Analysis

```bash
ps aux
pstree
lsof
```

## Load Average

```bash
uptime
w
```

## Swap Analysis

```bash
swapon -s
cat /proc/swaps
```
