## **IPv4 Addressing**

- **Size**: 32-bit → gives \~4.3 billion addresses.
- **Format**: `x.x.x.x` → 4 **octets**, each 8 bits (0–255).

  - Example: `192.168.1.0`

- **Components**:

  - `N` = Network portion
  - `H` = Host portion
  - `/8` (CIDR notation) indicates how many bits are for the network.

### **Classes of IPv4**

| Class | Range   | Format       | Total Hosts | Usable Hosts | Subnet Mask   | Use Case        |
| ----- | ------- | ------------ | ----------- | ------------ | ------------- | --------------- |
| A     | 0-126   | N.H.H.H      | 16,777,216  | 16,777,214   | 255.0.0.0     | Large networks  |
| B     | 128-191 | N.N.H.H      | 65,536      | 65,534       | 255.255.0.0   | Medium networks |
| C     | 192-223 | N.N.N.H      | 256         | 254          | 255.255.255.0 | Small networks  |
| D     | 224-239 | Multicast    | –           | –            | –             | Multicasting    |
| E     | 240-255 | Experimental | –           | –            | –             | Research        |

**Special addresses**:

- `127.0.0.1` = Localhost (your own computer)
- Private IPs (used inside networks, not on the Internet):

  - Class A: `10.0.0.0/8`
  - Class B: `172.16.0.0/16`
  - Class C: `192.168.0.0/24`

---

### **IPv4 Example – Class A:**

- Network: `10.0.0.0/8`
- First usable host: `10.0.0.1`
- Last usable host: `10.255.255.254`
- Broadcast address: `10.255.255.255`

Class B and C work similarly, just with fewer hosts.

---

## **IPv6 Addressing**

- **Size**: 128-bit → gives \~3.4×10³⁸ addresses (huge!)
- Created because IPv4 ran out of addresses.
- Format: `xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx`
- Can support virtually unlimited devices.

---

### **Key Points to Remember**

1. IPv4 = 32-bit → 4.3 billion addresses. IPv6 = 128-bit → practically infinite.
2. CIDR `/x` tells how many bits are network vs host.
3. Private IPs are **not routable on the Internet**.
4. Classes A, B, C differ mainly in the **size of the network and host portions**.
5. Broadcast address = used to send messages to all hosts in the network.
6. IPv6 solves the address exhaustion problem of IPv4.
