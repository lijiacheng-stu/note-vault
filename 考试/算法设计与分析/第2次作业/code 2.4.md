```c++
#include <stdio.h>
#include <math.h>

long long target_num;
long long total_length;
int left_bound;
int right_bound;

int count_ones(long long num, long long len, long long pos) {
    if (num == 0) {
        return 0;
    }
    if (num == 1) {
        if (pos >= left_bound && pos <= right_bound) {
            return 1;
        }
        return 0;
    }
    long long offset = (len + 1) / 4;
    if (pos < left_bound) {
        return count_ones(num / 2, len / 2, pos + offset);
    }
    if (pos > right_bound) {
        return count_ones(num / 2, len / 2, pos - offset);
    }
    if (pos >= left_bound && pos <= right_bound) {
        return (num % 2)
               + count_ones(num / 2, len / 2, pos - offset)
               + count_ones(num / 2, len / 2, pos + offset);
    }
    return 0;
}

int main() {
    scanf("%lld %d %d", &target_num, &left_bound, &right_bound);
    total_length = 0;
    for (int k = 0; ; k++) {
        long long pow_val = (long long)pow(2, k);
        if (pow_val >= target_num) {
            break;
        }
        total_length += pow_val;
    }
    long long mid_pos = (total_length + 1) / 2;
    int res = count_ones(target_num, total_length, mid_pos);
    printf("%d\n", res);
    return 0;
}

```