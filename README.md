# 🔐 Cisco Secure Network

A hands-on Cisco networking project built in **Cisco Packet Tracer** to practice VLAN segmentation, VTP, trunking, SSH remote management, and Layer 2 port security.

## 🎯 Project Objective

The goal of this project was to design and configure a small segmented network and apply basic security controls to protect access ports from unauthorized devices.

## 🗺️ Network Overview

The network consists of two Cisco switches and multiple end devices divided into three departments:

| VLAN | Department |
| ---- | ---------- |
| 10   | IT         |
| 20   | HR         |
| 30   | Finance    |

![Network Topology](screenshots/topology.png)

### Technologies Used

* Cisco Packet Tracer
* VLANs
* VTP
* 802.1Q Trunking
* SVI Management
* SSH
* Port Security
* Sticky MAC
* ICMP/Ping testing

---

## ⚙️ Configuration

### VLANs

Created and assigned VLANs according to the department structure.

```bash
show vlan brief
```

#### SW1

![SW1 VLAN Configuration](screenshots/vlan-configuration-sw1.png)

#### SW2

![SW2 VLAN Configuration](screenshots/vlan-configuration-sw2.png)

---

### VTP

Configured the switches using:

* **SW1:** VTP Server
* **SW2:** VTP Client
* **Domain:** `OFFICE`

```bash
show vtp status
```

#### SW1 — VTP Server

![SW1 VTP Status](screenshots/vtp-status-sw1.png)

#### SW2 — VTP Client

![SW2 VTP Status](screenshots/vtp-status-sw2.png)

---

### Management IP

Configured management IP addresses on VLAN 10:

* SW1: `192.168.10.2/24`
* SW2: `192.168.10.3/24`

```bash
show ip interface brief
```

#### SW1

![SW1 Management IP](screenshots/management-ip-sw1.png)

#### SW2

![SW2 Management IP](screenshots/management-ip-sw2.png)

---

### Trunking

Configured the switch-to-switch connection as an 802.1Q trunk and allowed VLANs 10, 20, and 30.

```bash
show interfaces fa0/4 switchport
```

#### SW1

![SW1 Trunk Configuration](screenshots/trunk-sw1.png)

#### SW2

![SW2 Trunk Configuration](screenshots/trunk-sw2.png)

---

### SSH

Configured SSH for secure remote management and verified access from SW2 to SW1.

```bash
ssh -l admin 192.168.10.2
```

![SSH Test](screenshots/ssh-test.png)

---

### Port Security

Enabled Port Security on user-facing access ports with:

* Maximum MAC addresses: `1`
* Sticky MAC learning
* Violation mode: `Shutdown`

```bash
show port-security
show port-security address
```

![Port Security](screenshots/port-security.png)

---

## 🧪 Testing & Verification

The network was tested at multiple levels.

### ✅ Same-VLAN Connectivity

Devices within the same VLAN successfully communicated using ICMP/Ping.

![Successful Connectivity Test](screenshots/connectivity-test.png)

---

### 🚫 VLAN Isolation

A connectivity test between devices in different VLANs resulted in packet loss, confirming the expected Layer 2 segmentation.

![VLAN Isolation Test](screenshots/vlan-isolation-test.png)

---

### 🚨 Port Security Violation

A different device was connected to a protected port.

The switch detected the unauthorized MAC address and placed the port into:

```text
Secure-shutdown
```

The violation was confirmed using:

```bash
show port-security interface fa0/1
```

![Security Violation](screenshots/security-violation.png)

After removing the unauthorized device, the port was restored and returned to:

```text
Secure-up
```

![Port Recovery](screenshots/port-recovery.png)

---

## 🏁 Result

The network was successfully configured, tested, and secured as a Cisco Packet Tracer project.

The project demonstrates practical implementation of **VLAN segmentation, VTP, 802.1Q trunking, switch management, SSH, connectivity testing, VLAN isolation, and Layer 2 Port Security**.
