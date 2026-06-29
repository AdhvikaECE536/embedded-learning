<img width="952" height="971" alt="image" src="https://github.com/user-attachments/assets/785f7e2a-ea31-4335-bf41-c212f3e09c86" />

```c

#include <stdio.h>
#define MAXLEN 20

int main()
{
    int c, len, i;
    int wlen[MAXLEN];
    
    for (i = 0; i < MAXLEN; ++i)
        wlen[i] = 0;
    
    len = 0;
    while ((c = getchar()) != EOF)
    {
        if (c == ' ' || c == '\n' || c == '\t')
        {
            if (len > 0)
            {
                if (len < MAXLEN)
                    ++wlen[len];
                len = 0;
            }
        }
        else
            ++len;
    }
    
    printf("\nWord Length Histogram:\n");
    for (i = 1; i < MAXLEN; ++i)
    {
        if (wlen[i] > 0)
        {
            printf("%2d | ", i);
            for (int j = 0; j < wlen[i]; ++j)
                printf("*");
            printf("\n");
        }
    }
return 0;

}
```
