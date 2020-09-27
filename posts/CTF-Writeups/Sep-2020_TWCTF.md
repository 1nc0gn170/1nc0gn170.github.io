# TokyoWestrens-CTF
## urlcheck-v1
### Source Code:
<script src="https://gist.github.com/n41n4/496691de46d5202aec5585a722763ffa.js?file=urlcheck-v1.py"></script>

### Solution:
So the functionality is so simple.This application will fetch the source code of any ip address that we supply,if it obey the following conditions.
1. Url must satisfy the regular expression - `re.compile('\A(\d+)\.(\d+)\.(\d+)\.(\d+)\Z')`  () => [\<number\>.\<number\>.\<number\>.\<number\>]
2. Checks if the ip address is private or not.It fetches the source code of url only if it is a public ip address. 
```python 
  if ip[0] in [0, 10, 127] \
		or (ip[0] == 172 and (ip[1] > 15 or ip[1] < 32)) \
		or (ip[0] == 169 and ip[1] == 254) \
		or (ip[0] == 192 and ip[1] == 168):
		return False
	return True
```

Now our aim to access the 127.0.0.1/admin-status (localhost) which is a private ip address by bypassing the second check.

### Bypass:
We can use octal notation to bypass the second check i.e, 0177.0.0.1 .Initially ip address will be splitted to [0177,0,0,1] and then ip[0] ie 177 checked against [0,10,127,172,169,192] and bypasses the check,
then the server requests 0177.0.0.1 which will converted back from octal to normal ip as [0177-> 127] then it requests 127.0.0.1/admin status and we get the flag 

`http://urlcheck1.chal.ctf.westerns.tokyo/check-status?url=http://0177.0.0.1/admin-status`

## urlcheck-v2
### Source Code:
<script src="https://gist.github.com/n41n4/496691de46d5202aec5585a722763ffa.js?file=urlcheck-v2.py"></script>

### Solution:
This is same as the above challenge but this time it will accept domain name.Then that domain name is passed through a function called `valid_fqdn()` which gets the ip from the domain name.Finally that ip address is passed to `valid_ip()` which checks if the ip address is public or private.

### Bypasss:
This time octal like 0177.0.0.1 won't work as `socket.gethostbyname(fqdn)` will convert it to 127.0.0.1 here itself and then passed to valid_ip where it checks if the ip is public or private,As it is a public ip obviously the checks gets failed. :(

Here comes the `DNS-rebind` part.For more info [Read This](https://geleta.eu/2019/my-first-ssrf-using-dns-rebinfing/).
```
DNS rebinding is a technique of changing the ip address of a domain rapidly with in a very short time to live (TTL) record,
preventing the DNS response from being cached.
```
So Lets see how this works in our context.\
Suppose our domain name has an ip address of 34.68.23.54(Some Public ip).Now we rebind our domain with 127.0.0.1 and 34.68.23.54.\
Then our ip address of the domain gets switched between themselves (34.68.23.54 -> 127.0.0.1 | 127.0.0.1 -> 34.68.23.54) within a short TTL. 

- When start dns rebinding our domain might get public ip(34.68.23.54) in validate_fqdn() function.\
- Then when server tries to access our domain ip address that gets switched to (127.0.0.1) which means we bypassed the check and we get the flag.

