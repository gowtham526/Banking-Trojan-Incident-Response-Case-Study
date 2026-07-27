# Banking Trojan Incident Response Case Study

> A beginner-friendly SOC investigation documenting the analysis of a Banking Trojan infection using Wireshark, VirusTotal, and CyberChef.
![Platform](https://img.shields.io/badge/Platform-Windows%2011-blue)
![Analysis](https://img.shields.io/badge/Analysis-Wireshark-success)
![Threat%20Intel](https://img.shields.io/badge/Threat%20Intel-VirusTotal-red)
![Language](https://img.shields.io/badge/Documentation-Markdown-orange)

## Author

**Katreddy Gowtham Kumar Reddy**

## Dataset Source

The network traffic capture (PCAP) analyzed in this repository was obtained from **Malware-Traffic-Analysis.net** for educational and malware traffic analysis purposes. The investigation presented in this repository is based on the analysis performed using this publicly available dataset.

---

## Executive Summary

This repository documents the investigation of a Banking Trojan infection using a publicly available malware network traffic capture (PCAP). The objective of the investigation was to identify the infected host, reconstruct the attack timeline, extract indicators of compromise (IOCs), and validate the findings using threat intelligence.

The investigation identified a phishing-based malware infection that resulted in the download of malicious files and subsequent communication with a command-and-control (C2) server. Network traffic analysis and threat intelligence were correlated to reconstruct the attack and document the findings.

> **Note:** This repository is intended for educational and portfolio purposes. The analysis was performed in a controlled lab environment using a publicly available malware traffic sample.

---

## Lab Environment

| Component | Details |
|-----------|---------|
| Host Operating System | Windows 11 |
| Analysis Virtual Machine | Kali Linux |
| Network Analysis Tool | Wireshark |
| Threat Intelligence | VirusTotal |
| Hash Verification | CyberChef |
| Capture Format | PCAP |

---

## Tools Used

- Wireshark
- VirusTotal
- CyberChef
- Kali Linux
- Git
- GitHub

---

## Investigation Objectives

- Identify the infected host.
- Reconstruct the attack timeline.
- Identify malicious network communications.
- Extract Indicators of Compromise (IOCs).
- Validate malware artifacts using VirusTotal.
- Document the investigation in a structured format.

---

## Repository Structure

```text
.
├── evidence/
├── investigation/
├── intelligence/
├── diagrams/
├── report/
├── README.md
└── LICENSE
```

---
## Attack Overview

The investigation revealed a multi-stage Banking Trojan infection that began with a phishing link and ended with command-and-control (C2) communication. By analyzing the PCAP file in Wireshark and validating artifacts with VirusTotal, the complete attack sequence was reconstructed.

### Attack Flow

```text
Phishing Email
      │
      ▼
Victim Clicks Malicious Link
      │
      ▼
HTTP GET Request
      │
      ▼
HTTP 302 Redirect
      │
      ▼
Download.rar
      │
      ▼
Download.vbe
      │
      ▼
Gravar.zip
      │
      ▼
dmw.exe
      │
      ▼
Host Profiling
      │
      ▼
Command & Control (C2) Communication
```

---

## Investigation Process

The investigation followed a structured workflow to reconstruct the malware infection.

### 1. Initial Access

The infected system accessed a phishing URL hosted on **www.ica.ufmg.br**. Analysis of the HTTP traffic showed that the victim requested the resource `/rha/images/pdf.php`.

**Evidence**

- `evidence/wireshark/04_initial_get.png`

---

### 2. HTTP Redirect

The web server responded with **HTTP 302 Found**, redirecting the victim to an external domain that hosted the malicious archive.

This redirect was the first indicator that the victim was being sent to an attacker-controlled resource.

### Evidence

![Initial HTTP GET](evidence/wireshark/04_initial_get.png)
---
### Evidence

**HTTP 302 Redirect**

![HTTP Redirect](evidence/wireshark/05_demojoomla_redirect.png)

### 3. Malware Download

The redirected connection downloaded **Download.rar**, which contained additional malware components.

During threat intelligence analysis, the downloaded archive was detected by multiple antivirus vendors on VirusTotal, confirming that the downloaded file was malicious.

### Evidence

**DemoJoomla DNS Resolution**

![DemoJoomla DNS](evidence/wireshark/06_demojoomla_dns.png)

**VirusTotal Detection**

![Download RAR](evidence/virustotal/01_download_rar.png)

![Download RAR Hash](evidence/virustotal/02_download_rar_hash.png)
---

### 4. Host Profiling

After execution, the malware transmitted information about the infected computer to the remote server.

The HTTP POST request contained details such as:

- Computer Name
- Operating System
- Browser Information
- Antivirus Information

This behavior is commonly used by malware operators to identify and profile newly infected systems.

**Evidence**

- `evidence/wireshark/08_post_requests.png`
- `evidence/wireshark/09_http_stream_and_infected_ips.png`

---

### 5. Command and Control (C2)

The malware communicated with the domain **australiano2015.com.br** using HTTP POST requests.

This communication allowed the malware to exchange information with the remote server after the infection had been established.

##Evidence##
**Australiano DNS**

![Australiano DNS](evidence/wireshark/07_australiano_dns.png)

**POST Requests**

![POST Requests](evidence/wireshark/08_post_requests.png)

**HTTP Stream**

![HTTP Stream](evidence/wireshark/09_http_stream_and_infected_ips.png)

---

## Investigation Summary

The network traffic analysis successfully reconstructed the malware infection from the initial phishing link to the final command-and-control communication. Multiple stages of the attack were identified, including the malicious redirect, malware download, host profiling, and outbound HTTP POST requests. Threat intelligence validation confirmed that the downloaded malware archive had been detected by multiple antivirus vendors, supporting the findings from the network investigation.

---
## Additional Documentation

Detailed investigation files are available in the `investigation/` directory:

- `attack-timeline.md`
- `iocs.md`
- `findings.md`
- `lessons-learned.md`

---

## Project Files

| File | Description |
|------|-------------|
| `investigation/attack-timeline.md` | Attack timeline reconstructed from the PCAP |
| `investigation/findings.md` | Detailed investigation findings |
| `investigation/iocs.md` | Indicators of Compromise identified during the investigation |
| `investigation/lessons-learned.md` | Skills and lessons gained from this investigation |

---

## References

- Malware-Traffic-Analysis.net (PCAP Dataset)
- Wireshark Documentation
- VirusTotal
- CyberChef

---

## Disclaimer

This repository is intended for educational and portfolio purposes only. All malware samples, domains, IP addresses, and indicators discussed are part of a publicly available malware traffic dataset used in a controlled analysis environment.
## Personal Reflection

This investigation challenged me to move beyond simply applying Wireshark filters. I learned that effective malware analysis requires understanding how network events relate to each other, validating findings with multiple sources, and documenting evidence in a structured way.

One of the most valuable lessons from this project was that a single indicator is rarely enough to determine whether activity is malicious. Packet behavior, communication patterns, downloaded files, and threat intelligence all need to be correlated before reaching a conclusion.

This project strengthened my understanding of network forensics and gave me practical experience in documenting an incident in a way that resembles a real SOC investigation.

## Key Investigation Insight

During this investigation, the downloaded malware archive (`Download.rar`) was detected by multiple antivirus vendors on VirusTotal. However, the associated IP address and domain did not have current detections.

This demonstrates an important lesson in threat hunting and incident response:

- A clean IP reputation does **not** automatically mean the activity is benign.
- Infrastructure such as IP addresses and domains may change ownership, be cleaned up, or lose their historical reputation over time.
- Malware files may continue to be detected long after the infrastructure is no longer active.
- Analysts should evaluate packet behavior, communication patterns, downloaded files, and supporting threat intelligence together instead of relying on a single reputation score.

This investigation reinforces the importance of evidence-based analysis rather than making decisions based only on reputation services.

## Analyst Approach

The investigation followed an evidence-driven methodology rather than assuming that every external IP address or domain was malicious.

Each stage of the attack was verified by examining:

- DNS activity
- HTTP requests and responses
- HTTP redirects
- Downloaded malware artifacts
- HTTP POST communications
- VirusTotal results
- Host information transmitted by the malware

Correlating multiple sources of evidence helped reconstruct the complete attack chain and reduced the risk of drawing conclusions from a single indicator.

## Skills Demonstrated

- Network Traffic Analysis
- Malware Traffic Investigation
- Wireshark Analysis
- HTTP Protocol Analysis
- DNS Analysis
- IOC Extraction
- Threat Intelligence Correlation
- Attack Timeline Reconstruction
- Technical Documentation

## Investigation Workflow

1. Opened the PCAP file in Wireshark.
2. Identified the infected host.
3. Examined DNS activity.
4. Investigated HTTP requests and responses.
5. Followed the malware delivery chain.
6. Identified command-and-control communication.
7. Extracted Indicators of Compromise (IOCs).
8. Validated malware artifacts using VirusTotal.
9. Documented findings and reconstructed the attack timeline.

## Final Thoughts

This project represents my effort to investigate a real malware traffic capture using publicly available datasets and industry-standard tools. My goal was not only to identify malicious activity but also to document the investigation in a clear, structured, and evidence-based manner.

As I continue learning SOC operations, threat hunting, and digital forensics, I plan to expand future investigations with additional detection engineering techniques and deeper analysis.

## Attack Flow

```mermaid
flowchart TD
A[Phishing Email] --> B[Victim Clicks Malicious Link]
B --> C[HTTP GET Request]
C --> D[HTTP 302 Redirect]
D --> E[Download.rar]
E --> F[Download.vbe]
F --> G[Gravar.zip]
G --> H[dmw.exe Executed]
H --> I[Host Profiling]
I --> J[HTTP POST Communication]
J --> K[Command & Control Server]
```

> **Analyst Note:** Reputation services such as VirusTotal should support an investigation, not replace it. During this analysis, the downloaded malware sample was detected as malicious, while the related IP address had no current detections. This highlights the importance of analyzing packet behavior, HTTP requests, DNS activity, and the complete attack chain instead of relying solely on reputation scores.
