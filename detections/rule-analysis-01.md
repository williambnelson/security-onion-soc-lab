## Rule Analysis 01


**Rule:** zeek.conn

**Source:** Zeek

**Logic:** The zeek.conn alert triggers every time it detects TCP, UDP, or ICMP traffic on the network. It records UID, timestamps, source and destination IP addresses, and source and destination ports.

**Expected True Positive:** Since zeek.conn triggers any time it detects TCP, UDP, or ICMP traffic, any detected connection would be a “true positive”. However, in a security context, a true positive would be a connection from an unusual source or for an unusual reason.

**Likely False Positives:** A false positive for zeek.conn would be an ordinary connection flagged by the system. Alternatively, it could involve traffic that did not involve TCP, UDP, or ICMP.
