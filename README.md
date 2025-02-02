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

"During host discovery: if the target does not respond to these probes, Nmap assumes the host is down and skips the port scanning phase."

---

Generate the mindmap using `npx markmap-cli host-discovery.md`

## port scanning

"Users can skip the discovery by disabling host discovery (-Pn)"

During port scanning: Nmap sends packets to the 1000 most commonly used TCP ports and observes the target's responses to classify ports as:
 * Open: A SYN-ACK is received.
 * Closed: A RST is received.
 * Filtered: No response or an ICMP "destination unreachable" message is received.

### specify ports

`nmap -p-` option will scan all TCP ports. `nmap -p80` or `nmap -p 80` will scan port 80. `nmap -p 80,445`. `nmap -p80-3000`...

`nmap -F` will scan fewer ports (fast scan)

### `nmap -sV` service Version scan

```
nmap -Pn -sV -p 80 192.168.1.23
nmap -Pn -sV -p80 192.168.1.23
```

---

enerate the mindmap using `npx markmap-cli port-scanning.md`

## no host discovery nor port scanning...

"To skip host discovery and port scan, while still allowing NSE to run, use the two options -Pn -sn together"

## NMAP SCRIPTING ENGINE (NSE)

[https://nmap.org/book/nse.html](https://nmap.org/book/nse.html)

[https://nmap.org/book/nse-usage.html#nse-categories](https://nmap.org/book/nse-usage.html#nse-categories)

`-sC` Performs a script scan using the default set of scripts. It is equivalent to `--script=default`

`--script`

`nmap -A` is `nmap -sV -O -sC`

### Example: `--script vuln`

```
nmap -Pn --script vuln 10.10.142.156
```
retourne :
```
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-22 20:39 CEST
Pre-scan script results:
| broadcast-avahi-dos: 
|   Discovered hosts:
|     224.0.0.251
|   After NULL UDP avahi packet DoS (CVE-2011-1002).
|_  Hosts are all up (not vulnerable).
Nmap scan report for 10.10.142.156
Host is up (0.033s latency).
Not shown: 991 closed tcp ports (conn-refused)
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3389/tcp  open  ms-wbt-server
|_ssl-ccs-injection: No reply from server (TIMEOUT)
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49158/tcp open  unknown
49159/tcp open  unknown

Host script results:
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
|_smb-vuln-ms10-054: false
|_samba-vuln-cve-2012-1182: NT_STATUS_ACCESS_DENIED
|_smb-vuln-ms10-061: NT_STATUS_ACCESS_DENIED

Nmap done: 1 IP address (1 host up) scanned in 122.41 seconds
```

## OS detection

`nmap -O` detects OS


## divers

### speed, verbosity
```
sudo nmap -sn -v -T4 192.168.79.201
```

### input list

sudo nmap -iL
nmap -iL

### output formats

`nmap -T<0,5>` for lower or faster exec. Normal is 3

```
sudo nmap -sn -oN eth0_output_1.txt 10.1.0.0/16

nmap -oX results.xml

sudo nmap -sn -T5 -oG - 10.1.0.0/16

sudo nmap -sn -T5 -oG eth0_output_2.txt 10.1.0.0/16

awk '/Host:/ {print $2}' eth0_output_2.txt
```