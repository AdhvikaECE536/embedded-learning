<img width="926" height="761" alt="image" src="https://github.com/user-attachments/assets/a7b92aa7-99d8-4ea1-82da-dd2c0d158ad0" />

#### Code:

```c
#include <stdio.h>

int calc(int a, int b, char op) {
    switch (op) {
        case '+': return a + b;
        case '-': return a - b;
        case '*': return a * b;
        case '/': return b ? a / b : 0;
        default: return 0;
    }
}

int main(void) {
    int a, b; char op;
    scanf("%d %c %d", &a, &op, &b);
    printf("%d %c %d = %d\n", a, op, b, calc(a, b, op));
    return 0;
}
```
