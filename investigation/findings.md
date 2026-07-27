# Investigation Findings

## Overview

This document summarizes the key findings from the investigation of a Banking Trojan infection using a publicly available malware traffic capture.

---

## Finding 1 – Initial Access

The investigation identified that the victim system accessed a phishing URL hosted on the domain:

```
www.ica.ufmg.br
```

The requested resource was:

```
/rha/images/pdf.php
```

The captured HTTP request indicates the beginning of the infection chain.

Evidence:

- 04_initial_get.png

---

## Finding 2 – HTTP Redirect

The phishing page responded with an **HTTP 302 Found** response.

Instead of serving normal content, the victim was redirected to another server hosting the malware.

This redirect initiated the malware download stage.

Evidence:

- 05_demojoomla_redirect.png

---

## Finding 3 – Malware Download

The victim downloaded the archive:

```
Download.rar
```

Further investigation showed that the archive contained additional malware components including:

- Download.vbe
- Gravar.zip
- dmw.exe

VirusTotal detected the downloaded archive as malicious.

Evidence:

- 06_demojoomla_dns.png
- 01_download_rar.png
- 02_download_rar_hash.png

---

## Finding 4 – Host Profiling

The malware transmitted information about the infected system using HTTP POST requests.

Information observed included:

- Computer Name
- Windows Version
- Browser Information
- Antivirus Information

This indicates that the malware attempted to profile the infected system before continuing communication.

Evidence:

- 08_post_requests.png
- 09_http_stream_and_infected_ips.png

---

## Finding 5 – Command and Control Communication

The infected host communicated with:

```
australiano2015.com.br
```

using HTTP POST requests.

This communication represents the Command-and-Control (C2) stage of the attack.

Evidence:

- 07_australiano_dns.png
- 08_post_requests.png

---

## Overall Assessment

The investigation successfully reconstructed the complete malware infection process from the initial phishing request through malware download and C2 communication using only network traffic analysis and supporting threat intelligence.
