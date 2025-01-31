---
title: nmap mindmap
markmap:
  colorFreezeLevel: 2
---

npx markmap-cli port-scanning.md






| sudo ? | commande | description |
| ------------- | ------------- | ------------- |
| sudo | nmap | *Host discovery* : cf `nmap -sn`. *Port Scanning* : Nmap uses a TCP SYN Scan `-sS`  |
| | nmap | *Host discovery* : cf `nmap -sn`. *Port Scanning* : falls back to a TCP Connect Scan `-sT` |

During host discovery: if the target does not respond to these probes, Nmap assumes the host is down and skips the port scanning phase. However you can skip this phase with the `-Pn` option, instructing Nmap to assume the target is alive and proceed directly to port scanning.

| sudo ? | commande | description |
| ------------- | ------------- | ------------- |
| sudo | nmap -sn | ICMP echo request, TCP SYN to port 443, TCP ACK to port 80, and an ICMP timestamp request. On a local ethernet network, ARP requests are used unless --send-ip was specified |
|| nmap -sn | only SYN packets are sent (using a connect call) to ports 80 and 443 |


```
nmap -sn --send-ip 192.168.79.201
```
![nmap_unpriv_sn](./docs/nmap_unpriv_sn.png?raw=true)


```
nmap -sn -PE 192.168.79.201
```

Unprivileged nmap -sn always make a TCP handshake (connect call).

![nmap_unpriv_sn_PE](./docs/nmap_unpriv_sn_PE.png?raw=true)


```
sudo nmap -sn -PE 192.168.79.201
```

On a local ethernet network, ARP requests are used unless --send-ip was specified

![nmap_priv_sn_PE](./docs/nmap_priv_sn_PE.png?raw=true)


```
sudo nmap -sn -PE --send-ip 192.168.79.201
```
![nmap_priv_sn_PE_send-ip](./docs/nmap_priv_sn_PE_send-ip.png?raw=true)


```
nmap -sn --send-ip -PS 192.168.79.201
nmap -sn -PS 192.168.79.201
```

Unprivileged nmap -sn always make a TCP handshake (connect call).

![nmap_unpriv_sn_PS](./docs/nmap_unpriv_sn_PS.png?raw=true)


```
nmap -sn -PS443 192.168.79.201
```
![nmap_unpriv_sn_PS443](./docs/nmap_unpriv_sn_PS443.png?raw=true)


Aussi :
```
nmap -sn -PS1-1000 192.168.79.201
```

On voit que nmap s'arrête après 10 retours RST ACK

![nmap_unpriv_sn_P1-1000](./docs/nmap_unpriv_sn_PS1-1000.png?raw=true)


```
sudo nmap -sn -PS 192.168.79.201
```

On a local ethernet network, ARP requests are used unless --send-ip was specified

![nmap_priv_sn_PS](./docs/nmap_priv_sn_PS.png?raw=true)


```
sudo nmap -sn -PS --send-ip  192.168.79.201
```
![nmap_priv_sn_PS_send-ip](./docs/nmap_priv_sn_PS_send-ip.png?raw=true)



```
nmap -sn -PA 192.168.79.201
nmap -sn -PA --send-ip 192.168.79.201
```

Unprivileged nmap -sn always make a TCP handshake (connect call).

![nmap_unpriv_sn_PA](./docs/nmap_unpriv_sn_PA.png?raw=true)


```
sudo nmap -sn -PA 192.168.79.201
```

On a local ethernet network, ARP requests are used unless --send-ip was specified

![nmap_priv_sn_PA](./docs/nmap_priv_sn_PA.png?raw=true)


```
sudo nmap -sn -PA --send-ip 192.168.79.201
```
![nmap_priv_sn_PA_send-ip](./docs/nmap_priv_sn_PA_send-ip.png?raw=true)



```
sudo nmap -sn -v -T4 192.168.79.201
```

then
```
sudo nmap -sn -PS21,22,25,80,443,445,3389,8080 -T4 192.168.79.201
```

then
```
sudo nmap -sn -PS21,22,25,80,443,445,3389,8080 -PU137,138 -T4 192.168.79.201
```


```
sudo nmap -sn -oN eth0_output_1.txt 10.1.0.0/16

sudo nmap -sn -T5 -oG - 10.1.0.0/16

sudo nmap -sn -T5 -oG eth0_output_2.txt 10.1.0.0/16

awk '/Host:/ {print $2}' eth0_output_2.txt
```

Or
```
nmap -Pn -sV -p 80 demo.ine.local
```


During port scanning: Nmap sends packets to the 1000 most commonly used TCP ports and observes the target's responses to classify ports as:
 * Open: A SYN-ACK is received.
 * Closed: A RST is received.
 * Filtered: No response or an ICMP "destination unreachable" message is received.

`nmap -p-` option will scan all TCP ports. `nmap -p80` or `nmap -p 80` will scan port 80. `nmap -p 80,445`. `nmap -p80-3000`...

`nmap -F` will scan fewer ports (fast scan)

`nmap -sU` will scan UDP ports

`nmap -sV` service Version scan

`nmap -O` detects OS

`nmap -sC` performs a script scan using the default set of scripts. It is equivalent to `--script=default`

`nmap -A` is `nmap -sV -O -sC`

`nmap -T<0,5>` for lower or faster exec. Normal is 3

`nmap -oN results.txt`, `nmap -oX results.xml`

| sudo ? | commande | description |
| ------------- | ------------- | ------------- |
| sudo | nmap -iL | ... |
| | nmap -iL | ... |
| sudo | nmap -sL | ... |
|| nmap -sL | ... |
| sudo | nmap -sn | ICMP echo request, TCP SYN to port 443, TCP ACK to port 80, and an ICMP timestamp request. On a local ethernet network, ARP requests are used unless --send-ip was specified |
|| nmap -sn | only SYN packets are sent (using a connect call) to ports 80 and 443 |
| sudo | nmap -sn -PS | ... |
|| nmap -sn -PS | ... |
| sudo | nmap -PR -sn | ... |
|| nmap -PR -sn | ... |
| sudo | nmap -PE -sn | ... |
|| nmap -PE -sn | ... |
| sudo | nmap -PP -sn | ... |
|| nmap -PP -sn | ... |


```
map -sV --script=vulscan/scipag_vulscan/vulscan.nse 10.10.142.156
```
ne retourne que des "No findings"...

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
