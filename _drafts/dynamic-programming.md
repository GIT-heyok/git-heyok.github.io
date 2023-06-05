---
layout: post
title: USACO Gold 2019 US Open - Snakes
description: 
image: 
category: 
tags: 
math: true
---
[Snakes](http://www.usaco.org/index.php?page=viewproblem2&cpid=945)
minimum waste를 찾는 것이 핵심인 문제이다.
$$
dp[i][j] = dp[i-1][j]
$$
```c++
#include <bits/stdc++.h>
using namespace std;

#define FAST                     \
    ios::sync_with_stdio(false); \
    cin.tie(nullptr);            \
    cout.tie(nullptr);
#define endl '\n'
using namespace std;
void setFile(string s){
    freopen((s+".in").c_str(), "r", stdin);
    freopen((s+".out").c_str(), "w", stdout);
}
const int inf = 1234567890;
int main()
{
    FAST
    setFile("snakes");
    int n, k;
    cin >> n >> k;
    int arr[n+1];
    for (int i1 = 1; i1 <= n; i1++)
    {
        cin >> arr[i1];
    }
    int memo[n+1][k+1];
    memset(memo, 0, sizeof(memo));
    int mxm = -1, totSpace = 0;
    for (int i1 = 1; i1 <= n; i1++)
    {
        mxm = max(mxm, arr[i1]);
        memo[i1][0] = mxm*(i1);
        for (int i2 = 1; i2 <= k; i2++)
        {
            memo[i1][i2] = inf;
            int net = arr[i1];
            for (int i3 = i1-1; i3 >= 0; i3--)
            {
                memo[i1][i2] = min(memo[i1][i2], memo[i3][i2-1] + net*(i1-i3));
                net = max(net, arr[i3]); 
            }
            
        }
        totSpace += arr[i1];   
    }
    cout<<memo[n][k] - totSpace<<endl;
    
} 
```