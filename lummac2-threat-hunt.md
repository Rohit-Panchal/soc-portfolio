# Client-Initiated Threat Hunting: LummaC2 Malware

## 📅 Date
Ad hoc request received during business hours (weekday)

## 🎯 Summary
A financial sector client requested proactive threat hunting related to **LummaC2**, a rapidly evolving infostealer malware. Although no alerts had been triggered in Microsoft Sentinel, the client expressed concern following media coverage and sector-specific threat advisories.

The security team launched a targeted hunting effort, engaged with the client for context, and implemented new detections for better visibility and protection.

## 🧭 Scope
- Investigate potential exposure to LummaC2 using historical and live telemetry.
- Create new detection mechanisms to future-proof against similar threats.
- Provide the client with assurance and clear communication on findings.

## 🛠️ Investigation Steps

1. **Client Request Acknowledgment**
   - Received request via ITSM and direct communication.
   - Understood the urgency and sensitivity due to client’s industry.

2. **Reviewed LummaC2 Threat Intel**
   - Collected known IOCs from public and private sources:
     - Malicious IPs
     - Suspicious URLs
     - Hashes, domain names
     - C2 infrastructure patterns

3. **Historical Threat Hunting (90 days)**
   - Queried Microsoft Sentinel and Zscaler logs using KQL:
     - Looked for access to LummaC2-related URLs and IPs
     - Checked DNS queries and proxy traffic patterns
   - No matches found in client’s environment.

4. **Endpoint & Identity Activity Review**
   - Checked Microsoft 365 Defender and Defender for Endpoint:
     - DeviceProcessEvents, Sign-in logs, AuditLogs
     - No unusual sign-ins or endpoint behaviors tied to known indicators

5. **Proactive Threat Detection Deployment**
   ✅ Created **two new analytic rules** in Microsoft Sentinel:
   - `Infostealer Threat IP Detection` — monitors traffic to known C2 IPs
   - `Infostealer URL Click Detection` — alerts on user access to malicious URLs

   ✅ Built **watchlists** in Sentinel:
   - Malicious domains associated with LummaC2
   - Known threat IP addresses from active campaigns

6. **Client Communication**
   - Drafted and sent a summary email providing:
     - Assurance based on findings
     - Transparency on new proactive controls
     - Offer to follow up on any questions or concerns

## 🔍 Detection Rules (KQL)

**LummaStealer Domain Match – Zscaler Logs**
```kql
let watchlist = (_GetWatchlist('LummaStealerDomainWatchList') | project SearchKey);
ZScalerWeb_Parser
| where DestinationHostName has_any (watchlist)


