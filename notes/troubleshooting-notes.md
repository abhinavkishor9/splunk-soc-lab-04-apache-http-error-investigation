# Troubleshooting Notes

## Overview

This document records troubleshooting performed during the Apache HTTP Error Investigation.

---

# Issue 1

## Problem

No results returned for:

```spl
index=main status=404
```

## Cause

The dataset may not contain 404 errors.

## Resolution

Verify available status codes:

```spl
index=main
| stats count by status
```

---

# Issue 2

## Problem

No results returned for:

```spl
index=main status=500
```

## Cause

The dataset may not contain server-side errors.

## Resolution

Document the finding as a valid investigative outcome.

---

# Issue 3

## Problem

No results returned for:

```spl
index=main
| stats count by clientip
```

## Cause

Field extraction issues.

## Resolution

Verify available fields using:

```spl
index=main
| fieldsummary
```

---

# Issue 4

## Problem

Unexpected field names.

## Cause

Apache field extraction differences.

## Resolution

Review Interesting Fields and adjust SPL queries accordingly.

---

# Verification Queries

## Verify Events

```spl
index=main
| stats count
```

## Verify Sources

```spl
index=main
| stats count by source
```

## Verify Sourcetypes

```spl
index=main
| stats count by sourcetype
```

## Review Sample Events

```spl
index=main
| head 20
```

---

# Lessons Learned

- Not all datasets contain 404 or 500 errors.
- Missing results are valid investigative findings.
- Field validation should occur before writing SPL queries.
- HTTP status codes provide valuable visibility into web application health and activity.
- Verification should be performed before beginning an investigation.
