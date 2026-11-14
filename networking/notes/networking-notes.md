# Networking Fundamentals — CoderCo DevOps

## 1. Introduction to Networking

Computer networking allows devices to communicate and exchange data.

- **LAN (Local Area Network):** Connects devices within a limited area, such as a home or office.
- **WAN (Wide Area Network):** Connects networks across larger geographical areas.
- **Router:** Forwards packets between different networks using routing tables.
- **Switch:** Connects devices within a local network and forwards Ethernet frames using MAC addresses.

## 2. OSI and TCP/IP Models

The OSI model divides network communication into seven layers:

| Layer | Name | Responsibility |
|---|---|---|
| 7 | Application | Network services used by applications, such as HTTP and DNS |
| 6 | Presentation | Data formatting, encoding and encryption |
| 5 | Session | Managing communication sessions |
| 4 | Transport | End-to-end transport using TCP or UDP |
| 3 | Network | Logical addressing and routing using IP |
| 2 | Data Link | Local network delivery using MAC addresses |
| 1 | Physical | Transmission of bits over physical media |

The TCP/IP model is commonly represented using four layers: Application, Transport, Internet and Link.

**Encapsulation** occurs when protocol headers are added as data moves down the networking stack. **Decapsulation** removes the relevant protocol information as data moves up the receiving stack.

## 3. IP Addressing and Subnetting

An IP address identifies a network interface for communication using the Internet Protocol.

- **IPv4:** Uses 32-bit addresses, such as `192.168.1.10`.
- **IPv6:** Uses 128-bit addresses.
- **Private IP:** Used for internal network communication and generally not directly reachable from the public internet.
- **Public IP:** Used for internet-facing communication.

### CIDR and Subnetting

CIDR notation specifies how many bits belong to the network prefix.

Examples:

| CIDR | Subnet Mask | Usable IPv4 Hosts (Typical) |
|---|---|---|
| /24 | 255.255.255.0 | 254 |
| /26 | 255.255.255.192 | 62 |
| /27 | 255.255.255.224 | 30 |

Subnetting divides larger networks into smaller logical networks, helping organise addressing and control network boundaries.

## 4. DNS and DHCP

### DNS — Domain Name System

DNS translates domain names into information such as IP addresses.

Common record types:

- **A:** Maps a domain name to an IPv4 address.
- **AAAA:** Maps a domain name to an IPv6 address.
- **CNAME:** Creates an alias pointing to another domain name.
- **MX:** Identifies mail servers for a domain.

In my AWS project, I configured a Cloudflare A record pointing my domain to my EC2 instance's public IPv4 address.

### DHCP — Dynamic Host Configuration Protocol

DHCP automatically provides network configuration to clients, including IP addresses, subnet masks, default gateways and DNS server information.

The typical DHCP process is:

1. Discover
2. Offer
3. Request
4. Acknowledge

## 5. TCP, UDP and Ports

### TCP

TCP is a connection-oriented transport protocol that provides reliable, ordered delivery of data.

It uses mechanisms including acknowledgements, sequence numbers and retransmissions.

### UDP

UDP is connectionless and has less protocol overhead. It does not guarantee delivery or ordering.

Applications can use UDP where low latency is important or implement reliability themselves.

### Common Ports

| Protocol or Service | Port |
|---|---|
| SSH | TCP 22 |
| DNS | UDP/TCP 53 |
| HTTP | TCP 80 |
| HTTPS | TCP 443 |

In my project, I used SSH on port 22 to administer my Ubuntu instance and HTTP on port 80 to access NGINX.

## 6. Routing and NAT

### Routing

Routers use routing tables to determine where packets should be forwarded.

- **Static routing:** Routes configured manually.
- **Dynamic routing:** Routes learned or updated through routing protocols.
- **OSPF:** A routing protocol commonly used within organisations.
- **BGP:** A routing protocol used to exchange reachability information between autonomous systems.

### NAT — Network Address Translation

NAT translates IP address information as traffic passes through a network device.

Common types include:

- **Static NAT:** A fixed one-to-one address mapping.
- **Dynamic NAT:** Uses addresses from a configured pool.
- **PAT:** Allows multiple private addresses to share a public address by translating ports.

## 7. Network Troubleshooting

Common troubleshooting commands:

```bash
ping 8.8.8.8
traceroute example.com
nslookup example.com
```

- **ping:** Tests whether a host responds to ICMP echo requests and measures round-trip time.
- **traceroute:** Helps identify the network path towards a destination.
- **nslookup:** Queries DNS to investigate name resolution.

A failed ping does not automatically mean the internet connection is down, because ICMP traffic may be blocked.

## 8. AWS Networking Concepts

### VPC — Virtual Private Cloud

A VPC is a logically isolated virtual network in AWS where cloud resources can be deployed.

### EC2

Amazon EC2 provides virtual servers that can run operating systems and applications.

### Security Groups

Security groups are stateful virtual firewalls controlling allowed inbound and outbound traffic for associated resources.

For my project, I configured:

- SSH (TCP 22) restricted to my public IPv4 address.
- HTTP (TCP 80) open to internet users.

### Public and Private IP Addresses

My EC2 instance used a private IPv4 address within the VPC and a public IPv4 address for internet connectivity.

## 9. Practical Application

Through the CoderCo networking assignment, I:

- Deployed an Ubuntu Linux server on AWS EC2.
- Connected remotely using SSH authentication.
- Installed and verified an NGINX web server.
- Configured inbound security group rules.
- Created a Cloudflare DNS A record.
- Verified that my website was accessible through its domain name.

This project helped connect theoretical networking concepts with practical cloud infrastructure configuration.