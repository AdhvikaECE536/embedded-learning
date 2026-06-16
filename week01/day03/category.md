<img width="924" height="501" alt="image" src="https://github.com/user-attachments/assets/26d43ffd-8b1a-4268-8e19-b6a72dc52028" />

#### Code:

```c
#include <stdio.h>

int main()
{
    int c, ndigit, nwhite, nother;
    ndigit = nwhite = nother = 0;

    while ((c = getchar()) != EOF)
    {
        if (c >= '0' && c <= '9')
            ndigit++;
        else if (c == ' ' || c == '\n' || c == '\t')
            nwhite++;
        else
            nother++;
    }

    printf("digits = %d, white space = %d, other = %d\n",
            ndigit, nwhite, nother);
}
