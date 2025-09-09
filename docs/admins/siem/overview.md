---
title: Aggregate Audit Logs to SIEM - Overview
description: Stream your organization’s audit logs to a SIEM platform for centralized monitoring and analysis.
tags:
  - Audit Logs
  - SIEM
  - Security
  - Monitoring
  - Compliance
---

It is common for security operations teams to want the audit logs forwarded to their SIEM to ensure they can perform forensics and analytics in a standardized manner.

---

## Supported Targets

- Splunk
- Splunk Cloud
- Datadog
- AWS CloudWatch
- SumoLogic

---

## Approach

It is common for users to operate their SIEMs in private security domains i.e. aggregation endpoints are not directly visible and not open on the Internet. To ensure audit logs can still be aggregated in deployments such as this, a Helm Chart is provided to deploy on one of their managed clusters that has line of sight to the SIEM aggregation endpoint.

Once deployed, the "log aggregation" workload will automatically scrape the latest audit logs from your Org's audit logging system to the configured SIEM (self hosted or Cloud). The audit log harvester workload can be operated on a small infrastructure cluster that is available 24/7.


!!!Note
    Only one instance is needed for the entire organization.
