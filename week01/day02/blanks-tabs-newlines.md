<img width="928" height="652" alt="image" src="https://github.com/user-attachments/assets/95133a8a-4200-41a9-8ca4-ebd01c80ebaf" />

#### Code:

```c
#include <stdio.h>

int main(){

int blank, tab, newline, c;

blank = 0;
tab = 0;
newline = 0;

while ((c = getchar()) != EOF)
{
	if (c== ' ') ++blank;
	if (c== '\t') ++tab;
	if (c== '\n') ++newline;
}

printf("blanks: %d\ntabs: %d\nnewlines: %d", blank, tab, newline);
return 0;
}
```
