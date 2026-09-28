# INTERNSHIP PROJECT REPORT

---

&nbsp;

&nbsp;

&nbsp;

<div align="center">

# DESIGN AND IMPLEMENTATION OF A SECURE NETWORK USING pfSense, UBUNTU, NAT, NMAP AND TCPDUMP

&nbsp;

&nbsp;

**Prepared by:** ___________________________________________

&nbsp;

**Department:** _____________________________________________

&nbsp;

**University/College:** _______________________________________

&nbsp;

**Organization:** ____________________________________________

&nbsp;

**Supervisor:** ______________________________________________

&nbsp;

**Date:** September 2026

</div>

---

&nbsp;

&nbsp;

---

# DECLARATION

I declare that this internship report has been prepared to document the practical networking activities performed during my internship. The project focuses on the design and implementation of a controlled virtual network laboratory using pfSense as a firewall and router, Ubuntu as a client operating system, Network Address Translation (NAT) for private-to-external network communication, Nmap for authorized network and service discovery, and tcpdump for packet-level traffic analysis.

The configurations, tests, observations, and results presented in this report are based on practical activities performed in the laboratory environment. Results described as verified are supported by practical testing and corresponding evidence where available.

I confirm that the work presented in this report is intended for educational and authorized laboratory purposes.

&nbsp;

**Student Name:** ______________________________

**Signature:** ___________________________________

**Date:** _______________________________________

---

# ACKNOWLEDGEMENT

I would like to express my sincere appreciation to my university/college, internship organization, instructors, and supervisor for their guidance, support, and encouragement throughout my internship period.

I am especially grateful for the opportunity to gain practical experience in computer networking and network security. The internship allowed me to move beyond theoretical concepts and work with real networking technologies in a controlled virtual laboratory.

I would also like to acknowledge the importance of virtualization platforms such as VirtualBox and VMware in providing an environment where network devices and operating systems can be tested without requiring a large amount of physical networking equipment.

Through this project, I gained practical knowledge of pfSense firewall configuration, Ubuntu network administration, IP addressing, DHCP, DNS, NAT, network connectivity testing, Nmap network discovery, and tcpdump packet analysis.

Finally, I would like to thank everyone who contributed directly or indirectly to the successful completion of this internship project.

---

# ABSTRACT

This internship project presents the design and practical implementation of a small secure network laboratory using pfSense, Ubuntu, Network Address Translation (NAT), Nmap, and tcpdump. The laboratory was implemented using virtualization to create a controlled networking environment without requiring multiple physical computers and network appliances.

pfSense was deployed as the central firewall and router. It was configured with a LAN gateway of **192.168.1.1/24**, while the Ubuntu client was connected to the same internal LAN network. The pfSense WAN interface provided connectivity toward the external network, while the LAN interface provided controlled connectivity to the internal client.

Automatic outbound NAT was used to translate private LAN traffic before it was forwarded toward the WAN. DHCP was used to provide network configuration to the Ubuntu client, while DNS-related connectivity was tested using `nslookup`. Connectivity was verified using `ping` tests to the pfSense gateway, an external IP address, and a domain name.

Nmap was used in the authorized laboratory environment to identify reachable hosts and exposed services. tcpdump was used to capture and analyze network traffic, including ICMP and DNS-related traffic. These tools provided visibility into how packets were generated, forwarded, translated, and returned.

The project demonstrates the integration of network addressing, routing, firewalling, NAT, network discovery, packet capture, and troubleshooting in a practical environment.

**Keywords:** pfSense, Ubuntu, NAT, Nmap, tcpdump, DHCP, DNS, firewall, networking, packet analysis, virtualization.

---

# LIST OF ABBREVIATIONS

| Abbreviation | Meaning |
|---|---|
| DHCP | Dynamic Host Configuration Protocol |
| DNS | Domain Name System |
| IP | Internet Protocol |
| LAN | Local Area Network |
| NAT | Network Address Translation |
| NIC | Network Interface Card |
| Nmap | Network Mapper |
| OS | Operating System |
| PCAP | Packet Capture |
| TCP | Transmission Control Protocol |
| UDP | User Datagram Protocol |
| VM | Virtual Machine |
| WAN | Wide Area Network |
| WebGUI | Web Graphical User Interface |

---

# TABLE OF CONTENTS

| Section | Title | Page |
|---|---|---|
| | Declaration | ii |
| | Acknowledgement | iii |
| | Abstract | iv |
| | List of Abbreviations | v |
| | Table of Contents | vi |
| | List of Figures | vii |
| **Chapter 1** | **Introduction** | **1** |
| 1.1 | Background | 1 |
| 1.2 | Problem Statement | 2 |
| 1.3 | General Objective | 2 |
| 1.4 | Specific Objectives | 3 |
| 1.5 | Scope of the Project | 3 |
| 1.6 | Significance of the Project | 4 |
| 1.7 | Methodology | 4 |
| 1.8 | Organization of the Report | 5 |
| **Chapter 2** | **Background and Theoretical Concepts** | **6** |
| 2.1 | Introduction | 6 |
| 2.2 | Computer Networking | 6 |
| 2.3 | Network Components | 7 |
| 2.4 | LAN and WAN | 7 |
| 2.5 | IP Addressing | 8 |
| 2.6 | IPv4 Addressing | 8 |
| 2.7 | Private IP Addresses | 8 |
| 2.8 | Subnet Mask and CIDR | 9 |
| 2.9 | Default Gateway | 9 |
| 2.10 | DHCP | 9 |
| 2.11 | DNS | 10 |
| 2.12 | Routing | 10 |
| 2.13 | Firewall | 10 |
| 2.14 | pfSense | 11 |
| 2.15 | NAT | 11 |
| 2.16 | Network Discovery | 11 |
| 2.17 | Nmap | 12 |
| 2.18 | Packet Capture and Analysis | 12 |
| 2.19 | tcpdump | 12 |
| 2.20 | ICMP | 13 |
| 2.21 | TCP and UDP | 13 |
| 2.22 | Network Security Principles | 13 |
| 2.23 | Virtualization in Networking | 14 |
| **Chapter 3** | **System Requirements and Network Design** | **15** |
| 3.1 | Introduction | 15 |
| 3.2 | Hardware Requirements | 15 |
| 3.3 | Software Requirements | 15 |
| 3.4 | Virtualization Environment | 16 |
| 3.5 | Network Architecture | 16 |
| 3.6 | Network Components | 17 |
| 3.7 | IP Addressing Plan | 17 |
| 3.8 | Network Traffic Flow | 17 |
| 3.9 | Security Design | 18 |
| 3.10 | Practical Evidence Methodology | 18 |
| **Chapter 4** | **Practical Implementation** | **19** |
| 4.1 | Introduction | 19 |
| 4.2 | Creating the pfSense Virtual Machine | 19 |
| 4.3 | Configuring pfSense Network Adapters | 19 |
| 4.4 | Installing pfSense | 20 |
| 4.5 | Assigning WAN and LAN Interfaces | 20 |
| 4.6 | Configuring the LAN Address | 20 |
| 4.7 | Accessing the pfSense WebGUI | 21 |
| 4.8 | Configuring DHCP | 21 |
| 4.9 | Configuring DNS | 21 |
| 4.10 | Configuring Firewall Rules | 22 |
| 4.11 | Configuring NAT | 22 |
| 4.12 | Preparing Ubuntu | 22 |
| 4.13 | Ubuntu Network Verification | 23 |
| 4.14 | Gateway Connectivity Test | 23 |
| 4.15 | Internet Connectivity Test | 23 |
| 4.16 | DNS Connectivity Test | 24 |
| 4.17 | End-to-End Connectivity | 24 |
| **Chapter 5** | **Nmap Network Scanning** | **25** |
| 5.1 | Introduction | 25 |
| 5.2 | Purpose of Nmap | 25 |
| 5.3 | Installing Nmap | 25 |
| 5.4 | Checking the Ubuntu IP Address | 26 |
| 5.5 | Basic Host Scan | 26 |
| 5.6 | Port Scanning | 26 |
| 5.7 | Service and Version Detection | 27 |
| 5.8 | Selected-Port Scanning | 27 |
| 5.9 | Interpreting Nmap Results | 27 |
| 5.10 | Security Considerations | 28 |
| **Chapter 6** | **tcpdump Traffic Analysis** | **29** |
| 6.1 | Introduction | 29 |
| 6.2 | Checking Network Interfaces | 29 |
| 6.3 | Capturing ICMP Traffic | 29 |
| 6.4 | Capturing DNS Traffic | 30 |
| 6.5 | Capturing ICMP and DNS Together | 30 |
| 6.6 | Saving Packet Captures | 30 |
| 6.7 | Reading Capture Statistics | 31 |
| 6.8 | Interpreting Packets | 31 |
| 6.9 | Packet-Level NAT Analysis | 31 |
| **Chapter 7** | **NAT Configuration and Verification** | **32** |
| 7.1 | Introduction | 32 |
| 7.2 | Purpose of NAT | 32 |
| 7.3 | Private and External Addressing | 32 |
| 7.4 | pfSense Outbound NAT | 33 |
| 7.5 | Automatic Outbound NAT | 33 |
| 7.6 | NAT Traffic Flow | 33 |
| 7.7 | NAT Verification | 34 |
| 7.8 | Packet-Level NAT Verification | 34 |
| **Chapter 8** | **Testing and Results** | **35** |
| 8.1 | Introduction | 35 |
| 8.2 | Testing Methodology | 35 |
| 8.3 | Gateway Connectivity Test | 35 |
| 8.4 | Internet IP Connectivity Test | 36 |
| 8.5 | DNS Resolution Test | 36 |
| 8.6 | Domain Connectivity Test | 36 |
| 8.7 | DHCP Verification | 37 |
| 8.8 | NAT Verification | 37 |
| 8.9 | Nmap Verification | 37 |
| 8.10 | tcpdump Verification | 38 |
| 8.11 | Overall Results | 38 |
| **Chapter 9** | **Challenges and Solutions** | **39** |
| 9.1 | Introduction | 39 |
| 9.2 | Virtual Network Adapter Problems | 39 |
| 9.3 | DHCP Problems | 39 |
| 9.4 | Gateway Connectivity Problems | 40 |
| 9.5 | Internet Connectivity Problems | 40 |
| 9.6 | DNS Problems | 40 |
| 9.7 | NAT Problems | 41 |
| 9.8 | Nmap Scanning Problems | 41 |
| 9.9 | tcpdump Interface Problems | 41 |
| 9.10 | Lessons Learned | 42 |
| **Chapter 10** | **Conclusion and Recommendations** | **43** |
| 10.1 | Conclusion | 43 |
| 10.2 | Recommendations | 44 |
| 10.3 | Future Improvements | 45 |
| | References | 46 |
| | Appendix A — Command Reference | 47 |
| | Appendix B — Screenshot/Evidence Checklist | 50 |

---

# LIST OF FIGURES

| Figure | Title | Page |
|---|---|---|
| Figure 1 | Virtual Machine Configuration | 19 |
| Figure 2 | pfSense Console | 20 |
| Figure 3 | pfSense LAN Configuration | 20 |
| Figure 4 | pfSense DHCP Configuration | 21 |
| Figure 5 | Ubuntu IP Address | 23 |
| Figure 6 | Ubuntu Routing Table | 23 |
| Figure 7 | Gateway Ping | 23 |
| Figure 8 | Internet Ping | 24 |
| Figure 9 | DNS Resolution | 24 |
| Figure 10 | Domain Ping | 24 |
| Figure 11 | Firewall Rules | 22 |
| Figure 12 | NAT Configuration | 33 |
| Figure 13 | Nmap Installation | 25 |
| Figure 14 | Nmap Basic Scan | 26 |
| Figure 15 | Nmap Service Detection | 27 |
| Figure 16 | tcpdump ICMP Capture | 29 |
| Figure 17 | tcpdump DNS Capture | 30 |
| Figure 18 | Saved PCAP | 30 |
| Figure 19 | NAT Packet Analysis | 34 |

---

# CHAPTER ONE — INTRODUCTION

## 1.1 Background

Computer networking is one of the fundamental technologies used to connect computers, servers, applications, and other devices so that they can exchange information. Modern organizations depend on computer networks for Internet access, communication, file sharing, centralized applications, cloud services, security systems, and business operations.

A functional network requires more than simply connecting computers. Devices must have appropriate IP addresses, routing information, gateways, DNS configuration, and security policies. Network traffic must also be monitored and analyzed when problems occur.

For this reason, practical networking education requires a laboratory in which network configurations can be implemented and tested.

This internship project establishes such an environment using virtualization. The project uses pfSense as a firewall/router, Ubuntu as a client operating system, NAT for outbound communication, Nmap for authorized network discovery, and tcpdump for packet-level analysis.

The laboratory allows networking concepts to be studied from both configuration and operational perspectives.

---

## 1.2 Problem Statement

Learning networking only through theoretical explanations does not always provide sufficient understanding of how network traffic actually behaves.

For example, a student may understand that a firewall blocks unwanted traffic, but practical implementation is necessary to understand:

- how firewall rules are created;
- how interfaces are assigned;
- how clients receive IP addresses;
- how a default gateway works;
- how NAT changes packet addressing;
- how DNS requests are generated;
- how open ports can be discovered;
- and how packets can be observed during communication.

Therefore, a controlled practical environment is required to demonstrate these concepts.

The project addresses this problem by creating a virtual laboratory in which the complete process can be configured, tested, monitored, and documented.

---

## 1.3 General Objective

The general objective of this project is:

**To design and implement a practical secure networking laboratory using pfSense, Ubuntu, NAT, Nmap, and tcpdump.**

---

## 1.4 Specific Objectives

The specific objectives are to:

1. Create a virtual networking laboratory.
2. Install and configure pfSense.
3. Configure pfSense WAN and LAN interfaces.
4. Configure a private LAN using 192.168.1.0/24.
5. Configure pfSense LAN gateway as 192.168.1.1/24.
6. Configure DHCP for internal clients.
7. Configure and verify DNS-related connectivity.
8. Configure automatic outbound NAT.
9. Connect Ubuntu to the pfSense LAN.
10. Verify Ubuntu network configuration.
11. Test communication between Ubuntu and pfSense.
12. Test Internet connectivity.
13. Test DNS name resolution.
14. Install and use Nmap for authorized network discovery.
15. Identify reachable ports and services.
16. Capture network traffic using tcpdump.
17. Analyze ICMP and DNS traffic.
18. Demonstrate the operation of NAT.
19. Troubleshoot network problems systematically.
20. Document configuration and testing evidence.

---

## 1.5 Scope of the Project

The project focuses on a small virtual network laboratory.

The main components are:

- pfSense firewall/router;
- Ubuntu client;
- virtual WAN network;
- virtual LAN network;
- DHCP;
- DNS-related connectivity;
- NAT;
- Nmap;
- tcpdump.

The project does not attempt to reproduce a complete enterprise network. Advanced technologies such as OSPF, large-scale VLAN architecture, redundant firewalls, enterprise wireless controllers, and multi-site VPN infrastructure may be considered future extensions.

---

## 1.6 Significance of the Project

The project is significant because it provides practical experience in several important areas of networking and security.

It demonstrates how:

**Client → LAN → Firewall/Router → NAT → WAN → Internet**

works in practice.

It also demonstrates the relationship between configuration and monitoring.

Therefore, the project combines:

- configuration;
- connectivity;
- security;
- discovery;
- monitoring;
- troubleshooting.

---

## 1.7 Methodology

The project follows a practical implementation methodology consisting of:

1. Requirement identification.
2. Network design.
3. Virtual machine preparation.
4. pfSense installation.
5. Interface configuration.
6. LAN configuration.
7. DHCP configuration.
8. Firewall configuration.
9. NAT configuration.
10. Ubuntu configuration.
11. Connectivity testing.
12. Nmap scanning.
13. tcpdump packet capture.
14. Result analysis.
15. Troubleshooting.
16. Documentation.

Testing is performed progressively. Local connectivity is checked before Internet connectivity, and IP connectivity is checked before DNS connectivity.

---

## 1.8 Organization of the Report

The report is organized into ten main chapters.

Chapter One introduces the project.

Chapter Two explains the theoretical concepts required to understand the implementation.

Chapter Three describes the system requirements and network design.

Chapter Four explains the practical implementation.

Chapter Five discusses Nmap scanning.

Chapter Six explains tcpdump traffic analysis.

Chapter Seven focuses specifically on NAT.

Chapter Eight presents testing and results.

Chapter Nine discusses challenges and solutions.

Chapter Ten provides the conclusion, recommendations, and future improvements.

---

# CHAPTER TWO — BACKGROUND AND THEORETICAL CONCEPTS

## 2.1 Introduction

This chapter presents the theoretical concepts required to understand the practical laboratory.

The main technologies discussed are:

- computer networking;
- IP addressing;
- DHCP;
- DNS;
- routing;
- firewalls;
- pfSense;
- NAT;
- Nmap;
- tcpdump;
- ICMP;
- TCP/UDP;
- virtualization.

---

## 2.2 Computer Networking

A computer network is a collection of interconnected devices that communicate using agreed protocols.

Devices may include:

- computers;
- servers;
- routers;
- switches;
- firewalls;
- wireless access points;
- printers;
- virtual machines.

Communication requires addressing and protocols.

Networking therefore involves several related functions:

**Addressing → Routing → Forwarding → Filtering → Translation → Monitoring**

---

## 2.3 Network Components

The major components in this project are:

### Client
Ubuntu acts as the client system.

### Firewall/Router
pfSense acts as the central firewall and routing device.

### Network Interface
Each virtual machine requires virtual network interfaces to communicate.

### WAN
The WAN interface provides connectivity toward the external network.

### LAN
The LAN interface provides internal network connectivity.

### Network Services
DHCP and DNS-related services support client network operation.

### Diagnostic Tools
Nmap and tcpdump provide network visibility.

---

## 2.4 LAN and WAN

### LAN
A Local Area Network connects devices within a limited area.

The laboratory LAN is: **192.168.1.0/24**

The pfSense LAN gateway is: **192.168.1.1**

### WAN
A Wide Area Network connects networks across a larger geographical area.

In this laboratory, the WAN represents the external network through which pfSense reaches the Internet.

The separation between LAN and WAN is important because pfSense can apply security and NAT policies between them.

---

## 2.5 IP Addressing

An IP address identifies a network interface logically.

IPv4 uses 32-bit addresses. An example is: **192.168.1.100**

An IPv4 address contains:
- network information;
- host information.

The subnet mask determines which portion identifies the network.

---

## 2.6 IPv4 Addressing

The laboratory uses IPv4. The main network is: **192.168.1.0/24**

The subnet mask is: **255.255.255.0**

The address range is: **192.168.1.0 — 192.168.1.255**

Normally:
- Network address = 192.168.1.0
- First usable address = 192.168.1.1
- Last usable address = 192.168.1.254
- Broadcast = 192.168.1.255

The pfSense LAN interface uses: **192.168.1.1**

---

## 2.7 Private IP Addresses

Private IPv4 addresses are intended for internal networks.

The major private ranges are:

| Range | CIDR |
|---|---|
| 10.0.0.0 — 10.255.255.255 | 10.0.0.0/8 |
| 172.16.0.0 — 172.31.255.255 | 172.16.0.0/12 |
| 192.168.0.0 — 192.168.255.255 | 192.168.0.0/16 |

The laboratory uses: **192.168.1.0/24**

Because this address space is private, NAT is normally required when internal hosts communicate with the public Internet.

---

## 2.8 Subnet Mask and CIDR

CIDR stands for Classless Inter-Domain Routing.

The notation **192.168.1.0/24** means that the first 24 bits identify the network.

The equivalent subnet mask is: **255.255.255.0**

The `/24` network provides 256 total addresses, of which 254 are normally usable for hosts.

---

## 2.9 Default Gateway

A default gateway is the device that forwards traffic destined for networks outside the local subnet.

In this laboratory: **Ubuntu → Default Gateway → pfSense LAN**

The gateway is: **192.168.1.1**

If Ubuntu wants to communicate with 8.8.8.8, the destination is outside 192.168.1.0/24, so Ubuntu sends the traffic to the default gateway.

---

## 2.10 DHCP

DHCP stands for Dynamic Host Configuration Protocol. It automatically provides network configuration to clients.

Information may include:
- IP address;
- subnet mask;
- default gateway;
- DNS server;
- lease information.

The normal DHCP process is commonly described as DORA:

**Discover → Offer → Request → Acknowledgement**

In the laboratory, pfSense provides DHCP service to the Ubuntu client.

---

## 2.11 DNS

DNS stands for Domain Name System. It converts domain names into IP addresses.

For example: **google.com → IP address**

The command:

```bash
nslookup google.com
```

can be used to test DNS resolution.

---

## 2.12 Routing

Routing is the process of determining where packets should be forwarded.

```text
Ubuntu
192.168.1.x
      |
      v
pfSense LAN
192.168.1.1
      |
      v
pfSense WAN
      |
      v
Internet
```

pfSense examines destination information and forwards traffic through the appropriate interface.

---

## 2.13 Firewall

A firewall controls network traffic according to configured rules.

Rules may consider:
- source address;
- destination address;
- protocol;
- source port;
- destination port;
- interface.

The firewall can allow, block, or log traffic.

---

## 2.14 pfSense

pfSense is a firewall and routing platform that provides a web-based management interface.

Important functions include:
- firewall;
- routing;
- NAT;
- DHCP;
- DNS-related services;
- VPN;
- diagnostics;
- interface management.

In this project, pfSense is the central network device. It separates the internal LAN from the external WAN and controls traffic between them.

---

## 2.15 NAT

NAT stands for Network Address Translation. It changes IP addressing as traffic passes between networks.

Conceptually:

```text
Before NAT:
Source = 192.168.1.100

After NAT:
Source = pfSense WAN address
```

This allows private LAN hosts to communicate with external networks.

---

## 2.16 Network Discovery

Network discovery is the process of identifying hosts and services available on a network.

Administrators can use discovery tools to:
- identify active hosts;
- identify open ports;
- identify services;
- understand the network attack surface.

Discovery should always be performed only against systems for which authorization has been obtained.

---

## 2.17 Nmap

Nmap stands for Network Mapper. It is commonly used for network discovery and security auditing.

Nmap can identify:
- reachable hosts;
- open ports;
- service information;
- version information under suitable conditions.

For this project, Nmap is used only against the authorized laboratory environment.

---

## 2.18 Packet Capture and Analysis

Packet capture provides visibility into actual network communication.

Packet analysis can show:
- source address;
- destination address;
- protocol;
- packet direction;
- packet count;
- ports;
- flags;
- responses.

This makes packet capture useful for troubleshooting.

---

## 2.19 tcpdump

tcpdump is a command-line packet capture utility. It can capture packets from a selected network interface.

For example:

```bash
sudo tcpdump -i enp0s3 icmp
```

The command means:
- `sudo` — execute with required privileges;
- `tcpdump` — start packet capture;
- `-i enp0s3` — capture on interface enp0s3;
- `icmp` — capture ICMP traffic.

---

## 2.20 ICMP

ICMP stands for Internet Control Message Protocol. It is used for network diagnostic and control messages.

The `ping` command uses ICMP Echo Request and Echo Reply messages.

```bash
ping -c 4 192.168.1.1
```

A tcpdump capture can show the corresponding ICMP traffic.

---

## 2.21 TCP and UDP

TCP provides connection-oriented and reliable communication.

Examples include:
- HTTP;
- HTTPS;
- SSH.

UDP is connectionless and has lower protocol overhead.

DNS commonly uses UDP port 53 for ordinary queries, although DNS can also use TCP under certain conditions.

---

## 2.22 Network Security Principles

The project demonstrates several network security principles.

### Confidentiality
Information should be protected from unauthorized access.

### Integrity
Information should not be improperly modified.

### Availability
Network services should remain accessible when required.

### Authentication
Users or systems should be identified before being granted access.

### Authorization
Users should only receive the permissions they require.

### Least Privilege
Only necessary access should be provided.

---

## 2.23 Virtualization in Networking

Virtualization allows multiple virtual computers to operate on a single physical computer.

A hypervisor such as VirtualBox or VMware can provide virtual:
- CPUs;
- memory;
- disks;
- network adapters.

The laboratory uses virtualization to create a network without requiring multiple physical computers. This reduces hardware requirements and makes experimentation easier.

---

# CHAPTER THREE — SYSTEM REQUIREMENTS AND NETWORK DESIGN

## 3.1 Introduction

This chapter describes the hardware, software, virtual machines, network adapters, IP addressing, and logical architecture used in the laboratory.

---

## 3.2 Hardware Requirements

The laboratory requires a computer capable of running virtualization software.

Recommended resources include:
- multi-core processor;
- at least 4 GB RAM;
- sufficient storage;
- network connectivity;
- virtualization support enabled where required.

More RAM is recommended when pfSense and Ubuntu are run simultaneously with additional tools.

---

## 3.3 Software Requirements

The main software components are:

| Software | Purpose |
|---|---|
| VirtualBox/VMware | Virtualization |
| pfSense | Firewall/router |
| Ubuntu | Client operating system |
| Nmap | Network discovery |
| tcpdump | Packet capture |
| Web Browser | pfSense WebGUI access |

---

## 3.4 Virtualization Environment

Two major virtual machines are used:

### VM 1 — pfSense
Role: **Firewall + Router + NAT + DHCP**

### VM 2 — Ubuntu
Role: **Network Client + Testing + Nmap + tcpdump**

---

## 3.5 Network Architecture

The logical architecture is:

```text
                              INTERNET
                                  |
                                WAN
                    +--------------+---------------+
                    |          pfSense             |
                    |    Firewall/Router           |
                    +--------------+---------------+
                                LAN
                                  |
                      192.168.1.1/24
                                  |
                    +-------------+-------------+
                    |         Ubuntu            |
                    |         Client            |
                    +---------------------------+
```

The communication path for Internet traffic is:

```text
Ubuntu → LAN → pfSense Firewall → NAT → WAN → Internet
```

---

## 3.6 Network Components

| Component | Role |
|---|---|
| pfSense | Firewall/router |
| Ubuntu | Client |
| LAN | Internal network |
| WAN | External network |
| DHCP | Automatic client addressing |
| DNS | Name resolution |
| NAT | Private-to-external translation |
| Nmap | Authorized network discovery |
| tcpdump | Packet analysis |

---

## 3.7 IP Addressing Plan

| Component | Address |
|---|---|
| LAN Network | 192.168.1.0/24 |
| pfSense LAN | 192.168.1.1/24 |
| Ubuntu | DHCP-assigned 192.168.1.x |
| Broadcast | 192.168.1.255 |
| Default Gateway | 192.168.1.1 |

The exact Ubuntu address should be recorded from the actual laboratory using:

```bash
ip -4 addr
```

---

## 3.8 Network Traffic Flow

For Internet communication:

1. Ubuntu creates a packet.
2. Ubuntu determines that the destination is outside its local subnet.
3. Ubuntu sends the packet to its default gateway.
4. pfSense receives the packet on the LAN interface.
5. pfSense applies firewall rules.
6. pfSense performs outbound NAT.
7. pfSense forwards the translated packet through WAN.
8. The external destination responds.
9. pfSense receives the response.
10. pfSense reverses the translation.
11. The response is forwarded to Ubuntu.

This process demonstrates why routing, firewalling, NAT, and addressing must all work correctly.

---

## 3.9 Security Design

The laboratory separates the internal LAN from the external WAN. pfSense provides the security boundary.

```text
UNTRUSTED/EXTERNAL NETWORK
            |
          WAN
            |
      [ pfSense ]
    Firewall/NAT
            |
          LAN
            |
        Ubuntu
```

This design allows security rules to be applied at the boundary.

---

## 3.10 Practical Evidence Methodology

Each major practical activity should follow this structure:

**Objective → Configuration → Command/Action → Output → Screenshot → Explanation → Result**

---

# CHAPTER FOUR — PRACTICAL IMPLEMENTATION

## 4.1 Introduction

This chapter explains how the laboratory was implemented.

---

## 4.2 Creating the pfSense Virtual Machine

A virtual machine was created for pfSense.

The VM should have:
- appropriate RAM;
- virtual CPU;
- virtual hard disk;
- pfSense ISO;
- two network adapters.

The two adapters are important because pfSense requires separate network interfaces for WAN and LAN operation.

---

## 4.3 Configuring pfSense Network Adapters

The recommended laboratory design is:

### Adapter 1
**NAT** — Purpose: **WAN/Internet**

### Adapter 2
**Host-Only/Internal/Private Network** — Purpose: **LAN**

The important requirement is that the Ubuntu VM must connect to the same virtual LAN network as pfSense's LAN adapter.

---

## 4.4 Installing pfSense

The pfSense ISO is attached to the virtual machine. The VM is then started and the installation procedure is followed.

After installation:
1. The system reboots.
2. The ISO is detached.
3. pfSense starts from the virtual disk.
4. Network interfaces are identified.
5. WAN and LAN assignments are confirmed.

---

## 4.5 Assigning WAN and LAN Interfaces

The interfaces must be correctly assigned.

Conceptually:
```text
em0 → WAN
em1 → LAN
```

The exact interface names may vary depending on the virtual network hardware.

Correct interface assignment is critical. If WAN and LAN are reversed, Internet connectivity and WebGUI access may fail.

---

## 4.6 Configuring the LAN Address

The pfSense LAN interface is configured with:

**IP address: 192.168.1.1**

**Subnet mask: /24**

Therefore: **LAN = 192.168.1.0/24**

The LAN interface becomes the default gateway for Ubuntu.

---

## 4.7 Accessing the pfSense WebGUI

After LAN configuration, the Ubuntu client can access the pfSense management interface through the LAN address.

The management address is: **192.168.1.1**

The WebGUI is used to configure:
- interfaces;
- firewall;
- DHCP;
- DNS-related settings;
- NAT;
- diagnostics.

---

## 4.8 Configuring DHCP

DHCP is configured on the LAN interface.

The DHCP pool must:
- belong to 192.168.1.0/24;
- exclude the pfSense gateway;
- avoid conflicts with static addresses.

For example, a pool may be: **192.168.1.100 — 192.168.1.200**

The Ubuntu client can then automatically obtain an address.

---

## 4.9 Configuring DNS

pfSense can provide or forward DNS-related services.

Ubuntu's configuration can be examined using:

```bash
resolvectl status
```

or:

```bash
cat /etc/resolv.conf
```

---

## 4.10 Configuring Firewall Rules

Firewall rules are configured under the pfSense firewall rule interface.

A LAN rule may allow required outbound communication.

Security should follow the principle:

**Allow required traffic; restrict unnecessary traffic.**

---

## 4.11 Configuring NAT

Navigate to: **Firewall → NAT → Outbound**

Automatic Outbound NAT can be selected when appropriate.

The general logic is:
```text
LAN private network
192.168.1.0/24
        ↓
Outbound NAT
        ↓
WAN address
        ↓
Internet
```

---

## 4.12 Preparing Ubuntu

Ubuntu is used as the client and testing platform.

After booting Ubuntu, the network interface is checked.

```bash
ip -4 addr
```

shows IPv4 addresses.

```bash
ip route
```

shows routing information.

---

## 4.13 Ubuntu Network Verification

Run:

```bash
ip -4 addr
```

This identifies the IPv4 address assigned to Ubuntu.

Then:

```bash
ip route
```

A route similar to:

```text
default via 192.168.1.1
```

indicates that pfSense is being used as the default gateway.

---

## 4.14 Gateway Connectivity Test

```bash
ping -c 4 192.168.1.1
```

If the result shows **0% packet loss** then Ubuntu can communicate with pfSense.

---

## 4.15 Internet Connectivity Test

```bash
ping -c 4 8.8.8.8
```

This tests IP connectivity without depending on DNS name resolution.

---

## 4.16 DNS Connectivity Test

```bash
nslookup google.com
```

If an IP address is returned, the DNS lookup succeeded.

---

## 4.17 End-to-End Connectivity

```bash
ping -c 4 google.com
```

This test combines:
1. DNS resolution;
2. IP communication;
3. routing;
4. firewall handling;
5. NAT;
6. return traffic.

A successful result demonstrates end-to-end functionality.

---

# CHAPTER FIVE — NMAP NETWORK SCANNING

## 5.1 Introduction

Nmap is used in this project to perform authorized network discovery. The purpose is not to attack systems but to understand the services exposed by the laboratory devices.

---

## 5.2 Purpose of Nmap

Nmap can help determine:
- whether a host is reachable;
- which ports are accessible;
- which services may be running;
- possible service/version information.

---

## 5.3 Installing Nmap

Update Ubuntu:

```bash
sudo apt update
```

Install Nmap:

```bash
sudo apt install nmap
```

Verify:

```bash
nmap --version
```

---

## 5.4 Checking the Ubuntu IP Address

Before scanning, identify the Ubuntu address:

```bash
ip -4 addr
```

The laboratory subnet is: **192.168.1.0/24**

---

## 5.5 Basic Host Scan

A basic authorized scan of the pfSense LAN address is:

```bash
nmap 192.168.1.1
```

The actual ports reported must be taken from the real Nmap output.

---

## 5.6 Port Scanning

A specific port can be tested using:

```bash
nmap -p 80 192.168.1.1
```

Multiple ports can be tested:

```bash
nmap -p 22,53,80,443 192.168.1.1
```

The possible results include:
- **open** — An application is listening and reachable.
- **closed** — The host is reachable, but no application is accepting connections on that port.
- **filtered** — A firewall or filtering mechanism prevents Nmap from determining the state clearly.

---

## 5.7 Service and Version Detection

```bash
sudo nmap -sV 192.168.1.1
```

The `-sV` option attempts to identify services and versions.

---

## 5.8 Selected-Port Scanning

```bash
nmap -p 22,53,80,443 192.168.1.1
```

The report should include the screenshot of the command and complete relevant output.

---

## 5.9 Interpreting Nmap Results

Nmap results provide information about the exposed attack surface.

For example:

```text
PORT        STATE   SERVICE
443/tcp     open    https
```

would indicate that TCP port 443 is reachable and Nmap identified HTTPS-related service behavior.

However, if the output shows:

```text
443/tcp   filtered
```

the report must state that the port is filtered, not open.

---

## 5.10 Security Considerations

Nmap scanning should only be performed against:
- systems you own;
- systems you administer;
- systems for which you have explicit authorization.

In this project, the scan target is part of the controlled laboratory.

---

# CHAPTER SIX — TCPDUMP TRAFFIC ANALYSIS

## 6.1 Introduction

tcpdump provides packet-level visibility. It is especially useful because a successful ping only tells us that communication succeeded. tcpdump can show the packets responsible for that communication.

---

## 6.2 Checking Network Interfaces

Run:

```bash
ip link
```

or:

```bash
ip -br addr
```

The interface may be named `enp0s3` but interface names can vary. The actual interface name should always be taken from the Ubuntu system.

---

## 6.3 Capturing ICMP Traffic

Start:

```bash
sudo tcpdump -i enp0s3 icmp
```

Then open another terminal:

```bash
ping -c 4 8.8.8.8
```

tcpdump should display ICMP packets if the selected interface carries that traffic.

---

## 6.4 Capturing DNS Traffic

A DNS capture can be performed using:

```bash
sudo tcpdump -i enp0s3 port 53
```

Then execute:

```bash
nslookup google.com
```

---

## 6.5 Capturing ICMP and DNS Together

Use:

```bash
sudo tcpdump -i enp0s3 'port 53 or icmp'
```

Then perform:

```bash
nslookup google.com
```

and:

```bash
ping -c 2 google.com
```

---

## 6.6 Saving Packet Captures

A capture can be saved:

```bash
sudo tcpdump -i enp0s3 'port 53 or icmp' -w network-test.pcap
```

The `-w` option writes packets to a PCAP file. The file can later be examined using tcpdump or Wireshark.

---

## 6.7 Reading Capture Statistics

When tcpdump is stopped using **Ctrl+C**, it displays statistics such as:
- packets captured;
- packets received by filter;
- packets dropped by kernel, where applicable.

---

## 6.8 Interpreting Packets

For an ICMP packet, important fields include:
- source address;
- destination address;
- ICMP type;
- sequence number;
- packet size.

For DNS traffic, relevant information may include:
- source;
- destination;
- UDP/TCP;
- port 53;
- query/response information.

---

## 6.9 Packet-Level NAT Analysis

NAT can be demonstrated more strongly by capturing traffic on both sides of pfSense.

On the LAN side:
```text
Source = Ubuntu private address
```

On the WAN side:
```text
Source = pfSense WAN-side address
```

This provides practical evidence that pfSense translated the source address before forwarding the traffic.

---

# CHAPTER SEVEN — NAT CONFIGURATION AND VERIFICATION

## 7.1 Introduction

NAT is one of the central technologies in this project because the Ubuntu client uses a private address while accessing an external network.

---

## 7.2 Purpose of NAT

Private addresses are intended for internal networks and are not normally routed directly across the public Internet.

NAT solves this problem by translating the private source address.

```text
Ubuntu: 192.168.1.100
        ↓
pfSense NAT
        ↓
WAN address
```

---

## 7.3 Private and External Addressing

The Ubuntu client may use: **192.168.1.x** (private address)

pfSense has a WAN-side address provided by the external/virtual network.

The NAT process allows Ubuntu's traffic to leave through the WAN.

---

## 7.4 pfSense Outbound NAT

Navigate to: **Firewall → NAT → Outbound**

The system can use automatic outbound NAT. The NAT configuration should be examined and documented.

---

## 7.5 Automatic Outbound NAT

Automatic outbound NAT generates the appropriate translation rules for internal networks.

Conceptually:

```text
Source:
192.168.1.0/24

Interface:
WAN

NAT Address:
WAN address
```

---

## 7.6 NAT Traffic Flow

The complete process is:

```text
[Ubuntu]
192.168.1.100
      |
      | Private traffic
      v
[pfSense LAN]
192.168.1.1
      |
      | Firewall processing
      v
[NAT]
      |
      | Translated source
      v
[pfSense WAN]
      |
      v
[Internet]
```

The response follows the reverse path.

---

## 7.7 NAT Verification

NAT can be verified indirectly through successful outbound connectivity:

```bash
ping -c 4 8.8.8.8
```

and:

```bash
ping -c 4 google.com
```

---

## 7.8 Packet-Level NAT Verification

A LAN-side capture can show:

```text
Source = 192.168.1.x
```

while a WAN-side capture can show:

```text
Source = WAN address
```

This demonstrates address translation at the packet level.

---

# CHAPTER EIGHT — TESTING AND RESULTS

## 8.1 Introduction

Testing verifies whether the implemented network performs according to the design. Testing should proceed from simple local tests to more complex end-to-end tests.

---

## 8.2 Testing Methodology

The recommended order is:

1. Check interface status.
2. Check IP address.
3. Check routing table.
4. Test pfSense gateway.
5. Test external IP.
6. Test DNS.
7. Test domain connectivity.
8. Verify DHCP.
9. Verify NAT.
10. Perform Nmap scanning.
11. Perform tcpdump analysis.

---

## 8.3 Gateway Connectivity Test

**Command:**

```bash
ping -c 4 192.168.1.1
```

**Purpose:** To verify Ubuntu-to-pfSense communication.

**Result:** 0% packet loss

**Interpretation:** Ubuntu successfully reached the pfSense LAN gateway.

---

## 8.4 Internet IP Connectivity Test

**Command:**

```bash
ping -c 4 8.8.8.8
```

**Purpose:** To test Internet connectivity without depending on DNS.

**Result:** 0% packet loss

**Interpretation:** The Ubuntu client was able to communicate with the external IP through pfSense.

---

## 8.5 DNS Resolution Test

**Command:**

```bash
nslookup google.com
```

**Purpose:** To verify domain-name resolution.

**Interpretation:** DNS resolution was functioning during the test.

---

## 8.6 Domain Connectivity Test

**Command:**

```bash
ping -c 4 google.com
```

**Purpose:** To test DNS resolution and IP connectivity together.

**Result:** 0% packet loss

---

## 8.7 DHCP Verification

On Ubuntu:

```bash
ip -4 addr
```

and:

```bash
ip route
```

These commands verify the address and gateway assigned to the client.

---

## 8.8 NAT Verification

NAT configuration should be checked through:

**Firewall → NAT → Outbound**

The Internet connectivity test provides functional evidence that outbound communication works.

---

## 8.9 Nmap Verification

Run:

```bash
nmap 192.168.1.1
```

and, where required:

```bash
sudo nmap -sV 192.168.1.1
```

The actual results should be included as screenshots.

---

## 8.10 tcpdump Verification

Run:

```bash
sudo tcpdump -i enp0s3 icmp
```

Then:

```bash
ping -c 4 8.8.8.8
```

For DNS:

```bash
sudo tcpdump -i enp0s3 'port 53 or icmp'
```

Then perform:

```bash
nslookup google.com
```

and:

```bash
ping -c 2 google.com
```

---

## 8.11 Overall Results

| Test | Method | Purpose |
|---|---|---|
| LAN Gateway | `ping -c 4 192.168.1.1` | Test Ubuntu-to-pfSense connectivity |
| Internet IP | `ping -c 4 8.8.8.8` | Test external IP connectivity |
| DNS | `nslookup google.com` | Test name resolution |
| Domain | `ping -c 4 google.com` | Test DNS + connectivity |
| DHCP | `ip -4 addr` | Verify client addressing |
| Routing | `ip route` | Verify default gateway |
| NAT | pfSense Outbound NAT | Verify translation configuration |
| Nmap | `nmap 192.168.1.1` | Discover accessible services |
| Nmap Service | `nmap -sV 192.168.1.1` | Attempt service identification |
| tcpdump | ICMP capture | Observe ICMP traffic |
| tcpdump | DNS/ICMP capture | Observe DNS and ICMP traffic |

---

# CHAPTER NINE — CHALLENGES AND SOLUTIONS

## 9.1 Introduction

Networking laboratories often encounter configuration problems because several components must work together.

A failure may be caused by:
- incorrect virtual adapter configuration;
- incorrect IP address;
- incorrect gateway;
- DHCP failure;
- firewall rules;
- NAT;
- DNS;
- incorrect interface selection.

---

## 9.2 Virtual Network Adapter Problems

If the Ubuntu VM and pfSense LAN interface are connected to different virtual networks, they cannot communicate.

**Solution:** Ensure both are connected to the same internal/host-only/private virtual network.

---

## 9.3 DHCP Problems

If Ubuntu does not receive an IP address automatically, possible causes include:
- DHCP disabled;
- wrong LAN interface;
- wrong virtual network;
- incorrect DHCP range.

**Solution:** Check `ip -4 addr` and verify DHCP configuration in pfSense.

---

## 9.4 Gateway Connectivity Problems

If `ping -c 4 192.168.1.1` fails, Internet testing should not be attempted first.

Check:
1. Ubuntu interface;
2. Ubuntu IP;
3. subnet mask;
4. pfSense LAN address;
5. virtual network;
6. firewall configuration.

---

## 9.5 Internet Connectivity Problems

If the gateway works but `ping -c 4 8.8.8.8` fails, investigate:
- pfSense WAN;
- default route;
- firewall rules;
- NAT;
- upstream connectivity.

---

## 9.6 DNS Problems

If `ping -c 4 8.8.8.8` works but `nslookup google.com` fails, the problem is likely related to DNS rather than basic IP connectivity.

Check:
- DNS configuration;
- resolver;
- pfSense DNS service;
- Ubuntu resolver configuration.

---

## 9.7 NAT Problems

If Ubuntu can reach pfSense but cannot reach the Internet, check:

**Firewall → NAT → Outbound**

Verify that the private LAN network has an appropriate outbound NAT rule.

---

## 9.8 Nmap Scanning Problems

Nmap may show different results depending on firewall rules.

A port may be open, closed, or filtered. The firewall can therefore affect what Nmap can observe.

The report must use the actual Nmap output rather than assumptions.

---

## 9.9 tcpdump Interface Problems

If tcpdump captures nothing, the selected interface may not carry the traffic.

Check:

```bash
ip link
```

or:

```bash
ip -br addr
```

Then select the correct interface.

---

## 9.10 Lessons Learned

The project demonstrates that network troubleshooting should be systematic.

A good sequence is:

```text
Interface → IP Address → Gateway → Routing → Firewall → NAT → DNS → Application
```

Testing in this order reduces unnecessary troubleshooting.

---

# CHAPTER TEN — CONCLUSION AND RECOMMENDATIONS

## 10.1 Conclusion

The internship project successfully demonstrates the design and implementation of a practical secure network laboratory using pfSense, Ubuntu, NAT, Nmap, and tcpdump.

pfSense was used as the central firewall and router, providing the connection between the internal LAN and external WAN. The LAN was configured using the private IPv4 network **192.168.1.0/24**, with **192.168.1.1/24** configured as the pfSense LAN gateway.

Ubuntu was connected to the internal network and used as the main client and network testing platform. DHCP provided automatic network configuration, while IP addressing and routing were verified using Linux networking commands.

Connectivity tests demonstrated communication between Ubuntu and the pfSense gateway. Internet connectivity was tested using an external IP address, while DNS functionality was tested using `nslookup` and domain-based connectivity tests.

Nmap provided a practical method for authorized network and service discovery. It demonstrated how administrators can identify accessible ports and services within a controlled environment.

tcpdump provided packet-level visibility. ICMP and DNS-related traffic could be observed during connectivity and name-resolution tests, helping demonstrate how network communication occurs at the packet level.

NAT was particularly important because it allowed private LAN addresses to communicate through the WAN connection. The project therefore demonstrated the relationship between private addressing, routing, firewall rules, NAT, DNS, network discovery, and packet analysis.

Overall, the project provided practical experience in network implementation, security, monitoring, testing, and troubleshooting.

---

## 10.2 Recommendations

The following improvements are recommended:

### 1. Use Strong Administrative Credentials
The pfSense administrative account should use a strong password.

### 2. Restrict Management Access
Management interfaces should not be exposed unnecessarily to untrusted networks.

### 3. Minimize Exposed Services
Only required services should be enabled.

### 4. Maintain Firewall Rules
Firewall rules should be reviewed regularly.

### 5. Perform Authorized Network Scanning
Nmap scans should be performed periodically against authorized systems.

### 6. Monitor Network Traffic
tcpdump or another packet-analysis tool can be used when investigating suspicious or unexpected traffic.

### 7. Back Up Configuration
pfSense configuration backups should be maintained.

### 8. Document Network Changes
Every major configuration change should be recorded.

### 9. Use Network Segmentation
Future versions of the laboratory can introduce VLANs to separate clients, servers, management systems, and other network segments.

### 10. Introduce VPN
A future version can implement a site-to-site or remote-access VPN.

---

## 10.3 Future Improvements

Future work may extend the laboratory with:

- VLAN segmentation;
- multiple Ubuntu clients;
- additional servers;
- IDS/IPS;
- VPN;
- IPv6;
- centralized logging;
- network monitoring;
- Wireshark analysis;
- multiple pfSense firewalls;
- redundancy;
- cloud networking;
- OSPF;
- site-to-site VPN;
- more advanced firewall policies.

---

# REFERENCES

1. pfSense Documentation — Firewall, NAT, interfaces, DHCP, DNS, and diagnostics.

2. Nmap Documentation and Reference Guide — Network discovery and service identification.

3. Ubuntu Documentation — Network configuration and Linux administration.

4. tcpdump Manual — Packet capture and filtering.

5. Computer Networking Fundamentals — IP addressing, routing, DNS, DHCP, TCP/IP, and network security.

6. VirtualBox/VMware Documentation — Virtual machine and virtual network configuration.

---

# APPENDIX A — COMMAND REFERENCE

## A.1 Display IPv4 Address

```bash
ip -4 addr
```

**Purpose:** Displays IPv4 addresses assigned to interfaces.

---

## A.2 Display Interfaces

```bash
ip link
```

**Purpose:** Displays network interfaces and their states.

---

## A.3 Display Routing Table

```bash
ip route
```

**Purpose:** Displays routes and the default gateway.

---

## A.4 Test pfSense Gateway

```bash
ping -c 4 192.168.1.1
```

**Purpose:** Tests local LAN connectivity.

---

## A.5 Test External IP

```bash
ping -c 4 8.8.8.8
```

**Purpose:** Tests external IP connectivity without relying on DNS.

---

## A.6 Test DNS

```bash
nslookup google.com
```

**Purpose:** Tests DNS resolution.

---

## A.7 Test Domain Connectivity

```bash
ping -c 4 google.com
```

**Purpose:** Tests DNS resolution and IP connectivity together.

---

## A.8 Update Ubuntu Packages

```bash
sudo apt update
```

**Purpose:** Updates package information.

---

## A.9 Install Nmap

```bash
sudo apt install nmap
```

**Purpose:** Installs Nmap.

---

## A.10 Check Nmap Version

```bash
nmap --version
```

**Purpose:** Confirms that Nmap is installed.

---

## A.11 Basic Nmap Scan

```bash
nmap 192.168.1.1
```

**Purpose:** Scans the authorized pfSense laboratory host.

---

## A.12 Nmap Service Detection

```bash
sudo nmap -sV 192.168.1.1
```

**Purpose:** Attempts to identify services and versions.

---

## A.13 Selected-Port Scan

```bash
nmap -p 22,53,80,443 192.168.1.1
```

**Purpose:** Tests selected TCP ports.

---

## A.14 Capture ICMP

```bash
sudo tcpdump -i enp0s3 icmp
```

**Purpose:** Captures ICMP packets.

---

## A.15 Capture DNS

```bash
sudo tcpdump -i enp0s3 port 53
```

**Purpose:** Captures traffic associated with port 53.

---

## A.16 Capture DNS and ICMP

```bash
sudo tcpdump -i enp0s3 'port 53 or icmp'
```

**Purpose:** Captures both DNS-port traffic and ICMP traffic.

---

## A.17 Save Packet Capture

```bash
sudo tcpdump -i enp0s3 'port 53 or icmp' -w network-test.pcap
```

**Purpose:** Saves captured packets to a PCAP file.

---

## A.18 Display Listening Services

```bash
ss -tuln
```

**Purpose:** Displays listening TCP and UDP sockets on Ubuntu.

---

# APPENDIX B — SCREENSHOT/EVIDENCE CHECKLIST

## Figure 1 — Virtual Machine Configuration

**Evidence should show:**
- pfSense VM;
- Ubuntu VM;
- memory;
- CPU;
- network adapters.

**Explanation:** The screenshot demonstrates the virtualization environment used to create the laboratory.

---

## Figure 2 — pfSense Console

**Evidence should show:**
- WAN interface;
- LAN interface;
- interface addresses.

**Explanation:** This verifies the initial pfSense network configuration.

---

## Figure 3 — pfSense LAN Configuration

**Evidence should show:** **192.168.1.1/24**

**Explanation:** This confirms the LAN gateway configuration.

---

## Figure 4 — pfSense DHCP Configuration

**Evidence should show:**
- DHCP enabled;
- LAN interface;
- address pool.

**Explanation:** This demonstrates automatic IP address allocation.

---

## Figure 5 — Ubuntu IP Address

**Command:** `ip -4 addr`

**Explanation:** The screenshot demonstrates the IPv4 address assigned to the Ubuntu client.

---

## Figure 6 — Ubuntu Routing Table

**Command:** `ip route`

**Explanation:** The screenshot demonstrates the default gateway and connected network routes.

---

## Figure 7 — Gateway Ping

**Command:** `ping -c 4 192.168.1.1`

**Explanation:** This proves local connectivity between Ubuntu and pfSense.

---

## Figure 8 — Internet Ping

**Command:** `ping -c 4 8.8.8.8`

**Explanation:** This demonstrates external IP connectivity.

---

## Figure 9 — DNS Resolution

**Command:** `nslookup google.com`

**Explanation:** This demonstrates successful DNS name resolution.

---

## Figure 10 — Domain Ping

**Command:** `ping -c 4 google.com`

**Explanation:** This demonstrates successful DNS resolution followed by network connectivity.

---

## Figure 11 — Firewall Rules

**Evidence should show:** pfSense firewall rules.

**Explanation:** The screenshot demonstrates how pfSense controls network traffic.

---

## Figure 12 — NAT Configuration

**Evidence should show:** Firewall → NAT → Outbound.

**Explanation:** This demonstrates the configured outbound NAT mechanism for private LAN traffic.

---

## Figure 13 — Nmap Installation

**Command:** `nmap --version`

**Explanation:** This confirms Nmap is installed.

---

## Figure 14 — Nmap Basic Scan

**Command:** `nmap 192.168.1.1`

**Explanation:** This demonstrates authorized discovery of accessible services on the pfSense laboratory host.

---

## Figure 15 — Nmap Service Detection

**Command:** `sudo nmap -sV 192.168.1.1`

**Explanation:** This demonstrates service/version detection where supported.

---

## Figure 16 — tcpdump ICMP Capture

**Commands:**
```bash
sudo tcpdump -i enp0s3 icmp
ping -c 4 8.8.8.8
```

**Explanation:** The screenshot demonstrates ICMP Echo Request and Echo Reply traffic.

---

## Figure 17 — tcpdump DNS Capture

**Commands:**
```bash
sudo tcpdump -i enp0s3 'port 53 or icmp'
nslookup google.com
```

**Explanation:** The screenshot demonstrates packet-level observation of DNS-related and/or ICMP traffic on the selected interface.

---

## Figure 18 — Saved PCAP

**Command:**
```bash
sudo tcpdump -i enp0s3 'port 53 or icmp' -w network-test.pcap
```

**Explanation:** This demonstrates that network traffic was saved for later analysis.

---

## Figure 19 — NAT Packet Analysis

**Evidence should show:** LAN-side packet source and WAN-side translated source.

**Explanation:** This provides packet-level evidence of NAT translation.

---

# SCREENSHOT STANDARDS

Every screenshot included in the final report should follow these standards:

1. Clearly show the device or VM name.
2. Clearly show the command or configuration page.
3. Show the complete relevant output.
4. Avoid unrelated information.
5. Use a readable terminal size.
6. Do not crop important command output.
7. Include the figure number in the report.
8. Include a descriptive caption.
9. Explain what the screenshot proves.
10. Ensure the screenshot corresponds to the actual configuration.
11. Do not claim a result that is not visible in the evidence.
12. Use consistent figure numbering throughout the report.

---

# EXAMPLE FIGURE CAPTION FORMAT

**Figure 7: Ubuntu-to-pfSense LAN Gateway Connectivity Test**

The figure demonstrates that the Ubuntu client successfully communicated with the pfSense LAN gateway at 192.168.1.1. The successful replies and absence of packet loss confirm local connectivity between the client and firewall/router.

---

# FINAL PROJECT TRAFFIC FLOW

```text
                              INTERNET
                                  |
                                WAN
                    +-------------+-------------+
                    |          pfSense          |
                    |                           |
                    |   Firewall                |
                    |   Router                  |
                    |   NAT                     |
                    |   DHCP/DNS                |
                    +-------------+-------------+
                                  |
                                LAN
                                  |
                      192.168.1.1/24
                                  |
                    +-------------+-------------+
                    |         Ubuntu            |
                    |         Client            |
                    +---------------------------+
                                  |
                   +--------------+--------------+
                   |              |              |
                 Ping            DNS           Nmap
                   |              |              |
                   +--------------+--------------+
                                  |
                              tcpdump
                                  |
                          Packet Analysis
```

**The overall communication process:**

```text
Ubuntu
  ↓ IP Address
  ↓ Default Gateway
  ↓ pfSense Firewall
  ↓ Firewall Rule
  ↓ NAT
  ↓ WAN
  ↓ Internet
  ↓ Response
  ↓ pfSense
  ↓ NAT Reverse Translation
  ↓ Ubuntu
```

This architecture demonstrates how the major technologies used in the project operate together rather than functioning as independent tools.
