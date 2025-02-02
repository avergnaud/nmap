---
title: nmap mindmap
markmap:
  colorFreezeLevel: 2
---

# (unprivileged) nmap -Pn

## TCP Connect Scan `-sT` (default)

- 
  ```
  nmap -Pn 192.168.1.23
  ```
  ![nmap_unpriv_Pn_ethernet_single_FULL](./docs/nmap_unpriv_Pn_ethernet_single_FULL.png?raw=true)
  Focus on port 80:
  ![nmap_unpriv_Pn_ethernet_single](./docs/nmap_unpriv_Pn_ethernet_single.png?raw=true)
  "The simple command nmap target scans 1,000 TCP ports on the host target". TCP Connect Scan `-sT`

## TCP SYN Scan `-sS`

- 
  ```
  nmap -Pn -sS 192.168.1.23 
  You requested a scan type which requires root privileges.
  QUITTING!
  ```

## UDP scans `-sU`

- 
  ```
  nmap -Pn -sU 192.168.1.23
  You requested a scan type which requires root privileges.
  QUITTING!
  ```

# sudo nmap -Pn

## TCP Connect Scan `-sT`

- Same as unprivileged TCP Connect Scan `-sT`

## TCP SYN Scan `-sS` (default)

- 
  ```
  sudo nmap -Pn 192.168.1.23
  ```
  ![nmap_priv_Pn_ethernet_single](./docs/nmap_priv_Pn_ethernet_single.png?raw=true)
  Focus on port 80:
  ![nmap_priv_Pn_ethernet_single_focus80](./docs/nmap_priv_Pn_ethernet_single_focus80.png?raw=true)
  "SYN scan works against any compliant TCP stack rather than depending on idiosyncrasies of specific platforms as Nmap's FIN/NULL/Xmas, Maimon and idle scans do. It also allows clear, reliable differentiation between the open, closed, and filtered states."

## UDP scans `-sU`

- 
  "UDP scan is activated with the -sU option. It can be combined with a TCP scan type such as SYN scan (-sS) to check both protocols during the same run."


