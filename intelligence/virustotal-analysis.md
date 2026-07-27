# VirusTotal Analysis

## Objective

VirusTotal was used to validate the reputation of malware artifacts extracted during the investigation.

---

## Files Analyzed

### Download.rar

**Result**

- Detected by multiple antivirus vendors.
- Classified as malicious.

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

A file may remain malicious long after the infrastructure used to deliver it has disappeared or been repurposed.

For this reason, analysts should evaluate:

- Packet captures
- Malware behavior
- HTTP requests
- DNS activity
- Threat intelligence

instead of relying only on reputation scores.
