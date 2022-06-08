# NMAP

## Syntax

```
nmap [scan type] [options] [target]
```

> nmap \[scan type] \[options] \[target]

## Cheat Sheet

### Scanning Options

| Nmap Options       | Description                                                           |
| ------------------ | --------------------------------------------------------------------- |
| 10.10.10.0/24      | Target network range                                                  |
| -sn                | Disables port scanning                                                |
| -Pn                | Disabled ICMP Echo Requests                                           |
| -n                 | Disables DNS resolution                                               |
| -PE                | Performs the ping scan by using ICMP Echo Requests against the target |
| --packet-trace     | Shows all packets sent and received                                   |
| --reason           | Displays the reason for a specific result                             |
| --disable-arp-ping | Disables ARP Ping Requests                                            |
| --top-ports \[num] | Scans specified number of most frequent ports                         |
| -p-                | Scan all ports                                                        |
| -p22-110           | Scann all ports between 22 and 110                                    |
| -p22.25            | Scans only specified ports                                            |
| -F                 | Scans top 100 ports                                                   |
| -sS                | Perform TCP SYN-Scan                                                  |
| -sA                | Perform TCP ACK-Scan                                                  |
| -sU                | Peforms a UDP scan                                                    |
| -sV                | Scans services for their version                                      |
| -sC                | Performs a Script scan with scripts that are categorised as default   |
| --script \[script] | Performs a Script Scan by using the specified scripts.                |
| -O                 | Performs an OS Detection scan to determine the OS of the target       |
| -A                 | Performs OS Detection, Service Detection, and tracert scans.          |
| -D RND:S           | Sets the number of random Decoys that will be used to scan the target |
| -e                 | Specifies the network interface that is used for the scan             |
| -S 10.10.10.200    | Specifies the source IP address for the scan                          |
| -g                 | Specifies source port for the scan                                    |
| --dns-server \[ns] | DNS resolution is performed by using a specified name server          |

### Output Options

| Nmap Options | Description                                                                        |
| ------------ | ---------------------------------------------------------------------------------- |
| -oA filename | Stores the results in all available formats starting with the name of **filename** |
| -oN filename | Stores the results in normal format with the name **filename**                     |
| -oG filename | Stores the results in **grepable** format with the name of **filename**            |
| -oX filename | Stores the results in XML format with the name of **filename**                     |

### Performance Options

| Nmap Options               | Description                                                  |
| -------------------------- | ------------------------------------------------------------ |
| --max-retires \[num]       | Sets the number of retries for scans of specific ports       |
| --stats-every=5s           | Displays scan's status every 5 seconds                       |
| -v/-vv                     | Displays verbose output during the scan                      |
| --initial-rtt-timeout 50ms | Sets the specified time value as initial RTT timeout         |
| --min-rate 300             | Sets the number of packets that will be sent silmultaneously |
| -T \[0-5]                  | Specifies the timine template                                |

## Example Commands

| Command                                 | Explanation                                    |
| --------------------------------------- | ---------------------------------------------- |
| `nmap --help`                           | Shows help menu                                |
| `nmap -sL -n 10.10.12.13/29`            | -n emits DNS from the results                  |
| `nmap -p 80 <IP-address>`               | Scan just port 80.                             |
| `nmap -p 1000-1500 <IP-address>`        | Scan ports 1000-1500.                          |
| `nmap -- -script=vuln <IP-address>`     | Activate all the scripts in the vuln category. |
| sudo nmap \[10.129.2.28] --top-ports=10 | Scans the top 10 ports                         |
