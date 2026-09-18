# Week 05 Journal – Internetworking

**Assessment:** COIT20246 Assessment 1 Part B  

**Student Name:** Rohit Hargovanbhai Prajapati  

**Student ID:** 12326317

---

# Task 1 – Knowledge Test

The Week 5 Knowledge Test was completed successfully through Moodle.

---

# Task 2 – View Routing Table

## Objective

The objective of this task was to use PowerShell to view the routing table of the primary network adapter and understand how the computer determines where network traffic should be sent.

## Command Used

```powershell
route print
```

The routing table can also be viewed using:

```powershell
Get-NetRoute
```

## Screenshot

![Routing Table](images/week5-task2-routing-table.png)

## Reading the Routing Table

A routing table contains entries that tell the computer how to reach different destination networks. Each row can be interpreted by looking at the destination network, network mask or prefix, gateway, interface, and metric.

The main information in each routing entry can be understood as follows:

| Routing Table Information | Description |
|---------------------------|-------------|
| Destination | The network or IP address that the computer is trying to reach. |
| Network Mask / Prefix | Defines the size of the destination network. |
| Gateway | The next-hop device used to forward traffic when the destination is not directly connected. |
| Interface | Identifies the local network interface through which the traffic will be sent. |
| Metric | A value used to determine the preferred route when more than one route is available. |

### My Routing Table Entries

The following table describes the important rows shown in my PowerShell routing-table screenshot.

| Destination | Netmask | Gateway | Interface | Description |
|-------------|---------|---------|-----------|-------------|
| `0.0.0.0` | `0.0.0.0` | `192.168.1.254` | `192.168.1.64` | Default route used to forward traffic to networks that do not have a more specific route. |
| `127.0.0.0` | `255.0.0.0` | `On-link` | `127.0.0.1` | Route for the local loopback network. Traffic remains within the computer. |
| `127.0.0.1` | `255.255.255.255` | `On-link` | `127.0.0.1` | Route for the local loopback address of the computer. |
| `127.255.255.255` | `255.255.255.255` | `On-link` | `127.0.0.1` | Loopback broadcast route for the local loopback network. |
| `192.168.1.0` | `255.255.255.0` | `On-link` | `192.168.1.64` | Directly connected local network. Devices on the `192.168.1.0/24` network can be reached through the Wi-Fi interface. |
| `192.168.1.64` | `255.255.255.255` | `On-link` | `192.168.1.64` | Route for the computer's own IPv4 address on the local network. |
| `192.168.1.255` | `255.255.255.255` | `On-link` | `192.168.1.64` | Broadcast address for the local `192.168.1.0/24` network. |
| `224.0.0.0` | `240.0.0.0` | `On-link` | `127.0.0.1` | Route for IPv4 multicast traffic associated with the loopback interface. |
| `224.0.0.0` | `240.0.0.0` | `On-link` | `192.168.1.64` | Route for IPv4 multicast traffic on the local Wi-Fi network. |
| `255.255.255.255` | `255.255.255.255` | `On-link` | `127.0.0.1` | Limited broadcast route associated with the loopback interface. |
| `255.255.255.255` | `255.255.255.255` | `On-link` | `192.168.1.64` | Limited broadcast route associated with the local Wi-Fi interface. |

The exact values in this table should match the entries visible in the routing-table screenshot.

## Discussion

The routing table is important because it allows the computer to decide where packets should be forwarded. A directly connected destination can normally be reached through the local interface, while traffic for a different network is normally forwarded to a configured gateway or router.

This activity helped me understand that routing decisions are made using destination networks and that the routing table provides the information required to forward packets correctly.

---

# Task 3 – IP Network Design

## Objective

The objective of this task was to design a small test network consisting of two switched Ethernet LANs connected through a 1 Gb/s Ethernet point-to-point WAN link.

The network contains five PCs, two Gigabit Ethernet switches and two routers. The two LANs use separate IPv4 /24 networks, while the routers provide communication between the networks.

## Project Team

| Team Member | Student ID |
|-------------|------------|
| Rohit Hargovanbhai Prajapati | 12326317 |
| Lehanul Islam Arnob | 12310097 |

---

## Network Design

The network was divided into three IPv4 networks:

- **LAN 1:** `63.17.1.0/24`
- **LAN 2:** `9.7.1.0/24`
- **WAN:** `10.0.0.0/24`

The first two decimal values of the first LAN were selected from the last four digits of my student ID, `6317`, resulting in the `63.17.x.x` address range.

The partner's student ID ends in `0097`. Following the task requirement, the first two decimal values used for the second LAN are `9.7`.

The WAN network uses a separate private IPv4 network because it is a point-to-point connection between the two routers.

---

## Part A – IPv4 Network Addresses and Device Assignments

### Network Addresses

| Network | Purpose | Network Address | Subnet Mask |
|---------|---------|-----------------|-------------|
| LAN 1 | Rohit's LAN | `63.17.1.0/24` | `255.255.255.0` |
| WAN | Router-to-router connection | `10.0.0.0/24` | `255.255.255.0` |
| LAN 2 | Arnob's LAN | `9.7.1.0/24` | `255.255.255.0` |

### Device and Interface Addressing

| Device | Interface | Network | IPv4 Address | Subnet Mask |
|--------|-----------|---------|--------------|-------------|
| PC1 | Ethernet | LAN 1 | `63.17.1.10` | `255.255.255.0` |
| PC2 | Ethernet | LAN 1 | `63.17.1.11` | `255.255.255.0` |
| PC3 | Ethernet | LAN 1 | `63.17.1.12` | `255.255.255.0` |
| Router 1 | LAN Interface | LAN 1 | `63.17.1.1` | `255.255.255.0` |
| Router 1 | WAN Interface | WAN | `10.0.0.1` | `255.255.255.0` |
| Router 2 | WAN Interface | WAN | `10.0.0.2` | `255.255.255.0` |
| Router 2 | LAN Interface | LAN 2 | `9.7.1.1` | `255.255.255.0` |
| PC4 | Ethernet | LAN 2 | `9.7.1.10` | `255.255.255.0` |
| PC5 | Ethernet | LAN 2 | `9.7.1.11` | `255.255.255.0` |

The switches are Layer 2 devices in this design, so an IP address is not required for their basic switching function.

### Default Gateway Configuration

| Device | IP Address | Default Gateway |
|--------|------------|-----------------|
| PC1 | `63.17.1.10` | `63.17.1.1` |
| PC2 | `63.17.1.11` | `63.17.1.1` |
| PC3 | `63.17.1.12` | `63.17.1.1` |
| PC4 | `9.7.1.10` | `9.7.1.1` |
| PC5 | `9.7.1.11` | `9.7.1.1` |

---

## Part B – Network Diagram

The network consists of two separate switched Ethernet LANs.

The first LAN contains three PCs connected to Switch 1. Switch 1 is connected to Router 1. The second LAN contains two PCs connected to Switch 2, which is connected to Router 2.

Router 1 and Router 2 are connected using a 1 Gb/s Ethernet point-to-point WAN link.

### Network Diagram

![IP Network Design](images/week5-task3-network.png)

### Original Draw.io File

`week5-task3-network.drawio`

---

## Network Topology

```text
PC1 ─┐
PC2 ─┼── Switch 1 ── Router 1 ═══ 1 Gb/s WAN ═══ Router 2 ── Switch 2 ──┬─ PC4
PC3 ─┘                                                                    └─ PC5
```

## Part C – Routing Tables

The routing tables below show the routes required for communication between the three IPv4 networks in the proposed network design.

### Router 1 Routing Table

| Destination Network | Next Hop | Interface | Description |
|----------------------|----------|-----------|-------------|
| `63.17.1.0/24` | Directly Connected | LAN Interface | Local LAN containing PC1, PC2 and PC3. |
| `10.0.0.0/24` | Directly Connected | WAN Interface | Point-to-point WAN network connecting Router 1 and Router 2. |
| `9.7.1.0/24` | `10.0.0.2` | WAN Interface | Remote LAN containing PC4 and PC5, reached through Router 2. |

Router 1 is directly connected to the `63.17.1.0/24` LAN and the `10.0.0.0/24` WAN network. The `9.7.1.0/24` network is a remote network, so Router 1 forwards packets for this network to Router 2 using `10.0.0.2` as the next hop.

### Router 2 Routing Table

| Destination Network | Next Hop | Interface | Description |
|----------------------|----------|-----------|-------------|
| `9.7.1.0/24` | Directly Connected | LAN Interface | Local LAN containing PC4 and PC5. |
| `10.0.0.0/24` | Directly Connected | WAN Interface | Point-to-point WAN network connecting Router 2 and Router 1. |
| `63.17.1.0/24` | `10.0.0.1` | WAN Interface | Remote LAN containing PC1, PC2 and PC3, reached through Router 1. |

Router 2 is directly connected to the `9.7.1.0/24` LAN and the `10.0.0.0/24` WAN network. The `63.17.1.0/24` network is a remote network, so Router 2 forwards packets for this network to Router 1 using `10.0.0.1` as the next hop.

### PC1 Routing Table

| Destination Network | Next Hop / Gateway | Interface | Description |
|----------------------|---------------------|-----------|-------------|
| `63.17.1.0/24` | Directly Connected | Ethernet | Local LAN containing PC1, PC2 and PC3. |
| `0.0.0.0/0` | `63.17.1.1` | Ethernet | Default route used to reach networks outside LAN 1. |

PC1 can communicate directly with devices on the `63.17.1.0/24` network. For traffic destined for another network, PC1 sends the packet to Router 1 at `63.17.1.1`.

### PC2 Routing Table

| Destination Network | Next Hop / Gateway | Interface | Description |
|----------------------|---------------------|-----------|-------------|
| `63.17.1.0/24` | Directly Connected | Ethernet | Local LAN containing PC1, PC2 and PC3. |
| `0.0.0.0/0` | `63.17.1.1` | Ethernet | Default route used to reach networks outside LAN 1. |

PC2 uses Router 1 at `63.17.1.1` as its default gateway when communicating with devices outside the local LAN.

### PC3 Routing Table

| Destination Network | Next Hop / Gateway | Interface | Description |
|----------------------|---------------------|-----------|-------------|
| `63.17.1.0/24` | Directly Connected | Ethernet | Local LAN containing PC1, PC2 and PC3. |
| `0.0.0.0/0` | `63.17.1.1` | Ethernet | Default route used to reach networks outside LAN 1. |

PC3 uses Router 1 at `63.17.1.1` as its default gateway for traffic destined for another IP network.

### PC4 Routing Table

| Destination Network | Next Hop / Gateway | Interface | Description |
|----------------------|---------------------|-----------|-------------|
| `9.7.1.0/24` | Directly Connected | Ethernet | Local LAN containing PC4 and PC5. |
| `0.0.0.0/0` | `9.7.1.1` | Ethernet | Default route used to reach networks outside LAN 2. |

PC4 can communicate directly with devices on the `9.7.1.0/24` network. For traffic destined for another network, PC4 sends the packet to Router 2 at `9.7.1.1`.

### PC5 Routing Table

| Destination Network | Next Hop / Gateway | Interface | Description |
|----------------------|---------------------|-----------|-------------|
| `9.7.1.0/24` | Directly Connected | Ethernet | Local LAN containing PC4 and PC5. |
| `0.0.0.0/0` | `9.7.1.1` | Ethernet | Default route used to reach networks outside LAN 2. |

PC5 uses Router 2 at `9.7.1.1` as its default gateway for traffic destined for another IP network.

### Switches

Switch 1 and Switch 2 are Layer 2 Ethernet switches. They forward Ethernet frames using MAC address tables rather than using IP routing tables.

| Device | Function |
|--------|----------|
| Switch 1 | Provides Ethernet connectivity between PC1, PC2, PC3 and Router 1. |
| Switch 2 | Provides Ethernet connectivity between PC4, PC5 and Router 2. |

### Routing Table Diagram

![Routing Tables](images/week5-task3-routing-tables.png)

---

# Part D – ICMP/IP Packet Analysis

To demonstrate communication between the two LANs, PC1 on LAN 1 sends an ICMP Echo Request to PC4 on LAN 2.

## Source and Destination Information

| Field | Value |
|-------|-------|
| Source Device | PC1 |
| Source IP Address | `63.17.1.10` |
| Destination Device | PC4 |
| Destination IP Address | `9.7.1.10` |
| Protocol | ICMP |
| ICMP Message | Echo Request |
| Source Network | `63.17.1.0/24` |
| Destination Network | `9.7.1.0/24` |
| WAN Network | `10.0.0.0/24` |

PC1 and PC4 are located on different IPv4 networks. Therefore, PC1 sends the packet to its default gateway, Router 1. Router 1 forwards the packet through the WAN link to Router 2, and Router 2 forwards it to PC4.

## Packet Flow

```text
PC1
63.17.1.10
    |
    | ICMP Echo Request
    v
Switch 1
    |
    v
Router 1
LAN: 63.17.1.1
WAN: 10.0.0.1
    |
    | 1 Gb/s Ethernet WAN
    | Network: 10.0.0.0/24
    v
Router 2
WAN: 10.0.0.2
LAN: 9.7.1.1
    |
    v
Switch 2
    |
    v
PC4
9.7.1.10
```

## ICMP/IP Encapsulation

The ICMP Echo Request is carried inside an IPv4 packet. The IPv4 packet is then carried inside an Ethernet frame.

```text
+--------------------------------------------------+
| Ethernet II Header                               |
| Source MAC:      Current sender interface        |
| Destination MAC: Next-hop interface              |
| EtherType:       0x0800 (IPv4)                   |
+--------------------------------------------------+
| IPv4 Header                                      |
| Source IP:      63.17.1.10                       |
| Destination IP: 9.7.1.10                         |
| Protocol:       ICMP                             |
| TTL:            Decreased at each router         |
+--------------------------------------------------+
| ICMP Header                                      |
| Type:           8 (Echo Request)                 |
| Code:           0                                |
| Checksum                                          |
| Identifier                                        |
| Sequence Number                                   |
+--------------------------------------------------+
| ICMP Data                                        |
+--------------------------------------------------+
```

## IP Addresses in the Packet

The end-to-end IP addresses are:

```text
Source IP:       63.17.1.10
Destination IP:  9.7.1.10
Protocol:        ICMP
```

The source IP address belongs to PC1 and the destination IP address belongs to PC4. The routers use the destination IP address to determine where the packet should be forwarded.

The IPv4 TTL is reduced when the packet passes through a router.

## Ethernet MAC Addresses

The Ethernet MAC addresses are different on each network segment.

### LAN 1 – PC1 to Router 1

```text
Source MAC:
PC1 Ethernet Interface MAC

Destination MAC:
Router 1 LAN Interface MAC
```

PC1 sends the Ethernet frame to Router 1 because PC4 is outside PC1's local `63.17.1.0/24` network.

### WAN – Router 1 to Router 2

When Router 1 forwards the packet through the WAN link, it creates a new Ethernet frame.

```text
Source MAC:
Router 1 WAN Interface MAC

Destination MAC:
Router 2 WAN Interface MAC
```

The IP addresses remain:

```text
Source IP:       63.17.1.10
Destination IP:  9.7.1.10
```

However, the Ethernet MAC addresses are now those of the WAN interfaces of Router 1 and Router 2.

### LAN 2 – Router 2 to PC4

Router 2 forwards the packet towards PC4 using another Ethernet frame.

```text
Source MAC:
Router 2 LAN Interface MAC

Destination MAC:
PC4 Ethernet Interface MAC
```

Therefore, the MAC addresses change when the packet moves between different Ethernet network segments.

## Packet Captured at Router 1

If the packet is captured on the LAN-side interface of Router 1, the frame can be represented as:

```text
+--------------------------------------------------+
| Ethernet II Header                               |
|                                                  |
| Source MAC:      PC1 Ethernet Interface MAC     |
| Destination MAC: Router 1 LAN Interface MAC     |
| EtherType:       0x0800 (IPv4)                   |
+--------------------------------------------------+
| IPv4 Header                                      |
|                                                  |
| Source IP:      63.17.1.10                       |
| Destination IP: 9.7.1.10                         |
| Protocol:       ICMP                             |
+--------------------------------------------------+
| ICMP Header                                      |
|                                                  |
| Type:           8 – Echo Request                 |
| Code:           0                                |
+--------------------------------------------------+
| ICMP Data                                        |
+--------------------------------------------------+
```

## MAC Address Summary

| Network Segment | Source MAC | Destination MAC |
|-----------------|------------|-----------------|
| LAN 1 | PC1 Ethernet Interface | Router 1 LAN Interface |
| WAN | Router 1 WAN Interface | Router 2 WAN Interface |
| LAN 2 | Router 2 LAN Interface | PC4 Ethernet Interface |

The task does not require the specific MAC addresses. It requires identifying which devices or interfaces provide the MAC addresses in the Ethernet frame.

## Packet Forwarding Explanation

When PC1 sends an ICMP Echo Request to PC4, PC1 determines that `9.7.1.10` is outside its local `63.17.1.0/24` network. PC1 therefore sends the Ethernet frame to its default gateway, Router 1.

Router 1 receives the frame and processes the IPv4 packet. It checks its routing table and determines that the `9.7.1.0/24` network can be reached through Router 2 using `10.0.0.2` as the next hop.

Router 1 forwards the packet through its WAN interface. A new Ethernet frame is used on the WAN link, with Router 1's WAN interface as the source MAC address and Router 2's WAN interface as the destination MAC address.

Router 2 receives the packet and checks its routing table. Since `9.7.1.0/24` is directly connected to Router 2, it forwards the packet through its LAN interface towards PC4.

Finally, Switch 2 forwards the Ethernet frame to PC4.

This demonstrates that the IP addresses identify the source and final destination of the packet, while the MAC addresses are used for delivery across each individual Ethernet network segment.

## Packet Diagram

![ICMP/IP Packet Diagram](images/week5-task3-packet.png)

### Original Draw.io File

`week5-task3-packet.drawio`

---

# Task 4 – Academic Integrity Outcomes

## Objective

The objective of this activity was to discuss a hypothetical academic integrity scenario and consider how students could avoid academic misconduct, the possible level of a breach, the likely consequences, and the future implications if the misconduct was not detected.

## Selected Scenario

### Scenario: Sharing and Copying an Individual Assignment

A student was required to complete an individual programming assignment. The assessment instructions stated that the work had to be completed independently and that students were not permitted to share their solutions with other students.

The student was struggling with the programming task and asked a classmate for help. Instead of only discussing the programming concepts, the classmate sent the student their completed assignment. The student copied significant sections of the solution, changed some variable names and formatting, and submitted the assignment as their own work.

The student who provided the completed assignment also knew that the assessment was an individual task but still shared their solution with the other student.

The issue was later identified when the two submissions were compared and significant similarities were found.

### Discussion

The selected scenario involved both students participating in behaviour that could compromise the integrity and fairness of an individual assessment.

The main issue was that the student who submitted the copied work represented another student's work as their own. The student who shared the completed assignment also contributed to the problem because the assessment instructions did not permit students to share their solutions.

This scenario was interesting because it demonstrated that academic integrity is not only about copying information from websites or sources. It can also involve students sharing answers or working together in ways that are not permitted by the assessment requirements.

CQUniversity explains that collusion can occur when students work together in ways that are not permitted, including sharing answers, co-writing individual assignments, or using another student's work. Academic misconduct can include plagiarism, collusion, cheating, file sharing and contract cheating.

## a) How the Students Could Have Avoided the Problem

The students could have avoided the problem by:

1. **Following the assessment instructions:**  
   The student should have completed the individual assessment independently and should not have copied another student's completed solution.

2. **Asking the tutor for help:**  
   If the student did not understand the programming task, they could have asked the tutor or Unit Coordinator for clarification rather than requesting another student's completed assignment.

3. **Discussing concepts rather than exchanging answers:**  
   Students can study together where collaboration is allowed, but they should avoid sharing completed answers or solutions when the assessment requires individual work.

4. **Starting the assessment earlier:**  
   Beginning the assessment earlier would have given the student more time to understand the requirements, practise the programming concepts and seek legitimate academic support.

5. **The other student should not have shared the completed assignment:**  
   Even though the second student had completed their own work, they should have refused to provide the solution because sharing it could contribute to academic misconduct.

## b) Academic Integrity Breach and Outcome

### Breach Level

**Breach type:** Potential academic misconduct involving **collusion and/or plagiarism**.

The student's submission could be considered a breach because significant parts of another student's work were submitted as their own. The student who shared the completed solution may also face academic integrity consequences because the sharing of assessment answers was not permitted.

CQUniversity identifies collusion as working together in ways that are not permitted, such as sharing answers, co-writing individual assignments, or using another student's work. Academic misconduct is considered a breach of academic integrity.

### Likely Outcome

The exact outcome would depend on the evidence, circumstances of the case, and CQUniversity's academic integrity process. It would not be appropriate to assume that every case automatically receives the same penalty.

Possible outcomes can include educational requirements or other academic integrity outcomes and penalties. Depending on the circumstances, CQU lists outcomes such as referral to the Academic Learning Centre, completion of Foundations of Academic Integrity, replacement assessment with a maximum pass grade, a fail for the assessment task, or a fail/not competent grade for the unit. More serious cases can have more significant consequences.

For this scenario, a likely academic consequence could be a penalty affecting the assessment result, such as receiving zero or a fail for the assessment, depending on the outcome of the academic integrity process.

### Is the Outcome Fair?

Our group discussed whether an academic integrity penalty would be fair.

We considered that academic integrity rules are important because students who complete their assessments honestly invest their own time and effort. If another student receives marks for copied work, it could create an unfair advantage over students who completed their work independently.

At the same time, we discussed that each case should be considered individually because the circumstances and evidence may differ between students. The university's process therefore allows the circumstances of an individual case to be considered before an outcome or penalty is determined.

## c) Future Ramifications

If a student performs academic misconduct but is not caught during the teaching term, there can still be future ramifications.

For the student who submitted the copied work:

- They may receive marks for knowledge and skills that they have not actually developed.
- They may struggle with later subjects because they did not properly understand the underlying concepts.
- The academic integrity issue could potentially be identified later through assessment reviews or other university processes.
- If the misconduct is subsequently investigated, the student may still face an academic integrity outcome or penalty.
- A fail result for a unit could affect future enrolments and study progression.

For the student who shared the work:

- They may also face academic integrity consequences if their involvement in sharing the assessment is established.
- Sharing completed assessment solutions can negatively affect other students and the fairness of the assessment process.
- It may create an academic integrity issue even though the student originally completed their own work.

For other students:

- Students who complete their assessments honestly may be disadvantaged if another student receives an academic result through copied work.
- It can reduce confidence that assessment results accurately represent individual knowledge and skills.

Therefore, avoiding academic misconduct is important not only for an individual student's results but also for maintaining fairness and trust within the university community.

## Recommendations to Other Students

### 1. Complete Assessment Work Honestly

Students should complete individual assessments using their own work and understanding. They should only use resources, collaboration, or assistance that are explicitly permitted by the assessment requirements. Students should never share or submit another student's completed assessment as their own.

### 2. Ask for Help When Unsure

If a student is struggling with an assessment, they should ask the tutor, Unit Coordinator or appropriate university support service for assistance. It is better to ask for legitimate academic support than to copy another student's work or share completed assessment answers.

## Conclusion

This scenario demonstrated that academic integrity applies to both the student who copies work and the student who knowingly shares work when sharing is not permitted. Academic misconduct can have consequences for individual students and can also affect the fairness of assessment for other students.

The main lesson from the discussion was that students should understand the assessment requirements, complete individual work independently, and seek appropriate academic support whenever they are unsure or experiencing difficulties.

---

## Task 5 – IP Address Lookup

### Objective

The objective of this task was to use an online IP address lookup service to investigate public IP addresses and determine what information can be identified from them. I used two public IP addresses that are associated with Melbourne, Victoria, Australia and compared the information returned by the lookup service.

### IP Addresses Used

| IP Address      | Location Identified            | Network / ISP   |
| --------------- | ------------------------------ | --------------- |
| `203.39.128.75` | Melbourne, Victoria, Australia | Telstra Limited |
| `124.254.76.26` | Melbourne, Victoria, Australia | Vocus Pty Ltd   |

The first IP address, `203.39.128.75`, is listed as a public IPv4 address located in Melbourne, Victoria, Australia and associated with Telstra Limited (AS1221). The second IP address, `124.254.76.26`, is also listed as being located in Melbourne, Victoria, Australia and is associated with Vocus Pty Ltd (AS4826).

### Results

#### IP Address 1 – 203.39.128.75

The lookup identified the following information:

* **IP Address:** `203.39.128.75`
* **Country:** Australia
* **State:** Victoria
* **City:** Melbourne
* **ISP/Organisation:** Telstra Limited
* **ASN:** AS1221
* **Timezone:** Australia/Melbourne

The lookup identified the city as Melbourne, but it did not identify a specific person's name, computer, house or exact street address.

#### IP Address 2 – 124.254.76.26

The lookup identified the following information:

* **IP Address:** `124.254.76.26`
* **Country:** Australia
* **State:** Victoria
* **City:** Melbourne
* **Postcode:** 3000
* **ISP/Organisation:** Vocus Pty Ltd
* **ASN:** AS4826
* **Timezone:** Australia/Melbourne

The lookup also provides approximate geographic coordinates for the IP address. However, these coordinates should not be interpreted as the exact physical location of the person using the IP address.

### How Accurate Is IP Geolocation?

IP geolocation can provide useful information such as the country, state, city, ISP and Autonomous System Number (ASN). However, it does not normally provide the exact physical location of the user.

For example, both IP addresses used in this task were identified as being in Melbourne. This means that the IP geolocation database associates the network addresses with Melbourne, but it does not prove that a particular person or computer is physically located at the exact coordinates shown.

IP geolocation is generally based on network registration, routing information and geolocation databases. Therefore, the accuracy can vary depending on the ISP and type of network. Mobile networks, VPNs, proxies and other network infrastructure can make the reported location different from the user's actual location.

### What Information Can Be Identified?

From a public IP address lookup, the following information may be available:

* Public IP address
* Country
* State or region
* Approximate city
* ISP or organisation
* Autonomous System Number (ASN)
* Timezone
* Approximate geographic coordinates
* Network or IP range

However, an IP lookup does **not** normally identify the exact person using the connection or their exact street address. The location information should therefore be treated as an approximation rather than a precise physical location.

### Comparison

Both IP addresses were associated with Melbourne, Victoria, Australia, but they belonged to different network providers.

`203.39.128.75` was associated with **Telstra Limited**, while `124.254.76.26` was associated with **Vocus Pty Ltd**. This demonstrates that IP geolocation can provide information about the network and approximate geographic area associated with an IP address.

### Conclusion

This task showed that an IP address can provide useful information about the network from which an Internet connection originates. The lookup services were able to identify Melbourne, Victoria, Australia for both test addresses and also provide information about their respective network providers.

However, IP geolocation should not be considered an exact location service. It can identify an approximate city or region, but it cannot reliably identify the exact physical location or identity of the person using the IP address. Therefore, IP address lookup is useful for general network and geographic identification, but its results have limitations.


## Discussion

This activity demonstrated that IP geolocation should not be treated as an exact method of identifying a person's physical location. The information provided by an IP lookup service is generally associated with the network or ISP and may identify a city or broader region rather than the exact location of the computer.

Using two different networks also demonstrated that a device can appear with a different public IP address depending on the network connection being used.

---

# Reflection

This week's activities improved my understanding of internetworking and how routers connect separate IP networks. Viewing the routing table helped me understand how a computer determines where packets should be sent and how gateways and interfaces are used during packet forwarding.

Designing the test network was useful because it required me to assign IPv4 addresses, separate the LANs into different networks, configure router interfaces conceptually, and create routing tables. The packet diagram also helped me understand the difference between IP addressing and Ethernet addressing. IP addresses identify the end hosts involved in communication, while MAC addresses are used for delivery across the current local network segment.

The academic integrity activity reinforced the importance of completing assessment work honestly and understanding the rules before submitting work. Finally, the IP address lookup activity showed that an IP address can provide general network and geographical information, but it does not necessarily reveal an exact physical location.

Overall, the Week 5 activities gave me a better practical understanding of routing, IPv4 network design, packet forwarding, Ethernet addressing, and the relationship between different network layers.
