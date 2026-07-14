<img width="927" height="459" alt="image" src="https://github.com/user-attachments/assets/4bfb08ab-23f2-4a54-8cf1-96a8d377cc80" />

```c
#include <stdio.h>
int main(){
	int a = 10; // an integer
	int *p = &a; // p holds the address of a

	printf("Value of a: %d\n", a);
	printf("Address of a: %p\n", &a);
	printf("Value of p: %p\n", p);
	printf("Address of p: %p\n", &p);
	printf("What p points to: %d\n", *p);

	return 0;
}
```
