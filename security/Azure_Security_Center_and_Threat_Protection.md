---
title: "Azure Security Center and Threat Protection"
author: "Randy Bordeaux"
date: "January 2026"
version: "1.0"
services:
  - Microsoft Defender for Cloud
  - Azure Policy
  - Azure Arc
  - Azure Monitor
  - Log Analytics
  - Microsoft Sentinel
  - Azure Automation
  - Azure Logic Apps
categories:
  - Security
  - Threat Detection
  - Compliance
  - Governance
---

# Azure Security Center and Threat Protection

**Author:** Randy Bordeaux  
**Version:** 1.0  
**Date:** January 2026  
**Azure Services:** Microsoft Defender for Cloud, Azure Policy, Azure Arc, Azure Monitor, Log Analytics, Microsoft Sentinel, Azure Automation, Azure Logic Apps

---

## Executive Summary

This whitepaper delivers a prescriptive approach to **hardening Azure workloads and detecting threats** using Microsoft Defender for Cloud (formerly Azure Security Center), Azure Policy, and Sentinel. It covers **onboarding, governance, continuous assessments, detections, response automation, and multi-cloud/Arc integration** to reduce mean time to detect (MTTD) and mean time to respond (MTTR).

**Key Outcomes:**
- Rapidly onboard subscriptions, Arc servers, and PaaS resources into Defender for Cloud with baseline policies
- Enforce **secure configurations** using policy assignments, recommendations, and just-in-time (JIT) access
- Detect threats with **built-in Defender plans**, analytics rules, and UEBA in Sentinel
- Automate **response and remediation** via Logic Apps, Automation runbooks, and ticketing integrations
- Maintain **governance and reporting** through secure score, regulatory standards, and evidence export

---

## Table of Contents

- [Executive Summary](#executive-summary)
- [Scope and Design Principles](#scope-and-design-principles)
- [Architecture and Onboarding](#architecture-and-onboarding)
- [Security Posture Management](#security-posture-management)
- [Threat Detection and Analytics](#threat-detection-and-analytics)
- [Incident Response and Automation](#incident-response-and-automation)
- [Data Sources and Log Engineering](#data-sources-and-log-engineering)
- [Governance, Reporting, and Evidence](#governance-reporting-and-evidence)
- [Operational Runbook](#operational-runbook)
- [Anti-Patterns and Tradeoffs](#anti-patterns-and-tradeoffs)
- [References and Resources](#references-and-resources)
- [Appendices](#appendices)

---

## Scope and Design Principles

### In Scope
- Defender for Cloud onboarding for Azure subscriptions, Arc-connected servers, and Kubernetes clusters
- Threat detection and response using Defender plans and Sentinel
- Governance via Azure Policy, secure score, and regulatory standards

### Out of Scope
- Sovereign clouds specifics
- On-prem SIEM/SOAR tooling beyond Sentinel connectors

### Principles
| Principle | Implementation |
|-----------|----------------|
| Secure by Default | Baseline initiatives assigned at management group; deny/DeployIfNotExists for critical misconfigurations |
| Least Privilege Operations | SOC RBAC (Reader + Security Reader; Sentinel Responder); JIT VM access |
| Evidence-Centered | Centralize alerts, assessments, and audit logs in Log Analytics/Sentinel; continuous export to storage |
| Automation First | Standard playbooks for containment, ticketing, and notification |
| Multi-Cloud Visibility | Use Arc + Defender CSPM for non-Azure assets |

---

## Architecture and Onboarding

- **Management Group targeting:** Assign the built-in Defender for Cloud initiative (e.g., `ASC Default`) at the tenant root or landing zone MG with parameters for exclusions.
- **Plan enablement:** Enable relevant Defender plans (Servers, SQL, App Service, Storage, Key Vault, Kubernetes, API) via REST, CLI, or portal; ensure per-subscription coverage.
- **Arc onboarding:** Use Azure Arc to connect on-prem and multicloud servers; deploy the Azure Monitor agent and Defender extensions.
- **JIT access:** Enable JIT for VMs and Arc servers to minimize exposed management ports.
- **Vulnerability management:** Enable MDE-based threat and vulnerability management; integrate with Update Management/guest patching.
- **Network protections:** Turn on Adaptive Network Hardening to recommend NSG rules; integrate with firewall/Private Link egress controls.
- **Container posture:** For AKS, enable Defender for Containers, image scanning (ACR tasks), and policy admission controls with Azure Policy.

---

## Security Posture Management

- **Secure Score:** Track posture via secure score; prioritize high-impact recommendations that reduce attack surface (internet exposure, missing MFA, unmanaged endpoints).
- **Initiatives and policies:**
  - Assign the **`[Preview] Configure Microsoft Defender for Cloud`** initiative or custom CSPM baseline.
  - Enforce diagnostics on key resource types (Key Vault, Storage, SQL, App Service) using DeployIfNotExists.
  - Deny public endpoints where feasible; require private endpoints for PaaS data services.
- **Regulatory compliance:** Enable regulatory standards (CIS, NIST, ISO) in Defender for Cloud; map to internal control IDs.
- **Deviation management:** Track suppressed recommendations with justification and expiry; review monthly.
- **Change management:** Use versioned policy artifacts in source control; deploy via pipelines (Bicep/Terraform) with change approvals.

---

## Threat Detection and Analytics

- **Built-in analytics:** Turn on alert rules provided by Defender for each plan (SQL injection, anomalous storage access, suspicious VM process, AKS escape attempts).
- **UEBA and fusion:** Enable Sentinel UEBA and fusion to correlate identity, endpoint, and cloud alerts.
- **Custom detections:** Add KQL-based analytics rules for:
  - Rare or first-time geography sign-ins followed by high-privilege operations
  - Service principal abuse (excessive app role assignments, multi-tenant consent)
  - Suspicious data exfil (large egress from storage or Key Vault access anomaly)
- **Deception signals:** Use honeytokens or decoy storage accounts with logging to detect credential misuse.
- **Alert enrichment:** Normalize alerts with asset tags (criticality, owner, environment) and MITRE ATT&CK mapping.

---

## Incident Response and Automation

- **Playbooks (Logic Apps):**
  - Containment: isolate VM/Arc server via NSG lock-down; disable compromised service principal; revoke SAS tokens.
  - Notification: post to Teams/Slack, create ticket (ServiceNow/Jira), page on-call.
  - Evidence: collect process tree, network connections, and relevant logs; attach to ticket.
- **Automation accounts/runbooks:**
  - Quarantine storage account keys, rotate Key Vault secrets, block IPs in firewall.
  - Auto-close benign alerts after enrichment (e.g., known scanner IP ranges) with audit trail.
- **SOAR workflow:** Define severity-based flows (High: contain + page; Medium: ticket + notify; Low: enrich + close if benign).
- **Testing:** Quarterly tabletop exercises; monthly playbook dry-runs in non-prod.

---

## Data Sources and Log Engineering

- **Core logs:** AzureActivity, Resource, SigninLogs, AuditLogs, Defender alerts, MDE alerts, and relevant PaaS diagnostics.
- **Network telemetry:** NSG flow logs v2 to Log Analytics with traffic analytics; firewall logs for egress control.
- **Data plane auditing:** Storage access logs, Key Vault audit logs, SQL auditing and Threat Detection, App Service HTTP logs.
- **Normalization:** Use DCRs to shape logs; apply KQL functions for enrichment (asset inventory, identity context).
- **Retention and costs:** Tier hot vs. archive; set caps and alerts on ingestion anomalies.

---

## Governance, Reporting, and Evidence

- **Secure score reporting:** Weekly reports by subscription/app team; trends over 90 days.
- **Regulatory dashboards:** Use Defender regulatory compliance blade; export assessments to Log Analytics and storage for audit evidence.
- **Waivers:** Maintain waiver registry with control ID, resource, owner, compensating control, and expiry; review quarterly.
- **CMMI cadence:** Monthly posture review board; action owners and due dates tracked in tickets.
- **Third-party visibility:** Offer scoped access via Azure Lighthouse for MSSP review with least privilege.

---

## Operational Runbook

1) **Daily**: Triage new high/medium alerts; confirm playbook execution succeeded.  
2) **Weekly**: Review new recommendations; remediate top secure score gaps; validate JIT access approvals.  
3) **Monthly**: Validate waiver list; regression-test automation; rotate incident access secrets.  
4) **Quarterly**: Tabletop exercise; gap assessment vs. regulatory standards; update detection content.  
5) **Annually**: Red-team or purple-team engagement; refresh threat models and asset criticality tags.

---

## Anti-Patterns and Tradeoffs

- Treating secure score as vanity without closing the highest-risk recommendations.
- Enabling Defender plans without connecting data sources (no agents/AMA) leading to blind spots.
- Broad SOC permissions; avoid Owner/Contributor—use Security Reader/Sentinel Responder and PIM.
- Alert fatigue from noisy analytics without suppression or tuning.
- Ignoring cost governance for log ingestion and Defender plan charges.

---

## References and Resources

- Microsoft Defender for Cloud documentation
- Azure Policy built-in definitions catalog
- Microsoft Sentinel analytics rules and UEBA guidance
- Azure Arc server onboarding and at-scale deployment
- MDE integration with Defender for Cloud

---

## Appendices

### Appendix A: Onboarding Checklist
- Management group assignments created and parameterized
- Defender plans enabled per subscription/resource type
- Log Analytics workspace and DCRs configured; AMA deployed
- Arc onboarding for non-Azure servers; JIT enabled where applicable
- Sentinel connected to workspace; essential analytics rules enabled

### Appendix B: Sample Sentinel Analytics (KQL)
```kql
SigninLogs
| where ResultType == "0" // success
| summarize count() by UserPrincipalName, bin(TimeGenerated, 1d), Location
| join kind=leftanti (
    SigninLogs
    | where TimeGenerated < ago(30d)
    | summarize by UserPrincipalName, Location
) on UserPrincipalName, Location
| where count_ > 0
| extend Severity = "High", Tactic = "Credential Access"
```

### Appendix C: RBAC and SOC Roles
- **Security Reader:** view posture and alerts; no write actions
- **Security Admin:** manage security policies and dismiss alerts; use PIM with approval
- **Sentinel Responder:** close/incidents and run playbooks; no workspace write access
- **Owner/Contributor:** avoid for SOC; reserve for platform engineering

### Appendix D: Playbook Skeleton (Logic Apps)
```json
{
  "triggers": { "When_a_response_to_an_Azure_Sentinel_alert_is_triggered": {} },
  "actions": {
    "Get_Alert_Details": { "type": "ApiConnection", "inputs": { "subscription": "<subId>", "resourceGroupName": "<rg>", "alertId": "@{triggerBody()?['SystemAlertId']}" } },
    "Post_Teams": { "type": "ApiConnection", "inputs": { "team": "SOC", "channel": "incidents", "message": "@{body('Get_Alert_Details')?['Essentials']?['Severity']} alert" } },
    "Create_Ticket": { "type": "ApiConnection", "inputs": { "system": "ServiceNow", "payload": { "short_description": "@{triggerBody()?['DisplayName']}", "severity": "@{triggerBody()?['Severity']}" } } }
  }
}
```
