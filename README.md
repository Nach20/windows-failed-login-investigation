# Windows Failed Login Investigation

**Portfolio project:** SOC Analyst Level 1  
**Status:** Training project using synthetic data  
**Author:** Naomi Amankwah
**Tools:**  CSV/log review; optional Splunk SPL or Microsoft Sentinel KQL

## 1. Objective

Investigate a simulated sequence of Windows authentication events to assess whether repeated failed logins followed by a successful login may indicate password guessing or another suspicious authentication pattern.

This is a learning exercise. The events and account names are fictional. The IP address `203.0.113.25` belongs to a documentation-only range and is not a real attacker address.

## 2. Scenario

A monitoring alert reports multiple failed logins for the fictional account `labuser`, followed shortly by a successful login from the same source address. The analyst must review the event sequence, assess the evidence, and recommend proportionate next steps.

## 3. Files in this repository

- `sample-auth-events.csv` — synthetic Windows-style authentication events.
- `investigation-queries.txt` — example searches for investigating the event pattern.
- `incident-report.md` — findings, assessment, limitations, and recommendations.

## 4. How to use the data

1. Open `sample-auth-events.csv` in a spreadsheet or text editor.
2. Sort by timestamp and review failed (`4625`) and successful (`4624`) logons.
3. Look for repeated failures against the same account, source, and time window.
4. Compare the findings with the example searches in `investigation-queries.txt`.
5. Read `incident-report.md` and adapt it after doing your own analysis.

## 5. Initial findings

The sample contains eight failed logon events for `labuser` from one source address over a short period, followed by a successful logon from that same address. This pattern is **suspicious and consistent with possible password guessing**, but the sample alone does not prove an attack. The successful logon could be legitimate, and more context is required.

## 6. What I would investigate next

- Confirm whether the source address and login time are expected.
- Check whether the account owner recognises the activity, using an approved process.
- Review adjacent events for other accounts, hosts, logon types, and privilege changes.
- Check endpoint and network telemetry for related activity.
- Escalate according to the organisation's incident response procedure if the activity is unexplained.

## 7. Learning notes

Record what you learned, any query changes you made, and what additional evidence would increase or decrease your confidence. Clearly distinguish observed facts from hypotheses.

## 8. Data handling

This repository contains synthetic data only. Do not upload employer logs, personal information, credentials, real IPs from private investigations, or restricted TryHackMe room answers. Follow the training platform's rules and credit any learning resources you use.

## 9. References

- Microsoft Learn: [Audit logon events](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/audit-logon)
- Microsoft Learn: [4625(F): An account failed to log on](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4625)
- Microsoft Learn: [4624(S): An account was successfully logged on](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4624)

---
*Replace “Your Name” with your preferred professional name before publishing. Update the report after you personally review the sample data.*
