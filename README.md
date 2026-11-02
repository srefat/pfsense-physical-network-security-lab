# 🛡️ Physical Network Security Lab Using pfSense Community Edition 2.7.2 

### pfSense Firewall Configuration | DNS Troubleshooting | Security Testing

**Project Type:** Physical Networking Home Lab  
**Platform:** pfSense Community Edition 2.7.2  
**Focus:** Network Engineering & Network Security  
**Status:** Core Lab Completed ✅

## 📌 Project Overview

This project demonstrates the configuration and testing of a **pfSense firewall using real physical networking equipment**, rather than a simulator or virtual machine.

I built a small network security lab to practice firewall administration, IP addressing, DHCP, DNS troubleshooting, traffic filtering, and firewall log analysis.

The project also involved identifying and resolving real network connectivity and DNS issues.

## 🖥️ Hardware & Software Used

| Device | Description |
|---|---|
| Firewall | Sharevdi Fanless Mini-PC |
| Firewall OS | pfSense Community Edition 2.7.2 |
| Switch | TP-Link TL-SG108E Managed Switch |
| Computer | Lenovo Windows Laptop |
| Network Adapter | USB-to-Ethernet Adapter |
| Cables | Cat6 Ethernet Cables |
| Console Display | External Monitor (HDMI) |
| Tools | pfSense WebGUI, Windows CMD, Ping, NSLookup |

## 🌐 Physical Network Topology

The lab was connected behind the existing home router to keep firewall testing separate from normal household devices.

<img width="660" height="384" alt="Physical Network Topology" src="https://github.com/user-attachments/assets/ae0d3b34-313c-43ed-90b2-c14f3a18f2b6" />

**Network Connections:**

Internet → Home Router → pfSense WAN → pfSense LAN → TP-Link Switch → Lenovo Laptop

## ⚙️ Network Configuration

| Parameter | Configuration |
|---|---|
| Firewall LAN IP | `192.168.10.1` |
| LAN Subnet | `192.168.10.0/24` |
| DHCP Range | `192.168.10.100 - 192.168.10.200` |
| Test Laptop IP | `192.168.10.100` |
| DNS | pfSense Unbound DNS Resolver |
| Management | `https://192.168.10.1` |

## 🔧 Configuration & Implementation

### 1. Physical Firewall Setup

- Connected the mini-PC firewall, managed switch, and laptop.
- Booted pfSense using the physical firewall appliance.
- Used an external monitor to access the firewall console.
- Configured LAN IP addressing and DHCP.
- Accessed the pfSense WebGUI from the laptop.
- Verified network and Internet connectivity.

### 2. DNS Troubleshooting

**Problem:** DNS queries were initially refused.

**Solution:**

- Checked network connectivity.
- Reviewed pfSense DNS Resolver settings.
- Corrected DNS Resolver access permissions.
- Tested DNS resolution using Windows CMD.

**Command:**

```cmd
nslookup google.com
```

**Result:** Successfully resolved `google.com` using the pfSense DNS Resolver.

### 3. Firewall Security Rule

Created a custom firewall rule to block ICMP traffic to `8.8.8.8`.

| Setting | Value |
|---|---|
| Action | Block |
| Interface | LAN |
| Protocol | IPv4 ICMP |
| Source | LAN Subnets |
| Destination | `8.8.8.8` |
| Logging | Enabled |

Placed the blocking rule above the default LAN allow rule.

### 4. Firewall Testing

**Test 1 — Blocked Traffic**

```cmd
ping 8.8.8.8
```
<img width="1021" height="645" alt="firewal rules" src="https://github.com/user-attachments/assets/43255d76-4b12-48da-b390-8a60fb2b2ec6" />

Result: 100% packet loss, confirming the targeted ICMP traffic was blocked.

**Test 2 — Allowed Traffic**

```cmd
ping 1.1.1.1
```
<img width="1053" height="700" alt="after disable" src="https://github.com/user-attachments/assets/cfbe8640-a9f3-4304-a503-60e3f62cb302" />

**Test 3 — Firewall Logs**

Navigated to **Status → System Logs → Firewall**.

Verified blocked ICMP traffic:

- Source: `192.168.10.100`
- Destination: `8.8.8.8`
- Interface: LAN
- Action: Block
<img width="887" height="542" alt="rule1 2" src="https://github.com/user-attachments/assets/049e1323-53f3-4a27-881a-d26b780ca1d7" />

**Test 4 — Connectivity Restoration**

Disabled the temporary blocking rule and tested again.

```cmd
ping 8.8.8.8
```
<img width="1059" height="234" alt="xsds" src="https://github.com/user-attachments/assets/c369d15c-eb69-45e3-92fb-ae861742e60c" />


Result: Successful replies. Connectivity was restored.

## 🛠️ Problems Encountered & Solutions

| Problem | Solution |
|---|---|
| Initial physical setup and interface identification | Checked console, network ports, and cable connections |
| DNS queries refused | Corrected pfSense DNS Resolver access permissions |
| Needed to block specific traffic | Created an IPv4 ICMP blocking rule |
| Needed to verify blocked traffic | Checked ping results and firewall logs |
| Needed to restore connectivity | Disabled the temporary blocking rule |

## ✅ Test Results

| Test | Result |
|---|---|
| Physical Firewall Boot | ✅ Passed |
| pfSense WebGUI Access | ✅ Passed |
| LAN & Internet Connectivity | ✅ Passed |
| DNS Resolution | ✅ Passed |
| ICMP Blocking | ✅ Passed |
| Firewall Log Verification | ✅ Passed |
| Connectivity Restoration | ✅ Passed |
| Graceful Firewall Shutdown | ✅ Passed |


## 🎯 Skills Demonstrated

- Physical Network Deployment
- pfSense Firewall Administration
- IPv4 Addressing & DHCP
- DNS Troubleshooting
- Firewall Rule Configuration
- ICMP Traffic Filtering
- Firewall Log Analysis
- Network Troubleshooting
- Security Testing & Validation

