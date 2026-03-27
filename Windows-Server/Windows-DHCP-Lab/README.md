# 🖥️ Windows Server DHCP Lab

---

## 📄 1. Objective
Configure a Windows Server DHCP server to dynamically assign IP addresses to client machines in a local network.

---

## 🧱 2. Lab Environment
- **Server OS**: Windows Server 2022  
- **Client OS**: Windows 10  
- **Virtualization**: VMware / VirtualBox  
- **Machines Used**: 2 (1 Server + 1 Client)

---

## 🌐 3. Network Design

- **Network**: 192.168.10.0/24  
- **DHCP Server IP**: 192.168.10.10  
- **DHCP Range**: 192.168.10.100 – 192.168.10.200  
- **Default Gateway**: 192.168.10.1  
- **DNS Server**: 8.8.8.8  

---

## 🧠 4. Concept Overview

DHCP (Dynamic Host Configuration Protocol) automatically assigns IP addresses to devices in a network.

It works using the **DORA process**:
- Discover  
- Offer  
- Request  
- Acknowledge  

This allows devices to join the network without manual configuration.

---

## 🛠️ 5. Implementation

### 🔹 Set Static IP on Server
Configured the server with a static IP:

- IP: 192.168.10.10  
- Subnet: 255.255.255.0  
- Gateway: 192.168.10.1  
- DNS: 8.8.8.8  

---

### 🔹 Install DHCP Role
Used Server Manager to install the DHCP Server role.

---

### 🔹 Post-Installation Configuration
Completed DHCP configuration and authorized the server.

---

### 🔹 Create DHCP Scope

Configured a new scope with:

- Start IP: 192.168.10.100  
- End IP: 192.168.10.200  
- Subnet Mask: 255.255.255.0  

---

### 🔹 Configure Scope Options

- Default Gateway: 192.168.10.1  
- DNS Server: 8.8.8.8  

---

### 🔹 Activate Scope
Activated the DHCP scope to start assigning IP addresses.

---

### 🔹 Configure Client
Set client to obtain IP automatically and ran:

```bash
ipconfig /release
ipconfig /renew
✅ 6. Verification & Testing
Client successfully received an IP address from the DHCP pool
Default gateway and DNS were assigned correctly
Connectivity verified using ping:
ping 192.168.10.10
⚠️ 7. Issues & Troubleshooting
Issue: Client did not receive IP
Cause: DHCP scope not activated
Fix: Activated the scope in DHCP Manager
Issue: Incorrect IP range assigned
Cause: Wrong scope configuration
Fix: Adjusted IP range to correct subnet
Issue: No network connectivity
Cause: Server not using static IP
Fix: Configured static IP properly
📸 8. Screenshots
Server Static IP Configuration
DHCP Role Installation
DHCP Scope Configuration
Scope Options (Gateway + DNS)
DHCP Service Running
Client IP Address حصول على IP
🧠 9. Key Takeaways
DHCP requires a static IP on the server to function correctly
Scope activation is essential for IP assignment
Small misconfigurations can prevent DHCP from working
Understanding the DORA process helps in troubleshooting
Windows DHCP configuration is GUI-based but still requires careful setup
🚀 10. Future Improvements
Implement DHCP Reservation (assign fixed IP to specific devices using MAC address)
Configure Exclusion Range to prevent certain IPs from being assigned
Adjust Lease Duration (controls how long an IP is assigned to a client before renewal)
Integrate DHCP with Active Directory
🔧 Additional Notes
🔹 DHCP Reservation

Allows assigning a specific IP address to a device based on its MAC address.
Useful for servers, printers, and important devices.

🔹 Exclusion Range

Used to exclude specific IP addresses within the DHCP scope so they are not assigned to clients.

🔹 Lease Duration

Defines how long a client can use an assigned IP address before it must renew it.
Short leases are used in dynamic environments, while longer leases are used in stable networks.
