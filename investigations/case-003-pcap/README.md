# Case 003 — Security Onion PCAP Alert Investigation

**Exercise Type:** Known Synthetic/Validation Exercise

1. **Scenario:** I downloaded a training PCAP online and uploaded it to Security Onion, then analyzed the generated alerts.
2. **Environment:** The environment is a Security Onion machine accessed through an Ubuntu Linux machine.
3. **Investigation Method:** The first thing I did was look at the generated network alerts. I filtered by category to try to find patterns in specific activity, taking note of specific IP addresses associated with different types of alerts. 
4. **Evidence:** I noticed a number of zeek.ldap alerts, which led me to believe the simulated attack was likely to steal user credentials. I also noticed some zeek.kerberos alerts, which I thought could indicate an attempt at a Kerberoasting attack. I noticed some issues listed with certificates, which I thought could indicate a faulty machine used as an entry point to access the network.
5. **Timeline:** Alerts like the indicated one started at 2:07:32 and ended at 2:21:32.
6. **ATT&CK Mapping:** 
7. **Manual Findings:** Upon further investigation, there were many plaintext or HTML files transferred during the network activity; Given the high volume of LDAP alerts, my theory about stealing user credentials was likely correct. However, hunting the Kerberos activity yielded no alerts, indicating it may have simply been normal network activity flagged by the system. Digging into the certificate problems, it appeared the issues were not with a specific machine, but rather with the network itself. 
8. **AI-Assisted Findings:** 
9. **Where AI Was Wrong:** As far as I can tell, the AI made no errors in its judgement.
10. **Final Analyst Judgment:** 
11. **Lessons Learned:** 
