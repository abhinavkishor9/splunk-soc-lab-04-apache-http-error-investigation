# Investigation Notes

## Overview

This document records findings from the Apache HTTP Error Investigation.

---

# Dataset Information

| Field | Value |
|---------|---------|
| Log Source | Apache Access Logs |
| SIEM | Splunk Enterprise |
| Index | main |

---

# Queries Executed

## HTTP Status Distribution

```spl
index=main
| stats count by status
| sort -count
```

## 404 Errors

```spl
index=main status=404
| stats count by uri
| sort -count
```

## 500 Errors

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

---

# Findings

## Total Events

```text
Document Results
```

## Status Code Distribution

```text
Document Results
```

## Top 404 URLs

```text
Document Results
```

## Top 500 URLs

```text
Document Results
```

## Most Active Source IPs

```text
Document Results
```

## Most Requested URLs

```text
Document Results
```

---

# Analyst Assessment

Determine whether activity represents:

- Normal Web Traffic
- Application Errors
- Broken Links
- Reconnaissance Activity
- Suspicious Web Requests

---

# Conclusion

Summarize findings and document recommended next steps.
