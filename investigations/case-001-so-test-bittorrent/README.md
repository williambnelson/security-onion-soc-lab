# Case 001 — Security Onion so-test BitTorrent Alert Investigation

### Exercise Type/Objective
This was a known-synthetic/validation exercise. The environment was a Security Onion machine accessed through an Ubuntu Linux machine. I ran the “so-test” command from Security Onion to generate alerts. The one I looked at was titled "ET P2P BitTorrent Peer Sync".

### Evidence/Trigger
I looked a bit into BitTorrent since I didn't fully understand its purpose yet. Based on my research, I concluded it was unusual to detect on a corporate network. I looked into the source and destination IP addresses of the alert. The source was from an internal IP address, and the destination led to Belem, Brazil. I thought this might indicate a communication with someone not related to the company. Alerts like the indicated one started at 10:48:20 and ended at 10:59:02.

### Hypotheses/Analysis
I hypothesized this was an attempt at data exfiltration from an unauthorized third party. To be specific, I thought this attack was a T1048: "Exfiltration through Alternate Protocol"; BitTorrent is not a protocol typically used by servers to communicate. 

Looking into the destination IP address, I learned it came from a legitimate Brazilian digital infrastructure company called V Tal. I theorized the alert may have been a false positive triggered by a corporate partner attempting to access resources. However, I found it strange they would use BitTorrent for such a purpose. I theorized this may have been attempted exfiltration either by a rogue V Tal employee or by a third party using them as a proxy. In addition to the above mapping, this would classify the attack as a T1199: "Trusted Relationship" method. 


After my initial investigation, I asked AI to analyze the alert. The AI found a few things I had overlooked, but there were two that stuck out. First of all, it determined based on packet capture there was little activity from BitTorrent, concluding the attempted exfiltration was unsuccessful. Therefore, it classified the alert as an "emerging threat", rather than an "indicator of compromise". I cannot call this conclusion definite; low traffic volume can characterize an event, but it cannot establish whether exfiltration was attempted or whether such an attempt succeeded. In either case, I would not assign T1048 as a confirmed ATT&CK technique at this time. 

Second, it noted the Brazilian destination IP as normal; BitTorrent servers are located around the world. This would mean the attack may have not even originated from Brazil. In addition, my initial hypothesis about the T1199 ATT&CK method was likely incorrect. In addition, IP ownership by a legitimate company does not demonstrate an existing relationship with the victim or an abuse of said relationship.


It should be noted the AI only had the context of the singular alert. After looking at alerts similar to the selected one, I noticed a number of destination IPs located around the globe. This fell in line with the earlier statement about destination IPs related to BitTorrent. Therefore, I determined all the alerts were likely part of the same attack, meaning this was not an attempt at connection from V Tal.

### Analyst Conclusion
The alert was a true positive for BitTorrent/P2P activity contained in known synthetic Security Onion test traffic. My initial hypothesis was that unexpected BitTorrent activity could indicate unauthorized data transfer or possible exfiltration. However, the available evidence does not prove that exfiltration actually occurred or that a malicious third party was responsible. In a production environment, I would investigate the endpoint process, user activity, transferred data, traffic volume, related connections, and other data before determining intent. 

### Lessons Learned
I learned three things. First, it is important to fully understand whatever activity is detected on the network. Second, it is often necessary to look at other alerts to gain the full context behind an alert's nature. Third, IP geolocation can provide useful investigative context, but it does not by itself establish attacker identity, physical location, or malicious intent.
