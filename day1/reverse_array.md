<img width="924" height="647" alt="image" src="https://github.com/user-attachments/assets/6e11aa71-c1e1-49cf-8f11-48664ca35b0c" />

#### Code:
```c
#include <stdio.h>

int main(void) {
    int arr[5];
    int i;

    printf("Enter 5 integers:\n");
    for (i = 0; i < 5; i++) {
        scanf("%d", &arr[i]);
    }

    printf("In reverse order:\n");
    for (i = 4; i >= 0; i--) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}
```
