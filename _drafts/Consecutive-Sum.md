---
layout: post
title: 1912 연속합
description: 백준 그룹 문제집 동적 계획법의 풀합 입니다.
image: 
category:
- Problem Solving
tags:
- DP
math: true
---
# ![Silver II 1912 연속합](https://d2gd6pc034wcta.cloudfront.net/tier/9.svg){: width="25" height="25" .normal} 1912 연속합 
[문제](https://www.acmicpc.net/problem/1912)
<details markdown="1">
<summary>힌트1</summary>
이 문제에서 n은 최대 100,000까지 커질 수 있기 때문에 단순히 시작점과 끝점을 잡고 전체를 탐색해보는 $O(n^2)$의 풀이로는 풀 수 없다.
> BOJ의 채점 컴퓨터는 초당 1억번의 기초 연산 (덧셈, 비교 등)을 할 수 있다고 생각하면 좋다.
{: .prompt-tip }
</details>

<details markdown="1">
<summary>힌트2</summary>
이 문제는 가장 큰 수를 뽑아서 그 주변을 자연스럽게 포함하는 방식으로 풀면 풀 수 없다. 

```
5 
10 -20 9 9 9
```

 와 같은 반례가 있다. 동적계획법으로 접근할 수 밖에 없다.
</details>

<details markdown="1">
<summary>힌트3</summary>
만약 입력에 있는 모든 수가 양수였다면 연속합의 최댓값은 1번부터 n번까지의 합이었을 것이다.
</details>

<details markdown="1">
<summary>힌트4</summary>
한 항씩 차근차근 계산해보면 `7 4 -15 21`의 경우에는 $1$번째부터 $i$번째까지의 연속합의 최댓값은 `7 11 11 21`이 되게 된다. 
</details>

<details markdown="1">
<summary>풀이</summary>
합을 저장할 변수 $curSum$, 이때까지의 최댓값을 저장할 변수 $mxm$을 만들어주자. 

연속합이기 때문에 그 전까지의 합이 0보다 작으면 
(`7 4 -15 21`에서 4번째 항을 계산할 때와 같은 경우이다.) 새로 시작하는 것이 낫다. 
위의 내용을 점화식으로 풀어보면


$$ 
curSum[n] = 
\begin{cases}
  vec[n] \quad if \quad curSum[n-1] < 0 \\
  curSum[n-1]+vec[n] \quad if \quad curSum[n-1] \geq 0
\end{cases}
$$

과 같은 식이 나오게 된다. 우리는 이 전체의 최댓값을 구해야 하므로 매번 

$$
mxm = max(mxm, curSum[i])
$$

를 해주면 된다.

```c++
const int MAX = 1234567890;
int mxm = -MAX, curSum = -MAX; 
for(int i=0; i<n; i++){
    if(curSum<0) //first case
        curSum = vec[i];
    else //second case
        curSum += vec[i];
    mxm = max(mxm, curSum);
}
cout<<mxm<<endl;
```
> $MAX$변수는 문제에서 $1 \leq n \leq 100000$의 최댓값인 100,000과 $-1000 \leq a_i \leq 1000$의 최댓값은 1,000의 곱인 1,000,000,000보다는 커야한다.

</details>
<details>
<summary>C++</summary>
<div markdown="1">
```c++
#include <bits/stdc++.h>
using namespace std;
const int MAX = 1234567890;
int main()
{
    int n;
    cin >> n;
	vector<int> vec(n);
	for(int i=0; i<n; i++){
	    cin >> vec[i];
	}
	int mxm = -MAX, curSum = -MAX;
	for(int i=0; i<n; i++){
	    if(curSum<0)
	        curSum = vec[i];
	    else
	        curSum += vec[i];
	   mxm = max(mxm, curSum);
	}
	cout<<mxm<<endl;
}
```
</div>
</details>


[DP 문제집](/posts/Dynamic-Programming-Question-Book)