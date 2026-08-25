# 🔐 Cisco Secure Network

A hands-on **Cisco Packet Tracer** project focused on VLAN segmentation, VTP, trunking, SSH, and Layer 2 Port Security.

## 🎯 Project Objective

The goal was to build a segmented LAN and secure access ports against unauthorized devices.

## 🗺️ Network Topology

The network contains two Cisco switches and six PCs divided into three departments:

| VLAN | Department |
| ---- | ---------- |
| 10   | IT         |
| 20   | HR         |
| 30   | Finance    |

**Figure 1: LAN Network Topology Using Cisco Packet Tracer**

![LAN Network Topology](screenshots/topology.jpeg)

---

## ⚙️ VLAN & VTP Configuration

VLANs 10, 20, and 30 were created and assigned to the appropriate access ports.

SW1 was configured as the **VTP Server**, while SW2 was configured as the **VTP Client** using the domain `OFFICE`.

```bash id="z7z1hf"
show vlan brief
show vtp status
```

**Figure 2: VLAN Configuration on SW1**

![VLAN Configuration](screenshots/vlan-configuration-sw1.jpeg)

**Figure 3: VTP Status on SW1**

![VTP Status](screenshots/vtp-status-sw1.jpeg)

---

## 🔗 Trunking & Management

The switch-to-switch link was configured as an **802.1Q trunk**, allowing VLANs 10, 20, and 30 to pass between the switches.

Management IPs were configured on VLAN 10:

* SW1: `192.168.10.2/24`
* SW2: `192.168.10.3/24`

```bash id="n3bflp"
show interfaces fa0/4 switchport
show ip interface brief
```

**Figure 4: Trunk Configuration on SW1**

![Trunk Configuration](screenshots/trunk-sw1.jpeg)

**Figure 5: Management IP Configuration on SW1**

![Management IP](screenshots/management-ip-sw1.jpeg)

---

## 🔐 SSH Remote Management

SSH was configured and successfully tested by accessing SW1 remotely from SW2.

```bash id="g4ukn6"
ssh -l admin 192.168.10.2
```

**Figure 6: Successful SSH Remote Access**

![SSH Test](screenshots/ssh-test.jpeg)

---

## 🧪 Connectivity & VLAN Testing

Ping testing was used to verify network connectivity and VLAN isolation.

The successful ping confirms connectivity between devices in the same VLAN, while the failed ping confirms that communication between different VLANs is blocked.

**Figure 7: Connectivity and VLAN Isolation Test**

![Connectivity and VLAN Isolation Test](screenshots/connectivity-test.jpeg)

---

## 🚨 Port Security Test

Port Security was configured with **Sticky MAC**, a maximum of **1 MAC address per port**, and **Shutdown** violation mode.

The switch learned the authorized devices and stored their MAC addresses as `SecureSticky`.

```bash id="egk5uh"
show port-security address
```

**Figure 8: Secure Sticky MAC Address Table**

![Port Security](screenshots/port-security.jpeg)

A different PC was then connected to **Fa0/1**. The switch detected the unauthorized MAC address and placed the port into **Secure-shutdown**.

```bash id="sybzwm"
show port-security interface fa0/1
```

**Figure 9: Port Security Violation**

![Security Violation](screenshots/security-violation.jpeg)

After removing the unauthorized device, the port was restored to **Secure-up**.

**Figure 10: Port Recovery**

![Port Recovery](screenshots/port-recovery.jpeg)

---

## 🏁 Result

The network was successfully configured, tested, and secured.

The project demonstrates practical implementation of **VLAN segmentation, VTP, 802.1Q trunking, SSH, connectivity testing, VLAN isolation, and Layer 2 Port Security**.

