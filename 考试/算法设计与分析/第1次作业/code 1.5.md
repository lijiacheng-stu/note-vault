```c++
#include <iostream>
#include <set>
using namespace std;
bool hasCommonDigit(long long a, long long b) {
    bool digitsA[10] = {false};
    while (a > 0) {
        digitsA[a % 10] = true;
        a /= 10;
    }
    while (b > 0) {
        if (digitsA[b % 10]) return true;
        b /= 10;
    }
    return false;
}

int main() {
    long long X;
    cin >> X;
    set<long long> factors;
    for (long long i = 1; i * i <= X; i++) {
        if (X % i == 0) {
            factors.insert(i);
            factors.insert(X / i);
        }
    }
    int count = 0;
    set<long long>::iterator it;
    for (it = factors.begin(); it != factors.end(); ++it) {
        long long D = *it;
        if (hasCommonDigit(D, X)) count++;
    }
    cout << count << endl;
    return 0;
}

```
