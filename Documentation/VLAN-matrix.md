# VLAN Matrix - Carlos NetPro Enterprise Network

## 📊 VLAN Summary Table

| VLAN ID | VLAN Name | Network | Gateway | DHCP Server | Purpose | QoS Class |
|---------|-----------|---------|---------|-------------|---------|-----------|
| **10** | DATA | 10.0.4.0/24 | 10.0.4.1 | 192.168.2.12, 10.0.2.12 | User Data Traffic | AF21 |
| **20** | VOICE | 10.0.5.0/24 | 10.0.5.1 |192.168.2.12, 10.0.2.12 | IP Phone Traffic | EF |
| **30** | GUEST | 10.0.6.0/24 | 10.0.6.1 | 192.168.2.12, 10.0.2.12 | Guest WiFi | AF11 |
| **40** | IOT | 10.0.7.0/24 | 10.0.7.1 | 192.168.2.12, 10.0.2.12 | IoT Devices | Default |
| **50** | MGMT | 10.0.0.0/23 | 10.0.0.1 | 192.168.2.12, 10.0.2.12 | Network Management | EF |
| **60** | SERVERS | 10.0.2.0/23 | 10.0.2.1 | 192.168.2.12, 10.0.2.12 | Server Infrastructure | AF21 |
| **70** | OOB | 10.0.8.0/24 | 10.0.8.1 | - | Out-of-Band Management | EF |

---

## 📊 Branch Office VLAN Summary

| VLAN ID | VLAN Name | Network |    Gateway     |      DHCP Server       | Purpose |
|---------|-----------|---------|---------|-------------------| ---------|
| **10** | B-DATA | 192.168.1.0/24 | 192.168.1.1 | 192.168.2.12,10.0.2.12 | Branch User Data |
| **20** | B-VOICE | 192.168.3.0/24 | 192.168.3.1 | 192.168.2.12,10.0.2.12 | Branch Voice |
| **30** | B-GUEST | 192.168.4.0/24 | 192.168.4.1 | 192.168.2.12,10.0.2.12 | Branch Guest |
| **40** | B-IOT | 192.168.5.0/24 | 192.168.5.1 | 192.168.2.12,10.0.2.12 | Branch IoT |
| **50** | B-MGMT | 192.168.6.0/24 | 192.168.6.1 | 192.168.2.12,10.0.2.12 | Branch Management |
| **60** | B-SERVERS | 192.168.2.0/24 | 192.168.2.1 | 192.168.2.12,10.0.2.12 | Branch Servers |

---

## 🔗 MSTP Mapping

| MSTP Instance | VLANs | Root Bridge | Secondary Root |
|---------------|-------|-------------|----------------|
| **Instance 1** | 10, 20, 30 | CORE1 (Priority 8192) | CORE2 (Priority 16384) |
| **Instance 2** | 40, 50, 60, 70 | CORE1 (Priority 8192) | CORE2 (Priority 16384) |

### MSTP Configuration

spanning-tree mst configuration
name kingstar-region
revision 1
instance 1 vlan 10, 20, 30
instance 2 vlan 40, 50, 60, 70
!
spanning-tree mst 1 root primary
spanning-tree mst 2 root primary

text

---

## 🎯 VLAN Descriptions & Usage

### VLAN 10 - DATA (10.0.4.0/24)
- **Purpose:** End-user workstation traffic
- **Users:** All employee desktops/laptops
- **Security:** Standard ACLs, Port Security
- **QoS:** AF21 - Medium Priority

### VLAN 20 - VOICE (10.0.5.0/24)
- **Purpose:** IP Telephony traffic
- **Devices:** Cisco IP Phones, Softphones
- **Security:** Protected VLAN
- **QoS:** EF (Expedited Forwarding) - Highest Priority

### VLAN 30 - GUEST (10.0.6.0/24)
- **Purpose:** Guest WiFi network
- **Users:** Visitors, Contractors
- **Security:** Isolated, Internet only
- **Restrictions:** HTTP/HTTPS/DNS only, No internal access
- **QoS:** AF11 - Low Priority

### VLAN 40 - IOT (10.0.7.0/24)
- **Purpose:** IoT devices
- **Devices:** Smart cameras, Sensors, Printers
- **Security:** No Internet access, Local only
- **Restrictions:** Blocked from Internet, Limited bandwidth
- **QoS:** Default - No Priority

### VLAN 50 - MGMT (10.0.0.0/23)
- **Purpose:** Network device management
- **Devices:** Network infrastructure management interfaces
- **Security:** ACL restricted, SSH only, TACACS+ authentication
- **QoS:** EF - High Priority

### VLAN 60 - SERVERS (10.0.2.0/23)
- **Purpose:** Server infrastructure
- **Servers:** AD, DHCP, DNS, NAC, TFTP, Syslog
- **Security:** DACLs, Server isolation
- 
---

## 🔒 VLAN Security Policies

| VLAN | Port Security | 802.1X | ACL | NAC |
|------|--------------|--------|-----|-----|
| **10** | ✅ Max 2 MACs | ✅ Required | Standard | ✅ |
| **20** | ✅ Max 2 MACs | ✅ Required | Voice | ✅ |
| **30** | ✅ Max 2 MACs | ❌ Optional | Restricted | ❌ |
| **40** | ✅ Max 1 MAC | ❌ Optional | Blocked | ❌ |
| **50** | ✅ Max 5 MACs | ✅ Required | Strict | ✅ |
| **60** | ✅ Max 10 MACs | ❌ Optional | Server | ❌ |

---

## 📊 DHCP Scopes

| VLAN | Pool Name | Start IP | End IP | Lease Time | Options |
|------|-----------|----------|--------|------------|---------|
| **10** | DATA-POOL | 10.0.4.10 | 10.0.4.254 | 8 hours | DNS: 192.168.2.12, 10.0.2.12 |
| **20** | VOICE-POOL | 10.0.5.10 | 10.0.5.254 | 24 hours | DNS: DNS: 192.168.2.12, 10.0.2.12 |
| **30** | GUEST-POOL | 10.0.6.10 | 10.0.6.254 | 4 hours | DNS: 8.8.8.8, 1.1.1.1 |
| **40** | IOT-POOL | 10.0.7.10 | 10.0.7.254 | 48 hours | DNS: 10.0.2.10 |
| **50** | MGMT-POOL | 10.0.0.10 | 10.0.0.254 | 12 hours | DNS: 192.168.2.12, 10.0.2.12 |
| **60** | SERVER-POOL | 10.0.2.100 | 10.0.2.254 | 24 hours | DNS: 192.168.2.12, 10.0.2.12 |

