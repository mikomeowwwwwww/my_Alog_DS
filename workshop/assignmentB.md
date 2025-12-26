# Assignment #B: dp

Updated 1448 GMT+8 Nov 18, 2025

2025 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### LuoguP1255 数楼梯

dp, bfs, https://www.luogu.com.cn/problem/P1255

思路：



代码：

```python
N = int(input())
a = [0]*(N+1)
a[0] = 1
a[1] = 1
for i in range(2,N+1):
    a[i] = a[i-1] + a[i-2]
print(a[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251125160744.png]]




### 27528: 跳台阶

dp, http://cs101.openjudge.cn/practice/27528/

思路：



代码：

```python
N = int(input())
a = [1]
for i in range(N):
    a.append(sum(a))
print(a[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251125160903.png]]




### M23421:《算法图解》小偷背包问题

dp, http://cs101.openjudge.cn/pctbook/M23421/

思路：



代码：

```python
def f(N, B, mix):
    mid = []
    for i in range(N):
        if i in mix:
            if B-mix[i][0] >= 0:
                a = mix.pop(i)
                mid.append(f(N, B-a[0], mix)+a[1])
                mix[i] = a
    if len(mid) == 0:
        return 0
    else:
        return max(mid)

N, B = map(int, input().split())
values = list(map(int, input().split()))
weights = list(map(int, input().split()))
mix = dict(zip([i for i in range(N)], zip(weights, values)))
print(f(N, B, mix))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251125160940.png]]




### M5.最长回文子串

dp, two pointers, string, https://leetcode.cn/problems/longest-palindromic-substring/

思路：



代码：

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        m = 0
        a = 0
        b = 0
        for i in range(len(s)):
            l = 1
            for j in range(1,i+1):
                try:
                    if s[i-j] == s[i+j]:
                        l += 2
                    else:
                        break
                except:
                    break
            if l > m:
                a = 1
                b = i
                m = l        
        for i in range(len(s)-1):
            l = 0
            for j in range(i+1):
                try:
                    if s[i-j] == s[i+1+j]:
                        l += 2
                    else:
                        break
                except:
                    break
            if l > m:
                a = 0
                b = i
                m = l
        if a:
            return s[int(b-(m-1)/2):int(b+(m-1)/2+1):]
        else:
            return s[int(b-m/2+1):int(b+m/2+1):]
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251125161025.png]]






### 474D. Flowers

dp, 1700 https://codeforces.com/problemset/problem/474/D

思路：



代码：

```python
t, k = map(int, input().split())
a = [0]*100001
M = 1000000007
for i in range(k):
    a[i] = 1
for i in range(k,len(a)):
    a[i] += (a[i-k]+a[i-1])%M
sum_dp = [0]*100001
for i in range(len(sum_dp)):
    sum_dp[i] = (sum_dp[i-1]+a[i])%M
for i in range(t):
    j, k = map(int, input().split())
    print((sum_dp[k]-sum_dp[j-1])%M)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251125161155.png]]




### M198.打家劫舍

dp, https://leetcode.cn/problems/house-robber/

思路：



代码：

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        dp = [[nums[0],0]]
        for i in range(1,len(nums)):
            dp.append([dp[-1][1]+nums[i],max(dp[-1])])
        return max(dp[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251125161245.png]]




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
无额外练习
1.无
2.无
3.学习了zip()方法
4.没用dp但还是能做出来，看了官方题解，我的做法类似于中心扩展算法
5.第一个dp我用数学中的组合数推导出来，但后面的sumdp没想到，导致会超时。我一开始以为是要用矩阵快速幂，但看了要求发现不是，最后问了ai想出了sumdp
6.无




