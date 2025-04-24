### 🛑 Incident Response Case Study – P1 Alert: Suspected Internal Credential Leak

**Date:** Saturday (Long Weekend)  
**Severity:** P1  
**Environment:** Internal SOC (Business Hours Monitoring)  
**Role:** On-Call Security Analyst  
**Tooling:** Microsoft Sentinel, ITSM, Audit Logs, Sign-in Logs

---

#### 🔔 Initial Alert

While on-call during a quiet Saturday, I received a high-severity alert from our monitoring system titled:  
**"Leaked credential involving one user."**  

To my surprise, when I opened the ITSM dashboard, I found **19 such alerts**, all associated with internal SOC accounts — an environment we typically monitored only during business hours.

The affected users included **security team members, team leads, our security lead, and even the general manager**, raising the urgency and sensitivity of the situation.

---

#### 🧭 First Response

Though initially alarmed, I quickly shifted into triage mode. I attempted to reach out to our team lead, but upon not receiving a response, I escalated to the **Security Head** to provide an early heads-up and requested standby support if needed.

The Security Head arranged for another team member to assist, but while waiting for their availability, I proceeded with the investigation independently.

---

#### 🔍 Investigation Steps

1. **Catalogued all 19 incident IDs and mapped associated user accounts.**  
2. Annotated each incident title with the affected user’s name for quick reference.  
3. **Reviewed each user’s sign-in and audit logs**, looking for anomalies or unauthorized activity.  
4. Documented all findings in the ITSM notes section with clear observations.  
5. Noted **consistent audit activity across all affected users**, but **no clear signs of malicious access** or credential compromise.

By the time the senior team member joined, we had a reasonably strong suspicion that this might be a **false positive**, but due to the high-profile users involved, we remained cautious.

---

#### 📞 Escalation & Mitigation

We convened a **briefing call** with the **Security Head**, **Senior Security Consultant**, and myself to discuss next steps.

While the Senior Consultant agreed the activity might be benign, I recommended a **precautionary password reset** for all affected users. The Senior Consultant — who had the necessary admin privileges — actioned the resets and created a support ticket advising the service desk team that users might face login issues and may need assistance.

A detailed list of impacted users was provided to the support team.

---

#### 📊 Findings & Conclusion

**Analysis & Observations:**
- Each incident was thoroughly reviewed.
- **No signs of suspicious access or credential abuse** were identified.
- All users showed **consistent audit patterns**, including:
  - `Update StsRefreshTokenValidFrom Timestamp`
  - `Update User` attributes
- These were likely triggered by **MACE Credential Revocation**, an automated enforcement mechanism that invalidates session tokens and forces reauthentication.

**Conclusion:**
This incident was ultimately assessed as a **false positive**, triggered by **automated revocation actions**—not by an actual breach. The reason only these 19 users were affected remains unclear, though **custom Conditional Access policies** may have played a role.

---

#### ✅ Outcome

Despite the unexpected timing and initial panic, the incident was handled with discipline and clear communication. The proactive and transparent approach was well received — both the **security team and general manager expressed appreciation** for how smoothly and decisively the response was executed.

## 🧠 Lessons Learned and things to remember

- **Stay calm under pressure** — panic can cloud judgment and slow down critical thinking.  
- **Take every alert seriously**, especially those involving high-privilege users.  
- **Plan your investigation before diving in** — sketch a mental map of steps and stick to it.  
- **Document everything** — write as you investigate to maintain a clear audit trail.  
- **Escalate early** — don’t wait too long to notify stakeholders, even if it’s just a heads-up.  
- **Teamwork is vital** — know when to request help and use available support.
