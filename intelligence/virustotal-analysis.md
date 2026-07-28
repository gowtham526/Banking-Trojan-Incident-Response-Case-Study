# VirusTotal Analysis

## Objective

VirusTotal was used to validate the reputation of malware artifacts extracted during the investigation.

---

## Files Analyzed

### Download.rar

**SHA-256:** `1c9b68f1ee6b842a3c7b01a7b41e74e6f22b1ee6925e6cfb067401ac573813be`

**Result**

- **34 / 61** security vendors flagged this file as malicious.
- Popular threat label: `trojan.dwnldr/psyme`
- Threat categories: trojan, downloader, banker
- Family labels: dwnldr, psyme, adodb

Evidence:

- `evidence/virustotal/01_download_rar.png`
- `evidence/virustotal/02_download_rar_hash.png`

---

## Domains

### australiano2015.com.br

Observed during HTTP POST communication.

VirusTotal showed no current malicious detections.

---

## IP Address

### 67.212.169.218

VirusTotal reported no current detections.

This does not prove that the communication was benign.

Infrastructure frequently changes ownership, becomes inactive, or loses historical reputation.

---

## Investigation Insight

This investigation reinforces an important SOC principle:

A file may remain malicious long after the infrastructure used to deliver it has disappeared or been repurposed. In this case, the file itself was confirmed malicious by 34 of 61 vendors, while the delivery and C2 infrastructure showed no current detections — a reminder that file reputation and infrastructure reputation can diverge significantly.

For this reason, analysts should evaluate:

- Packet captures
- Malware behavior
- HTTP requests
- DNS activity
- Threat intelligence

instead of relying only on reputation scores.
