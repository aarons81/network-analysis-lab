Network Analysis Lab — Nmap & Wireshark

A hands-on lab in which I mapped and analyzed my own home network using Nmap and Wireshark to build core network-security fundamentals: host discovery, service enumeration, and packet-level traffic analysis.

Objective

Before working with higher-level tooling like a SIEM, I wanted a solid grasp of what a network actually looks like at the packet level — what devices are present, what services they expose, and what normal traffic looks like on the wire. This lab establishes that baseline, which higher-level security work depends on.

Scope & authorization

All activity was limited to devices I personally own on my own home network. No external, third-party, or employer systems were scanned or captured. Defining scope up front — the rules of engagement — is a standard part of any legitimate security assessment.

Tools
Nmap — host discovery and service/version enumeration
Wireshark — live packet capture and traffic analysis
Windows 11 host (no virtualization required)
Network mapping with Nmap

Host discovery. Used Nmap to identify the live hosts on my local subnet and build an inventory of what was connected. The first step in any assessment is establishing what exists before probing further.

Show Image

Service enumeration. Ran a version-detection scan against a device I own to see which ports were open and what software was listening behind them. Open ports represent attack surface, and version detection is the bridge from "a port is open" to "this specific software is running here."

Show Image

Traffic analysis with Wireshark

ICMP (ping). Captured live traffic and isolated my own ping to a public DNS server — the echo request and echo reply that define what "ping" actually is.

Show Image

DNS resolution. Followed a DNS query and its response — the lookup that turns a domain name into an IP address before any connection is made.

Show Image

Unencrypted HTTP. Captured a plain HTTP request and read it in clear text, including the request and response contents.

Show Image

Encrypted TLS. Captured a normal HTTPS session showing the TLS handshake followed by encrypted application data that cannot be read on the wire — a practical illustration of why HTTPS matters.

Show Image

TCP three-way handshake. Isolated the SYN / SYN-ACK / ACK exchange that opens every TCP connection before data is allowed to flow.

Show Image

Capstone — capturing a scan

Ran an Nmap scan against a device I own while capturing in Wireshark, then filtered to the target to see the scan from the defender's perspective: a single source sending SYN packets to many ports in seconds — the same pattern an intrusion detection system or SIEM flags as suspicious. Observing one action from both sides, running the scan and watching it on the wire, connects offensive activity to what a defender actually sees.

Show Image

Key takeaways
Discovery and enumeration precede deeper analysis; you establish what exists before probing it.
Open ports are attack surface, and version detection ties a listening service to specific software that can be checked against known vulnerabilities.
Most web traffic is TLS-encrypted — visible as a handshake without readable payload — which is the practical reason HTTPS is standard.
Seeing a port scan from both sides connects the action to what a defender observes in monitoring tooling.
Next

Building a Wazuh SIEM lab to extend this into centralized log collection, endpoint telemetry, and detection.
