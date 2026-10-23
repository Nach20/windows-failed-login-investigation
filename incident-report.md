# Incident Report: Repeated Failed Logons Followed by Success

## Case details

- **Case ID:** LAB-AUTH-001
- **Environment:** Synthetic Windows authentication dataset
- **Severity:** Medium — provisional training assessment
- **Status:** Needs further investigation
- **Analyst:** Your Name
- **Date:** Add the date you performed your review

## Executive summary

A review of the supplied synthetic events identified eight failed logon attempts for the fictional account `labuser` from `203.0.113.25`, followed by a successful logon from the same address. The short sequence is suspicious and may be consistent with password guessing followed by successful authentication.

The available dataset is not sufficient to confirm compromise. The source address is reserved for documentation examples, and no endpoint, network, geographic, or user-confirmation evidence is provided.

## Scope and method

I reviewed `sample-auth-events.csv`, sorted the events chronologically, and compared the Windows-style event IDs:

- **4625:** Failed logon.
- **4624:** Successful logon.

I then assessed repetition, target account, source address, timing, and the transition from failures to success.

## Observed evidence

| Observation | Evidence in sample | Interpretation |
|---|---|---|
| Repeated failures | Eight 4625 events for `labuser` | Could indicate mistyped credentials, an automated process, or password guessing |
| Common source | All listed events use `203.0.113.25` | A single source is associated with the sequence |
| Short time window | Failures occur between 10:00 and 10:04 UTC | Concentrated activity warrants review |
| Success after failures | A 4624 event follows at 10:05 UTC | Raises concern that a credential may have worked, but does not prove compromise |

## Assessment

**Provisional conclusion:** Suspicious authentication pattern; further validation required.

The combination of repeated failures and a subsequent success is a useful detection lead. However, a responsible analyst should not label the event a confirmed brute-force attack based on this dataset alone. The source may represent a legitimate user, a test system, or a misconfigured service. The successful logon type and host context are not included.

## Recommended actions

1. **Validate the activity:** Check approved identity and access records and confirm whether the login is expected.
2. **Expand the timeline:** Search for failures against other accounts and successful logons from the same source.
3. **Review context:** Examine logon type, destination host, workstation name, authentication package, and account privileges where available.
4. **Correlate telemetry:** Review endpoint detection, VPN, firewall, and identity-provider logs for related activity.
5. **Contain if justified:** If evidence indicates an unauthorised login, follow the organisation's incident response procedure. This may include revoking sessions, resetting credentials, and escalating to the incident response team.
6. **Document the outcome:** Record evidence, decisions, timestamps, and the reason for any action taken.

Do not disable accounts or reset passwords solely because of this training example; real-world actions should follow approved procedures and verified evidence.

## Limitations

- All data is synthetic.
- The source IP is from a documentation-only range.
- No logon type, destination hostname, geographic context, endpoint telemetry, or user confirmation is available.
- The dataset cannot establish the actor's identity or intent.

## Lessons learned

- Repeated failed logons are signals to investigate, not proof of malicious activity.
- A success after repeated failures increases concern and deserves contextual review.
- Clear incident reports separate observed facts from hypotheses and state what evidence is still missing.

## Analyst sign-off

**Conclusion:** Suspicious; not confirmed.  
**Next step:** Correlate with additional authentication and endpoint telemetry.
