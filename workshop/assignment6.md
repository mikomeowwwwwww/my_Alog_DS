# Assignment #6: 矩阵、贪心

Updated 1432 GMT+8 Oct 14, 2025

2025 fall, Complied by <mark>同学的姓名、院系</mark>



>**说明：**
>
>1. **解题与记录：**
>
>  对于每一个题目，请提供其解题思路（可选），并附上使用Python或C++编写的源代码（确保已在OpenJudge， Codeforces，LeetCode等平台上获得Accepted）。请将这些信息连同显示“Accepted”的截图一起填写到下方的作业模板中。（推荐使用Typora https://typoraio.cn 进行编辑，当然你也可以选择Word。）无论题目是否已通过，请标明每个题目大致花费的时间。
>
>2. 提交安排：**提交时，请首先上传PDF格式的文件，并将.md或.doc格式的文件作为附件上传至右侧的“作业评论”区。确保你的Canvas账户有一个清晰可见的本人头像，提交的文件为PDF格式，并且“作业评论”区包含上传的.md或.doc附件。
> 
>4. **延迟提交：**如果你预计无法在截止日期前提交作业，请提前告知具体原因。这有助于我们了解情况并可能为你提供适当的延期或其他帮助。  
>
>请按照上述指导认真准备和提交作业，以保证顺利完成课程要求。





## 1. 题目

### M18211: 军备竞赛

greedy, two pointers, http://cs101.openjudge.cn/pctbook/M18211



思路：



代码

```python
# 
p = int(input())
n = list(map(int, input().split()))
n.sort()
if p < n[0]:
    print(0)
else:
    s = sum(n)
    if p >= s:
        print(len(n))
    else:
        a = 0
        b = 0
        for i in range(len(n)-1, -1, -1):
            s -= n[i]
            if s <= p:
                a = i
                b = len(n)-a-1
                break
            p += n[i]
            if p >= s:
                a = i
                b = len(n)-a
                break
        print(a-b)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-20 175855.png]]




### M21554: 排队做实验

greedy, http://cs101.openjudge.cn/pctbook/M21554/



思路：



代码

```python
n = int(input())
m = list(enumerate(list(map(int,input().split())), start=1))
m.sort(key=lambda i: i[1])
a = [i[0] for i in m]
print(" ".join(map(str, a)), end="\n")
t = 0
for i in range(n):
    t += m[i][1]*(n-i-1)
print(f"{t/n:.2f}")
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-20 175946.png]]




### E23555: 节省存储的矩阵乘法

implementation, matrices, http://cs101.openjudge.cn/pctbook/E23555



思路：



代码

```python
n = list(map(int, input().split()))
m1 = []
m2 = []
m3 = []
for i in range(n[0]):
    m1.append([0]*n[0])
    m2.append([0]*n[0])
    m3.append([0]*n[0])
for i in range(n[1]):
    a, b , c = map(int, input().split())
    m1[a][b] = c
for i in range(n[2]):
    a, b, c = map(int, input().split())
    m2[a][b] = c
for i in range(n[0]):
    for j in range(n[0]):
        for k in range(n[0]):
            m3[i][j] += m1[i][k]*m2[k][j]
for i in range(n[0]):
    for j in range(n[0]):
        if m3[i][j] != 0:
            print(str(i)+" "+str(j)+" "+str(m3[i][j]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-20 180038.png]]




### M12558: 岛屿周⻓

matrices, http://cs101.openjudge.cn/pctbook/M12558


思路：



代码

```python
# 
n, m = map(int, input().split())
s = [[0]*(m+2)]
for i in range(1,n+1):
    s.append([0])
    s[i].extend(list(map(int,input().split())))
    s[i].append(0)
s.append([0]*(m+2))
c = 0
for i in range(1,n+1):
    for j in range(1,m+1):
        if s[i][j] == 0:
            continue
        else:
            c += 4
            if s[i-1][j] == 1:
                c -= 1
            if s[i][j-1] == 1:
                c -= 1
            if s[i+1][j] == 1:
                c -= 1
            if s[i][j+1] == 1:
                c -= 1
print(c)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-20 180110.png]]




### M01328: Radar Installation

greedy, http://cs101.openjudge.cn/practice/01328/



思路：



代码

```python
import math
import sys

times = 0
while True:
    a = sys.stdin.readline().strip()
    if not a:
        continue
    times += 1
    a = list(map(int, a.split()))
    if a[0] == 0 and a[1] == 0:
        break
    if a[1] <= 0:
        print("Case "+str(times)+": -1")
        for i in range(a[0]):
            b = sys.stdin.readline().strip()
        continue
    b = []
    for i in range(a[0]):
        b.append(list(map(int, sys.stdin.readline().strip().split())))
    b.sort()
    try:
        for i in range(a[0]):
            j = math.sqrt(a[1]**2 - b[i][1]**2)
            MAX = b[i][0] + j
            MIN = b[i][0] - j
            b[i] = [MIN, MAX]
        counter = 0
    except:
        print("Case "+str(times)+": -1")
        continue
    try:
        while True:
            if b[-1][0] <= b[-2][1]:
                b[-2] = [max(b[-1][0],b[-2][0]), min(b[-1][1],b[-2][1])]
                b.pop()
            else:
                b.pop()
                counter += 1
    except IndexError:
        counter += 1
    print("Case "+str(times)+": "+str(counter))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-20 180147.png]]




### 545C. Woodcutters

dp, greedy, 1500, https://codeforces.com/problemset/problem/545/C



思路：



代码

```python
n = int(input())
if n == 0:
    print(0)
    exit()
trees = [tuple(map(int, input().split())) for _ in range(n)]
x = [t[0] for t in trees]
h = [t[1] for t in trees]

dp = [[0] * 3 for _ in range(n)]
right = [[0] * 3 for _ in range(n)]

# 初始化第0棵树的状态
dp[0][0] = 0
right[0][0] = x[0]
dp[0][1] = 1
right[0][1] = x[0]
dp[0][2] = 1
right[0][2] = x[0] + h[0]

for i in range(1, n):
    # 不砍当前树
    dp[i][0] = max(dp[i-1][0], dp[i-1][1], dp[i-1][2])
    right[i][0] = x[i]
    
    # 向左砍当前树
    max_prev = -float('inf')
    for j in range(3):
        if x[i] - h[i] > right[i-1][j]:
            if dp[i-1][j] > max_prev:
                max_prev = dp[i-1][j]
    dp[i][1] = max_prev + 1 if max_prev != -float('inf') else 0
    right[i][1] = x[i]
    
    # 向右砍当前树
    max_prev = -float('inf')
    if i == n - 1:
        for j in range(3):
            if dp[i-1][j] > max_prev:
                max_prev = dp[i-1][j]
    else:
        if x[i] + h[i] < x[i+1]:
            for j in range(3):
                if dp[i-1][j] > max_prev:
                    max_prev = dp[i-1][j]
    dp[i][2] = max_prev + 1 if max_prev != -float('inf') else 0
    right[i][2] = x[i] + h[i]

print(max(dp[n-1][0], dp[n-1][1], dp[n-1][2]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-20 204517.png]]




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
额外题目：
![[Pasted image 20251020204753.png]]
![[Pasted image 20251020204823.png]]
```python
N = int(input())
n = list(map(int, input().split()))
m = []
r = 0
c = 1
for i in range(N):
        m.append([i-n[i],i+n[i]])
        if i-n[i] <= 0 and i+n[i] > r:
            r = i+n[i]
m.sort(key = lambda x: x[1],reverse = True)
while r < len(n)-1:
    for i in m:
        if i[0] <= r+1:
            c += 1
            r = i[1]
            break
print(c)
```
![[Pasted image 20251020205002.png]]
![[Pasted image 20251020205027.png]]
```python
n, m = map(int, input().split())
a = [[0]*(m+2)]
g = []
for i in range(1,n+1):
    b = list(map(int, input().split()))
    g.append(b)
    a.append([0])
    a[i].extend(b)
    a[i].append(0)
a.append([0]*(m+2))
for i in range(1,n+1):
    for j in range(1,m+1):
        k = a[i+1][j]+a[i-1][j]+a[i][j+1]+a[i][j-1]+a[i+1][j+1]+a[i+1][j-1]+a[i-1][j+1]+a[i-1][j-1]
        if k == 2:
            pass
        elif k == 3:
            g[i-1][j-1] = 1
        else:
            g[i-1][j-1] = 0
for i in range(n):
    for j in range(m):
        print(g[i][j], end=' ')
    print()
```
![[Pasted image 20251020205158.png]]
![[Pasted image 20251020205234.png]]
```python
class Solution:

    def maxProfit(self, prices: List[int]) -> int:

        minnum = prices[0]

        maxnum = 0

        for i in prices:

            if i - minnum > maxnum:

                maxnum = i - minnum

            if i < minnum:

                minnum = i

        return maxnum
```
![[Pasted image 20251020205351.png]]
![[Pasted image 20251020205414.png]]
```python
N = int(input())
a0 = 1
a1 = 1
for i in range(N-1):
    mid = a1
    a1 += a0
    a0 = mid
print(a1)
```
![[Pasted image 20251020205519.png]]
![[Pasted image 20251020205546.png]]
```python
n, a, b, c = map(int, input().split())
dp = [-1] * (n + 1)
dp[0] = 0
for i in range(1, n + 1):
    if i >= a and dp[i - a] != -1:
        dp[i] = max(dp[i], dp[i - a] + 1)
    if i >= b and dp[i - b] != -1:
        dp[i] = max(dp[i], dp[i - b] + 1)
    if i >= c and dp[i - c] != -1:
        dp[i] = max(dp[i], dp[i - c] + 1)
print(dp[n])
```
1.无
2.用enumerate跟踪元素位置  
3.矩阵乘法
4.无
5.很难评价的一道题，题中确实没有说d>=0，但我无法想象出探测范围是负数的雷达:)，看了测试用例才做出来
6.使用了ai，这道题难点在于初始状态以及dp的思路




