---
layout: post
title: 11726 2xn 타일링 
description: 
image:
category: [Problem Solving]
tags: [DP]
math: true
---

# ![Silver III 11726 2xn 타일링](https://d2gd6pc034wcta.cloudfront.net/tier/8.svg){: width="25" height="25" .normal} 11726 2xn 타일링 

<details>
<summary>힌트1</summary>

</details>

<details>
<summary>C++</summary>
<div markdown="1">
```c++
#include <bits/stdc++.h>
using namespace std;
int main()
{
    int n;
    cin >> n;
    int memo[n];
    memo[0] = 1;
    memo[1] = 2;
    for (int i = 0; i < n-2; i++)
    {
        memo[i+2] = (memo[i]+memo[i+1])%MOD;
    }
    cout<<memo[n-1]<<endl;
}
```
</div>
</details>