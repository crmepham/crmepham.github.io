---
ID: 788
post_title: >
  VPN and VLAN for secure remote
  networking
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/academia/vpn-and-vlan-for-secure-remote-networking/
published: true
post_date: 2016-04-26 10:09:31
---
<strong>Introduction</strong>
This report will discuss the use of VPN technologies for secure communication across the internet. It will critically evaluate various VPN solutions and discuss the relevant security implications when adopting a VPN solution to support business goals. It will also describe the use of VLAN for logical segmentation of a private network for improved security.

<strong>What is a Virtual Private Network</strong>
A VPN is a networking technology based on the Client-Server  model. It enables secure communication over the internet, and is primarily used by those individuals or organisations that are concerned with ensuring their data is transferred securely. Many organisations use VPNs to allow their remote users to connect to their private network and use their internal systems as if they were directly connected to their LAN.
[caption id="attachment_791" align="aligncenter" width="357"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/vpn.gif"><img src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/vpn.gif" alt="VPN" width="357" height="191" class="size-full wp-image-791" /></a> VPN[/caption]

<strong>VPN Protocol</strong>
VPN is considered a superior security technology compared to standard secure data transmission methods, such as Secure Shell (SSH) and Transport Layer Security (TLS), because it uses the Internet Protocol Security (IPSec) suite of tools to authenticate and encrypt data packets at the Network layer of the OSI 7 layer model, in addition to encryption and authentication at the Application layer, lending a high degree of integrity to the data being transmitted.

IPSec supports two encryption modes: Transport and Tunnel. The more secure being Tunnel; which encrypts both the header and the payload of each packet. This is particularly useful for preventing deep packet inspection.

<strong>IPSec alternatives</strong>
OpenVPN is an open source tunnelling technology that uses SSL v3/TLS v1 protocols. It can be configured to run on any port, so can be disguised on port 443, for example. It does however require a third-party application to be installed because it isn’t integrated with any operating system.

Point-to-point (PPTP) was introduced in Windows 95 and as such is very well integrated into the Windows environment today, however, it is known to have many security vulnerabilities, like most ageing encryption-based technologies, and expert’s advice against using it.

<table class="table">
<tr><th></th><th>OpenVPN</th><th>IPSec</th><th>PPTP</th></tr>
<tr><td>OS</td><td>Windows, Mac OS, Linux, iOS, Android</td><td>Windows, Mac OS, iOS, Android</td><td>Windows, Mac OS, Linux, iOS, Android</td></tr>
<tr><td>Encryption</td><td>OpenSSL which supports 3DES, AES, RC5, Blowfish, with 128 or 256 bit keys.</td><td>IPSec protocol RFC 4835. 3DES or AES with maximum of 256 bit keys.</td><td>Microsofts point-to-point encryption protocol (MPPE) with maximum of 128 bit session keys.</td></tr>
<tr><td>Speed loss</td><td>Negligible</td><td>Encapsulates data twice, less efficient and slower than PPTP and OpenVPN.</td><td>Fastest due to less encryption overhead.</td></tr>
<tr><td>Ports</td><td>Any port using UDP or TCP.</td><td>Fixed protocols and ports.</td><td>Uses port 1723.</td></tr>
</table>

<strong>Benefits of using a VPN</strong>
1. A VPN is very useful for confidentiality because it will mask your IP address - making it much harder to be hacked or DDOSed.
2. A VPN will mask your geographic location. Useful for services that place restrictions based on your location, such as Netflix and Youtube.
3. Uses encryption and packet encapsulation via a tunnelling protocol. This will prevent the data being de-cyphered, and will prevent ISP’s throttling your speed depending on the type of data being transmitted.

<strong>Drawbacks of using a VPN</strong>
1. Older routers do not support VPN pass through. So would require a hardware upgrade.
2. Old copper wiring that causes a lot of packet loss may cause the VPN service to reconnect a lot because it suspects a MiTM attack.
3. High latency means it is not a good option for gaming which requires very low latency.

<strong>Security, authentication and anonymity</strong>
The following list includes some of the reasons VPNs improve security.

1.	Two layers of encryption
A VPN will use a tunnelling protocol with a strong encryption algorithm to encrypt data packets at the Network layer. The VPN service will then further encrypt the frames sent between the client and the server. This is where the term “tunnel” comes from. If a MiTM attack somehow managed to penetrate the tunnel encryption, it would then have to de-crypt the application layer encryption.

2.	IP and geo-location masking
Once connected to a VPN server the client is issued a new IP address dynamically. The client can usually choose which server it wishes to connect to, which may reside in many different countries. All HTTP requests are made using this VPN IP address and are routed through the VPN server.

3.	Public key Infrastructure (PKI)
A VPN server will use asymmetric encryption techniques. This requires the server to have a private key, and a public certificate which contains identifiable information and the public key which must be used with the private key to decipher encrypted data.

4.	Client authentication
Before a client can use a VPN service it must first be registered and authenticate itself when it connects to a VPN server. This way a VPN service provider can identify its users. This is useful for a business that only wants its employees connected to its VPN.

<strong>The Virtual Local Area Network</strong>
A virtual local area network is a level 2, logically-configured broadcast domain. VLANs are useful because they allow logical segmentation of existing physical topologies and as such are not constrained by geographic location. VLANs are also inherently more secure than traditional LANs because they further restrict dataflow on the network at a low level.

[caption id="attachment_798" align="aligncenter" width="404"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/vlan.png"><img src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/vlan.png" alt="vlan" width="404" height="219" class="size-full wp-image-798" /></a> vlan[/caption]

<strong>Configuring VLANs on a switch</strong>
The following diagram illustrates how to configure a Cisco switch for VLANs.
[caption id="attachment_800" align="aligncenter" width="564"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/basicSwitchSettings.png"><img src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/basicSwitchSettings.png" alt="Configuring a switch for VLAN" width="564" height="605" class="size-full wp-image-800" /></a> Configuring a switch for VLAN[/caption]

<strong>Configuring a switch and router for inter-VLAN routing</strong>
The following diagram illustrates how to assign a port on switch 3 as a Trunk port.
[caption id="attachment_801" align="aligncenter" width="581"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/switchTrunkVlan.png"><img src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/switchTrunkVlan.png" alt="switchTrunkVlan" width="581" height="762" class="size-full wp-image-801" /></a> Configuring a switch and router for inter-VLAN routing[/caption]

A trunk will also be established on interface f0/5 on S1. This will enable inter-VLAN routing by allowing packets from both switches and all VLANs to reach the router and be routed to the destination VLANs.

[caption id="attachment_802" align="aligncenter" width="523"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/routerTrunk.png"><img src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/04/routerTrunk.png" alt="Configuring a trunk" width="523" height="338" class="size-full wp-image-802" /></a> Configuring a trunk[/caption]

This form of inter-VLAN routing is known as “router on a stick”. This enables multiple VLAN’s to communicate provided the switches are connected to the main switch that has a VLAN trunk cable connected to the router. This trunk also has to permit the VLANs to transmit packets. The trunk interface on the router also has to be configured with the same encapsulation type (in this case 802.1q) and an IP address assigned to the sub interface matching the relevant VLAN.