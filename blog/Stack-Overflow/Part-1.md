```c
#include <stdio.h>
#include <unistd.h>

//gcc -fno-stack-protector -o snippet snippet.c

int main(int argc, char const *argv[])
{
	char secret[] = "Sup3r_S3cr37_S7r1n6";
	char key[128];
	read(0, key, 128);
	printf("Welcome %s",key);

	return 0;
}
```
