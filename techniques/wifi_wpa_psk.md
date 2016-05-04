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

Once you see your network, hit control+c to kill it.

(Note, this guide only shows how to break into your own WPA-PSK protected network)

```
airodump-ng -c 7 --bssid 00:1F:B3:B3:78:A9 -w ~/wpa-pskNEW wlan0 --output-format cap
```

For this command, we need to make a few modifications:

1) "-c 1" is specifying to use channel 1. Replace the "1" with the number from the CH column above for your network.

2) "--bssid 04:1E:64:98:96:AB" is specifying the unique ID of the actual wifi network you are targeting. Replace the "04:1E:64:98:96:AB" with the value from the BSSID column above for your network.

3) As always, replace wlan0 with your Interface name.

While leaving it running, open another terminal.

In the new terminal:

Unzip this password list if you haven't before:
```
gzip -d /usr/share/wordlists/rockyou.txt.gz
```

Then we're going to work with this command to crack the password
```
aircrack-ng ~/wpa-psk-01.cap -w /usr/share/wordlists/rockyou.txt
```
For this command, we need to make a modification: "~/wpa-psk-01.cap" is referring to the file storing the results of the dump from the previous command. In the previous command, we passed in a parameter "-w ~/wpa-psk" saying write the logs to our home directory. Go to your home directory, and find the .cap file located there, and replace the "wpa-psk-01.cap" in this command with the name of that file.

If you get a "failed" message. Just hit control+c and wait for more data to be collected, then try again.

When you achieve success, you should see something like this!

![](http://teachthe.net/topclipbox/2016-05-03_23-58-481DRT8X.png)
