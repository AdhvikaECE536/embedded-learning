<img width="926" height="693" alt="image" src="https://github.com/user-attachments/assets/67c10a03-07bb-468b-a872-31a0e035a4fc" />

```c
#include <stdio.h>

int power (int base, int n);

int main(){
	int i;
	for (i = 0; i<10; ++i)
		printf("%d %d %d\n", i, power(2,i), power(3,i));
	return 0;
}

int power (int base, int n)
{
	int i, p;

	p = 1;

	for (i = 1; i <= n; ++i)
		p = p*base;
	return p;
}


