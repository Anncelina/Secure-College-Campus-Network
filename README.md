## 🔐Secure College Campus Network:-

->A secure and structured college campus network designed and simulated using **Cisco Packet Tracer**.
->This project connects different college departments through a structured network while providing **network segmentation,
controlled communication, security, redundancy, dynamic routing, and external connectivity**.

## 📌 Project Overview:-
->The network is designed for a college campus containing five major departments:
        - ECE
        - CSE
        - Library
        - Lab
        - Admin
->Each department is separated using VLANs to improve network organization and security.
->The network follows a **two-tier architecture** consisting of:
                   - **Core Layer**
                   - **Access Layer**
->The **Core Switch** acts as the central connection point, while the departmental switches form the Access Layer and
  connect the end devices.
->The **Campus Router** provides Inter-VLAN Routing and DHCP services, while the **Edge Router** connects the 
  campus network to the external/ISP network.

 ## 🏗️ Network Architecture:-

                         🌐 ISP
                           |
                     Edge Router
                     203.0.113.2
                           |
                     10.0.0.0/30
                           |
                    Campus Router
                           |
                      Core Switch
                    /  /  |  \  \
                   /  /   |   \  \
                ECE CSE Library Lab Admin
                SW  SW    SW    SW   SW
                |   |     |     |    |
               PCs PCs   PCs   PCs  PCs

## Network Flow:-

                End Devices
                    ↓
              Access Switches
                    ↓
                Core Switch
                    ↓
              Campus Router
                    ↓
               Edge Router
                    ↓
          ISP / External Network

## 🧩 Technologies Used:-

The project implements the following networking technologies:

1)VLAN
2)802.1Q Trunking
3)Inter-VLAN Routing
4)DHCP
5)OSPF
6)STP
7)EtherChannel
8)Port Security
9)SSH
10)ACL
## Additional Technology
->NAT / PAT for external network connectivity

## 1️⃣ VLAN — Virtual Local Area Network:-
    ->VLANs are used to logically separate different college departments into individual broadcast domains.
    ->VLAN	Department	Network
         10	ECE	192.168.10.0/24
         20	CSE	192.168.20.0/24
         30	Library	192.168.30.0/24
         40	Lab	192.168.40.0/24
         50	Admin	192.168.50.0/24
         99	Native	192.168.99.0/24

Purpose:-
->Department separation
->Reduced broadcast traffic
->Better network organization
->Improved security

## 2️⃣ 802.1Q Trunking:-
        ->802.1Q trunking is used to carry traffic from multiple VLANs through a single physical link.
        ->The project uses trunk links between network devices.
        ->Native VLAN: VLAN 99
                 VLAN 10 ─┐
                 VLAN 20 ─┤
                 VLAN 30 ─┤
                 VLAN 40 ─┤── Trunk Link
                 VLAN 50 ─┤
                 VLAN 99 ─┘

Purpose:-
->Carry multiple VLANs over one link
->Efficient communication between switches and router
->Support the campus VLAN structure


## 3️⃣ Inter-VLAN Routing:-
        ->Different VLANs are separate networks. To allow controlled communication between them, 
the project uses Inter-VLAN Routing.
        ->The project implements Inter-VLAN Routing using Router-on-a-Stick.
        ->Router Subinterfaces
                  | Subinterface | IP Address   | VLAN |
                  | ------------ | ------------ | ---- |
                  | G0/1.10      | 192.168.10.1 | 10   |
                  | G0/1.20      | 192.168.20.1 | 20   |
                  | G0/1.30      | 192.168.30.1 | 30   |
                  | G0/1.40      | 192.168.40.1 | 40   |
                  | G0/1.50      | 192.168.50.1 | 50   |
                  | G0/1.99      | 192.168.99.1 | 99   |

Purpose:-
->Allows communication between different VLANs while allowing ACLs to control that communication.


## 4️⃣ DHCP — Dynamic Host Configuration Protocol:-
          ->DHCP automatically assigns network configuration to end devices.
          ->Instead of manually configuring every PC, DHCP provides:
                      ^-IP Address
                      ^-Subnet Mask
                      ^-Default Gateway
                      ^- DNS Server
           ->The project uses DHCP pools for the departmental networks.
           ->DHCP Process:-
                       Discover → Offer → Request → Acknowledge
Purpose:-
->Automatic IP configuration
->Less manual configuration
->Reduced configuration errors


## 5️⃣ OSPF — Open Shortest Path First:-
        ->OSPF is used as the dynamic routing protocol between the Campus Router and Edge Router.
        ->OSPF Configuration
               Campus Router → Router ID 2.2.2.2
               Edge Router   → Router ID 1.1.1.1
               Area          → 0
        ->The routers dynamically learn the available networks.
        ->The Edge Router learns the campus VLAN networks:
               192.168.10.0/24
               192.168.20.0/24
               192.168.30.0/24
               192.168.40.0/24
               192.168.50.0/24

Purpose:-
->Dynamic route learning
->Automatic route updates
->Easier network management
->Better scalability


## 6️⃣ STP — Spanning Tree Protocol:-
         ->STP is used to prevent Layer 2 switching loops.
         ->The project contains redundant links between switches for reliability.
         ->Without STP, redundant Layer 2 paths can create network loops and broadcast storms.
         ->STP prevents this by controlling the forwarding state of switch ports.

Purpose:-
->Prevent switching loops
->Prevent broadcast storms
->Maintain network stability
->Support redundant network paths


## 7️⃣ EtherChannel:-
           ->EtherChannel combines multiple physical links into a single logical link.
           ->The project uses LACP for EtherChannel.
           ->Configured Port-Channels include:
                       Po1
                       Po2
                       Po3
                       Po4
                       Po5

Example:

               Physical Link 1 ─┐
                                ├── Port-Channel
               Physical Link 2 ─┘


Purpose:-
->Increased bandwidth
->Link redundancy
->Better utilization of multiple physical links
->If one physical link fails, the remaining links can continue carrying traffic.

## 8️⃣ Port Security:-
              ->Port Security is used to prevent unauthorized devices from connecting through switch access ports.
              ->The project uses:
                        Maximum MAC addresses = 1
                        MAC learning          = Sticky
                        Violation mode        = Shutdown

Purpose:-
->Restrict unauthorized devices
->Control MAC addresses allowed on access ports
->Improve Layer 2 security
->If an unauthorized device is connected, the port can be placed into a shutdown state.


## 9️⃣ SSH — Secure Shell:-
       ->SSH is used for secure remote management of network devices.
       ->The project uses SSH Version 2.
       ->Instead of managing a switch physically, an administrator can securely access it remotely.
       ->Instead of managing a switch physically, an administrator can securely access it remotely.

                                          Administrator PC
                                                |
                                               SSH
                                                |
                                                ↓
                                           Switch/Router

Purpose:-
->Secure remote management
->Encrypted communication
->Safer alternative to Telnet

## 🔟 ACL — Access Control List:-
          ->ACLs are used to control communication between different departments.
          ->The project implements department-level security policies.
          ->Communication Policy
                       | Source  | Destination       | Access    |
                       | ------- | ----------------- | --------- |
                       | ECE     | CSE               | ❌ Blocked |
                       | ECE     | Admin             | ❌ Blocked |
                       | ECE     | Library           | ✅ Allowed |
                       | ECE     | Lab               | ✅ Allowed |
                       | CSE     | ECE               | ❌ Blocked |
                       | CSE     | Admin             | ❌ Blocked |
                       | CSE     | Library           | ✅ Allowed |
                       | CSE     | Lab               | ✅ Allowed |
                       | Library | Admin             | ❌ Blocked |
                       | Lab     | Admin             | ❌ Blocked |
                       | Admin   | Other Departments | ✅ Allowed |

            ->ACLs are applied to the appropriate router subinterfaces to enforce these security policies.

Purpose:-
->Control inter-department communication
->Restrict unauthorized access
->Implement network security policies

## 🌐 Additional Technology — NAT / PAT:-
                ->NAT is used to provide connectivity between the internal private network and the external/ISP network.
                ->Internal devices use private IP addresses such as:
                               192.168.x.x
                ->The Edge Router translates these addresses to the outside interface address.

Example:
                           Internal PC
                          192.168.10.2
                               ↓
                           Edge Router
                           203.0.113.2
                               ↓
                               ISP
                          203.0.113.1

              ->The project uses PAT (NAT Overload) so multiple internal devices can share the outside 
                interface address.

Purpose:-
->Translate private IP addresses
->Enable external connectivity
->Conserve public IP addresses

## 🔐 Security Design:-
          ->Security is implemented at multiple levels:

1)Department Level:
         ->VLANs separate different departments.
2)Communication Level:
         ->ACLs control which departments can communicate.
3)Device Access Level:
         ->Port Security restricts unauthorized devices.
4)Management Level:
         ->SSH provides secure remote management.
5)External Connectivity:
         ->NAT provides controlled translation between the internal and external networks.


## 📁 Project Structure:-
Secure-College-Campus-Network/
│
├── README.md
│
├── configurations/
│   ├── Admin-Switch.txt
│   ├── Campus-Router.txt
│   ├── Core-Switch.txt
│   ├── CSE-Switch.txt
│   ├── ECE-Switch.txt
│   ├── Edge-Router.txt
│   ├── ISP-Router.txt
│   ├── Lab-Switch.txt
│   └── Library-Switch.txt
│
├── Packet-Tracer/
│   └── Secure-College-Campus-Network.pkt
│
└── Screenshots/
    ├── VLAN
    ├── DHCP
    ├── NAT
    ├── STP
    └── Network Topology

## 🖥️ Tools Used:-
->Cisco Packet Tracer
->Visual Studio Code
->Git
->GitHub

## 🎯 Project Objectives:-
->Design a structured college campus network
->Separate departments using VLANs
->Enable controlled inter-VLAN communication
->Automate IP addressing using DHCP
->Implement dynamic routing using OSPF
->Provide redundancy using STP and EtherChannel
->Secure access ports using Port Security
->Provide secure device management using SSH
->Control departmental communication using ACLs
->Provide external connectivity using NAT

## 📚 Learning Outcomes
        ->Through this project, we gained practical experience in:

                     +Network design
                     +VLAN configuration
                     +Routing and switching
                     +Dynamic routing
                     +Network security
                     +Troubleshooting
                     +Cisco IOS configuration
                     +Packet Tracer simulation
                     +Git and GitHub project management

## 👥 Team:-
->Team Size: 2

## Project Type:-
          Cisco Networking | Network Security | Packet Tracer Simulation

## ⭐ Conclusion:-
           ->The Secure College Campus Network demonstrates how multiple networking technologies can work
together to build a structured, secure, reliable, and scalable campus network.
           ->From VLAN-based segmentation to ACL-based access control and NAT-based external connectivity, 
the project provides a practical implementation of core networking concepts using Cisco Packet Tracer.

