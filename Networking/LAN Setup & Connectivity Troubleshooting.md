# Windows LAN Setup & Connectivity Troubleshooting

## 🎯 Objective
Configure three Windows machines within the same Local Area Network (LAN) using static IP addressing and verify connectivity using ICMP (ping). Identify and resolve any connectivity issues.

---

## 🖥️ Lab Environment

**Hypervisor:** (VMware / VirtualBox – specify yours)  
**Operating Systems:**
- Windows Server 2019
- Windows 10 Client 1
- Windows 10 Client 2

**Network Type:** Internal Network (LAN only)  
**IP Assignment Method:** Static Configuration  

### IP Addressing Scheme

| Machine     | IP Address     | Subnet Mask       | Default Gateway |
|------------|---------------|-------------------|-----------------|
| Server     | 192.168.1.10  | 255.255.255.0     | Not Configured  |
| Client 1   | 192.168.1.20  | 255.255.255.0     | Not Configured  |
| Client 2   | 192.168.1.30  | 255.255.255.0     | Not Configured  |

> Note: Default gateway was not required as communication was limited to the local network.

---

## 🛠️ Configuration Steps

### Step 1: Configure Static IP Addresses
1. Open **Network and Sharing Center**
2. Navigate to **Change Adapter Settings**
3. Right-click network adapter → Properties
4. Select **Internet Protocol Version 4 (TCP/IPv4)**
5. Configure static IP according to the IP addressing scheme above

---

### Step 2: Verify Network Profile
Ensure all machines are set to **Private Network** to allow local communication.

---

### Step 3: Verify Connectivity

Open Command Prompt on each machine and run:

ipconfig
ping 192.168.1.10
ping 192.168.1.20
ping 192.168.1.30

---

## ❌ Problem Encountered

Client 1 was unable to ping Client 2.

Ping results:
Request timed out.

---

## 🔍 Troubleshooting Process

1. Verified IP configuration on all machines using:
ipconfig
→ All IP addresses were correctly configured within the same subnet.

2. Confirmed subnet mask consistency (255.255.255.0 on all machines).

3. Temporarily disabled Windows Defender Firewall.
→ Issue persisted.

4. Verified physical/virtual network configuration.
→ Discovered Client 2 was connected to a different internal network adapter.

---

## 🧠 Root Cause

Client 2 was attached to a different virtual network, preventing Layer 2 communication between machines.

---

## ✅ Resolution

- Reconfigured Client 2 network adapter to connect to the same internal network as other machines.
- Restarted network adapter.
- Retested connectivity.

Ping replies were successfully received from all machines.

---

## 📚 Lessons Learned

- Devices must be connected to the same Layer 2 network for LAN communication.
- Correct IP addressing alone does not guarantee connectivity.
- Always verify virtual/physical network configuration during troubleshooting.
- Systematic troubleshooting prevents unnecessary configuration changes.

---

## 🧾 Ticket-Style Summary

**Issue:** Client unable to communicate with another host on the same LAN.  
**Impact:** Internal network connectivity failure.  
**Root Cause:** Misconfigured virtual network adapter.  
**Resolution:** Corrected network adapter configuration and restored connectivity.  
**Status:** Resolved.
