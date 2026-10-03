# PENETRATION-TESTING-REPORT

## FOOTPRINTING & NETWORK SCANNING

**Week 2 • Cybersecurity / Ethical Hacking Practical**

---

## 📋 Report Details

| Report Field | Details |
| :--- | :--- |
| **Anlayst** | Tajalla Fatima |
| **Practical Focus** | Footprinting & reconnaissance, network discovery |
| **Primary Platforms** | Kali Linux and Windows |
| **Tools Covered** | WHOIS, WhatWeb, Nslookup, Curl, Wafw00f, DNSRecon, Zenmap |
| **Assessment Scope** | Authorized educational lab / controlled environment |
| **Sanitization** | Live IPs, domains, emails and other identifiers replaced with documentation-safe values |
| **Report Status** | Sanitized submission-ready draft |

> 💡 **Authorization & Safety Notice:**  
> All reconnaissance and scanning activities described in this report are presented as authorized educational exercises. The report intentionally uses documentation-only IP ranges and synthetic identifiers so that the final document does not expose live infrastructure details. Prepared for educational and portfolio use.

---

## 1. Executive Summary

This practical exercise covered two complementary cybersecurity activities: passive and low-impact footprinting of a web-domain environment (`W2-PM1`), followed by local network discovery with Zenmap (`W2-PM5`). The work demonstrated how a security professional can move from publicly observable information to a structured view of hosts and services without attempting exploitation.

The uploaded practical evidence showed the use of WHOIS, WhatWeb, Nslookup, Curl, Wafw00f and DNSRecon for reconnaissance, and Zenmap/Nmap for host discovery. This report documents what each tool contributes to the overall security analysis.

### Key Outcomes

| Area | Outcome |
| :--- | :--- |
| **Domain Footprinting** | Collected registration, DNS, web-technology, HTTP-header and WAF observations using 6 Kali tools. |
| **Network Discovery** | Used Zenmap/Nmap to identify an active host and observe exposed TCP services in the lab. |
| **Risk Interpretation** | Converted observations into potential risks without claiming that an observation is automatically a vulnerability. |
| **Data Protection** | Replaced live IPs and identifying values with safe documentation ranges/placeholders. |

---

## 2. Objectives

* Understand the purpose of footprinting before active security testing.
* Practice common Kali Linux reconnaissance commands and interpret their outputs (`W2-PM1`).
* Use Zenmap to discover live hosts and visible services on an authorized lab network (`W2-PM5`).
* Document evidence, security implications and recommendations in a professional report (`W2-PM-FINAL`).
* Produce a sanitized report that does not reproduce live IP addresses or sensitive identifiers.

---

## 3. Scope, Authorization & Methodology

The activities are framed as an authorized educational lab. Testing was strictly limited to systems where permission was secured.

| Phase | Module | Activity | Primary Tools | Evidence Type |
| :--- | :--- | :--- | :--- | :--- |
| **Phase 1** | W2-PM1 | Footprinting / Reconnaissance | WHOIS, WhatWeb, Nslookup, Curl, Wafw00f, DNSRecon | Terminal outputs |
| **Phase 2** | W2-PM5 | Network Discovery | ipconfig, Zenmap/Nmap | Scan output / topology |
| **Phase 3** | W2-PM-FINAL | Risk Interpretation | Manual analysis | Risk register |
| **Phase 4** | W2-PM-FINAL | Recommendations | Manual analysis | Mitigation guidance |

### Sanitization Standard

To reduce the possibility of accidental data exposure, this report does not reproduce live IP addresses, domain identifiers, or registrar values. External example IPs use documentation ranges such as `192.0.2.0/24`. Internal examples are presented as synthetic values.

> ⚠️ **Important:** Sanitized values are placeholders for documentation and do not reflect real-world target systems.

---

## 4. Tools Used

| Tool | Module | Purpose in the Practical |
| :--- | :--- | :--- |
| **Kali Linux** | Platform | Operating environment for reconnaissance commands. |
| **WHOIS** | W2-PM1 | Review publicly available domain-registration information and name servers. |
| **WhatWeb** | W2-PM1 | Fingerprint web technologies and server/application indicators. |
| **Nslookup** | W2-PM1 | Resolve a domain name through DNS. |
| **Curl -I** | W2-PM1 | Inspect HTTP response headers. |
| **Wafw00f** | W2-PM1 | Identify whether a web application firewall is detectable. |
| **DNSRecon** | W2-PM1 | Enumerate DNS record types and related infrastructure information. |
| **Zenmap / Nmap** | W2-PM5 | Discover live hosts and identify visible TCP services in an authorized network. |
| **Windows ipconfig** | W2-PM5 | Identify local host IP configuration and subnet before scanning. |

---

## 5. Module W2-PM1: Footprinting & Reconnaissance

The footprinting phase utilized 6 core Kali Linux tools to combine registration data, DNS information, web fingerprints, HTTP metadata, and WAF detection.

### 5.1 WHOIS

**Objective:** Identify publicly available domain-registration information and authoritative name servers.

```bash
whois example-lab.invalid
```

![WHOIS Terminal Output](whois.png)

* **Sanitized Observation:** Demonstrated that WHOIS exposes registrar details, domain status, and name-server configurations.
* **Security Relevance:** Provides structural and administrative context regarding target domain ownership.

### 5.2 WhatWeb

**Objective:** Fingerprint web technologies exposed by the target web application.

```bash
whatweb example-lab.invalid
```

![WhatWeb Terminal Output](whatweb.png)

* **Sanitized Observation:** Identified web server components, CMS frameworks, download handlers, and JavaScript libraries.
* **Security Relevance:** Technology identification assists in prioritizing software update requirements and defensive patch management.

### 5.3 Nslookup

**Objective:** Perform domain name resolution.

```bash
nslookup example-lab.invalid
```

![Nslookup Terminal Output](nslookup.png)

* **Sanitized Observation:** Resolved the target domain to a documentation-safe IP (`192.0.2.10`).

### 5.4 Curl -I

**Objective:** Inspect HTTP response headers.

```bash
curl -I https://example-lab.invalid
```

![Curl Terminal Output](curl.png)

* **Sanitized Observation:** Returned HTTP status codes, web server headers, caching parameters, and active API endpoints.

### 5.5 Wafw00f

**Objective:** Detect Web Application Firewall (WAF) presence.

```bash
wafw00f example-lab.invalid
```

![Wafw00f Terminal Output](wafw00f.png)

* **Sanitized Observation:** Detected active protection mechanisms (e.g., ModSecurity).

### 5.6 DNSRecon

**Objective:** Enumerate DNS zone details.

```bash
dnsrecon -d example-lab.invalid
```

![DNSRecon Terminal Output](dnsrecon.png)

* **Sanitized Observation:** Successfully enumerated SOA, NS, A, TXT, and SRV records.

---

## 6. Module W2-PM5: Network Scanning with Zenmap

Network discovery was conducted to evaluate reachable assets and listening services within the authorized lab subnet (`192.0.2.0/24`).

### 6.1 Local Network Identification

```cmd
ipconfig
```
Retrieved the host interface parameters prior to scanning.

### 6.2 Zenmap / Nmap Discovery

```bash
nmap -sn 192.0.2.0/24
```

The scan detected 1 active host (`192.0.2.25`) with three open TCP services:

| Sanitized Host | Port | State | Service | Description |
| :--- | :--- | :--- | :--- | :--- |
| 192.0.2.25 | 135/tcp | open | msrpc | Microsoft RPC Endpoint Mapper |
| 192.0.2.25 | 139/tcp | open | netbios-ssn | NetBIOS Session Service |
| 192.0.2.25 | 445/tcp | open | microsoft-ds | SMB File Sharing over IP |

### 6.3 Interpretation

Active ports 135, 139, and 445 indicate standard Windows network endpoints. Their detection highlights areas for administrative configuration review and service exposure auditing.

---

> 🛡️ **Safety Boundary:** No exploitation, password attacks, or unauthorized access attempts were conducted during this exercise.

---

## 7. Module W2-PM-FINAL: Risk Analysis & Impact

| # | Finding | Evidence / Observation | Potential Impact | Risk Level |
| :-: | :--- | :--- | :--- | :--- |
| **1** | Web Technology Information Exposed | WhatWeb identified application and server banners. | May assist adversaries in targeting version-specific vulnerabilities. | Medium |
| **2** | Public DNS Record Exposure | DNSRecon returned comprehensive zone details. | Contributes to broader external infrastructure profiling. | Medium |
| **3** | Multiple Open Network Services | Zenmap identified TCP 135, 139, and 445 on the host. | Unnecessary or unsegmented service exposure increases attack surface. | Medium |
| **4** | Visible HTTP Metadata | Curl response headers revealed server details. | Provides information useful for reconnaissance mapping. | Low |
| **5** | Identifiable WAF Protection | Wafw00f detected WAF defensive layers. | Informs analysis of existing perimeter defenses. | Low |

---

## 8. Recommendations & Mitigations

* **Header Suppression:** Suppress web server version banners and detailed software headers.
* **SMB Hardening:** Restrict ports 135, 139, and 445 to trusted management networks via firewalls.
* **Patch Management:** Maintain current patch levels across CMS engines and network services.
* **Internal Discovery:** Perform periodic Nmap scans to maintain host and service inventory accuracy.
* **DNS Auditing:** Audit published DNS records regularly to remove unneeded entry points.

---

## 9. Evidence Summary

| Evidence Item | Module | Used in Report | Sanitization |
| :--- | :--- | :--- | :--- |
| **WHOIS result** | W2-PM1 | Footprinting / Registration data | Registration identifiers omitted |
| **WhatWeb result** | W2-PM1 | Technology fingerprinting | Live domain/IP omitted |
| **Nslookup result** | W2-PM1 | DNS resolution | Replaced with `192.0.2.10` |
| **Curl -I result** | W2-PM1 | HTTP-header review | Live domain identifiers omitted |
| **Wafw00f result** | W2-PM1 | WAF detection | Target identifier omitted |
| **DNSRecon result** | W2-PM1 | DNS enumeration | Live records/IPs omitted |
| **Zenmap result** | W2-PM5 | Network discovery | Replaced with `192.0.2.0/24` range |

---

## 10. Conclusion

This Week 2 practical successfully fulfilled the requirements for elective module `W2-PM1` (Footprinting with 6 Kali tools) and essential module `W2-PM5` (Zenmap Network Scanning). The findings were documented and evaluated in accordance with `W2-PM-FINAL` reporting standards, reinforcing authorized, non-intrusive reconnaissance procedures.

---

## Appendices

### Appendix A – Command Reference

```bash
# W2-PM1: Footprinting Commands
whois example-lab.invalid
whatweb example-lab.invalid
nslookup example-lab.invalid
curl -I https://example-lab.invalid
wafw00f example-lab.invalid
dnsrecon -d example-lab.invalid

# W2-PM5: Network Scanning Commands
ipconfig
nmap -sn 192.0.2.0/24
```

### Appendix B – Sanitization Note

All target identifiers, domains, and IP addresses have been converted to synthetic documentation values (`example-lab.invalid` and `192.0.2.0/24`).

