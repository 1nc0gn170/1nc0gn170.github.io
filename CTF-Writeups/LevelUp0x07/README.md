# LevelUp0x07

## Port Knocking

### Description
```
Dear agent_521bcd5,

As ordered by Matriarch, I have created a backdoor console that will allow us to launch WannaSpy when time is right.

We're not worried about anyone getting in since they have to go through many doors to actually get in.

Once you are ready, you will find that the console lives on 3389.


Regards
agent_1337

```



```
Port knocking is a method of externally opening ports on a firewall by generating a connection attempt
on a set of  prespecified closed ports.Once a correct sequence of connection attempts is received, the
firewall rules are dynamically modified to allow the host which sent the connection attempts to connect
over specific port.
```

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
