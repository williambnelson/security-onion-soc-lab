## Hunt 3: Unusual Service/Protocol Activity

For this exercise, I conducted a manual investigation, then consulted AI on possible alternative pivots.

**Hypothesis:** The activity may be part of an attacker’s methods to exploit network protocols and gain information.

**Data:** 2026-10-01 PCAP downloaded from malware-traffic-analysis.net.

**Query:** “zeek.notice”, “zeek.ldap”, “zeek.http”

**Result:** A number of the zeek.notice alerts contained the message “SSL certificate validation failed with (unable to get local issuer certificate)”. All of those alerts originate from the IP address 10.10.1.128, and they are destined for a number of external IP addresses. The zeek.ldap alerts all had the source IP of 10.10.1.128 and the destination IP of 10.10.1.10, and appear to fall under ordinary LDAP traffic. The zeek.http alerts all originate from 10.10.1.128, are destined for a number of external IP addresses, and seem to involve different Microsoft services.

**Conclusion:** Thus far, I have not found any definitive evidence to prove or disprove my hypothesis. The zeek.notice and zeek.ldap alerts seem to have been triggered by ordinary network activity. The zeek.http alerts are a little suspicious, but they could also be ordinary queries of Microsoft services.

**Next Action:** Investigate the device at 10.10.1.128 to see if it has been compromised or tampered with. Continue monitoring the network for suspicious activity, particularly HTTP activity.

**AI Suggestions:** The AI first suggested starting with zeek.conn logs to find unexpected connections. It then suggested grouping by destination port or network protocol. Finally, it suggested to investigate DNS and TLS activity related to the alerts.

**Analyst Judgement:** Digging a bit deeper into the external connections falling under zeek.conn, I found a couple things I missed during my first hunt. Namely, some connections involved port 5355 (LLMNR) or port 443 (HTTPS). Neither of these indicate unusual or suspicious network traffic. Additionally, I was unable to find definitively suspicious activity upon grouping by destination port or protocol, or by examining DNS or TLS activity. It is possible there were things I overlooked or alternate paths I could have taken, but I could not find anything via my or the AI’s investigative paths.
