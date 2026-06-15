<img width="926" height="441" alt="image" src="https://github.com/user-attachments/assets/41b2832e-0655-47c5-a8c3-08fd1885de0e" />

#### Code:

```c
#include <stdio.h>

int main(){
int c, nl;
nl = 0;

while ((c= getchar())!= EOF)
	if (c== '\n')
	++nl;

printf("%d\n", nl);

return 0;
}
```
