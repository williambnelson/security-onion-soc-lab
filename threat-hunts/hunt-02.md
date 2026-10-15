## Hunt 2: Scanning/Connection Fan-Out

**Hypothesis:** Someone may be enumerating the devices on the network without permission.

**Data:** 2026-10-01 PCAP downloaded from malware-traffic-analysis.net.

**Query:** “zeek.conn”, “10.10.1.128”

**Result:** All connection events originate from the IP address 10.10.1.128. In terms of connections, the IP addresses involved mostly fall into a pattern: multiple connections to 10.10.1.10, followed by one or two connections to external IP addresses. Almost all connections involve ports within the dynamic range, except for two. Those connections both use port 137 (NetBIOS Name Service). One is destined for 10.10.1.10, while the other is destined for 10.10.1.255.

**Conclusion:** This does seem to be a scan of some kind, but I cannot say whether it is legitimate. The connections to external IP addresses have the same characteristics as normal connections to different websites. My hypothesis has not been proven or disproven.

**Next Action:** Look more into the device at 10.10.1.128 and determine if it is authorized to be on the network.
