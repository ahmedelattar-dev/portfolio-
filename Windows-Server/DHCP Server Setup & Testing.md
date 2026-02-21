# Windows Server DHCP Configuration & Client Testing

## Objective

Install and configure DHCP role on Windows Server 2022 to automatically assign IP addresses to client machines. Verify correct IP lease assignment and troubleshoot potential issues.

---

## Lab Environment

**Hypervisor:** (VMware / VirtualBox)  
**Server OS:** Windows Server 2022
**Client OS:** Windows 11
**Network Type:** Internal Network  

---

## Network Design

### DHCP Scope Configuration

- Network Address: 192.168.10.0
- Subnet Mask: 255.255.255.0
- Scope Range Start: 192.168.10.100
- Scope Range End: 192.168.10.200
- Default Gateway: 192.168.10.1
- DNS Server: 192.168.10.10

### Server Static IP

- IP Address: 192.168.10.10
- Subnet Mask: 255.255.255.0
- Default Gateway: 192.168.10.1
- DNS: 192.168.10.10

> Important: DHCP server must have a static IP.

---

## Configuration Steps

### Step 1: Configure Static IP on Server

1. Open Network Adapter Settings
2. Set:
   - IP: 192.168.10.10
   - Subnet: 255.255.255.0
   - Gateway: 192.168.10.1
   - DNS: 192.168.10.10

---

### Step 2: Install DHCP Role

1. Open Server Manager
2. Click "Add Roles and Features"
3. Select "DHCP Server"
4. Complete installation wizard
5. Authorize DHCP server (if domain environment)

---

### Step 3: Create New DHCP Scope

1. Open DHCP Management Console
2. Right-click IPv4 -> New Scope
3. Name: "LAN Scope"
4. IP Range: 192.168.10.100 – 192.168.10.200
5. Subnet Mask: 255.255.255.0
6. Configure Default Gateway: 192.168.10.1
7. Configure DNS Server: 192.168.10.10
8. Activate Scope

---

## Client Configuration

On Windows client:

1. Open Network Adapter Settings
2. Set IPv4 to:
   - Obtain IP address automatically
   - Obtain DNS automatically

---

## Testing DHCP Lease

On client machine, run:
ipconfig /release
ipconfig /renew
ipconfig

Expected Result:
Client receives IP between 192.168.10.100 – 192.168.10.200

---

##  Problem Encountered

Client received APIPA address:
169.254.x.x

This indicates DHCP server did not assign an IP address.

---

## Troubleshooting Process

1. Verified DHCP service is running:
   - Checked Services -> DHCP Server -> Running

2. Verified scope is activated.

3. Checked firewall settings.

4. Verified client and server are connected to the same network.

5. Confirmed server has static IP correctly configured.

---

## Root Cause

Client and server were connected to different virtual networks, preventing DHCP broadcast traffic from reaching the server.

---

## Resolution

- Reconfigured client network adapter to connect to the same internal network.
- Renewed IP lease.
- Client successfully received IP from DHCP scope.

---

## Lessons Learned

- DHCP relies on broadcast communication.
- Server must have static IP before installing DHCP.
- Scope must be activated.
- Network mismatch prevents DHCP assignment.
- APIPA address (169.254.x.x) indicates DHCP failure.

---

## Ticket Style Summary

**Issue:** Client not receiving IP address from DHCP server.  
**Impact:** Client unable to communicate on network.  
**Root Cause:** Network segmentation preventing DHCP broadcast.  
**Resolution:** Corrected network adapter configuration and renewed lease.  
**Status:** Resolved.
