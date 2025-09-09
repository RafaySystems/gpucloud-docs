---
title: Product Security - Audit Logs
description: How organization admins can use audit logs to track user activities and maintain compliance.
tags:
  - Audit Logs
  - Security
  - Compliance
  - Monitoring
---

Audit logs provide a chronological record of all activities performed by authorized users in the organization. Administrators can view logs but cannot delete them.

- Navigate to **System → Audit Logs** to access logs.

---

## System Logs

System logs contain the entire history of actions in the organization. Logs are sorted by date/time (latest first).  

![Audit Logs Console](img/audit/audits_overview.png)

---

## Filters

Use canned filters to quickly retrieve required data:  

- Project  
- Action type  
- User  
- Client type (Browser, CLI, KUBECTL)  
- Time range  

![Audit Logs Filtered](img/audit/audit_logs_filter.png)

Logs can also be expanded to view complete JSON payload.  

![Audit Logs Json](img/audit/log_json.png)

---

## KUBECTL Logs

Displays history of `kubectl` commands and API calls.  

![Kubectl Logs](img/audit/kubectl_log.png)

Options:  
- **Search** logs  
- **Clear Filters** to reset view  
- **Refresh** for latest logs  
- **Export** logs in CSV  

---

## Export to SIEM

Audit logs (system, kubectl, OPA) can be streamed to a corporate SIEM for centralized monitoring.  See [SIEM Integration](../admins/siem/overview.md) for additional details.
