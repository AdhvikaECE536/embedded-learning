<img width="924" height="471" alt="image" src="https://github.com/user-attachments/assets/88ea43ba-60f9-43e2-b9c7-39b7f789e10f" />

#### Code:
```c
#include <stdio.h>

int main(void) {
    int n, sum = 0, remainder;

    printf("Enter an integer: ");
    scanf("%d", &n);

    while (n != 0) {
        remainder = n % 10;   
        sum += remainder;       
        n /= 10;               
    }

    printf("Sum of digits = %d\n", sum);
    return 0;
}
