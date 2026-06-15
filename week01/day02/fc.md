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
```

<img width="926" height="668" alt="image" src="https://github.com/user-attachments/assets/007b7348-04af-488c-829c-340d3f89a924" />

#### Code:

```c
#include <stdio.h>

// printing Fahrenheit-Celsius table

int main()
{
float fahr, cel;

for (fahr= 0; fahr<=300 ; fahr += 20){
cel = (5.0/9.0) * (fahr-32.0);
printf("%f\t%f\n", fahr, cel);
}

return 0;
}
```
