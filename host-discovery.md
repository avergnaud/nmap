---
title: nmap host-discovery mindmap
markmap:
  colorFreezeLevel: 10
---

# (unprivileged) nmap -sn

## local network

### use raw ethernet

#### single IP

- `--send-eth`option IGNORED

#### IP range

- TODO

### use raw IP (default)

#### single IP

##### default
- 
  ```
  nmap -sn 172.31.33.32
  ```
  ![nmap_unpriv_sn_local](./docs/nmap_unpriv_sn_local.png?raw=true)
  "Unprivileged nmap -sn always make a TCP handshake (connect call) to ports 80 and 443"

- 
  ```
  nmap -sn --send-ip 192.168.79.201
  ```
  ![nmap_unpriv_sn](./docs/nmap_unpriv_sn.png?raw=true)
  "Unprivileged nmap -sn always make a TCP handshake (connect call) to ports 80 and 443"

##### `-PE` "ICMP echo"
- 
  ```
  nmap -sn -PE 192.168.79.201
  ```
  ![nmap_unpriv_sn_PE](./docs/nmap_unpriv_sn_PE.png?raw=true)
  Unprivileged nmap -sn -PE always (try to) make a TCP handshake (connect call) to port 80.

- 
  ```
  nmap -sn -PE 172.31.33.76
  ```
  ![nmap_unpriv_sn_PE_2](./docs/nmap_unpriv_sn_PE_2.png?raw=true)
  Unprivileged nmap -sn -PE always (try to) make a TCP handshake (connect call)  to port 80.

##### `-PP` "ICMP Timestamp"

- TODO

##### `-PM` "ICMP address mask"

- TODO

##### `-PS` "TCP SYN Ping"
- 
  ```
  nmap -sn --send-ip -PS 192.168.79.201
  nmap -sn -PS 192.168.79.201
  ```
  ![nmap_unpriv_sn_PS](./docs/nmap_unpriv_sn_PS.png?raw=true)
  Unprivileged nmap -sn always make a TCP handshake (connect call).

- 
  ```
  nmap -sn -PS443 192.168.79.201
  ```
  ![nmap_unpriv_sn_PS443](./docs/nmap_unpriv_sn_PS443.png?raw=true)
  Unprivileged nmap -sn always make a TCP handshake (connect call).

##### `-PA` "TCP ACK Ping"

- 
  ```
  nmap -sn -PA 192.168.79.201
  nmap -sn -PA --send-ip 192.168.79.201
  ```
  ![nmap_unpriv_sn_PA](./docs/nmap_unpriv_sn_PA.png?raw=true)
  Unprivileged nmap -sn always make a TCP handshake (connect call).

##### `-PU` "UDP Ping"

- 
  ```
  nmap -sn -PU137,138 192.168.1.23
  ```
  "Sorry, UDP Ping (-PU) only works if you are root (because we need to read raw responses off the wire) QUITTING!"

#### IP range

##### default

- TODO

##### `-PE` "ICMP echo"

- TODO

##### `-PP` "ICMP Timestamp"

- TODO

##### `-PM` "ICMP address mask"

- TODO

##### `-PS` "TCP SYN Ping"
- 
  ```
  nmap -sn -PS1-1000 192.168.79.201
  ```
  ![nmap_unpriv_sn_P1-1000](./docs/nmap_unpriv_sn_PS1-1000.png?raw=true)
  On voit que nmap s'arrête après 10 retours RST ACK


## external network

### use raw ethernet

#### single IP

- TODO

#### IP range

- TODO

### use raw IP

#### single IP

- TODO "only SYN packets are sent (using a connect call) to ports 80 and 443"

#### IP range

- TODO

# sudo nmap -sn

## local network

### use raw ethernet (default)

#### single IP

##### default

- TODO "ARP requests are used"

##### `-PE` "ICMP echo"

- 
  ```
  sudo nmap -sn -PE 192.168.79.201
  ```
  ![nmap_priv_sn_PE](./docs/nmap_priv_sn_PE.png?raw=true)
  On a local ethernet network, ARP requests are used unless --send-ip was specified

- 
  ```
  sudo nmap -sn -PE 172.31.33.76
  ```
  ![priv_sn_PE_2](./docs/nmap_priv_sn_PE_2.png?raw=true)
  On a local ethernet network, ARP requests are used unless --send-ip was specified

##### `-PP` "ICMP Timestamp"

- TODO

##### `-PM` "ICMP address mask"

- TODO

##### `-PS` "TCP SYN Ping"

- 
  ```
  sudo nmap -sn -PS 192.168.79.201
  ```
  ![nmap_priv_sn_PS](./docs/nmap_priv_sn_PS.png?raw=true)
  On a local ethernet network, ARP requests are used unless --send-ip was specified

- 
  ```
  sudo nmap -sn -PS21,22,25,80,443,445,3389,8080 -T4 192.168.79.201
  ```

##### `-PA` "TCP ACK Ping"

- 
  ```
  sudo nmap -sn -PA 192.168.79.201
  ```
  ![nmap_priv_sn_PA](./docs/nmap_priv_sn_PA.png?raw=true)
  On a local ethernet network, ARP requests are used unless --send-ip was specified


##### `-PU` "UDP Ping"

- 
  ```
  sudo nmap -sn -PU137,138 192.168.1.23
  ```
  ![nmap_priv_sn_PU](./docs/nmap_priv_sn_PU.png?raw=true)
  On a local ethernet network, ARP requests are used unless --send-ip was specified
  

#### IP range

- TODO

### use raw IP

#### single IP

##### default

- TODO

##### `-PE` "ICMP echo"

- 
  ```
  sudo nmap -sn -PE --send-ip  172.31.33.76
  ```
  ![nmap_priv_sn_PE_send-ip_2](./docs/nmap_priv_sn_PE_send-ip_2.png?raw=true)
  "ICMP echo discovery probes"

- 
  ```
  sudo nmap -sn -PE --send-ip 192.168.79.201
  ```
  ![nmap_priv_sn_PE_send-ip](./docs/nmap_priv_sn_PE_send-ip.png?raw=true)
  "ICMP echo discovery probes"

##### `-PP` "ICMP Timestamp"

- TODO

##### `-PM` "ICMP address mask"

- TODO

##### `-PS` "TCP SYN Ping"

- 
  ```
  sudo nmap -sn -PS --send-ip  192.168.79.201
  ```
  ![nmap_priv_sn_PS_send-ip](./docs/nmap_priv_sn_PS_send-ip.png?raw=true)
  "sends an empty TCP packet with the SYN flag set. The default destination port is 80. Alternate ports can be specified as a parameter"

##### `-PA` "TCP ACK Ping"

- 
  ```
  sudo nmap -sn -PA --send-ip 192.168.79.201
  ```
  ![nmap_priv_sn_PA_send-ip](./docs/nmap_priv_sn_PA_send-ip.png?raw=true)
  "he TCP ACK flag is set instead of the SYN flag. uses the same default port as the SYN probe (80) and can also take a list of destination ports in the same format"

##### `-PU` "UDP Ping"

- 
  ```
  sudo nmap -sn -PU137,138 --send-ip 192.168.1.23
  ```
  ![nmap_priv_sn_PU_send-ip](./docs/nmap_priv_sn_PU_send-ip.png?raw=true)
  "Upon hitting a closed port on the target machine, the UDP probe should elicit an ICMP port unreachable packet in return. This signifies to Nmap that the machine is up and available"


#### IP range

- TODO

## external network

### use raw ethernet

#### single IP

- TODO

#### IP range

- TODO

### use raw IP

#### single IP

- TODO

#### IP range

- TODO
