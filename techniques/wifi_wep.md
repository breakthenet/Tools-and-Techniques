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

![](http://teachthe.net/topclipbox/2016-05-03_22-34-28SOJ6M4.png)

Once you see your network, hit control+c to kill it.

(Note, this guide only shows how to break into your own WEP protected network)

```
airodump-ng -c 6 --bssid E8:DE:27:BD:CA:3C -w ~/ wlan0
```

For this command, we need to make a few modifications:

1) "-c 6" is specifying to use channel 6. Replace the "6" with the number from the CH column above for your network.

2) "--bssid 04:1E:64:98:96:AB" is specifying the unique ID of the actual wifi network you are targeting. Replace the "04:1E:64:98:96:AB" with the value from the BSSID column above for your network.

3) As always, replace wlan0 with your Interface name.

Now once this command is running, it will start listening to traffic on the network, gathering the info it needs to break in. You will observe over time the #Data column grows. Once it hits 20000, you're in a good spot to attempt the attack. It should look like this:

![](http://teachthe.net/topclipbox/2016-05-03_22-57-30BPM31I.png)

While leaving it running, open another terminal and run this command:

```
aircrack-ng -b E8:DE:27:BD:CA:3C ~/01.cap
```
For this command, we need to make a few modifications:

1) Replace "E8:DE:27:BD:CA:3C" with the BSSID from the previous command of the network you are targeting.

2) "~/01.cap" is referring to the file storing the results of the dump from the previous command. In the previous command, we passed in a parameter "-w ~/" saying write the logs to our home directory. Go to your home directory, and find the .cap file located there, and replace the "01.cap" in this command with the name of that file.

If you get a "failed" message. Just hit control+c and wait for more data to be collected, then try again.
