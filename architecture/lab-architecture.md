<img width="840" height="602" alt="image" src="https://drive.google.com/file/d/1Sqa0HRRUNUefqIMh7ilg6PjbfNj-VXPL/view?usp=sharing" />

## Network Design


The Lenovo system hosts a series of virtual machines via Oracle VirtualBox. These VMs are split across two isolated networks. The management network involves a Security Onion VM for monitoring, an Ubuntu Linux VM for managing Security Onion, and a Kali Linux VM for penetration testing. The monitored lab network connects to the Security Onion and Kali machines, as well as intentionally vulnerable VMs used as penetration testing targets. 


The Security Onion machine has two interfaces: A management interface connected to the management network, and a sniffing interface connected to the lab network. The Ubuntu machine uses the internet to connect to the management interface. Meanwhile, traffic from the lab network passes through the sniffing interface for Security Onion to observe.


Separating the management and lab networks lets Security Onion observe controlled traffic in an isolated environment. In addition, this approach reduces exposure of intentionally vulnerable systems, allowing management systems to connect to the internet without putting the network at risk.
