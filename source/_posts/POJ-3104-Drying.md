---
title: POJ 3104 Drying
date: 2014-08-21 19:23:22
categories: Exercise
toc: true
---
# 题目
源地址：

http://poj.org/problem?id=3104

# 理解
感觉是一道模拟的题目，使用二分来优化时间。

<!-- more -->

# 代码

```

#include <cstdio>
#include <cstdlib>
#include <cstring>
#include <cmath>
#include <ctime>
#include <iostream>
#include <algorithm>
#include <string>
#include <vector>
#include <deque>
#include <list>
#include <set>
#include <map>
#include <stack>
#include <queue>
#include <numeric>
#include <iomanip>
#include <bitset>
#include <sstream>
#include <fstream>
#define debug puts("-----")
#define pi (acos(-1.0))
#define eps (1e-8)
#define inf (1<<28)
using namespace std;

const int N = 100005;
int n;
int a[N];
int k;

bool check(int _value)
{
    int cnt = 0;
    for (int i = 0; i < n; ++i)
    {
        if (a[i] > _value)
        {
            double kk = ((double)(a[i] - _value)) / (k - 1);
            cnt += (int)kk;
            if (kk - (int)kk > 0)
            {
                ++cnt;
            }
            if (cnt > _value)
            {
                return false;
            }
        }
    }

    return (cnt <= _value);
}

int BinarySearch(int _low, int _high)
{
    int left = _low;
    int right = _high;
    int mid;
    int ans = _high;
    while (left <= right)
    {
        mid = (left + (right - left) * 0.5);
        if (check(mid))
        {
            ans = mid;
            right = mid - 1;
        }
        else
        {
            left = mid + 1;
        }
    }
    return ans;
}

void Test()
{
    int maxV = 0;
    for (int i = 0; i < n; ++i)
    {
        scanf("%d", &a[i]);
        if (maxV < a[i])
        {
            maxV = a[i];
        }
    }
    scanf("%d", &k);
    if (k == 1)
    {
        printf("%d\n", maxV);
    }
    else
        printf("%d\n", BinarySearch(0, maxV));
}

int main(int argc, char const *argv[])
{
    while (scanf("%d", &n) != EOF)
    {
        Test();
    }
    return 0;
}

```

# 更新日志
- 2014年08月21日 已AC。