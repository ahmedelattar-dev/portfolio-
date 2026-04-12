# Join Client to Active Directory Domain Lab

---

## 1. Objective
Join a client machine to an Active Directory domain to enable centralized authentication and management.

---

## 2. Lab Environment

- Server OS: Windows Server 20222  
- Client OS: Windows 11  
- Roles: Active Directory Domain Services + DNS + DHCP  
- Network: Internal Network (192.168.10.0/24)  

---

## 3. Network Design

- Domain: ahmed.local
- Domain Controller: 192.168.10.10  
- Client: DHCP (automatic IP and DNS)  

---

## 4. Concept Overview

Joining a client to a domain allows centralized management of users and systems.

Benefits include:
- Centralized authentication  
- Policy enforcement  
- Resource access control  

---

## 5. Implementation

### Step 1: Verify Client Network Configuration

On client machine:
```
  ipconfig
```
Ensure:
- IP in range 192.168.10.x  
- DNS = 192.168.10.10  

---

### Step 2: Test Connectivity
```
  ping 192.168.10.10  
  ping ahmed.local  
```
---

### Step 3: Open System Settings

- Right click This PC  
- Properties  
- Rename this PC (Advanced)  

---

### Step 4: Join Domain

- Click Change  
- Select Domain  
- Enter:
```
  ahmed.local
```
---

### Step 5: Enter Credentials

Username: ahmed\Administrator  
Password: (Your domain password)

---

### Step 6: Restart Client

Restart is required to apply changes.

---

### Step 7: Login with Domain User

At login screen:

ahmed\Administrator  

---

### Step 8: Verify in Active Directory

On Domain Controller:

- Open Active Directory Users and Computers  
- Check Computers container  
- Confirm client appears  

---

## 6. Verification & Testing

- Client successfully joined domain  
- Domain login successful  
- Client visible in Active Directory  

---

## 7. Issues & Troubleshooting

### Issue: Domain not found  
- Cause: Incorrect DNS  
- Fix: Set DNS to 192.168.10.10  

---

### Issue: Cannot contact domain  
- Cause: Network connectivity issue  
- Fix: Verify ping and network settings  

---

### Issue: Login failed  
- Cause: Incorrect username format  
- Fix: Use ahmed\Administrator  

---

## 8. Screenshots

Include:

- Client IP configuration  
- Domain join screen (ahmed.local)  
- Success message  
- Login screen (domain user)  
- Active Directory showing client  

---

## 9. Key Takeaways

- Domain join enables centralized authentication  
- DNS is critical for domain communication  
- Active Directory simplifies user and system management  
- Proper network configuration is essential  

---

## 10. Future Improvements

- Create users and groups  
- Apply Group Policy  
- Configure file sharing  

