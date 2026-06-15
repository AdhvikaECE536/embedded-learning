<img width="926" height="875" alt="image" src="https://github.com/user-attachments/assets/dd682565-b73e-4c24-9e61-febeac949094" />

#### Code
```c
#include <stdio.h>

// printing Fahrenheit-Celsius table

int main()
{
int fahr, cel;
int lower, upper, step;

lower = 0;
upper = 300;
step = 20;

fahr = lower;

while (fahr<= upper)
{
	cel = 5* (fahr-32)/9;
	printf("%d\t%d\n", fahr, cel);
	fahr = fahr + step;
}

return 0;
}
