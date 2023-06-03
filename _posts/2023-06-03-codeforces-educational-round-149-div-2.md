---
layout: post
title: Codeforces Educational Round 149 (Div. 2)
description: 
image: 
category:
- Problem Solving
tags:
- codeforces
math: true
date: 2023-06-03 19:43 +0900
---
My solutions for Codeforces Educational Round 149 (Div. 2)
```c++
#include <iostream>
#include <vector>
#include <stack>
#include <queue>
#include<sstream>
#include <string>
#include <algorithm>
#include <iomanip>
#include <set>
#include <map>
#include <cmath>
 
#define FAST ios::sync_with_stdio(false);\
cin.tie(nullptr);\
cout.tie(nullptr);
#define endl '\n'
#define all(x) (x).begin(), (x).end()
using namespace std;
typedef long long ll;
typedef long double ld;
typedef vector<int> vi;
typedef vector<ll> vll;
typedef pair<int, int> pI;
typedef pair<ll, ll> pLL;
const int MAX = 500001;
const ll INF = 1234567890ll;

int main(){
    FAST
    int T;
    cin >> T;
    while(T--){
        int n, k;
        cin >> n >> k;
        vector<pLL> vec;
        for (int i = 0; i < n; i++)
        {
            int temp;
            cin >> temp;
            vec.push_back({temp,i});
        }
        sort(all(vec));
        vector<pLL> next;
        for (int i = 0; i < k; i++)
        {
            next.push_back({vec[i].second, vec[i].first});   
        }
        // for (int i = 0; i < n; i++)
        // {
        //     cout<<vec[i].first<< " ";
        // }
        // cout<<endl;
        
        sort(all(next));
        // for (int i = 0; i < next.size(); i++)
        // {
        //     cout<<next[i].second<< " ";
        // }
        // cout<<endl;
        ll arr[next.size()+1];
        arr[0] = 0;
        for (int i = 0; i < next.size(); i++)
        {
            arr[i+1] = next[i].second+arr[i];   
        }
        ll sum = arr[next.size()];
        ll mnm = sum;
        for (int i = 1; i <= next.size(); i++)
        {
            mnm = min(mnm, max(arr[i],sum-arr[i]));
        }
        cout<<mnm<<endl;
        

    }
}
```
