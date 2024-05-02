# Networking - Questions and Answers

This folder compiles Networking-related questions that have surfaced during my learning, work, or interviews. Feel free to explore and contribute by adding your comments if you have insights to share.

### What do you know about VLANs?
**Fundamentals of VLANs**

* **Definition:** A Virtual Local Area Network (VLAN) is a logical segmentation of a physical network switch. It allows you to group devices into separate broadcast domains, even if they are physically located on different switch ports. 
* **Purpose:**
    * **Enhanced Security:** VLANs isolate traffic within specific groups, preventing unauthorized access and mitigating broadcast storms.
    * **Flexibility and Scalability:**  You can reconfigure network segments without physically rewiring,  making network growth and changes far easier.
    * **Network Performance:** Containing broadcasts within a VLAN reduces unnecessary traffic on other segments, optimizing network utilization.
    * **Organizational Segmentation:** VLANs can mirror organizational structures (e.g., departments, project teams), simplifying network management.

**How VLANs Work**

1. **VLAN Assignment:** Devices are assigned to VLANs either:
    * **Port-based:** Ports on a switch are statically configured to belong to a specific VLAN.
    * **MAC-based:**  Devices are assigned based on their MAC address, offering more flexibility.
2. **VLAN Tagging:** Ethernet frames are tagged with a VLAN ID (IEEE 802.1Q standard) to identify their VLAN membership.
3. **Traffic Control:** Switches use these VLAN IDs to  forward traffic only to ports within the same VLAN, efficiently regulating broadcast domains.

**VLAN Types**

* **Data VLAN:** The default type, carrying regular user data traffic.
* **Management VLAN:**  Dedicated to managing switches, routers, etc., often with enhanced security.
* **Voice VLAN:** Prioritizes Voice over IP (VoIP) traffic for optimal call quality.
* **Native VLAN:** The untagged VLAN on a switchport (often management traffic travels on this).
* **Guest VLAN:** Isolates guest users from the main network for security.

**VLAN Configuration**

1. **Creating VLANs:** Using switch management interfaces (CLI, web portal), you create VLANs and assign unique IDs.
2. **Assigning Ports:** Determine a port-based or MAC-based assignment method and link ports or devices to their respective VLANs.
3. **VLAN Trunking:** When traffic from multiple VLANs needs to traverse a link between switches, VLAN trunking is used. This ensures VLAN IDs remain intact across the link.

**Security Considerations**

While VLANs improve security, they shouldn't be your sole protection:

* **VLAN Hopping:**  Attacks where traffic escapes its designated VLAN.  Mitigation techniques include disabling unused switch ports and careful trunk port configuration.
* **Inter-VLAN Routing:**  Use routers or Layer 3 switches with firewalls and access control lists (ACLs) to manage traffic flow between VLANs carefully.

### What is a trunk in networking?
**Definition**

A trunk is a point-to-point link between two network devices, usually switches, that carries traffic from multiple VLANs simultaneously.

**Why Trunks Matter**

1. **Efficiency:** Without trunks, you'd need a separate physical link for each VLAN you want to extend between switches. Trunks streamline this by bundling multiple VLANs into a single channel.
2. **Scalability:** As you add VLANs to your network, trunks prevent the need for a massive number of physical cables, making your network easier to manage.

**How Trunks Work**

1. **VLAN Tagging:**  When a frame from a specific VLAN enters a trunk port, the switch adds a special tag (IEEE 802.1Q) to the Ethernet frame's header. This tag contains the VLAN ID.

2. **Traffic Across the Link:** The frames from multiple VLANs, complete with tags, travel across the trunk link.

3. **De-Tagging:** At the receiving switch, the trunk port analyzes the VLAN tags and strips them off, placing frames onto their correct destination VLANs.

**Key Points**

* **Trunk Ports:** Switch ports designated as trunks are configured to understand and process VLAN tags.
* **Trunking Protocol:**  Switches use protocols like 802.1Q (the most common) or Cisco's ISL (Inter-Switch Link) to manage VLAN tagging on trunks.
* **Native VLAN:**  On a trunk, one VLAN is usually the "native VLAN." Traffic on the native VLAN is not tagged.

**Analogy**

Imagine a multi-lane highway. Each lane could represent a VLAN, carrying traffic of a specific type.  A trunk is like this highway – it bundles all those streams of traffic efficiently for transport between two points.

### VLAN needs organizational planning
**Separate VLAN Instances**

When you define VLAN 10 on switch 1 and VLAN 30 on switch 2, even though they're labeled "finance", they are entirely separate VLANs. Devices within VLAN 10 on switch 1 cannot communicate directly with devices in VLAN 30 on switch 2. Think of them as parallel universes, each with its own isolated Finance department.

**VLANs for Segmentation**

The purpose of VLANs is to create logical segmentation within a network. This means devices in the same VLAN can communicate as if they were on the same physical switch, regardless of their physical location.

**How to Facilitate Communication**

To allow communication between VLAN 10 on switch 1 and VLAN 30 on switch 2, you'll need inter-VLAN routing:

* **Router:** A traditional router with interfaces connected to each VLAN would provide the necessary routing between these networks.
* **Layer 3 Switch:** A multilayer switch with routing capabilities can perform this function within the switch infrastructure itself.

**Organization-wide VLAN Planning**

Absolutely! For VLANs to work effectively for segmentation across your network, you need organization-wide planning. This involves:

* **Consistent VLAN IDs:**  VLAN 10 should represent the Finance department across ALL switches in your organization to establish a consistent scheme.
* **IP Addressing:** Plan IP subnets carefully to align with your VLAN structure, making routing easier to manage.
* **Inter-VLAN Routing:** Design a strategy for where and how routing will occur between different VLANs.

### What is meant by IPSEC VPN?
**What is IPsec?**

* **Core Concept:** IPsec (Internet Protocol Security) is a robust suite of protocols designed to provide end-to-end security for communications happening over IP networks.  It operates at the network layer (Layer 3 of the OSI model).

* **Key Functions:**
    * **Encryption:** IPsec protects the confidentiality of your data in transit using strong encryption algorithms like AES, 3DES, and others.
    * **Authentication:** Ensures data integrity and origin verification. IPsec protects against tampering and confirms that packets come from a trusted source. 
    * **Key Exchange:** IPsec uses mechanisms like Internet Key Exchange (IKE) to negotiate and establish secure communication channels between devices.

**IPsec VPNs**

* **Tunneling:** IPsec VPNs leverage the power of IPsec to create secure "tunnels" over public networks, usually the internet. Think of these as encrypted pathways for your data.

* **Use Cases:**
    * **Remote Access VPNs:**  Allow remote workers to securely connect to corporate networks as if they were physically in the office.
    * **Site-to-Site VPNs:** Connect entire networks (e.g., branch offices to headquarters) over an encrypted link. 

**IPsec Modes**

* **Transport Mode:** 
    * Encrypts only the payload of the IP packet, leaving the original IP header intact.
    * Often used for host-to-host communications within a network.

* **Tunnel Mode:** 
    * Encrypts and encapsulates the entire original IP packet within a new IP packet. This adds a new IP header.
    * Preferred for remote access and site-to-site VPNs where the original IP header may need to be masked.

**IPsec Components**

* **Authentication Header (AH):** Provides data integrity and origin authentication by calculating a hash over the IP packet.

* **Encapsulating Security Payload (ESP):** Provides confidentiality (encryption), and optionally data integrity and origin authentication using both encryption and hashing.

**Advantages of IPsec VPNs**

* **Strong Security:** Proven, industry-standard protocols offer robust encryption and authentication.
* **Transparency:**  Works at the network layer, making it largely invisible to applications, ensuring compatibility.
* **Flexibility:** Can be used for various VPN scenarios.
* **Interoperability:** Many devices and vendors support IPsec.

**Considerations**

* **Complexity:** Configuration and management can be more involved than some other VPN solutions.
* **Overhead:** Encryption and authentication processes can add some overhead, potentially impacting performance for sensitive applications.