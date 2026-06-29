<img width="917" height="808" alt="image" src="https://github.com/user-attachments/assets/e5e64a01-4e4c-4a7d-a4b3-b1f7cda4997c" />

```c

#include <stdio.h>
#define MAXCHAR 26 

int main()
{
    int c, i;
    int freq[MAXCHAR];

    for (i = 0; i < MAXCHAR; ++i)
        freq[i] = 0;

    while ((c = getchar()) != EOF)
    {
        if (c >= 'a' && c <= 'z')
            ++freq[c - 'a'];
        else if (c >= 'A' && c <= 'Z')
            ++freq[c - 'A'];   
    }

    printf("\nCharacter Frequency Histogram:\n");
    for (i = 0; i < MAXCHAR; ++i)
    {
        if (freq[i] > 0)
        {
            printf("%c | ", 'a' + i);
            for (int j = 0; j < freq[i]; ++j)
                printf("*");
            printf("\n");
        }
    }
return 0;
}
