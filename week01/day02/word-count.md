<img width="928" height="652" alt="image" src="https://github.com/user-attachments/assets/e96442ad-032f-44cf-9ad0-69cd364e88e3" />
#### Code:

```c
#include <stdio.h>
#define IN 1
#define OUT 0
/* inside a word */
/* outside a word */
/* count lines, words, and characters in input */
int main()
{
int c, nl, nw, nc, state;
state = OUT;
nl = nw = nc = 0;
while ((c = getchar()) != EOF) {
++nc;
if (c == '\n')
++nl;
if (c == ' ' || c == '\n' || c == '\t')
state = OUT;
else if (state == OUT) {
state = IN;
++nw;
}
}
printf("%d %d %d\n", nl, nw, nc);
return 0;
}
