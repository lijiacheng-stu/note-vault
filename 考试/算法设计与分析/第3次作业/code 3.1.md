```c
#include <stdio.h>

int maxLen(int a[], int n) {
    int max = 0;
    int dp[n][n];
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++)
            dp[i][j] = 2;
    }
    int j = 0;
    int k = 0;
    for (int i = 2; i < n; i++) {
        j = 0;
        k = i - 1;
        while (j < k) {
            if (a[j] + a[k] == a[i]) {
                dp[k][i] = dp[j][k] + 1;
                max = (max > dp[k][i]) ? max : dp[k][i];
                j++, k--;
            } else if (a[j] + a[k] > a[i]) {
                k--;
            } else {
                j++;
            }
        }
    }
    if (max < 3) {
        return 0;
    } else {
        return max;
    }
}

int main() {
    int n;
    scanf("%d", &n);
    int a[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &a[i]);
    }
    printf("%d\n", maxLen(a, n));
    return 0;
}

```