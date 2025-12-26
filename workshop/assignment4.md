# Assignment #4: T-primes + 贪心

Updated 1814 GMT+8 Sep 30, 2025

2025 fall, Complied by 李鑫，医学部



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

### 34B. Sale

greedy, sorting, 900, https://codeforces.com/problemset/problem/34/B



思路：



代码

```python
# 
n, m = map(int, input().split())
tv = list(map(int, input().split()))
price = 0
for i in range(m):
    if min(tv) < 0:
        price -= min(tv)
        del tv[tv.index(min(tv))]
    else:
        break
print(price)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-07 174256.png]]




### 160A. Twins

greedy, sortings, 900, https://codeforces.com/problemset/problem/160/A



思路：



代码

```python
n = int(input())
coin = list(map(int, input().split()))
sum = sum(coin)
summing = 0
counter = 0
while summing <= sum/2:
    summing += max(coin)
    counter += 1
    del coin[coin.index(max(coin))]
print(counter)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-07 174345.png]]




### 1879B. Chips on the Board

constructive algorithms, greedy, 900, https://codeforces.com/problemset/problem/1879/B



思路：



代码

```python
n = int(input())
for i in range(n):
    j = int(input())
    s1 = list(map(int, input().split()))
    s2 = list(map(int, input().split()))
    print(min(min(s1)*j+sum(s2),min(s2)*j+sum(s1)))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-07 180842.png]]




### M01017: 装箱问题

greedy, http://cs101.openjudge.cn/pctbook/M01017/


思路：



代码

```python
# 
import sys
import math

while True:
    s = list(map(int, sys.stdin.readline().strip().split()))
    if not s:
        break
    if sum(s) == 0:
        break
    for i in range(s[4]):
        if s[0]-11 >= 0:
            s[0] -= 11
        else:
            s[0] = 0
            break
    for i in range(s[3]):
        if s[1]-5 >= 0:
            s[1] -= 5
        elif s[1]*4+s[0]-20 >= 0:
            s[0] -= 20-s[1]*4
            s[1] = 0
        else:
            s[1] = 0
            s[0] = 0
            break
    s1 = s[0]%36
    s2 = s[1]%9
    s3 = s[2]%4
    if s3 == 0:
        s0 = int(math.ceil((s1+s2*4)/36))
    elif s3 == 1:
        if s2 >= 5:
            s2 -= 5
            if s1>= 7:
                s1 -= 7
                s0 = int(math.ceil((s1+s2*4)/36))+1
            else:
                s1 = 0
                s0 = int(math.ceil((s1+s2*4)/36))+1
        else:
            s1 -= 7+4*(5-s2)
            if s1 < 0:
                s1 = 0
            s2 = 0
            s0 = int(math.ceil((s1+s2*4)/36))+1
    elif s3 == 2:
        if s2 >= 3:
            s2 -= 3
            if s1>= 6:
                s1 -= 6
                s0 = int(math.ceil((s1+s2*4)/36))+1
            else:
                s1 = 0
                s0 = int(math.ceil((s1+s2*4)/36))+1
        else:
            s1 -= 6+4*(3-s2)
            if s1 < 0:
                s1 = 0
            s2 = 0
            s0 = int(math.ceil((s1+s2*4)/36))+1
    elif s3 == 3:
        if s2 >= 1:
            s2 -= 1
            if s1>= 5:
                s1 -= 5
                s0 = int(math.ceil((s1+s2*4)/36))+1
            else:
                s1 = 0
                s0 = int(math.ceil((s1+s2*4)/36))+1
        else:
            s1 -= 5+4*(1-s2)
            if s1 < 0:
                s1 = 0
            s2 = 0
            s0 = int(math.ceil((s1+s2*4)/36))+1
    print(s[5]+s[4]+s[3]+int(s[2]//4)+int(s[1]//9)+int(s[0]//36)+s0)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-07 202755.png]]




### M01008: Maya Calendar

implementation, http://cs101.openjudge.cn/practice/01008/



思路：



代码

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### 230B. T-primes（选做）

binary search, implementation, math, number theory, 1300, http://codeforces.com/problemset/problem/230/B



思路：



代码

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
无额外练习题
1.无
2.无
3.题中条件可进行转换，如本题可转换为每行至少有一个或每列至少有一个chip
4.分类讨论，如本题在安排完6\*6, 5\*5,4\*4后，分类讨论3\*3,2\*2,1\*1的放置情况




