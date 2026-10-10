# Basic Network Scanning with Nmap

## 1. Objective

The objective of this task is to learn how to identify open ports and
services on a system using Nmap and understand the security implications
of the scan results.

## 2. Environment

- Operating System: Fedora Linux
- Tool: Nmap
- Target 1: Localhost (127.0.0.1)
- Target 2: My own machine's local network IP address

All scans were performed on my own machine and local environment.

## 3. Commands Used

### Basic port scan
```bash
nmap 127.0.0.1
```

### Service version detection
```bash
nmap -sV 127.0.0.1
```

### Operating system detection
```bash
sudo nmap -O 127.0.0.1
```

### Scan of my own network interface IP
```bash
nmap -sV 192.168.1.83
```

## 4. Findings

- The localhost scan identified TCP port 631 as open.
- Service detection identified the service on port 631 as IPP, with CUPS
  version 2.4 reported by Nmap.
- The OS detection scan did not identify an exact operating system match.
- The scan of my own local network IP reported the 1,000 commonly scanned
  TCP ports as closed.

The complete scan outputs are saved in `nmap_scan_results.txt`.
The individual outputs are also retained in `scan_basic.txt`,
`scan_services.txt`, `scan_os.txt`, and `scan_local_ip.txt`.

## 5. Security Analysis

Port 631 is associated with Internet Printing Protocol (IPP), commonly
used by printing services such as CUPS on Linux systems.

An open port indicates that a service is listening at the scanned
address. The presence of a printing service is not automatically a
vulnerability; its exposure and configuration determine the risk.

In this scan, the CUPS service was found listening on the loopback
addresses `127.0.0.1` and `::1`. This indicates that the listener
checked with `ss` was bound to localhost rather than the machine's
network interface. This limits direct access through the network
interface, although it does not by itself prove that the service is
free of vulnerabilities.

The OS detection result was inconclusive. Nmap could not determine an
exact operating system match, so no definitive OS identification is
claimed.

The local-IP scan showed no open ports among the 1,000 common TCP ports
tested. This does not establish that every port is closed or that the
machine has no security risks.

## 6. What I Learned

- How to perform a basic Nmap port scan.
- How to identify service names and reported versions with `-sV`.
- How to attempt OS detection with `-O`.
- How to interpret open and closed ports.
- Why scan results must be evaluated in context instead of treating
  every open port as a vulnerability.

## 7. Ethical Considerations

Network scanning should only be performed on systems that I own or
have explicit permission to test. These scans were limited to my own
machine and local environment.
