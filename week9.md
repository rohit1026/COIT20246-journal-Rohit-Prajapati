# Week 09 – Attacks and Vulnerabilities

**Assessment:** COIT20246 Assessment 1 Part B  

**Student Name:** Rohit Hargovanbhai Prajapati  

**Student ID:** 12326317

---

## Task 1 – Complete the Knowledge Test

I completed the Week 09 Knowledge Test during the tutorial.


---

# Task 2 – CIA Protections

## Introduction

For this task, I considered the important assets in our project network and used the CIA Triad to identify what needs to be protected.

The CIA Triad consists of:

- **Confidentiality** – preventing unauthorised people from accessing information.
- **Integrity** – preventing unauthorised or incorrect changes to information.
- **Availability** – making sure systems and information are available when they are needed.

Our project test network contains two LANs connected through two routers. LAN1 contains three PCs and LAN2 contains two PCs. The network also includes two switches and a router-to-router WAN connection.

## Important Assets and CIA Protections

| Asset | Confidentiality | Integrity | Availability | Reason |
|---|---|---|---|---|
| PC1 on LAN1 | Yes | Yes | Yes | PC1 may contain project files, configuration files and other information that should not be accessed or changed by unauthorised users. It also needs to remain available for network testing. |
| PC2 on LAN1 | Yes | Yes | Yes | The computer is part of the network and may store or process project information. Unauthorised access or changes could affect the network tests. |
| PC3 on LAN1 | Yes | Yes | Yes | The PC is an important endpoint in the LAN and needs protection against unauthorised access, modification and service disruption. |
| PC4 on LAN2 | Yes | Yes | Yes | PC4 is an endpoint on the second LAN and should be protected from unauthorised access and changes. It also needs to be available for communication tests. |
| PC5 on LAN2 | Yes | Yes | Yes | PC5 participates in the second LAN and may be used for network testing. Loss of integrity or availability could affect testing. |
| Switch 1 | No | Yes | Yes | The switch controls communication between devices on LAN1. Unauthorised configuration changes could disrupt or redirect network traffic. |
| Switch 2 | No | Yes | Yes | The switch is important for communication on LAN2. Incorrect or malicious configuration changes could interrupt network connectivity. |
| Router 1 | Yes | Yes | Yes | Router 1 connects LAN1 to the WAN. Its configuration contains network information and incorrect changes could affect communication between networks. |
| Router 2 | Yes | Yes | Yes | Router 2 connects the WAN to LAN2. It needs to remain correctly configured so traffic can reach the second LAN. |
| WAN link between routers | No | Yes | Yes | The WAN link allows the two LANs to communicate. If it is unavailable, communication between the two networks will fail. |
| IP addressing and routing information | Yes | Yes | Yes | Correct IP addresses and routing information are required for communication. Unauthorised changes could send traffic to the wrong destination or stop communication. |
| Project configuration files | Yes | Yes | Yes | Configuration files may contain network settings and design information. They should not be exposed or modified without permission and should be available when required. |

## Most Important CIA Protections

Some assets require all three CIA protections.

For example, **router configurations** need confidentiality because they may contain network information, integrity because an attacker should not be able to change routing settings, and availability because the router must continue forwarding traffic.

The **WAN link** is particularly important for availability because it provides the connection between the two LANs. If the WAN link is unavailable, devices on the two LANs cannot communicate through the routers.

The **project configuration files** also require all three protections. Confidentiality prevents unauthorised people from viewing them, integrity prevents unauthorised changes, and availability ensures that the files can be accessed when the project team needs them.

---

# Task 3 – Threat Sources and Motivation

## Introduction

For our project network, I considered several realistic adversarial threat sources and what they might want to achieve. The threat sources below are based on the type of network we are designing and testing.

| Threat Source | Possible Motivation |
|---|---|
| Unauthorised person on LAN1 | Wants to access systems or network resources without permission. |
| Unauthorised person on LAN2 | Wants to gain access to devices or information on the second LAN. |
| Attacker using a compromised PC | Wants to use an infected computer as a starting point to attack other network devices. |
| Malicious insider | May intentionally change network configurations, access information or disrupt network services. |
| External attacker | Wants to gain unauthorised access to the network or discover weaknesses in the network security. |
| Malware or automated attacker | Attempts to compromise vulnerable systems and spread to other devices. |
| Curious or inexperienced user | May access or change network resources without understanding the security consequences. |
| Attacker attempting denial of service | Wants to make network devices or services unavailable to legitimate users. |

## Threat Source Details

### 1. Unauthorised Person on LAN1

**Motivation:**  
The attacker may want to access other computers or network resources without permission. They may attempt to discover devices, services or weaknesses on the LAN.

### 2. Unauthorised Person on LAN2

**Motivation:**  
The attacker may want to access devices or information on LAN2. They could also attempt to use the second LAN as a starting point for attacking other parts of the network.

### 3. Attacker Using a Compromised PC

**Motivation:**  
If an endpoint has already been compromised, an attacker may use it to explore the network, collect information or attempt to compromise other devices.

### 4. Malicious Insider

**Motivation:**  
An insider already has some level of legitimate access. They may misuse that access to view information, change configurations or disrupt network services.

### 5. External Attacker

**Motivation:**  
An external attacker may try to identify exposed services and vulnerabilities and then gain unauthorised access to the network.

### 6. Malware or Automated Attacker

**Motivation:**  
Malware may attempt to compromise vulnerable systems, collect information, damage files or spread to additional computers.

### 7. Curious or Inexperienced User

**Motivation:**  
This type of threat may not have a deliberate malicious goal. The user might access or change something simply because they are curious or do not understand the security implications.

### 8. Denial-of-Service Attacker

**Motivation:**  
The goal is to reduce or prevent availability of network devices or services. For this project network, this could prevent normal communication between the two LANs.

---

# Task 4 – Explore Vulnerabilities

## Introduction

For this task, I used the NIST National Vulnerability Database (NVD) to examine recent CVEs. The tutorial requires three different vulnerabilities from the previous 12 months: one **Critical**, one **High**, and one **Medium** severity vulnerability.

The three CVEs selected for the required categories are:

1. **CVE-2026-9891 – Critical**
2. **CVE-2026-9999 – High**
3. **CVE-2026-9996 – Medium**

All three are vulnerabilities affecting Google Chrome.

---

## 4.1 Critical CVE – CVE-2026-9891

| Field | Details |
|---|---|
| CVE ID | **CVE-2026-9891** |
| Company | **Google** |
| Product | **Google Chrome** |
| Published Date | **28 May 2026** |
| CVSS Version | **3.1** |
| CVSS Base Score | **9.0** |
| Severity | **Critical** |
| CWE | **CWE-416 – Use After Free** |
| Component | **Chrome Extensions** |
| Affected Version | Chrome before **148.0.7778.216** on affected configurations |

### CVE Description

CVE-2026-9891 is a use-after-free vulnerability in the Extensions component of Google Chrome. A remote attacker who has compromised the renderer process could potentially use a crafted Chrome Extension to escape the browser sandbox.

### CVSS v3.1 Vector

```text
CVSS:3.1/AV:N/AC:H/PR:N/UI:N/S:C/C:H/I:H/A:H
```

### CIA Impact

| CIA Element | Impact |
|---|---|
| Confidentiality | **High** |
| Integrity | **High** |
| Availability | **High** |

### Product Description

Google Chrome is a web browser used to access websites and web applications. Chrome also supports browser extensions that provide additional functionality.

### Simple Explanation

A use-after-free vulnerability occurs when software continues to use a section of memory after that memory has already been released. If the memory is reused, the old reference can point to an invalid or unexpected area of memory.

In this vulnerability, exploitation could potentially allow an attacker who has already compromised the renderer process to escape the Chrome sandbox using a specially crafted extension.

### Detection

A basic detection method is to check the installed Google Chrome version and compare it with the affected versions. Vulnerability-management and endpoint-management tools can also be used to identify outdated browser installations.

### Mitigation

The main mitigation is to update Google Chrome to a version containing the security fix. Organisations should also keep browser updates managed and applied regularly.

### Sources

- NVD: https://nvd.nist.gov/vuln/detail/CVE-2026-9891
- Chrome Security Advisory: https://chromereleases.googleblog.com/2026/05/stable-channel-update-for-desktop_0877304591.html
- Chromium Issue: https://issues.chromium.org/issues/513508128

---

## 4.2 High CVE – CVE-2026-9999

| Field | Details |
|---|---|
| CVE ID | **CVE-2026-9999** |
| Company | **Google** |
| Product | **Google Chrome** |
| Published Date | **28 May 2026** |
| CVSS Version | **3.1** |
| CVSS Base Score | **8.8** |
| Severity | **High** |
| CWE | **CWE-269 – Improper Privilege Management** |
| Component | **ANGLE** |
| Affected Version | Chrome before **148.0.7778.216** on the affected Mac configuration |

### CVE Description

CVE-2026-9999 is an inappropriate implementation issue in ANGLE in Google Chrome. A remote attacker could potentially execute arbitrary code inside the Chrome sandbox through a specially crafted HTML page.

### CVSS v3.1 Vector

```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H
```

### CIA Impact

| CIA Element | Impact |
|---|---|
| Confidentiality | **High** |
| Integrity | **High** |
| Availability | **High** |

### Product Description

Google Chrome is a web browser. ANGLE is a graphics abstraction component used by Chrome to translate graphics API calls between different graphics systems.

### Simple Explanation

The vulnerability is related to how Chrome's ANGLE component processes specially crafted web content. An attacker could create a malicious HTML page and persuade a user to open it. Processing that content could potentially allow arbitrary code execution inside the browser sandbox.

### Detection

The installed Chrome version can be checked on affected Mac systems. Vulnerability-management or endpoint-management tools can also be used to identify systems running vulnerable versions.

### Mitigation

The main mitigation is to upgrade Google Chrome to a fixed version for the affected configuration. Keeping browsers updated reduces exposure to known vulnerabilities.

### Sources

- NVD: https://nvd.nist.gov/vuln/detail/CVE-2026-9999
- Chrome Security Advisory: https://chromereleases.googleblog.com/2026/05/stable-channel-update-for-desktop_0877304591.html
- Chromium Issue: https://issues.chromium.org/issues/513364480

---

## 4.3 Medium CVE – CVE-2026-9996

| Field | Details |
|---|---|
| CVE ID | **CVE-2026-9996** |
| Company | **Google** |
| Product | **Google Chrome** |
| Published Date | **28 May 2026** |
| CVSS Version | **3.1** |
| CVSS Base Score | **6.5** |
| Severity | **Medium** |
| CWE | **CWE-125 – Out-of-bounds Read** |
| Component | **WebRTC** |
| Affected Version | Chrome before **148.0.7778.216** on the affected Mac configuration |

### CVE Description

CVE-2026-9996 is an out-of-bounds read vulnerability in WebRTC in Google Chrome on Mac. A remote attacker could potentially obtain sensitive information from process memory through specially crafted HTML content.

### CVSS v3.1 Vector

```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:N/A:N
```

### CIA Impact

| CIA Element | Impact |
|---|---|
| Confidentiality | **High** |
| Integrity | **None** |
| Availability | **None** |

### Product Description

Google Chrome is a web browser. WebRTC provides browser technologies that support real-time communication, including audio and video communication.

### Simple Explanation

An out-of-bounds read happens when software reads memory outside the area that it is supposed to access. In this case, specially crafted web content could potentially cause the WebRTC component to read information from memory that should not be exposed.

### Detection

The installed Chrome version can be checked on affected Mac systems. Vulnerability-management tools can also be used to identify outdated versions.

### Mitigation

The main mitigation is to update Google Chrome to the fixed version or later for the affected configuration. Browser updates should be applied regularly.

### Sources

- NVD: https://nvd.nist.gov/vuln/detail/CVE-2026-9996
- Chrome Security Advisory: https://chromereleases.googleblog.com/2026/05/stable-channel-update-for-desktop_0877304591.html
- Chromium Issue: https://issues.chromium.org/issues/513268100

---

## 4.4 CVE Selection Note

I initially considered **CVE-2026-91742** for the Medium category because the Chromium advisory describes its security severity as Medium.

However, the current NVD record is still **Awaiting Analysis**, and available CVSS v3.1 information reports a **9.8 Critical** score. Therefore, I did not use it as the Medium CVSS example.

Instead, I selected **CVE-2026-9996**, which has a CVSS v3.1 base score of **6.5 (Medium)** and therefore matches the category required by the tutorial.

For reference:

- CVE-2026-91742: https://nvd.nist.gov/vuln/detail/CVE-2026-91742
- Chrome September 2026 advisory: https://chromereleases.googleblog.com/2026/09/stable-channel-update-for-desktop_0541751186.html
- Chromium Issue: https://issues.chromium.org/issues/513858387

---

## 4.5 CVE Comparison

| Requirement | CVE | Product | CVSS v3.1 Score | Severity | CWE |
|---|---|---|---:|---|---|
| Critical | CVE-2026-9891 | Google Chrome | **9.0** | **Critical** | CWE-416 – Use After Free |
| High | CVE-2026-9999 | Google Chrome | **8.8** | **High** | CWE-269 – Improper Privilege Management |
| Medium | CVE-2026-9996 | Google Chrome | **6.5** | **Medium** | CWE-125 – Out-of-bounds Read |

## CIA Comparison

| CVE | Confidentiality | Integrity | Availability |
|---|---|---|---|
| CVE-2026-9891 | High | High | High |
| CVE-2026-9999 | High | High | High |
| CVE-2026-9996 | High | None | None |

## Task 4 Conclusion

The three CVEs demonstrate different vulnerability types and different levels of impact.

CVE-2026-9891 involves a use-after-free issue in Chrome Extensions and can potentially lead to a sandbox escape after renderer compromise.

CVE-2026-9999 involves an issue in the ANGLE component and can potentially result in arbitrary code execution inside the browser sandbox through specially crafted HTML content.

CVE-2026-9996 involves an out-of-bounds read in WebRTC and can potentially expose sensitive information from process memory.

This task showed me that CVSS severity, CIA impact, CWE classification, affected versions and vendor information are all useful when analysing a vulnerability.

---

# Task 5 – Vulnerability Disclosures

## My Viewpoint on Vulnerability Disclosure

I think vulnerability disclosure should normally follow a coordinated or responsible disclosure process.

When a security researcher discovers a vulnerability, immediately publishing all technical details can create a risk because attackers may use the information before the vendor has had enough time to develop and release a fix. This is especially important for vulnerabilities that are easy to exploit or affect widely used software.

At the same time, vendors should not keep vulnerabilities private indefinitely. Users need security updates and information about vulnerabilities so they can protect their systems. A long delay can leave many users exposed without knowing that a security problem exists.

I think a reasonable process is for the researcher to report the vulnerability privately to the vendor first. The report should contain enough technical information for the vendor to reproduce and investigate the problem. The vendor should then be given a reasonable period to develop and test a fix.

The amount of time needed can depend on the vulnerability. A simple vulnerability affecting a small product may be fixed relatively quickly, while a serious vulnerability affecting widely used software may require more time for development, testing and coordinated release. For a high-impact vulnerability, the researcher and vendor should communicate during the process rather than simply waiting without updates.

If the vendor does not respond, the researcher should normally make further attempts to contact the vendor or use an appropriate coordinated disclosure channel. If disclosure eventually becomes necessary, the researcher should avoid unnecessarily releasing exploit details that would make attacks easier, particularly while many users are still unpatched.

Bug bounty programs can also improve this process because they provide security researchers with an official way to report vulnerabilities. They can encourage researchers to report problems privately while giving vendors a structured process for handling the reports.

Overall, I believe the main goal should be to reduce the risk to users. Researchers need a way to receive recognition or rewards for finding vulnerabilities, while vendors need enough time to investigate and fix them. Coordinated disclosure provides a practical balance between transparency and protecting users.

## Key Points

- Researchers should normally report vulnerabilities privately to the vendor first.
- Vendors should investigate reports and communicate with the researcher.
- Vendors need enough time to develop and test a security fix.
- The disclosure period should depend on the seriousness and complexity of the vulnerability.
- Vendors should not delay disclosure indefinitely.
- Researchers should avoid releasing unnecessary exploit details before users have had a reasonable opportunity to patch.
- Bug bounty programs can provide an organised reporting channel.
- The main objective should be reducing risk to affected users.

## Sources

- OWASP Vulnerability Disclosure Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Vulnerability_Disclosure_Cheat_Sheet.html
- Microsoft Coordinated Vulnerability Disclosure: https://www.microsoft.com/en-us/msrc/cvd
- Carnegie Mellon Software Engineering Institute – Vulnerability Disclosure: https://resources.sei.cmu.edu/library/asset-view.cfm?assetid=503330
- Broadcom Vulnerability Management: https://www.broadcom.com/support/security-center/vulnerability-management
- MITRE CVE Researcher Reservation Guidelines: https://cve.mitre.org/cve/researcher_reservation_guidelines

---

# Final Week 09 Summary

This week's activities covered the relationship between network assets, security protections, threat sources and software vulnerabilities.

In **Task 2**, I identified important assets in our project network and considered confidentiality, integrity and availability for each asset.

In **Task 3**, I identified possible threat sources and their motivations, including unauthorised users, compromised systems, malicious insiders and external attackers.

In **Task 4**, I investigated three recent Chrome CVEs and selected one Critical, one High and one Medium CVSS v3.1 vulnerability. I compared their CVSS scores, CIA impacts, CWE classifications, affected products and mitigation approaches.

In **Task 5**, I considered vulnerability disclosure and concluded that coordinated disclosure provides a practical way to balance transparency, vendor remediation and user safety.

Overall, the activities helped me understand that cybersecurity is not only about identifying vulnerabilities. It also involves protecting important assets, understanding who might attack them, why they might attack, and how vulnerabilities should be handled responsibly.
