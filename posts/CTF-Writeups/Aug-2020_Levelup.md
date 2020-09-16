# LevelUp0x07

## Port Knocking

This is the challenge from LevelUp0x07 ctf conducted by Bugcrowd.So in this ctf we've to find 7 flags, this is the writeup for 5th Flag.
So far with the previous levels knowledge I've have 10 images and this description.

### Description
```
Dear agent_521bcd5,

As ordered by Matriarch, I have created a backdoor console that will allow us to launch WannaSpy when time is right.

We're not worried about anyone getting in since they have to go through many doors to actually get in.

Once you are ready, you will find that the console lives on 3389.


Regards
agent_1337

```
So from the above description there is a backdoor on port 3389.So I fired up nmap for port scan and I found that port was filtered. :(

```bash

inc0gn1t0@inc0gn1t0-VirtualBox:~$ sudo nmap -p 3389 165.227.54.122
Starting Nmap 7.70 ( https://nmap.org ) at 2020-08-18 01:24 IST
Nmap scan report for 165.227.54.122
Host is up (0.00059s latency).

PORT     STATE    SERVICE
3389/tcp filtered ms-wbt-server

Nmap done: 1 IP address (1 host up) scanned in 0.50 seconds

```

I've no clue what to do.Then going through the ctf discord channel I saw some thing like `Port Knocking`.
To be frank,I never heard that before.So with a  quick google search I got this. 


```
Port knocking is a method of externally opening ports on a firewall by generating a connection attempt
on a set of  prespecified closed ports.Once a correct sequence of connection attempts is received, the
firewall rules are dynamically modified to allow the host which sent the connection attempts to connect
over specific port.
```
Yeah now I have a target port,and I need to find the closed ports and thier order.As I said earlier I have 10 more images along with descripton.4 out of those 10 contains numbers on them.
Now I need to knock the ports,So I grabbed a script from online cause my own script didn't work properly xD.   

```python
#!/usr/bin/env python

from socket import *
from itertools import permutations
import time

ip = "165.227.54.122" 

def Knockports(ports):
  for port in ports:
      try:
          print "[*] Knocking on port: ", port
          s2 = socket(AF_INET, SOCK_STREAM)
          s2.settimeout(0.1)           
          s2.connect_ex((ip, port))
          s2.close()
      except Exception, e:
          print "[-] %s" % e

def main():
  s = socket(AF_INET, SOCK_STREAM)
  s.connect((ip, 3389))              
  r = [1337,415,2099,921]  
  s.close()

  print "received: ", r

  for comb in permutations(r):       
      print "\n[*] Trying sequence %s" % str(comb)
      Knockports(comb)

  print "[*] Done"


main()
```

After running this script I found that port is open.Opening it in  browser shows blank page.
Checking the respond headers reveals that it's a python server.
I tried to access the console and Boom!!!.Using console I got the flag $_$.

Thanks for reading
