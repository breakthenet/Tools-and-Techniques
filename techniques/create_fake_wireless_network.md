Boot / Install Kali

If on virtualbox, you will need a USB wifi stick. Once added, click the usb icon in the bottom right and add the device to your guest OS
![](http://teachthe.net/topclipbox/2016-05-03_22-29-253QLRLY.png)

```shell
airmon-ng
```

You should see something like this
![](http://teachthe.net/topclipbox/2016-05-03_22-31-4102HNZ4.png)

From the above, get your Interface name and use it below in place of 'wlan0'

```
airmon-ng start wlan0
```

This should tell us monitor mode is enabled for this interface.

```
airodump-ng wlan0
```

This will show us all wifi points detected by the card, along with their encryption type. It should look like this:

![](http://teachthe.net/topclipbox/2016-05-03_23-47-24LP16AR.png)

Once you see the network you want to fake, hit control+c to kill it.

```
airbase-ng -a 04:1E:64:98:96:AB --essid "MyNetwork" -c 1 wlan0
```

For this command, we need to make a few modifications:

1) "-c 1" is specifying to use channel 1. Replace the "1" with the number from the CH column above for your network.

2) "-a 04:1E:64:98:96:AB" is specifying the unique ID of the actual wifi network you are targeting. Replace the "04:1E:64:98:96:AB" with the value from the BSSID column above for your network.

3) '--essid "MyNetwork"' is specifying the 'human' name of your network as "MyNetwork". Replace that.

4) As always, replace wlan0 with your Interface name.

We now have a clone of that wifi network up and running with the same name, channel, and SSID number. Computers will always connect to the most powerful router with this name automatically, so let's max the power of our fake network:

```
iwconfig wlan0 txpower 27
```

(Note, if you go higher than 27 you might damage your card)

