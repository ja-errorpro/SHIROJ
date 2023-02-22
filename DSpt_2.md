# 資結練習題P2-鐵路

UVA514

使用堆疊模擬火車進出站

## STL版
```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int n, m;
    cin >> n >> m;
    for(int t = 0; t < m; ++t){
        bool flag = true;
        vector<int> train(n);
        stack<int> station;
        for(int i = 0; i < n; ++i){
            cin >> train[i];
            train[i]--;
        }
        for(int i = 0, j = 0; i < n && j < n; ++i){
            station.push(i);
            while(!station.empty() && station.top() == train[j]){
                station.pop();
                ++j;
            }
        }
        cout << (station.empty() ? "Yes" : "No") << endl;
    }
    
    return 0;
}
```

## 實作版
```cpp
# include <iostream>
using namespace std;
struct Stack{
    int data[1000];
    int top;
    Stack(){
        top = -1;
    }
    void push(int x){
        data[++top] = x;
    }
    void pop(){
        --top;
    }
    bool empty(){
        return top == -1;
    }
};

int main()
{
    int n, m;
    cin >> n >> m;
    for(int t = 0; t < m; ++t){
        bool flag = true;
        int train[1000];
        Stack station;
        for(int i = 0; i < n; ++i){
            cin >> train[i];
            train[i]--;
        }
        for(int i = 0, j = 0; i < n && j < n; ++i){
            station.push(i);
            while(!station.empty() && station.data[station.top] == train[j]){
                station.pop();
                ++j;
            }
        }
        cout << (station.empty() ? "Yes" : "No") << endl;
    }
    
    return 0;
}
```