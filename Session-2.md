## 🧪 Session 2 — Connecting PCs, Switches & Understanding Ping

### 🗓️ Overview

In this session, we learned how to **connect multiple computers** using **Cisco Packet Tracer** and explore how devices **communicate through IP addressing and the ping command**.
We were also introduced to **switches, routers, hubs**, and the **command-line modes** used to configure network devices.

---

## 🔌 Part 1 — Building a Simple Network in Cisco Packet Tracer

### 🧱 Components Used

| Device                               | Function                                              |
| :----------------------------------- | :---------------------------------------------------- |
| **PCs (End Devices)**                | Represent individual computers on a network           |
| **Switch**                           | Connects multiple PCs in the same local network (LAN) |
| **Cables (Copper Straight-Through)** | Used to connect PCs to the switch                     |

> 💡 **Tip:** Use *“Copper Straight-Through”* cables when connecting **different device types** (e.g., PC ↔ Switch). Use *“Crossover”* cables only between **similar device types** (e.g., PC ↔ PC).

---

### ⚙️ Steps Performed

1. Open **Cisco Packet Tracer**.
2. Add **3 PCs** from the *End Devices* panel.
3. Add **1 Switch** (e.g., `2960` series switch) from the *Switches* panel.
4. Connect each PC to the switch using *Copper Straight-Through* cables.
5. Click each PC → **Desktop tab → IP Configuration**.
6. Assign **IP addresses** and **Subnet Masks** manually, e.g.:

| Device | IP Address  | Subnet Mask   |
| :----- | :---------- | :------------ |
| PC1    | 192.168.1.1 | 255.255.255.0 |
| PC2    | 192.168.1.2 | 255.255.255.0 |
| PC3    | 192.168.1.3 | 255.255.255.0 |

7. Open **Command Prompt** on one PC → type:

   ```bash
   ping 192.168.1.2
   ```

   If the setup is correct, you’ll receive **reply messages** from the target computer.

---

## 📡 Part 2 — Understanding How `ping` Works

### 🔍 What Is Ping?

`ping` is a **network utility** used to test whether one device can reach another over a network.

When you type `ping <IP address>`:

1. Your computer sends an **ICMP Echo Request** message.
2. The target computer (if reachable) replies with an **ICMP Echo Reply**.
3. The round-trip time is measured and displayed.

> 📚 **ICMP** stands for *Internet Control Message Protocol* — it operates at the **Network Layer (Layer 3)** of the OSI model.

---

### ⚙️ Ping Message Types

| Message Type                    | Description                                               |
| :------------------------------ | :-------------------------------------------------------- |
| **Echo Request**                | Sent by the source computer to test connectivity          |
| **Echo Reply**                  | Sent by the target computer as a response                 |
| **Destination Unreachable**     | Indicates the target can’t be reached                     |
| **Time Exceeded (TTL Expired)** | Packet’s lifetime expired before reaching the destination |

---

### ⏱️ What Is TTL (Time to Live)?

* Each packet sent in a network has a **TTL value**, usually starting at 64, 128, or 255.
* Every time the packet passes through a **router**, the TTL decreases by 1.
* If TTL reaches **0**, the packet is **discarded** (dropped).
* This prevents packets from looping endlessly in the network.

> 💡 Think of TTL as a packet’s *expiration date*.

---

## 🔄 Part 3 — Hub vs Switch vs Router

| Device     | OSI Layer           | Function                                                    | Key Points                           |
| :--------- | :------------------ | :---------------------------------------------------------- | :----------------------------------- |
| **Hub**    | Layer 1 (Physical)  | Sends data to all connected devices (no intelligence)       | Old & rarely used; causes collisions |
| **Switch** | Layer 2 (Data Link) | Sends data **only** to the target device (uses MAC address) | Forms the basis of LANs              |
| **Router** | Layer 3 (Network)   | Connects **different networks** together using IP addresses | Directs traffic between networks     |

> ⚡ **Summary:**
>
> * Use **Switches** to connect devices **within the same network**.
> * Use **Routers** to connect **different networks** (e.g., LAN ↔ Internet).

---

## 🧮 Part 4 — Device Command Modes (Switch/Router CLI)

Cisco devices have different modes that determine your level of control.

| Mode                          | Prompt Example    | Access Level | Description                                    |
| :---------------------------- | :---------------- | :----------- | :--------------------------------------------- |
| **User EXEC Mode**            | `Switch>`         | Limited      | Basic monitoring (no configuration allowed)    |
| **Privileged EXEC Mode**      | `Switch#`         | Intermediate | View device details, enter configuration mode  |
| **Global Configuration Mode** | `Switch(config)#` | Full         | Configure the device (interfaces, VLANs, etc.) |

### ⚙️ Moving Between Modes

```bash
Switch> enable                # Enter privileged mode
Switch# configure terminal     # Enter global configuration mode
Switch(config)# exit           # Return to privileged mode
Switch# disable                # Return to user mode
```

> 💡 **Tip:**
>
> * User mode = *view only*
> * Privileged mode = *view & diagnose*
> * Global config = *make actual changes*

---

## 🧠 Exam Notes & Common Mistakes

* Don’t confuse **Hub** and **Switch** — only the switch learns MAC addresses.
* **Ping** doesn’t use TCP or UDP; it uses **ICMP**.
* TTL doesn’t measure time in seconds — it counts **network hops**.
* You cannot `ping` across different networks **without a router**.
* Make sure **all devices are in the same subnet** (same first 3 octets in IPv4) when testing connectivity in a LAN.

---

## 🏁 Summary

In this lab, we:

* Connected multiple PCs using a **switch**.
* Assigned **static IP addresses**.
* Verified connectivity using the **ping command**.
* Understood **ICMP**, **TTL**, and **device types (hub/switch/router)**.
* Learned about **Cisco command modes** for configuration.
