# 🛡️ Security Assessments: Overview
## 🔍 Vulnerability Assessment
- **Goal:** Identify as many vulnerabilities as possible across systems.
- **Scope:** Each host is assessed **individually**.
- **Approach:**
  - Use of **automated tools** (e.g., Nessus, OpenVAS).
  - Minimal technical expertise required.
  - Systems may be **allowlisted** to avoid interference.
- **No exploitation is performed.**
- **Outcome:** A prioritized list of vulnerabilities for remediation.
## 🧪 Penetration Testing
- **Goal:** Go beyond identification to **demonstrate impact**.
- **Includes:**
  - Exploiting discovered vulnerabilities.
  - Post-exploitation tasks (e.g., data extraction, pivoting).
- **Focus:** Understand how vulnerabilities can be **chained** and affect the **entire network**.
- **Benefits:**
  - Tests compensatory controls.
  - Reveals possible lateral movement.
  - Provides insights on detection and security measure effectiveness.
## 🚨 Limitations of Penetration Testing
- **Too Loud:** Pentesters usually don’t care about being stealthy.
- **Time-Boxed:** Limited time = possible security relaxations.
- **Missing Vectors:**
  - Social engineering.
  - Physical attacks.
  - Zero-day exploits may not be covered.
## 👤 Advanced Persistent Threats (APT)
- **Definition:** Long-term, stealthy, and skilled attackers (often nation-state or criminal groups).
- **Target:** Critical infrastructure, finance, government.
- **Tactics:** Blend technical + non-technical vectors (e.g., phishing, zero-days).
- **Persistence:** Can remain undetected for **months**.
- **Challenge:** Traditional pentests may not detect or prepare for such threats.
## 🟥 Red Team Engagements
- **Purpose:** Simulate **real-world attacker behavior**.
- **Difference from Pentesting:**
  - Focus on **stealth**, **persistence**, and **realistic threat modeling**.
  - Test **people, process, and technology**.
- **Includes:**
  - Phishing
  - Physical intrusion
  - Evasion of detection
## ✅ Summary Table
| Assessment Type       | Exploitation | Scope             | Realism | Stealth | Time-Conscious |
|-----------------------|--------------|-------------------|---------|---------|----------------|
| Vulnerability Scan    | ❌ No         | Per-host          | Low     | N/A     | ✅ Yes         |
| Penetration Test      | ✅ Yes        | Network-wide      | Medium  | ❌ No    | ✅ Yes         |
| Red Team Engagement   | ✅ Yes        | Realistic Scenario| High    | ✅ Yes  | ❌ No          |
## 🔴 Red Team Engagements: Advanced Threat Simulations
- **Purpose:** Test the blue team’s detection and response capabilities by simulating real-world threat actors.
- **Not a replacement** for pentests—focus is on **detection/response**, not just prevention.
- **Origin:** Military term; red team simulates attackers, blue team defends.

## 🎯 Goals and Approach
- **Defined Objectives:** Known as *crown jewels* (e.g., data theft, critical host compromise).
- **Blue team is unaware** of the test to ensure realistic behavior.
- **Minimal interaction** with the network to avoid detection.
- **Avoids mass scanning**; focuses on stealth paths to goals.

## 🧠 Key Focus Areas
- **Realistic TTPs:** Mimics attacker tactics, techniques, and procedures.
- **Stealth:** Evade security mechanisms (AV, EDR, IPS, firewalls).
- **No full-network scans**—only target paths to the goal.

## 🆚 Red vs Blue
- **Goal:** Not to "win" but to improve the blue team's ability to detect/respond.
- **Outcome:** Adjust or enhance security controls based on red team actions.

## 🧩 Attack Surfaces Considered
- **Technical Infrastructure:** Like in pentesting, but with stealth.
- **Social Engineering:** Phishing, phone calls, social media manipulation.
- **Physical Intrusion:** Lockpicking, RFID cloning, bypassing access control.

## 🛠️ Engagement Types
- **Full Engagement:** End-to-end attack simulation from external to internal compromise.
- **Assumed Breach:** Red team starts with pre-gained access (e.g., credentials, workstation).
- **Table-top Exercise:** Scenario-based discussions to evaluate blue team response (no live attacks).

## ✅ Summary Table
| Red Team Element       | Description                                                       |
|------------------------|-------------------------------------------------------------------|
| Goal                   | Simulate real threats to test detection and response              |
| Approach               | Stealthy, goal-oriented, TTP-based                                |
| Blue Team Aware?       | ❌ Usually not                                                    |
| Attack Surfaces        | Technical, Social, Physical                                       |
| Tools Used             | Phishing kits, custom malware, RFID tools, physical intrusion gear|
| Key Outcome            | Identify gaps in detection and incident response                  |

## 👥 Red Team Engagement Structure

### 🔄 Core Engagement Cells
| Team       | Definition |
|------------|------------|
| **Red Cell**  | Offensive unit simulating attacker behavior and tactics against a target. |
| **Blue Cell** | Defensive unit including internal staff, defenders, and management working to detect/respond. |
| **White Cell**| Neutral observers and coordinators. Enforce Rules of Engagement (ROE), control environment, correlate actions, and ensure fair play. |

> Source: *redteam.guide*

---

### 🔴 Red Cell Role Hierarchy

| Role                  | Responsibilities                                                                              |
| --------------------- | --------------------------------------------------------------------------------------------- |
| **Red Team Lead**     | Plans and manages engagements at a high level. Assigns tasks to assistant lead and operators. |
| **Assistant Lead**    | Supports team lead in managing operations. Helps with documentation and planning.             |
| **Red Team Operator** | Executes technical tasks. Follows engagement plans and performs specific assignments.         |

- Role responsibilities vary by organization; structure shown is a common example.
# 🔴 Red Team & Cyber Kill Chains

## Overview
- **Core Function**: Adversary emulation — simulate real-world attacker behaviors using their tools/methods.
- **Purpose**: Assess how defenders respond to real attacks.
- **Cyber Kill Chains**: Used by red and blue teams to map adversary TTPs (Tactics, Techniques, Procedures).

## 🧰 Common Cyber Kill Chains

| Kill Chain                  | Description                                |
|----------------------------|--------------------------------------------|
| **Lockheed Martin**        | Focuses on perimeter breaches; standardized |
| **Unified Kill Chain**     | Covers both external and internal steps     |
| **Varonis Kill Chain**     | Data-centric perspective                    |
| **AD Attack Cycle**        | Specific to Active Directory environments   |
| **MITRE ATT&CK Framework** | TTP-based matrix of real-world behaviors    |

> 🔸 In this room, we reference **Lockheed Martin Cyber Kill Chain**, commonly used by both red and blue teams.
> 🔹 Limitation: Focuses on **external breach**, not detailed on **internal movement**.

---

## 📌 Lockheed Martin Cyber Kill Chain

| Technique           | Purpose                                              | Examples                              |
|---------------------|------------------------------------------------------|----------------------------------------|
| **Reconnaissance**  | Obtain information on the target                     | OSINT, harvesting emails               |
| **Weaponization**   | Craft exploit + payload                              | Malicious DOCX with backdoor           |
| **Delivery**        | Transmit the weapon to the victim                    | Email, USB, malicious websites         |
| **Exploitation**    | Trigger the exploit on the victim system             | MS17-010, ZeroLogon                    |
| **Installation**    | Install malware/tooling on target                    | Mimikatz, Rubeus                       |
| **Command & Control** | Establish remote control over compromised systems | Empire, Cobalt Strike                  |
| **Actions on Objectives** | Achieve final goal (e.g., exfiltration, impact) | Ransomware (Conti, LockBit2.0), etc.  |
