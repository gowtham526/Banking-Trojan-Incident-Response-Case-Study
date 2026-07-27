# Attack Timeline

## Overview

The following timeline reconstructs the Banking Trojan infection based on the analysis of the PCAP file. The timeline was created by examining HTTP requests, DNS queries, and network communications captured in Wireshark.

---

## Attack Sequence

| Stage | Activity | Evidence |
|--------|----------|----------|
| 1 | Victim accessed the phishing URL hosted on `www.ica.ufmg.br`. | `04_initial_get.png` |
| 2 | The server responded with an HTTP **302 Found** redirect. | `05_demojoomla_redirect.png` |
| 3 | The victim was redirected to `downloadpdf.demojoomla.com`. | `06_demojoomla_dns.png` |
| 4 | The malware archive **Download.rar** was downloaded. | `01_download_rar.png` |
| 5 | The archive contained additional malware components such as `Download.vbe`, `Gravar.zip`, and `dmw.exe`. | Wireshark HTTP Stream |
| 6 | The malware collected host information including computer name, operating system, browser, and antivirus details. | `08_post_requests.png` |
| 7 | The infected system communicated with `australiano2015.com.br` using HTTP POST requests. | `07_australiano_dns.png` |
| 8 | The downloaded malware sample was validated using VirusTotal. | `02_download_rar_hash.png` |

---

## Summary

The investigation confirmed that the infection followed a typical multi-stage malware delivery process:

1. Initial access through a phishing link.
2. HTTP redirect to an attacker-controlled server.
3. Malware download.
4. Host profiling.
5. Command-and-control communication.

This sequence was reconstructed using network traffic analysis and supporting threat intelligence.
