Boot / Install Kali

If on virtualbox, you will need a USB wifi stick. Once added, click the usb icon in the bottom right and add the device to your guest OS
![](http://teachthe.net/topclipbox/2016-05-03_22-29-253QLRLY.png)

NOTE - Your network should be in Bridged Adapter mode.

Running this command in terminal will allow you to spoof an email
```
sendEmail -u "email subject line" -t to@email.com -f from@email.com -s smtp.sendgrid.net:587 -xu MYUSERNAME -xp MYPASSWORD -m "Hey, this is my email message..."
```

Note that you need an SMTP server. If you create a Heroku instance and install the free version of the sendgrid add-on, then look at your environmental variables, you'll see the username and password of a free smtp server you can use.