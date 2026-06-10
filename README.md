# 🔍 Splunk Home Lab

![Splunk](https://img.shields.io/badge/Splunk-Core%20User-black?logo=splunk)
![Security+](https://img.shields.io/badge/CompTIA-Security%2B-red)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

A personal cybersecurity home lab focused on log ingestion, threat detection, and SOC analyst workflows using Splunk.

## About

IT professional with a background in Cyber Defence and hands-on experience building detection and monitoring workflows in Splunk.  
Currently pursuing CompTIA Security+ and transitioning into cybersecurity — specifically SOC analysis and cloud security roles.

**Skills:** Splunk SPL · Log Analysis · Threat Detection · Network Fundamentals · Git

## Lab Setup

| Component | Details |
|-----------|---------|
| SIEM | Splunk Enterprise (free license) |
| OS | macOS |
| Hosting | Docker Desktop (local container) |
| Interface | Terminal |

## Projects

### 🔎 Failed Login Detection
Monitored authentication logs to identify brute-force attempts.  
**Tools:** Splunk, Windows Event Logs  
**SPL:** See [`searches/failed_logins.spl`](searches/failed_logins.spl)

---

## 📊 Dashboard: Security Overview

Built a real-time dashboard tracking login attempts, network activity, and alerts.

**Screenshot:* 

Screenshots coming soon

---

## Investigation Methodology — BOTS v1 Web Attack

A structured hunting workflow moving from broad visibility to confirmed compromise.

### Step 1 — Identify noisiest sources

```spl
index=botsv1 sourcetype=iis | stats count by c_ip | sort - count
```

### Step 2 — Profile the suspect IP
```spl
index=botsv1 sourcetype=iis c_ip=40.80.148.42 | stats count by cs_uri_stem | sort - count
```

### Step 3 — Analyze server responses
```spl 
index=botsv1 sourcetype=iis c_ip=40.80.148.42 cs_uri_stem="/joomla/index.php/component/search/" | stats count by sc_status
```

### Step 4 — Confirm admin access
```spl
index=botsv1 sourcetype=iis c_ip=40.80.148.42 cs_uri_stem="/joomla/administrator/index.php" cs_method=POST sc_status=200
```

## Certifications & Goals

- [ ] CompTIA Security+ *(in progress)*
- [ ] Splunk Core Certified User
- [ ] CompTIA CySA+
- [ ] AWS Cloud Practitioner
