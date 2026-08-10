DNS is a way to translate the human readable address (www.xyz.com) to Machine understandable IP address (129.23.4.5)
#### DNS Resolver:
- When browser sends the query to server it'll check for DNS Resolver
- DNS Resolver is basically translate the Human readable address to machine understandable IP address
- ![[Pasted image 20260407222304.png  | 1000]]

- If the DNS server don't have address in the cache, then It'll ask it for authoritative nameserver
- ![[Pasted image 20260407222607.png | 1000]]
---
## There are Three Levels of the Authoritative DNS servers
- ![[Pasted image 20260407222742.png | 700]]

- ![[Pasted image 20260407222117.png | 1000]]

#### 1. Root Nameservers
- Root name servers stores the IP addresses of the TLD (Top Level Domain)
- There are 13 Logical Root Nameservers and for each there is unique IP address is assigned and there are many physical servers behind each IP address.
- Through the Magic of anycast we get routed to the one closet to us
- ![[Pasted image 20260407223039.png | 700]]

#### 2. TLD Nameservers (Top Level Domain):
TLD stores the IP addresses of authoritative nameservers for all the domains under them.

#### 3. Authoritative Nameservers:
AN for the domain provides answer to DNS queries

How does DNS work:
![[Pasted image 20260407223708.png | 1000]]

---
#### TTL (Time To Live): Expiry Time of the Data
- DNS population is slow because there is TTL for each DNS
- There could be the some buggy TTL (Expired data too early or Stays too long that fear of stale data) which might harm the server.
- To overcome this there are mainly Two approach
	1. Reduce the TTL for the record that we want to change to something very short.

---