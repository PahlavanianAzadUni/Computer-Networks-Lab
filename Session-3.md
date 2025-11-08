## 🔗 Session 3 — Connecting Two LANs Using a Router

### 🗓️ Overview

In this session, we extended our previous lab setup in **Cisco Packet Tracer** to connect **two separate LANs** using a **router**. This introduced us to the concept of **inter-network communication** and how routers forward data between different subnets.

We also learned how to manually **configure router interfaces** using the **Command-Line Interface (CLI)**.

---

## 🔌 Part 1 — Network Topology

### 🖊️ Description

We began with two separate LANs:

* **LAN 1**: 3 PCs connected to **Switch 1**, using IPs in the range `192.168.1.0/24`.
* **LAN 2**: 3 PCs connected to **Switch 2**, using IPs in the range `192.168.2.0/24`.

Each LAN was then connected to a **Router** via FastEthernet interfaces:

* **FastEthernet0/0** connected to **Switch 1**.
* **FastEthernet0/1** connected to **Switch 2**.

---

### ⛰️ ASCII Topology Diagram

```text
                      +--------------------------+
                      |           Router         |
                      |--------------------------|
                      |    Fa1/0   |    Fa2/0    |
                      |192.168.1.1 |  192.168.2.1|
                      +------------+-------------+
                            |           |
                     +------+           +------+
                     |                         |
              +-------------+           +-------------+
              |   Switch 1  |           |   Switch 2  |
              +------+------+           +------+------+
                     |                         |
              192.168.1.0/24              192.168.2.0/24
                (3 PCs)                     (3 PCs)
```

> 💡 **Tip:** Each LAN must have a **unique network ID**. Routers connect different networks, so their connected interfaces must belong to **different subnets**.

---

## 🧮 Part 2 — Configuring the Router (CLI)

The router starts with no active interfaces. We configured two FastEthernet ports, one for each LAN.

### ⚙️ Step-by-Step Configuration

```bash
Router> enable                       # Enter privileged mode
Router# configure terminal            # Enter global configuration mode
Router(config)# interface fastethernet 1/0  # Access interface Fa1/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0   # Assign IP for LAN 1
Router(config-if)# no shutdown                     # Enable the interface
Router(config-if)# exit
Router(config)# interface fastethernet 2/0          # Access interface Fa2/0
Router(config-if)# ip address 192.168.2.1 255.255.255.0   # Assign IP for LAN 2
Router(config-if)# no shutdown                     # Enable the interface
Router(config-if)# exit
Router(config)# exit
Router#
```

> 💡 **Remember:** The `no shutdown` command is crucial. Without it, the router interface remains in a *down* state (orange light in Packet Tracer).

---

## 🔌 Part 3 — Configuring the PCs

### 🔧 LAN 1 PCs

| Device | IP Address  | Subnet Mask   | Default Gateway |
| :----- | :---------- | :------------ | :-------------- |
| PC1    | 192.168.1.2 | 255.255.255.0 | 192.168.1.1     |
| PC2    | 192.168.1.3 | 255.255.255.0 | 192.168.1.1     |
| PC3    | 192.168.1.4 | 255.255.255.0 | 192.168.1.1     |

### 🔧 LAN 2 PCs

| Device | IP Address  | Subnet Mask   | Default Gateway |
| :----- | :---------- | :------------ | :-------------- |
| PC4    | 192.168.2.2 | 255.255.255.0 | 192.168.2.1     |
| PC5    | 192.168.2.3 | 255.255.255.0 | 192.168.2.1     |
| PC6    | 192.168.2.4 | 255.255.255.0 | 192.168.2.1     |

> 💡 **Gateway:** This is the IP address of the **router interface** connected to the same LAN. It acts as the exit point for all traffic leaving the LAN.

---

## 🛠️ Part 4 — Testing the Setup

Once all interfaces and PCs were configured:

1. Wait for the **link lights** on the router and switches to turn **green** (indicating the interfaces are up).

2. From a PC in **LAN 1**, open the Command Prompt and ping a PC in **LAN 2**.

   ```bash
   ping 192.168.2.2
   ```

3. If configured correctly, you should receive successful replies — proving that the router is forwarding packets between the two networks.

---

## 🧠 Concepts Learned

* **Routers connect different networks** and make inter-network communication possible.
* **Each LAN** must have a **unique IP network**.
* **Router interfaces** act as gateways for each subnet.
* **`no shutdown`** activates an interface that is *administratively down*.
* **Packet Tracer LED colors:**

  * **Orange** = interface detected but inactive
  * **Green** = interface active and operational

---

## 📚 Exam Tips

* **Never reuse IP addresses** between different LANs.
* The **first usable IP (x.x.x.1)** is often given to the **router** (gateway).
* If `ping` fails, verify:

  * The correct **gateway** is set on each PC.
  * Router interfaces are **not shut down**.
  * Each LAN uses the correct **subnet mask**.
* **Routers work at OSI Layer 3**, using **IP addresses**.
* **Switches work at OSI Layer 2**, using **MAC addresses**.

---

## 🏁 Summary

In this lab, we:

* Connected two LANs through a **router**.
* Assigned **IP addresses** and **subnet masks** to all devices.
* Configured router interfaces with the **CLI**.
* Verified connectivity using **ping**.
* Understood the role of routers in **interconnecting networks**.

