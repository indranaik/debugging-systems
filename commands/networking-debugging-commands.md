# Networking Debugging Commands

## TCP & Socket Analysis

```bash
ss -s
netstat -s
```

## Packet Loss & Connectivity

```bash
ping
mtr
traceroute
```

## DNS Debugging

```bash
nslookup
dig
host
```

## Packet Capture

```bash
tcpdump
wireshark
```

## Interface Statistics

```bash
ip -s link
sar -n DEV 1
```

## Connection Tracking

```bash
cat /proc/sys/net/netfilter/nf_conntrack_count
cat /proc/sys/net/netfilter/nf_conntrack_max
```

## MTU Validation

```bash
ping -M do -s 1472 <host>
```
