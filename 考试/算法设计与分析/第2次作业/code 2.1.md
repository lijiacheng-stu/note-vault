```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <functional> 
using namespace std;

vector<int> answer;

void build_from_sorted(const vector<int>& arr, int left, int right) {
    if (left > right) {
        return;
    }
    int mid = left + (right - left) / 2;
    answer.push_back(arr[mid]);
    build_from_sorted(arr, left, mid - 1);
    build_from_sorted(arr, mid + 1, right);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    int n;
    cin >> n;
    vector<int> arr(n);
    for (int i = 0; i < n; ++i) {
        cin >> arr[i];
    }
    sort(arr.begin(), arr.end());
    answer.reserve(n);
    build_from_sorted(arr, 0, n - 1);
    for (int i = 0; i < n - 1; ++i) {
        cout << answer[i] << " ";
    }
    cout << answer[n - 1] << endl;
    return 0;
}

```