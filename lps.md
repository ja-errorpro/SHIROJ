# 題目
如果一個字串反過來讀跟原本的一樣，就稱為迴文。例如：abba、acbca、唧唧復唧唧都是迴文。
現在給你一個字串 S ( |S| <= 5000 )，你可以刪除 S 的頭或尾來得到 S 的子字串。請問你最少要刪除多少個字元，才能讓
S 變成迴文？

# 解析：
可以觀察規律，如果一個字串是迴文，它刪除頭尾後也還是迴文，一直刪到剩下一個字元或空字串時，稱此時的字元或空字元為中心。

我們只要枚舉所有可能的中心，每次向外擴張直到不符合迴文條件為止，就可以得到所有的迴文子字串。

在複雜度上，枚舉所有中心需要 O(|S|)，而每次向外擴張最差需要 O(|S|)，因此總複雜度為 O(|S|^2)。

實作上，需要考慮字串長度為奇數與偶數的情況。

你可以選擇兩種方式處理：
1. 將字串長度為奇數與偶數的情況分開處理。
2. 在頭尾與每個字中間插入特殊字元('$')，就能當同樣的情況處理。

延伸：
請試著將複雜度降到 O(|S|)。( Hint: Manacher's Algorithm )

// Code

```cpp
#include <iostream>
#include <string>
using namespace std;

void Solve() {
    string s;
    cin >> s;
    int max_length = 0;
    int head, tail;
    int N = s.length();
    for (int i = 0; i < N; ++i) {
        // 奇數長度
        int k = 0;
        while (i - k >= 0 && i + k < N && s[i - k] == s[i + k]) ++k;
        if (max_length < 2 * k - 1) {
            max_length = 2 * k - 1;
            head = i - k + 1;
            tail = i + k - 1;
        }
        // 偶數長度
        k = 0;
        while (i - k >= 0 && i + k + 1 < N && s[i - k] == s[i + k + 1]) ++k;
        if (max_length < 2 * k) {
            max_length = 2 * k;
            head = i - k + 1;
            tail = i + k;
        }
    }

    cout << max_length << endl;
}

int main() { Solve(); }
```