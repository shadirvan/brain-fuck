## CVSS
- It is a security assessment framework that provides a standardized method for rating a severity of vulnerabilities.
- It helps organisations prioritize vulnerabilities and enables consistent communication between different stakeholders.
- CVE are used for tracking vulnerabilities while CVSS is used for assessing and rating their severity.
- Owned and managed by First.org
#### Base Metrics : Exploitability

| Attack Vector (AV)       | Network(N) <br> Adjacent(A) <br> Local (L)<br> Physical (P) |
| ------------------------ | ----------------------------------------------------------- |
| Attack Complexity (AC)   | Low (L)<br> High (H)                                        |
| Privileges Required (PR) | None (N)<br>Low(L)<br>High(H)<br>                           |
| User Interaction (UI)    | None(N)<br> Required(R)                                     |
#### Base Metrics: Impact
| Confidentiality (A) | None (N)<br> Low (L)<br> High(H) |
| ------------------- | -------------------------------- |
| Integrity (I)       | None(N)<br> Low (L)<br> High(H)  |
| Availability (A)    | None (N)<br> Low(L)<br> High (H) |
#### Base Metrics : Scope
| Scope(C) | Unchanged (U)<br> Changed (C) |
| -------- | ----------------------------- |


#### Temporal Metrics

| Metric                    | Values |
|----------------------------|--------|
| Exploit Code Maturity (E) | Not Defined (X)<br>Unproven (U)<br>Proof-of-Concept (P)<br>Functional (F)<br>High (H) |
| Remediation Level (RL)    | Not Defined (X)<br>Official Fix (O)<br>Temporary Fix (T)<br>Workaround (W)<br>Unavailable (U) |
| Report Confidence (RC)    | Not Defined (X)<br>Unknown (U)<br>Reasonable (R)<br>Confirmed (C) |

#### Environmental Metrics: Modified

| Metric  | Values |
|---------|--------|
| Base Metrics | Modified Attack Vector (MAV)<br>Modified Attack Complexity (MAC)<br>Modified Privileges Required (MPR)<br>Modified User Interaction (MUI)<br>Modified Scope (MS)<br>Modified Confidentiality (MC)<br>Modified Integrity (MI)<br>Modified Availability (MA) |
#### Environmental Metrics: Requirements

| Metric                          | Values |
|---------------------------------|--------|
| Confidentiality Requirement (CR) | Not Defined (X)<br>Low (L)<br>Medium (M)<br>High (H) |
| Integrity Requirement (IR)       | Not Defined (X)<br>Low (L)<br>Medium (M)<br>High (H) |
| Availability Requirement (AR)    | Not Defined (X)<br>Low (L)<br>Medium (M)<br>High (H) |

- https://cvss.ramhacks.org is an online tool for decoding cvss vector strings
- For a critical remote exploit the cvss vector would be : `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H`
- https://cvssadvisor.com/ shows how we can increase the severity to get more bounty.
