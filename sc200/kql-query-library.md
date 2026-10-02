## KQL Practice Queries

**1.	From SecurityEvent, return all events from the IP Address 10.10.10.5 over the past 24 hours.**

SecurityEvent | where IpAddress == 10.10.10.5 and TimeGenerated >= ago(24h)

**2.	From Syslog, return all events from the past hour where ProcessName is “sshd-session”. Sort by oldest first.**

Syslog | where TimeGenerated >= ago(1h) and ProcessName == "sshd-session" | sort by TimeGenerated asc

**3.	From SecurityEvent, return distinct destination IP addresses contacted in the past 24 hours by 10.10.10.5. Sort by newest first.**

SecurityEvent | where SourceIP == 10.10.10.5 and TimeGenerated >= ago(1d) | distinct DestinationIP | sort by TimeGenerated desc

**4.	From Syslog, summarize events originating from 10.10.10.5 over the past 24 hours across 1-hour intervals. Project TimeGenerated and the number of events.**

Syslog | where IpAddress == 10.10.10.5 and TimeGenerated >= ago (1d) | summarize Events = count() by bin(TimeGenerated, 1h) | project TimeGenerated, Events

**5.	From Alerts, get every event over the past hour with a severity of 2 or higher. Sort by severity, descending.**

Alerts | where TimeGenerated >= ago(1h) and Severity >= 2 | sort by Severity desc

**6.	From Alerts, get the top 5 IP addresses over the past hour with the greatest number of associated alerts.**

Alerts | where TimeGenerated >= ago(1h) | summarize Events = count() by IpAddress | top 5 by Events | project IpAddress

**7.	From Case1, return alerts where the source ports are one of: 20, 21, 22, 23, 36. Project Source Port, Source IP, Time Generated.**

let ports = dynamic([20, 21, 22, 23, 36]);
Case1 | where SourcePort in ports | project SourcePort, SourceIP, TimeGenerated

**8.	From Case2, return alerts where the rule violated mentions “TCP” or “UDP”. Project severity, rule name, Source IP, Time Generated.**

let protocols = dynamic([“tcp”, “udp”]);
Case2 | where RuleName has_any (protocols) | project Severity, RuleName, SourceIP, TimeGenerated

**9.	From SecurityEvent, return successful logins from the past hour where the device name equals “Kali”, treating case loosely. Sort by time generated.**

SecurityEvent | where EventID == 4624 and DeviceName ~= “kali” and TimeGenerated >= ago(1h) | sort by TimeGenerated

**10.	From Syslog, return the average severity of events per IP address over the past 24 hours as AverageSeverity. Sort by AverageSeverity descending.**

Syslog | where TimeGenerated >= ago(24h) | summarize AverageSeverity=avg(Severity) by IpAddress | sort by AverageSeverity desc

**11.	From Alerts, return the most recent occurrences of a specific alert based on rule name.**

Alerts | summarize arg_max(TimeGenerated) by RuleName

**12.	From Vulnerabilities, return the “Priority” of a vulnerability based on severity times exploitability. Project Name, Severity, Exploitability and Priority. Sort by priority descending.**

Vulnerabilities | project Name, Severity, Exploitability | extend Priority == Severity * Exploitability | sort by Priority desc

**13.	From Alerts, summarize the number of alerts over every five-minute interval for the past two hours.**

Alerts | where TimeGenerated >= ago(2h) | summarize EventCount = count() by bin(TimeGenerated, 5m)

**14.	From Case1, return every destination IP address with at least 5 associated alerts over the past hour. Order by alert count, descending.**

Case1 | where TimeGenerated >= ago(1h) | summarize IPAlerts = count() by DestinationIP | where IPAlerts >= 5 | sort by IPAlerts desc

**15.	Return the alerts from Case1 or Case2 with a source IP address of 10.10.10.5. Include the source. Sort by time generated, descending.**

Union withsource = SourceCase kind=inner (Case1 | where SourceIP == 10.10.10.5 | extend SourceCase = “Case 1”), (Case2 | where SourceIP == 10.10.10.5 | extend SourceCase = “Case 2”) | sort by TimeGenerated desc

**16.	From Alerts, return the most recent case of every alert by rule name.**

Alerts | summarize arg_max(TimeGenerated) by RuleName

**17.	From Alerts, return every alert from the IP 10.10.10.5 between September 21 and 25, 2026.**

Alerts | where TimeGenerated between (datetime(2026-09-21) .. datetime(2026-09-25))

**18.	In SecurityEvent, return possible candidates for brute-force in the past 24 hours by finding accounts with more than 3 failed login attempts. Sort by failed login attempts, descending.**

SecurityEvent | where TimeGenerated >= ago(24h) and EventID == 4625 | summarize Failures = count(), by Account, IpAddress | where Failures >= 3 | sort by Failures desc

**19.	From Case1, group alerts in the past 24 hours by rule name and return by alert count, descending.**

Case1 | where TimeGenerated >= ago(24h) | summarize AlertCount = count() by RuleName | sort by AlertCount desc

**20.	From Alerts, return the maximum severity of an event for every day for the past seven days. Project RuleName, Source IP, and Destination IP. Sort by time generated, descending.**

Alerts | where TimeGenerated >= ago(7d) | summarize MaxSeverity = max(Severity) by bin(TimeGenerated, 1d) | extend RuleName, SourceIP, DestinationIP | sort by TimeGenerated desc
