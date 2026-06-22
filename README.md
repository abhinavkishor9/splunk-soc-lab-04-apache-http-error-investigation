# splunk-soc-lab-04-apache-http-error-investigation

## Overview

This lab demonstrates how to investigate Apache HTTP errors using Splunk Enterprise.

Web server errors can reveal application issues, missing resources, reconnaissance activity, misconfigurations, and potential attack attempts. Security analysts frequently review HTTP status codes to identify abnormal behavior and improve visibility into web applications.

The objective of this lab is to analyze Apache access logs, investigate HTTP error responses, identify trends, and develop practical web log investigation skills.

---

# Lab Environment

- Splunk Enterprise
- Search & Reporting App
- Apache Access Logs
- Windows Host

---

# Scenario

The SOC team has received reports of abnormal web application behavior.

As a SOC Analyst, your task is to review Apache access logs, identify HTTP errors, investigate their causes, analyze traffic patterns, and determine whether suspicious activity exists.

---

# Objectives

- Analyze HTTP status codes
- Investigate 404 errors
- Investigate 500 errors
- Identify top source IPs
- Review frequently accessed URLs
- Analyze error trends
- Develop web log investigation skills

---

# MITRE ATT&CK Mapping

| Technique | Description |
|------------|------------|
| T1595 | Active Scanning |
| T1190 | Exploit Public-Facing Application |
| T1046 | Network Service Discovery |

---

# Severity

**Medium**

HTTP errors may indicate application issues, reconnaissance activity, scanning, or attempted exploitation.

---

# Detection Logic

## HTTP Status Distribution

```spl
index=main
| stats count by status
| sort -count
```

## 404 Error Investigation

```spl
index=main status=404
| stats count by uri
| sort -count
```

## 500 Error Investigation

```spl
index=main status=500
| stats count by uri
| sort -count
```

## Top Source IPs

```spl
index=main
| stats count by clientip
| sort -count
```

## Top Requested URLs

```spl
index=main
| stats count by uri
| sort -count
```

## Error Timeline

```spl
index=main (status=404 OR status=500)
| timechart count by status
```

## HTTP Methods

```spl
index=main
| stats count by method
```

---

# False Positives

- User typing incorrect URLs
- Website redesigns
- Broken links
- Search engine crawlers
- Automated monitoring tools

---

# Recommended Containment

Investigate repeated error requests, review web server configurations, verify missing resources, and monitor suspicious source IP activity.

---

# Skills Demonstrated

- Splunk SPL
- Web Log Analysis
- Threat Hunting
- Apache Log Investigation
- SIEM Operations
- Security Monitoring
- Detection Engineering

---

# Lessons Learned

This lab improves understanding of:

- HTTP response codes
- Web application monitoring
- Error analysis
- Traffic analysis
- Security investigations
- Splunk search techniques
