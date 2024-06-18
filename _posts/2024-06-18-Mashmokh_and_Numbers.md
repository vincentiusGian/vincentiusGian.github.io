---
layout: post
title: Motion Analysis - 1
date: 14-06-2024
categories: [Competitive Programming, Math]
tags: [Math]     # TAG names should always be lowercase

math: true

---

# Problem
https://codeforces.com/problemset/problem/414/A

# Observation
Notice that to clarify this problem, all sequence as long it fits the $n$ and $k$ input, you'll get correct answer. 

## First Observation
Notice that the minimum number of $k$ is 1, since the sequence is a set of integers. Then, the number $k$ shouldn't be less than $\frac{n}{2}$. The reason is simply because of Bimokh stops when the remain sequence contains less than 2 elements. So, if $k < \frac{n}{2}$ return -1 or invalid.

## Second Observation (Ultimate)
The idea is to make the $\gcd(a_i,a_{i+1})$ = 1 and the rest is $k - k_{min}$. It's the optimal and ultimate solution for this problem. The construction would be like this.

Let the first element be $x$ and $x = k-k_{min}$, then the second element is $2\times x$. This construct that if $n$ is even, the $gcd$ of non-relative-prime sequence is still x. 

After that, construct the next 2 elements by $2x+1$ and $2x+2$. And do it for the rest of sequence. If n is odd, add extra largest (def free) prime numbers at the end of the sequence so $gcd(a_n,$extra$) = 1$.

Don't forget to handle when $n == 1$ and $k == 0$, and $n == 1$.

# Code
```c++
#include <bits/stdc++.h>
#define ll long long
#define AC ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define nl '\n'
#define input int n,k; cin >>n>>k;

const int extra = 1e9;

using namespace std;

void solve()
{
    input;

    if(n/2 > k)
    {
        cout << -1;
    } else if(n == 1 && k == 0) 
    {
        cout << 1;
    } else if(n == 1)
    {
        cout << -1;
    } else
    {
        int k_min = (n-2)/2;
        int x = k - k_min;
        cout << x << " " << 2*x << " ";

        int i = 2*x+1;

        while(k_min--)
        {
            cout << i << " " << i+1 << " ";
            i+=2;
        }

        if(n&1) cout << extra << nl;
    }
    
    
}


int main()
{
    AC
    solve();

    return 0;
}
```

# Complexity Analysis
The time complexity of the code is $O(n)$ because the main function calls the solve function, which iterates through the input size 'n' to perform calculations and output the result. The loop inside the solve function runs 'n' times, making the overall time complexity linear in terms of the input size 'n'.