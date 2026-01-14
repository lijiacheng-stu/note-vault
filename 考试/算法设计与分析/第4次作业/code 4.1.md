```c++
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

bool isPalindrome(const char* s, int i, int k) {
    while (i < k) {
        if (s[i] != s[k]) {
            return false;
        }
        i++;
        k--;
    }
    return true;
}

bool isMagic(const char* s) {
    int i = 0, k = strlen(s) - 1;
    while (i < k) {
        if (s[i] != s[k]) {
            return isPalindrome(s, i + 1, k) || isPalindrome(s, i, k - 1);
        }
        i++;
        k--;
    }
    return true;
}

int main() {
    char s[100000];
    scanf("%s", s);
    if (isMagic(s)) {
        printf("true\n");
    } else {
        printf("false\n");
    }
    return 0;
}

```