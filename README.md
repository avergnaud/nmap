# nmap

Nmap's scanning process typically consists of two distinct phases:
1. Host Discovery: Determines if the target is alive (reachable on the network).
2. Port Scanning: Identifies open ports on the target.

During host discovery: if the target does not respond to these probes, Nmap assumes the host is down and skips the port scanning phase.

## list scan

"Users can skip the discovery step entirely with a list scan (-sL)"

"The list scan is a degenerate form of host discovery that simply lists each host of the network(s) specified, without sending any packets to the target hosts. By default, Nmap still does reverse-DNS resolution on the hosts to learn their names."

```
nmap -sL 192.168.1.0/30
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-02-01 10:18 CET
Nmap scan report for 192.168.1.0
Nmap scan report for 192.168.1.1
Nmap scan report for 192.168.1.2
Nmap scan report for 192.168.1.3
Nmap done: 4 IP addresses (0 hosts up) scanned in 0.00 seconds
```
![nmap_sL.png](./docs/nmap_sL.png?raw=true)

## host discovery

See mind map [host-discovery.html](./docs/host-discovery.html?raw=true)

## port scanning

"Users can skip the discovery by disabling host discovery (-Pn)"
...

## divers

### speed, verbose
```
sudo nmap -sn -v -T4 192.168.79.201
```

### output formats
```
sudo nmap -sn -oN eth0_output_1.txt 10.1.0.0/16

sudo nmap -sn -T5 -oG - 10.1.0.0/16

sudo nmap -sn -T5 -oG eth0_output_2.txt 10.1.0.0/16

awk '/Host:/ {print $2}' eth0_output_2.txt
```