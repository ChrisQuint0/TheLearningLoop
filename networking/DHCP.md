## **Complete Guide: Configuring Basic DHCPv4 on a Router**

### **Topology**

```
[PC-A]—(Switch1)—G0/0 R1 S0/0/0—S0/0/0 R2 S0/0/1—S0/0/1 ISP
[PC-B]—(Switch2)—G0/1 R1
```

### **Addressing Table**

| Device | Interface    | IP Address      | Subnet Mask     | Default Gateway |
| ------ | ------------ | --------------- | --------------- | --------------- |
| R1     | G0/0         | 192.168.0.1     | 255.255.255.0   | N/A             |
| R1     | G0/1         | 192.168.1.1     | 255.255.255.0   | N/A             |
| R1     | S0/0/0 (DCE) | 192.168.2.253   | 255.255.255.252 | N/A             |
| R2     | S0/0/0       | 192.168.2.254   | 255.255.255.252 | N/A             |
| R2     | S0/0/1 (DCE) | 209.165.200.226 | 255.255.255.224 | N/A             |
| ISP    | S0/0/1       | 209.165.200.225 | 255.255.255.224 | N/A             |
| PC-A   | NIC          | DHCP            | DHCP            | DHCP            |
| PC-B   | NIC          | DHCP            | DHCP            | DHCP            |

---

## **Part 1: Basic Network Configuration**

### **Step 1: Build and Cable the Network**

- Connect devices as shown in the topology using appropriate cables.
- Ensure serial links use DCE/DTE cables:

  - R1 S0/0/0 → DCE
  - R2 S0/0/1 → DCE

---

### **Step 2: Erase and Reload All Devices**

On each router and switch:

```
enable
write erase
delete vlan.dat     (for switches)
reload
```

When prompted, type **no** to the initial configuration dialog.

---

### **Step 3: Configure Basic Settings**

#### **Common Base Configuration (for all routers)**

```
no ip domain-lookup
service password-encryption
enable secret class
banner motd #
Unauthorized access is strictly prohibited. #
line con 0
password cisco
login
logging synchronous
line vty 0 4
password cisco
login
```

---

### **R1 Configuration**

```
hostname R1
interface g0/0
 ip address 192.168.0.1 255.255.255.0
 no shutdown
exit

interface g0/1
 ip address 192.168.1.1 255.255.255.0
 no shutdown
exit

interface s0/0/0
 ip address 192.168.2.253 255.255.255.252
 clock rate 128000
 no shutdown
exit
```

Verify:

```
show ip interface brief
```

---

### **R2 Configuration**

```
hostname R2
interface s0/0/0
 ip address 192.168.2.254 255.255.255.252
 no shutdown
exit

interface s0/0/1
 ip address 209.165.200.226 255.255.255.224
 clock rate 128000
 no shutdown
exit
```

Verify:

```
show ip interface brief
```

---

### **ISP Configuration**

```
hostname ISP
interface s0/0/1
 ip address 209.165.200.225 255.255.255.224
 no shutdown
exit
```

---

## **Step 4: Configure Routing**

### **R1 (RIPv2)**

```
router rip
version 2
network 192.168.0.0
network 192.168.1.0
network 192.168.2.252
no auto-summary
```

---

### **R2 (RIPv2 + Default Route)**

```
router rip
version 2
network 192.168.2.252
default-information originate
no auto-summary
exit
ip route 0.0.0.0 0.0.0.0 209.165.200.225
```

---

### **ISP (Static Route)**

```
ip route 192.168.0.0 255.255.252.0 209.165.200.226
```

---

### **Verify Routing**

On R1 and R2:

```
show ip route
```

You should see **R** (RIP) routes and a default route (S\*).

---

### **Test Connectivity**

```
R1# ping 192.168.2.254
R2# ping 209.165.200.225
R1# ping 209.165.200.225
```

All should succeed.

---

## 💡 **Part 2: Configure DHCPv4**

### **R2 — DHCP Server**

#### Exclude Reserved Addresses

```
ip dhcp excluded-address 192.168.0.1 192.168.0.9
ip dhcp excluded-address 192.168.1.1 192.168.1.9
```

#### Create DHCP Pools

```
ip dhcp pool R1G0
 network 192.168.0.0 255.255.255.0
 default-router 192.168.0.1
 dns-server 209.165.200.225
 domain-name ccna-lab.com
exit

ip dhcp pool R1G1
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 209.165.200.225
 domain-name ccna-lab.com
exit
```

Verify:

```
show run | section dhcp
```

---

### **R1 — DHCP Relay Agent**

```
interface g0/0
 ip helper-address 192.168.2.254
exit

interface g0/1
 ip helper-address 192.168.2.254
exit
```

---

## **Step 8: Verify DHCP Operation**

On **PC-A** and **PC-B**:

1. Set NIC to **DHCP** mode.
2. Open Command Prompt → `ipconfig /all`
3. Confirm:

   - IP Address is between `.10` and `.254`
   - Default Gateway matches R1’s interface
   - DNS = `209.165.200.225`

---

### **Additional Verification (on R2)**

```
show ip dhcp binding
show ip dhcp server statistics
```

You should see leased addresses and DHCP message counters.

---

## **Final Summary**

- **R1:** DHCP relay agent
- **R2:** DHCP server + default route to ISP
- **ISP:** Static route summarizing internal networks
- **PCs:** Receive IPs automatically via DHCP through relay
