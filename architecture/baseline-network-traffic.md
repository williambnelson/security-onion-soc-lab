# Day 8: Baseline Network Traffic

## Exercise Type: Known Benign/Baseline Exercise

## Objective

Establish what ordinary network activity looks like in Security Onion before beginning controlled attack exercises.

## Traffic Generated:
- ICMP Ping
- DNS Queries
- HTTP Request
- HTTPS REquest
- Normal Web Browsing

## Collection Method

Normal traffic was generated from the Ubuntu Lab VM and captured to a PCAP. The PCAP was imported into Security Onion for processing by Zeek and Suricata.

## Zeek Findings


### ICMP
There were quite a few ICMP logs listed under zeek.conn. A variety of activities may have generated these, including normal web browsing and ICMP ping requests. The ping request was for 8.8.8.8, which queries Google's public DNS server. The destination IP is located in Chicago, Illinois, which is likely where the nearest Google server is.

### DNS


### HTTP
There was a single zeek.http log, generated when I used curl to connect to http://example.com. The destination IP traces back to Boston, MA, which is likely where one of example.com's networks is located.

### TLS/HTTPS


## Suricata Findings
From the data I gathered, there were no alerts from Suricata. This may be because there is notable overlap between Zeek and Suricata fields, and Zeek simply has priority in the system. Listing Zeek and Suricata would lead to redundant traffic, so the system doesn't do so. Alternately, there may be issues with how Suricata is configured. I will have to investigate further to reach a conclusion.

## Zeek vs. Suricata
I cannot reach a conclusion in regards to Suricata findings, as it generated no alerts.

## Lessons Learned
I learned how web traffic is generated and how a system can produce different types of traffic.
