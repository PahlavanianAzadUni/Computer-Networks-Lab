## 🌐 Session 4 — Connecting Two Routers via Serial Interface

### 🗓️ Overview

In this session, we extended our previous Packet Tracer lab by connecting **two separate LAN-based networks**, each with its own router. The goal was to enable **inter-router communication** using **Serial interfaces** — a key concept in WAN connections.

This setup demonstrated how data can travel between **multiple networks** through routers interconnected by a **point-to-point serial link**, introducing the concept of **DCE/DTE roles**, **clock rate configuration**, and **static routing fundamentals**.

> 🔍 **Concept Recap:**
>
> * **DCE (Data Communications Equipment)** — provides the clock signal (timing) that synchronizes data transfer across the serial link. In Packet Tracer, one side of the serial cable is automatically designated as DCE.
> * **DTE (Data Terminal Equipment)** — receives the clock signal and adjusts its transmission accordingly.
> * **Clock Rate** — defines how fast bits are sent on the serial link. It must be configured on the DCE side using the `clock rate` command.
> * **Static Routing Fundamentals** — define explicit network paths. Although not deeply configured in this session, understanding that routers use routing tables to forward packets between subnets lays the groundwork for future labs.

---

## 🧩 Part 1 — Network Topology Overview

We built a network with two main segments:

* **Router 1** connected to two LANs (via two switches).
* **Router 2** connected to two LANs (via two switches).
* **Routers 1 and 2** connected directly using **Serial interfaces**.

Each LAN was assigned a unique subnet to avoid IP conflicts. This was crucial since routers only forward packets between **different networks**.

### 🖊️ Addressing Summary

| Network     | Router Interface | IP Address  | Subnet Mask   | Description                                                |
| :---------- | :--------------- | :---------- | :------------ | :--------------------------------------------------------- |
| LAN 1       | R1 Fa0/0         | 192.168.1.1 | 255.255.255.0 | Connected to Switch 1, serves as the gateway for LAN 1 PCs |
| LAN 2       | R1 Fa0/1         | 192.168.2.1 | 255.255.255.0 | Connected to Switch 2, gateway for LAN 2 PCs               |
| LAN 3       | R2 Fa0/0         | 192.168.3.1 | 255.255.255.0 | Connected to Switch 3, gateway for LAN 3 PCs               |
| LAN 4       | R2 Fa0/1         | 192.168.4.1 | 255.255.255.0 | Connected to Switch 4, gateway for LAN 4 PCs               |
| Serial Link | R1 S0/1/0        | 192.168.5.1 | 255.255.255.0 | Connects Router 1 to Router 2 (DCE side)                   |
| Serial Link | R2 S0/1/1        | 192.168.5.2 | 255.255.255.0 | Connects Router 2 to Router 1 (DTE side)                   |

> 🧭 **Explanation:**
>
> * Each router acts as the **default gateway** for the PCs in its LAN. For example, PCs in the 192.168.1.0/24 network will use 192.168.1.1 as their gateway.
> * The **serial link** (192.168.5.0/24) is a separate network connecting the two routers. Each router’s serial interface has its own IP in this range.
> * By maintaining separate subnets, routers can identify which network packets belong to and decide how to route them.

---

## 🧱 Part 2 — ASCII Network Diagram

```text
              ┌────────────────────────────┐
              │        Router 1 (R1)       │
              │----------------------------│
              │ S0/0 → 192.168.2.1         │───┐
              │ S0/1 → (connected to R2)   │   │
              └────────────────────────────┘   │
                       |                      (Serial Link)
                       |                       │
                       |                       │
              ┌────────────────────────────┐   │
              │        Router 2 (R2)       │   │
              │----------------------------│   │
              │ S0/0 → 192.168.5.2         │◄──┘
              │ S0/1 → (connected to R1)   │
              └────────────────────────────┘
                       
          LAN A (behind R1)                    LAN B (behind R2)
    ┌──────────────────────┐             ┌──────────────────────┐
    │ Switch A             │             │ Switch B             │
    │----------------------│             │----------------------│
    │ PCs:                 │             │ PCs:                 │
    │ 192.168.2.2          │             │ 192.168.5.3          │
    │ 192.168.2.3          │             │ 192.168.5.4          │
    └──────────────────────┘             └──────────────────────┘
          │      │                            │      │
          └──────┘                            └──────┘
          LAN: 192.168.2.0/24                 LAN: 192.168.5.0/24



Notes:
- The **serial connection** between R1 and R2 uses a **DCE–DTE link**.  
  - R1 (DCE) must define the **clock rate**: `clock rate 19200`
  - R2 (DTE) simply receives the timing signal.
- Each router’s **Serial interface (S0/x)** connects to the other router.
- Each router also connects to its **local LAN** via a **FastEthernet** or **GigabitEthernet** interface.
- The **Static routes** allow LAN A and LAN B to communicate across routers.
```

> 🔌 **Serial Connection Explanation:**
> The serial cable connects Router 1 and Router 2 using the Serial0/1/x interfaces. In Packet Tracer, you can identify the **DCE side** by hovering over the cable — it shows a small tag. The DCE side must define the **clock rate** to provide synchronization. Without it, the routers won’t establish a stable link, and the serial interface LEDs will stay **orange** instead of turning **green**.

---

## ⚙️ Part 3 — Router Configuration (CLI)

Below are the key configuration commands taken directly from the whiteboard and practiced in Packet Tracer.

### 🖥️ Router 1 Configuration

```bash
Router(config)# interface Serial0/1/0
Router(config-if)# ip address 192.168.5.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# clock rate 19200      # Set clock rate for DCE side
Router(config-if)# exit
```

### 🖥️ Router 2 Configuration

```bash
Router(config)# interface Serial0/1/1
Router(config-if)# ip address 192.168.5.2 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
```

> 🧩 **DCE/DTE Reminder:** Only the **DCE** side sets a clock rate. Use the command `show controllers serial` in Packet Tracer to determine which side is DCE.

---

## 🔄 Part 4 — Verification and Testing

After configuration, both routers and switches were checked for **green link lights** to confirm interface activation.

Then, from any PC in LAN 1, you could test connectivity to a PC in LAN 3 (across routers) by running:

```bash
ping 192.168.3.2
```

If the ping was successful, it meant the inter-router serial communication and routing worked correctly.

---

## 🧠 Part 5 — OSI Layer Perspective

| OSI Layer           | Device/Function in this Lab      | Example                                   |
| :------------------ | :------------------------------- | :---------------------------------------- |
| Layer 1 — Physical  | Serial Cable (DCE/DTE), Ethernet | Clock rate defines timing synchronization |
| Layer 2 — Data Link | Switches                         | Frame forwarding using MAC addresses      |
| Layer 3 — Network   | Routers                          | IP addressing, routing between subnets    |
| Layer 4–7           | Not directly configured          | Ping (ICMP) operates at Layer 3–4         |

> 💡 **Insight:** The serial link operates at both the **Physical (Layer 1)** and **Network (Layer 3)** layers, bridging data between routers that operate as the main Layer 3 devices.

---

## 📚 Concepts Reinforced

* Routers connect **different networks** via serial or Ethernet interfaces.
* **DCE vs DTE:** The DCE device provides clock rate (timing) for synchronization.
* **Clock Rate Command:** Required on the DCE side to ensure communication stability.
* **Each LAN** must have its **own IP subnet**.
* **`no shutdown`** activates router interfaces.
* **`ping`** is used to verify end-to-end connectivity.
* Routers operate at **OSI Layer 3**, while switches operate at **Layer 2**.
* **Serial connections** simulate **WAN links**, used to connect distant networks or branch routers.

---

## 🧾 Exam Tips

* Always identify which side of the serial cable is **DCE** — only that side requires a `clock rate`.
* Remember that **each router interface** (FastEthernet or Serial) must be on a **different subnet**.
* If the serial link LED stays **orange**, verify that:

  * You used `no shutdown` on both sides.
  * The DCE side has a clock rate set.
* Use `show ip interface brief` to confirm interface status and IP assignment.
* Use `ping` to verify connectivity — if it fails, check gateway and subnet mask configurations.
* Routers work at **OSI Layer 3** (IP routing), while switches handle **Layer 2** (frame switching).
* **Clock rate** is unique to serial links, not Ethernet.
* This lab bridges LAN and WAN — expect related exam questions about inter-router communication and DCE/DTE behavior.

---

## 🏁 Summary

In Session 4, we:

* Expanded our setup to **two routers**, each managing multiple LANs.
* Established a **Serial connection** between the routers.
* Configured IP addresses and **clock rate** on the serial link.
* Observed **DCE/DTE roles** in Packet Tracer.
* Verified connectivity across **four LANs** using `ping`.
* Reinforced understanding of **Layer 3 routing**, **WAN fundamentals**, and **serial synchronization**.

> 🧭 *This session bridges LAN concepts from earlier labs with WAN fundamentals, providing the first step toward understanding large-scale inter-network communication.*
