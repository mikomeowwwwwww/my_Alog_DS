# Assignment #7: 矩阵、队列、贪心

Updated 1315 GMT+8 Oct 21, 2025

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

### M12560: 生存游戏

matrices, http://cs101.openjudge.cn/pctbook/M12560/

思路：



代码

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



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251028153006.png]]




### M04133:垃圾炸弹

matrices, http://cs101.openjudge.cn/pctbook/M04133/

思路：



代码

```python
d = int(input())
n = int(input())
a = []
left = 1024
right = 0
up = 0
down = 1024
m = 0
c = 0
for i in range(n):
    b = list(map(int, input().split()))
    left = min(left,b[0])
    right = max(right,b[0])
    up = max(up,b[1])
    down = min(down,b[1])
    a.append(b)
for i in range(max(0,left-d),min(1024,right+d)+1):
    for j in range(max(0,down-d),min(1024,up+d)+1):
        x = 0
        for k in a:
            if abs(k[0]-i) <= d and abs(k[1]-j) <= d:
                x += k[2]
        if x > m:
            m = x
            c = 1
        elif x == m:
            c += 1
print(str(c)+" "+str(m))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251028153040.png]]




### M02746: 约瑟夫问题

implementation, queue, http://cs101.openjudge.cn/pctbook/M02746/

思路：



代码

```python
import sys

def josephus(n, m):
    if n == 1:
        return 1  # 1-based编号
    return (josephus(n-1, m) + m - 1) % n + 1

while True:
    a = list(map(int, sys.stdin.readline().strip().split()))
    if not sum(a):
        break
    n = a[0]
    m = a[1]
    print(josephus(n, m))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251028153103.png]]




### M26976:摆动序列

greedy, http://cs101.openjudge.cn/pctbook/M26976/


思路：



代码

```python
n = int(input())
m = list(map(int, input().split()))
if n == 0 or n == 1:
    print(n)
else:
    c = 0
    x = 0
    for i in range(1, n):
        if x ==0 and m[i] != m[i - 1]:
            x = m[i] - m[i - 1]
            c += 1
        elif x != 0 and (m[i] - m[i - 1])*x < 0:
            x = m[i] - m[i - 1]
            c += 1
    print(c+1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251028153129.png]]




### T26971:分发糖果

greedy, http://cs101.openjudge.cn/pctbook/T26971/

思路：



代码

```python
n = int(input())
m = list(map(int, input().split()))
a = [1]*n
for i in range(1,n):
    if m[i] > m[i-1]:
        a[i] = a[i-1]+1
m.reverse()
a.reverse()
for i in range(1,n):
    if m[i] > m[i-1]:
        a[i] = max(a[i-1]+1, a[i])
print(sum(a))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251028153206.png]]




### 1868A. Fill in the Matrix

constructive algorithms, implementation, 1300, https://codeforces.com/problemset/problem/1868/A

思路：



代码

```python
t = int(input())
for i in range(t):
    n, m = map(int, input().split())
    if m == 1:
        for j in range(n+1):
            print(0)
        continue
    if n >= m-1:
        print(m)
        a = [i for i in range(m)]
        for j in range(1, m):
            for k in range(j, j+m):
                print(a[k%m], end=" ")
            print()
        for j in range(n-m+1):
            for k in range(1, m+1):
                print(a[k%m], end=" ")
            print()
    else:
        print(n+1)
        a = [i for i in range(n+1)]
        for j in range(1, n+1):
            for k in range(j, j+n+1):
                print(a[k % (n+1)], end=' ')
            for k in range(n+1, m):
                print(k, end=' ')
            print()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251028153304.png]]




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
无额外习题
1.在外层包裹一层0
2.通过优化减少计算
3.使用了ai，主要是递归与数学方法
4.运用数学思维（函数的增减性）
5.两层约束（先从左到右，再从右到左）
6.画图，找规律




