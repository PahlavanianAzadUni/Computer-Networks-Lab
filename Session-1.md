# 🌐 Computer Networks Lab — Session 1

## 1. Network Topology: Star Topology

### 🧩 What Is a Network Topology?
A **network topology** defines the layout or structure of how devices (computers, routers, switches, etc.) are connected in a network.

### ⭐ Star Topology
In a **star topology**, all devices are connected to a central device (like a **switch** or **hub**). This central device manages and controls all communication between devices.

#### 🖼️ Visual Representation

                     [PC1]
                        |
                        |
        [PC2] ---- [Switch/Hub] ---- [PC3]
                      |
                      |
                     [PC4]


### ⚙️ Characteristics
- Each device has a **dedicated connection** to the central hub.
- If one connection fails, only that device is affected.
- The hub or switch acts as the **central communication point**.

### ✅ Advantages
- Easy to install and manage.
- Easy to detect faults or remove devices.

### ❌ Disadvantages
- If the central hub fails, the whole network goes down.
- Requires more cabling than some other topologies.

---

## 2. DNS (Domain Name System)

### 🧠 Concept
**DNS** stands for **Domain Name System**. It translates **human-friendly domain names** (like `google.com`) into **machine-friendly IP addresses** (like `8.8.8.8`).

### ⚙️ How It Works
When you type `www.yahoo.com` in your browser:
1. Your computer asks a **DNS server** for the IP of that domain.
2. The DNS server replies with the IP address (e.g., `74.6.231.20`).
3. Your computer connects to that IP — **not** the domain name.

### 💡 Analogy
Think of DNS as the **Internet’s phonebook** — it maps names to numbers.

---

## 3. IP Addresses

### 🧩 What Is an IP Address?
An **IP address (Internet Protocol address)** is a unique identifier for each device connected to a network.

It’s like a **home address** for your device — it tells where data should go and where it came from.

---

### 🧮 IPv4 (Internet Protocol Version 4)
- **Format:** Four numbers (0–255), separated by dots — e.g. `192.168.1.1`
- **Example Range:** `0.0.0.0` to `255.255.255.255`
- **Total possible addresses:** ≈ 4.3 billion
- **Problem:** IPv4 addresses are running out due to the massive number of devices.

---

### 🧮 IPv6 (Internet Protocol Version 6)
- **Format:** Eight groups of four hexadecimal digits — e.g. `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- **Total possible addresses:** ≈ 340 undecillion (a number with 36 zeros!)
- Designed to handle the explosion of Internet-connected devices (IoT, sensors, smart devices).

---

### 🧱 IP Address Classes (IPv4)
IPv4 is divided into **five classes** based on range and usage.

| Class | Range of First Octet | Example IP       | Default Subnet Mask | Use Type              |
|:------|:----------------------|:------------------|:--------------------|:----------------------|
| A     | 1 – 126               | 10.0.0.1          | 255.0.0.0           | Very large networks   |
| B     | 128 – 191             | 172.16.0.1        | 255.255.0.0         | Medium networks       |
| C     | 192 – 223             | 192.168.1.1       | 255.255.255.0       | Small networks        |
| D     | 224 – 239             | 224.0.0.1         | —                   | Multicasting          |
| E     | 240 – 255             | —                 | —                   | Experimental          |

---

### 🌍 Private IP Ranges (Not Publicly Routable)
Only **three IPv4 ranges** are reserved for **private networks** (LANs):

| Class | Private Range           | Example Use Case           |
|:------|:------------------------|:----------------------------|
| A     | 10.0.0.0 – 10.255.255.255 | Large private LANs         |
| B     | 172.16.0.0 – 172.31.255.255 | Medium private LANs      |
| C     | 192.168.0.0 – 192.168.255.255 | Home/office networks  |

These IPs are **free to use locally** but **not reachable on the Internet**.

---

## 4. Subnet Mask and VLSM

### 🧩 Subnet Mask
A **subnet mask** defines which part of an IP address refers to the **network** and which part refers to the **host** (the device).

Example:
IP Address: 192.168.1.10
Subnet Mask: 255.255.255.0

This means:
- `192.168.1` → Network portion
- `.10` → Host portion

So, this network can have **254 hosts** (1–254).

---

### 🧮 VLSM (Variable Length Subnet Mask)
**VLSM** allows dividing a network into **sub-networks of different sizes**, improving IP address efficiency.

Example:
- Instead of giving every department a `/24` (256 addresses), you can give:
  - `/26` for a 50-device department
  - `/28` for a 10-device department

---

## 5. Types of Communication

| Type | Description | Example |
|:-----|:-------------|:--------|
| **Unicast** | One sender → One receiver | A PC sends a file to another PC |
| **Multicast** | One sender → Selected group | Streaming video to specific subscribers |
| **Broadcast** | One sender → All devices in network | Sending an ARP request |

---

## 6. MAC Address (Media Access Control)

### 🧩 Definition
A **MAC address** is a **unique hardware identifier** assigned to a network interface card (NIC).

- It is **burned into the hardware**.
- It works at the **Data Link Layer (Layer 2)**.
- **Format:** 6 pairs of hexadecimal numbers  
  Example: `00:1A:2B:3C:4D:5E`

### ⚙️ Difference Between IP and MAC
| Property | IP Address | MAC Address |
|:----------|:------------|:-------------|
| Type | Logical (can change) | Physical (fixed) |
| Layer | Network Layer | Data Link Layer |
| Assigned By | ISP or network admin | Device manufacturer |
| Example | 192.168.1.10 | 00:1A:2B:3C:4D:5E |

---

## 7. Static vs Dynamic IP

| Type | Description | Assigned By | Example Use |
|:------|:-------------|:-------------|:-------------|
| **Static IP** | Permanently assigned; doesn’t change | Manually set or bought | Servers, domains |
| **Dynamic IP** | Temporarily assigned; changes over time | DHCP (usually your ISP) | Home Internet connections |

### ⚙️ How Dynamic IP Works
- When you connect your modem or router to your ISP:
  1. It sends a request to the **DHCP server**.
  2. The DHCP server **assigns a temporary IP** (lease).
  3. When you disconnect or after some time, it may change.

So, your home network **shares one public IP** from the ISP, while each device at home gets a **local private IP** (e.g., 192.168.x.x).

Your router uses **NAT (Network Address Translation)** to connect all your local devices to the Internet through that one public IP.

---

## 8. IPv6 and IoT (Internet of Things)

### 🧩 Why IPv6?
IPv4 can’t provide enough unique addresses for billions of new IoT devices — smart homes, cars, sensors, etc. IPv6 solves this by offering **vast address space**.

### 🌾 IoT Example
A smart farm with:
- Soil sensors
- Drones
- Smart irrigation
- Weather monitors

Each device may need a **unique IP** to connect to the cloud directly — that’s why IPv6 is crucial.

---

## 9. Local Networks and Global Internet

### 🌐 Local Network
You can assign any private IPs locally (e.g., `192.168.1.x`), but those are **not globally unique** — they only work inside your LAN.

### ☁️ Global Connectivity
If a device needs to **connect to the Internet (cloud)** directly, it must have a **public IP** that is unique worldwide.

That’s why your idea of one IP per modem works **for local communication**, but **not for global Internet access** — only the modem/router has the public IP, and internal devices share it via **NAT**.

---

## 🧠 Summary

| Concept | Description |
|:---------|:-------------|
| **Star Topology** | All devices connect to a central hub/switch |
| **DNS** | Translates domain names to IP addresses |
| **IP Address** | Unique identifier for a device |
| **IPv4 vs IPv6** | IPv6 created to solve IPv4 address exhaustion |
| **Subnet Mask** | Separates network and host parts of an IP |
| **VLSM** | Efficient subnetting technique |
| **Unicast / Multicast / Broadcast** | Different message delivery types |
| **MAC Address** | Unique hardware identifier |
| **Static/Dynamic IP** | Permanent vs temporary address assignment |
| **NAT** | Allows multiple private devices to share one public IP |
| **IPv6 & IoT** | Provides massive address space for connected devices |

---
