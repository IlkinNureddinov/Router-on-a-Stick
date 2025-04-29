# Router-on-a-Stick
Configure Inter-Vlan-Routing
# 🖧 Inter-VLAN Routing (Router-on-a-Stick) – Cisco Lab Setup

This lab simulates a basic **Router-on-a-Stick** topology using a Cisco router and Layer 2 switch. The goal is to enable communication between VLANs by using router sub-interfaces.

---

## 🧱 Network Topology

- **VLAN 10**: Accounting – 192.168.10.0/24
- **VLAN 20**: HR – 192.168.20.0/24
- **Router**: Acts as the default gateway for both VLANs using sub-interfaces.
- **Switch**: Manages VLAN segmentation and provides trunk connection.

---

## ⚙️ Cisco Router Configuration (Router-on-a-Stick)

```
enable
configure terminal

! Create sub-interface for VLAN 10
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
 no shutdown
exit

! Create sub-interface for VLAN 20
interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
 no shutdown
exit

! Activate the main interface
interface GigabitEthernet0/0
 no shutdown
exit

write memory

📌 Explanation:

.10 and .20 are sub-interfaces using 802.1Q tagging.

Each sub-interface is the gateway for its respective VLAN.

Cisco Switch Configuration

enable
configure terminal


vlan 10
 name ACCOUNTING
exit

vlan 20
 name HR
exit

! Assign ports to VLANs
interface FastEthernet0/3
 switchport mode access
 switchport access vlan 10
exit



! Configure trunk port toward the router
interface FastEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20
exit

write memory

 PC Configuration
PC (Accounting VLAN 10)
IP: 192.168.10.10

Subnet Mask: 255.255.255.0

Default Gateway: 192.168.10.1

✅ Verification & Testing
From Router

show ip interface brief


From Switch

show vlan brief
show interfaces trunk
From PC (Windows CLI)


powershell
ping 192.168.10.1
ping 192.168.20.1

🔥 Skills Covered
VLAN Creation and Tagging

Sub-interface Configuration (Router-on-a-Stick)

Access & Trunk Port Management

Gateway IP Assignment

Basic Troubleshooting & Ping Tests

📘 Notes
Trunk configuration is crucial. A missing trunk will break inter-VLAN routing.

TTL expired or request timed out errors often relate to wrong IP or VLAN mapping.

Use show run and show ip interface brief often to validate.

💡 Conclusion
This project showcases a complete Inter-VLAN Routing setup using sub-interfaces. It’s ideal for CCNA/CCNP labs and real-world network segmentation scenarios.

🔥 Skills Covered
VLAN Creation and Tagging

Sub-interface Configuration (Router-on-a-Stick)

Access & Trunk Port Management

Gateway IP Assignment

Basic Troubleshooting & Ping Tests

📘 Notes
Trunk configuration is crucial. A missing trunk will break inter-VLAN routing.

TTL expired or request timed out errors often relate to wrong IP or VLAN mapping.

Use show run and show ip interface brief often to validate.

💡 Conclusion
This project showcases a complete Inter-VLAN Routing setup using sub-interfaces. It’s ideal for CCNA/CCNP labs and real-world network segmentation scenarios.


 ![configurations on switch](https://github.com/user-attachments/assets/5e2e2e6b-8c01-41e5-84e7-444c01132167)
![switch](https://github.com/user-attachments/assets/534a3490-b1eb-429d-bc40-ca9a8b60a133)
![sub interfaces](https://github.com/user-attachments/assets/d313419c-6e7a-49e4-8ffa-46353351f519)
![interface statuses](https://github.com/user-attachments/assets/8939c97b-7670-4e51-8e7e-fcbea099b92c)
![confirmation of pings](https://github.com/user-attachments/assets/62d2de2b-f992-4ce0-adf5-1fb260569694)



