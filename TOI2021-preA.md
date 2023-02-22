# 原始人排序

轉成二進位後依照1的個數排序。

如果1的個數相同，依輸入順序輸出。

使用bitset來轉換成二進位。

且需使用穩定排序(如std::stable_sort、bubble sort)。

```cpp
#include <bits/stdc++.h>
using namespace std;
bool cmp1(int a, int b)
{
    bitset<32> x(a);
    bitset<32> y(b);
    return x.count() < y.count();
}
bool cmp2(int a, int b)
{
    bitset<32> x(a);
    bitset<32> y(b);
    return x.count() > y.count();
}
int main()
{
    int n;
    cin >> n;
    vector<int> v;
    for (int i = 0; i < n; i++)
    {
        int x;
        cin >> x;
        v.push_back(x);
    }
    stable_sort(v.begin(), v.end(), cmp1);
    /*for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n - 1; j++)
        {
            if (cmp2(v[j], v[j + 1]))
                swap(v[j], v[j + 1]);
        }
    }*/
    for (auto i : v)
        cout << i << " ";
    return 0;
}
```