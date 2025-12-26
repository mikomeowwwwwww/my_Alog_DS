# Assignment #C: bfs & dp

Updated 1436 GMT+8 Nov 25, 2025

2025 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### sy321迷宫最短路径

bfs, https://sunnywhy.com/sfbj/8/2/321

思路：



代码：

```python
class Node:

    def __init__(self, parent_node=None, value=None):

        self.parent_node = parent_node

        self.value = value

  

    def is_in(self, val):

        if val == self.value:

            return True

        elif self.parent_node is None:

            return False

        else:

            return self.parent_node.is_in(val)

  

    def print(self):

        if self.parent_node is None:

            print(' '.join(map(str, self.value)))

        else:

            self.parent_node.print()

            print(' '.join(map(str, self.value)))

  

n, m = map(int, input().split())

a = []

for i in range(n):

    a.append(list(map(int, input().split())))

c = [Node(value = (1,1))]

while True:

    c_t =[]

    end = False

    for i in c:

        x = i.value[0]

        y = i.value[1]

        if x+1 == n and y == m:

            Node(i, (x+1, y)).print()

            end = True

            break

        elif x == n and y+1 == m:

            Node(i, (x, y+1)).print()

            end = True

            break

        if x+1 <= n and a[x][y-1] == 0 and not i.is_in((x+1, y)):

            c_t.append(Node(i, (x+1, y)))

        if x-1 >= 1 and a[x-2][y-1] == 0 and not i.is_in((x-1, y)):

            c_t.append(Node(i, (x-1, y)))

        if y+1 <= m and a[x-1][y] == 0 and not i.is_in((x, y+1)):

            c_t.append(Node(i, (x, y+1)))

        if y-1 >= 1 and a[x-1][y-2] == 0 and not i.is_in((x, y-1)):

            c_t.append(Node(i, (x, y-1)))

    if end:

        break

    c = c_t
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251221023453.png]]




### sy324多终点迷宫问题

bfs, https://sunnywhy.com/sfbj/8/2/324

思路：



代码：

```python
n, m = map(int, input().split())

a = []

for i in range(n):

    mid = list(map(int, input().split()))

    for j in range(m):

        mid[j] = -mid[j]

    a.append(mid)

step = 1

c = {(0,0)}

while True:

    c_t = set()

    while len(c) != 0:

        mid = c.pop()

        a[mid[0]][mid[1]] = step

        if mid[0] - 1 >= 0 and a[mid[0] - 1][mid[1]] == 0:

            c_t.add((mid[0] - 1, mid[1]))

        if mid[1] - 1 >= 0 and a[mid[0]][mid[1] - 1] == 0:

            c_t.add((mid[0], mid[1] - 1))

        if mid[0] + 1 < n and a[mid[0] + 1][mid[1]] == 0:

            c_t.add((mid[0] + 1, mid[1]))

        if mid[1] + 1 < m and a[mid[0]][mid[1] + 1] == 0:

            c_t.add((mid[0], mid[1] + 1))

    step += 1

    if len(c_t) == 0:

        break

    else:

        c = c_t

for i in range(n):

    for j in range(m):

        if a[i][j] == 0:

            a[i][j] = -1

        elif a[i][j] > 0:

            a[i][j] -= 1

for i in range(n):

    print(*a[i])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251221023550.png]]




### M02945: 拦截导弹

dp, greedy http://cs101.openjudge.cn/pctbook/M02945

思路：



代码：

```python
k = int(input())
nums = list(map(int, input().split()))
dp = [1] * k 
for i in range(1, k):
    for j in range(i):
        if nums[i] <= nums[j]:
            dp[i] = max(dp[i], dp[j] + 1)
print(max(dp))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251221023704.png]]




### 189A. Cut Ribbon

brute force/dp, 1300, https://codeforces.com/problemset/problem/189/A

思路：



代码：

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



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251221023801.png]]






### M01384: Piggy-Bank

dp, http://cs101.openjudge.cn/practice/01384/

思路：



代码：

```python
for _ in range(int(input())):
    E, F = map(int, input().split())
    weight = F - E
    coins = []
    for i in range(int(input())):
        P, W = map(int, input().split())
        coins.append((W, P))
    coins.sort()
    v = [float('inf')] * (weight + 1)
    v[0] = 0
    for i in range(weight):
        if v[i] != float('inf'):
            try:
                for W, P in coins:
                    v[i + W] = min(v[i + W], v[i] + P)
            except:
                pass
    if v[weight] == float('inf'):
        print('This is impossible.')
    else:
        print('The minimum amount of money in the piggy-bank is ' + str(v[weight]) + '.')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251221023851.png]]




### M02766: 最大子矩阵

dp, kadane, http://cs101.openjudge.cn/pctbook/M02766

思路：



代码：

```python
import sys

data = list(map(int, sys.stdin.read().split()))
N = data[0]
matrix = [[0]*N for i in range(N)]
for i in range(N):
    for j in range(N):
        matrix[i][j] = data[i*N+j+1]
m = float('-inf')
for i in range(N):
    nums = [0]*N
    for j in range(i, N):
        for k in range(N):
            nums[k] += matrix[j][k]
        t_m = float('-inf')
        for k in range(N):
            t_m = max(t_m+nums[k], nums[k])
            m = max(m, t_m)
print(m)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251221023918.png]]




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
无额外练习
1.用了整活做法，但最后用时比答案给的做法要少，很神奇
2.无，当然我现在bfs不这么写了
3.无
4.我记得这题做过来着
5.pypy3神力，同样的代码python跑TLE了
6.学到了kadane





