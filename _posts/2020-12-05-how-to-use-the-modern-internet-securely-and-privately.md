---

classes: wide
tags: [web, internet, secure, security, private, privacy, self-hosted, hosting, vpn, tunnel]

---

Having grown up with the internet, and watched as it has matured in the Web 2.0 era, I have developed a keen interest in the tools that can help individuals use the internet securely and privately in a time when it is now widely considered a basic utility that everyone must use for all aspects of their lives. But, as we have seen, many of the web services that have been built on top of the internet have become increasingly centralised. The most popular services are controlled by a few corporations that now have access to the private information of a vast number of people. Yes, the majority of people do not care that they are trading their personal information in exchange for "free" use of web services. But it doesn't have to be this way.

There are good alternatives to alot of the services we use online, and it does not take too much technical knowledge in order to set the majority of them up.

The following is a collection of good alternatives to some of the most common web services out there, as well as techniques to aid in using the internet more responsibly.

## Virtual Private Network (VPN)

When browsing the internet; make sure that you are always connected to a [VPN](https://en.wikipedia.org/wiki/Virtual_private_network). A VPN will allow you to route all of your internet traffic through a server in a completely different geographical location. When connected to a VPN network, you are creating am encrypted tunnel between your device and the VPN server. Now, no one can know your precise geographical location.

Because a VPN provides you with a closed network that is accessible from anywhere, you can deploy services within this network that can only be accessed by you and anyone else that is connected to your VPN.

There are numerous paid-for VPN services available, but we cannot be sure that the data we send via these third party VPN services is always secure and private if it is being controlled by someone else, for profit. 

[OpenVPN](https://openvpn.net/) solves this issue by allowing you to host your own VPN server.

## TL;DR
- Setup your own web-server and install your own [OpenVPN](https://openvpn.net/) server. Always be connected to this VPN when using the internet.
- Setup your own email server using [iRedMail](https://www.iredmail.org/).
- Use [DuckDuckGo](https://duckduckgo.com/) for searching the web. It doesn't "personalise" the search results based on your usage history, and doesn't track your usage.
- Setup your own [Bitwarden](https://bitwarden.com/download/) server for storing all of your passwords, credit cards, and notes. Also install a browser addon for Bitwarden to populate login information easily. Here's the [addon](https://addons.mozilla.org/en-US/firefox/addon/bitwarden-password-manager/) for Firefox.
- Setup your own file server, [harden it](https://is.gd/S2rtf4), and enable [SFTP](https://en.wikipedia.org/wiki/SSH_File_Transfer_Protocol) so that you can easily transfer files to it for backup purposes.
- Use the following browser extensions/addons:

 - [Adblock Plus](https://addons.mozilla.org/en-US/firefox/addon/adblock-plus/)
 - [Cookie Autodelete](https://addons.mozilla.org/en-US/firefox/addon/cookie-autodelete/)
 - [Decentraleyes](https://addons.mozilla.org/en-US/firefox/addon/decentraleyes/)
 - [Firefox Multi-account containers](https://addons.mozilla.org/en-US/firefox/addon/multi-account-containers/)
 - [HTTPS everywhere](https://addons.mozilla.org/en-US/firefox/addon/https-everywhere/)
 - [Privacy badger](https://addons.mozilla.org/en-US/firefox/addon/privacy-badger17/)
 - [uBlock Origin](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/)

