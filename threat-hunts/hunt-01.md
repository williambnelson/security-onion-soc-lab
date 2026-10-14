## Hunt 1: Unusual DNS Behavior

**Hypothesis:** A malicious actor may be performing reconnaissance to find an entry point into the network.

**Data:** 2026-10-01 PCAP downloaded from malware-traffic-analysis.net.

**Query:** dataset: “zeek.dns”

**Result:** The communications are all over port 5353, which is reserved for Multicast Domain Name System (mDNS). This service lets devices query DNS services without needing a central DNS server. This occurs via queries to 224.0.0.251 for IPv4 or ff02::fb for IPv6. Looking at the results, all the communications involve one of those two IP addresses. The IPv4 communications all originate from 192.168.56.1, while the IPv6 communications originate from fe80::800:27ff:fe00:0.

**Conclusion:** Both source IP addresses are internal IP addresses, meaning the devices involved likely originate from inside the network. This likely indicates my hypothesis is false, as an internal device would not need to find an entry point.

**Next Action:** Continue monitoring the network for suspicious activity. Ensure the involved devices are secure.
