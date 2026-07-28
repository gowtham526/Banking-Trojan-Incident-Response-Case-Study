# Indicators of Compromise (IOCs)

## Domains

| Type | Value |
|------|-------|
| Phishing Website | www.ica.ufmg.br |
| Malware Hosting | downloadpdf.demojoomla.com |
| Command & Control | australiano2015.com.br |

---

## IP Addresses

| IP Address | Description |
|------------|-------------|
| 150.164.130.253 | Phishing redirector (www.ica.ufmg.br) |
| 67.212.169.218 | Malware hosting server |
| 69.49.115.40 | Command-and-Control server |

---

## Downloaded Files

| File |
|------|
| Download.rar |
| Download.vbe |
| Gravar.zip |
| dmw.exe |

---

## File Hashes

| File | SHA-256 | VirusTotal Detection |
|------|---------|----------------------|
| Download.rar | `1c9b68f1ee6b842a3c7b01a7b41e74e6f22b1ee6925e6cfb067401ac573813be` | 34/61 vendors flagged as malicious |

**Threat classification:** Trojan / Downloader / Banker
**Family labels:** dwnldr, psyme, adodb

---

## Notes

During the investigation, the downloaded malware archive was identified as malicious by VirusTotal (34/61 vendors). However, the associated IP addresses and domains did not show current detections. This demonstrates that infrastructure reputation can change over time, while malware samples may continue to be detected. Network evidence should therefore be correlated with file reputation and other indicators instead of relying on a single source.
