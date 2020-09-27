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

## urlcheck-v2
### Source Code:
<script src="https://gist.github.com/n41n4/496691de46d5202aec5585a722763ffa.js?file=urlcheck-v2.py"></script>

### Solution:
