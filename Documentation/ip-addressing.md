# IP Addressing Scheme - Carlos NetPro Enterprise Network

## 🏢 Headquarters (HQ) - 10.0.0.0/16

### Subnet Allocation

| Subnet | CIDR | VLAN | Purpose | Gateway |
|--------|------|------|---------|---------|
| 10.0.0.0 | /23 | 50 | Management | 10.0.0.1 |
| 10.0.2.0 | /23 | 60 | Servers | 10.0.2.1 |
| 10.0.4.0 | /24 | 10 | Data | 10.0.4.1 |
| 10.0.5.0 | /24 | 20 | Voice | 10.0.5.1 |
| 10.0.6.0 | /24 | 30 | Guest | 10.0.6.1 |
| 10.0.7.0 | /24 | 40 | IoT | 10.0.7.1 |
| 10.0.8.0 | /24 | 70 | OOB Management | 10.0.8.1 |
| 10.0.100.0 | /29 | - | WAN (To FortiGate) | - |
| 10.0.200.0 | /30 | - | WAN (Secondary) | - |

---

### Network Devices - HQ

| Device | Interface | IP Address | VLAN | Description |
|--------|-----------|------------|------|-------------|
| **CORE1** | Vlan10 | 10.0.4.1 | 10 | Gateway - Data VLAN |
| | Vlan20 | 10.0.5.1 | 20 | Gateway - Voice VLAN |
| | Vlan30 | 10.0.6.1 | 30 | Gateway - Guest VLAN |
| | Vlan40 | 10.0.7.1 | 40 | Gateway - IoT VLAN |
| | Vlan50 | 10.0.0.1 | 50 | Gateway - Management |
| | Vlan60 | 10.0.2.1 | 60 | Gateway - Servers |
| | Eth3/0 | 10.0.100.2 | - | Uplink to FortiGate |
| | Eth3/2 | 10.0.200.2 | - | Secondary WAN |
| | Router-ID | 4.4.4.4 | - | OSPF Router ID |
| **CORE2** | Vlan10 | 10.0.4.2 | 10 | Backup Gateway |
| | Vlan20 | 10.0.5.2 | 20 | Backup Gateway |
| | Vlan30 | 10.0.6.2 | 30 | Backup Gateway |
| | Vlan40 | 10.0.7.2 | 40 | Backup Gateway |
| | Vlan50 | 10.0.0.2 | 50 | Backup Gateway |
| | Vlan60 | 10.0.2.2 | 60 | Backup Gateway |
| | Eth3/0 | 10.0.100.3 | - | Backup Uplink |
| | Eth3/2 | 10.0.200.3 | - | Secondary WAN |
| | Router-ID | 5.5.5.5 | - | OSPF Router ID |
| **HQ-ROUTER** | G0/0 | 192.168.201.174 | - | LAN Interface |
| | G0/1 | 172.16.1.2 | - | Internal Network |
| | G0/2 | 10.0.100.1 | - | Uplink to CORE1 |
| | Tunnel0 | 10.10.2.1 | - | VPN to Branch (Cisco) |
| | Tunnel1 | 10.10.3.1 | - | VPN to Branch (FortiGate) |
| | Router-ID | 2.2.2.2 | - | OSPF Router ID |
| **DIST-SW** | Vlan50 | 10.0.0.6 | 50 | Management |
| | Vlan60 | 10.0.2.30 | 60 | Server Access |
| **SERVER-SW** | Vlan50 | 10.0.0.5 | 50 | Management |
| | Vlan60 | 10.0.2.4 | 60 | Server Access |
| **ACCESS-SW** | Vlan50 | 10.0.0.6 | 50 | Management |
| | Vlan60 | 10.0.2.30 | 60 | Server Access |

---

### Servers - HQ

| Server | IP Address | VLAN | Services | Description |
|--------|------------|------|----------|-------------|
| **AD-DHCP-DNS-01** | 10.0.2.12 | 60 | AD, DHCP, DNS, TACACS+ | Primary Domain Controller |
| **AD-DHCP-DNS-02** | 192.168.2.12 | 60 | AD, DHCP, DNS | Secondary Domain Controller |
| **NAC-SERVER** | 10.0.2.10 | 60 | RADIUS, 802.1X | Network Access Control |
| **TFTP-SERVER** | 10.0.2.13 | 60 | TFTP | Configuration Backup |
| **SYSLOG-SERVER** | 10.0.2.10 | 60 | Syslog | Log Aggregation |
| **FORTIGATE** | 192.168.201.173 | - | Firewall, SSL VPN | NGFW |

---

## 🏢 Branch Office - 192.168.0.0/16

### Subnet Allocation

| Subnet | CIDR | VLAN | Purpose | Gateway |
|--------|------|------|---------|---------|
| 192.168.1.0 | /24 | 10 | Data | 192.168.1.1 |
| 192.168.2.0 | /24 | 60 | Servers | 192.168.2.1 |
| 192.168.3.0 | /24 | 20 | Voice | 192.168.3.1 |
| 192.168.4.0 | /24 | 30 | Guest | 192.168.4.1 |
| 192.168.5.0 | /24 | 40 | IoT | 192.168.5.1 |
| 192.168.6.0 | /24 | 50 | Management | 192.168.6.1 |
| 192.168.100.0 | /30 | - | WAN Link | - |
| 192.168.201.0 | /24 | - | WAN Transit | - |
| 192.168.245.0 | /23 | - | SSL VPN Pool (FortiGate) | - |
| 192.168.147.0 | /23 | - | SSL VPN Pool (Cisco) | - |

---

### Network Devices - Branch

| Device | Interface | IP Address | VLAN | Description |
|--------|-----------|------------|------|-------------|
| **BRNCH-ROUTER** | G0/0 | 192.168.201.180 | - | WAN Interface |
| | G0/2 | 192.168.100.2 | - | Uplink to Branch Core |
| | Tunnel0 | 10.10.2.2 | - | VPN to HQ (Cisco) |
| | Tunnel1 | 10.10.3.2 | - | VPN to HQ (FortiGate) |
| | Router-ID | 3.3.3.3 | - | OSPF Router ID |
| **BRNCH-CORE2** | Vlan10 | 192.168.1.1 | 10 | Gateway - Data |
| | Vlan20 | 192.168.3.1 | 20 | Gateway - Voice |
| | Vlan30 | 192.168.4.1 | 30 | Gateway - Guest |
| | Vlan40 | 192.168.5.1 | 40 | Gateway - IoT |
| | Vlan50 | 192.168.6.1 | 50 | Gateway - Management |
| | Vlan60 | 192.168.2.1 | 60 | Gateway - Servers |
| | Eth0/0 | 192.168.100.1 | - | Uplink to Router |
| | Router-ID | 8.8.8.8 | - | OSPF Router ID |
| **B-SERVER-SW** | Vlan60 | 192.168.2.2 | 60 | Server Access |
| **BRNCH-ACCESS-SW** | Vlan50 | 192.168.6.6 | 50 | Management |
| | Vlan60 | 192.168.2.6 | 60 | Server Access |

---

## 🔗 VPN Subnets

| VPN Type | Vendor | Pool | Range | Max Users |
|----------|--------|------|-------|-----------|
| **SSL VPN** | Cisco | SSL-VPN-POOL | 192.168.147.1 - 192.168.148.254 | 500 |
| **SSL VPN** | FortiGate | SSL-VPN-POOL | 192.168.245.1 - 192.168.246.254 | 1000 |
| **Site-to-Site** | Cisco | Tunnel0 | 10.10.2.0/30 | - |
| **Site-to-Site** | FortiGate | Tunnel1 | 10.10.3.0/30 | - |

---

## 📊 IP Address Allocation Summary

### DHCP Scopes

| Location | VLAN | Scope | Range | Exclusions |
|----------|------|-------|-------|------------|
| HQ | 10 | 10.0.4.0/24 | 10.0.4.10 - 10.0.4.254 | 10.0.4.1 - 10.0.4.9 |
| HQ | 20 | 10.0.5.0/24 | 10.0.5.10 - 10.0.5.254 | 10.0.5.1 - 10.0.5.9 |
| HQ | 30 | 10.0.6.0/24 | 10.0.6.10 - 10.0.6.254 | 10.0.6.1 - 10.0.6.9 |
| HQ | 40 | 10.0.7.0/24 | 10.0.7.10 - 10.0.7.254 | 10.0.7.1 - 10.0.7.9 |
| HQ | 50 | 10.0.0.0/23 | 10.0.0.10 - 10.0.0.254 | 10.0.0.1 - 10.0.0.9 |
| HQ | 60 | 10.0.2.0/23 | 10.0.2.100 - 10.0.2.254 | 10.0.2.1 - 10.0.2.99 |
| Branch | 10 | 192.168.1.0/24 | 192.168.1.10 - 192.168.1.254 | 192.168.1.1 - 192.168.1.9 |
| Branch | 20 | 192.168.3.0/24 | 192.168.3.10 - 192.168.3.254 | 192.168.3.1 - 192.168.3.9 |
| Branch | 30 | 192.168.4.0/24 | 192.168.4.10 - 192.168.4.254 | 192.168.4.1 - 192.168.4.9 |
| Branch | 40 | 192.168.5.0/24 | 192.168.5.10 - 192.168.5.254 | 192.168.5.1 - 192.168.5.9 |
| Branch | 50 | 192.168.6.0/24 | 192.168.6.10 - 192.168.6.254 | 192.168.6.1 - 192.168.6.9 |
| Branch | 60 | 192.168.2.0/24 | 192.168.2.100 - 192.168.2.254 | 192.168.2.1 - 192.168.2.99 |
