# Assignment #5: 20251009 cs101 Mock Exam寒露第二天

Updated 1651 GMT+8 Oct 9, 2025

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

### E29895: 分解因数

implementation, http://cs101.openjudge.cn/practice/29895/



思路：
用时5min


代码

```python
# 
n = int(input())
if n == 1:
    print(1)
elif n == 2:
    print(2)
for i in range(2,n):
    if n%i == 0:
        print(int(n/i))
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-10 153649.png]]




### E29940: 机器猫斗恶龙

greedy, http://cs101.openjudge.cn/practice/29940/



思路：
用时5min


代码

```python
n = int(input())
m = list(map(int, input().split()))
minhp = 0
counter = 0
for i in m:
    counter += i
    if counter < minhp:
        minhp = counter
print(1-minhp)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-10 153833 1.png]]




### M29917: 牛顿迭代法

implementation, http://cs101.openjudge.cn/practice/29917/



思路：
用时20min


代码

```python
import sys

while True:
    n = sys.stdin.readline().strip()
    if not n:
        break
    n = float(n)
    x1 = 1
    x2 = x1 - (x1**2-n)/(2*x1)
    counter = 1
    while abs(x1 - x2) > 1E-6:
        x1 = x2
        x2 = x1 - (x1**2-n)/(2*x1)
        counter += 1
    print(counter, "{:.2f}".format(x1))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-10 154035.png]]




### M29949: 贪婪的哥布林

greedy, http://cs101.openjudge.cn/practice/29949/


思路：
用时10min


代码

```python
# 
N, M = map(int, input().split())
a = {}
for i in range(N):
    v, w = map(int, input().split())
    if v/w in a:
        a[v/w] += w
    else:
        a[v/w] = w
b = list(a.items())
b.sort()
b.reverse()
value = 0
for i in range(len(b)):
    if M == 0:
        break
    m = max(0, M-b[i][1])
    value += (M-m)*b[i][0]
    M = m
print("{:.2f}".format(value))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-10 154226.png]]




### M29918: 求亲和数

implementation, http://cs101.openjudge.cn/practice/29918/



思路：
问了ai


代码

```python
n = int(input())
num_sum = [0]*(n+1)
a = []
for i in range(1,n//2+1):
    for j in range(i*2,n+1,i):
        num_sum[j] += i
for i in range(1,n+1):
    if num_sum[i] <=n and num_sum[num_sum[i]] == i and num_sum[i] != i and num_sum[i] > i:
        a.append((min(num_sum[i],i),max(num_sum[i],i)))
for i in a:
    print(i[0], i[1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-10 154422.png]]




### T29947:校门外的树又来了（选做）

http://cs101.openjudge.cn/practice/29947/



思路：
用时3h+


代码

```python
def is_mergeable(a, b):
    if a[0]-1 <= b[0] <= a[1]+1 or a[0]-1 <= b[0] <= a[1]+1 or b[0]-1 <= a[0] <= b[1]+1 or b[0]-1 <= a[1] <= b[1]+1:
        return True
    else:
        return False

def merge(a):
    return [min(i[0] for i in a),max(i[1] for i in a)]

L,M = map(int, input().split())
roads = []
for i in range(M):
    road = list(map(int, input().split()))
    mergeable = []
    unmergeable = []
    for j in roads:
        if is_mergeable(j, road):
            mergeable.append(j)
        else:
            unmergeable.append(j)
    mergeable.append(road)
    merged_road = merge(mergeable)
    roads.clear()
    roads.extend(unmergeable)
    roads.append(merged_road)
length = 0
for r in roads:
    length += r[1]-r[0]+1
print(L-length+1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-10 154525.png]]




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
无额外练习
1.无
2.无
3.看题，n可能是小数，用int ()会爆RE,以及格式化输出
4.同上，格式化输出
5.之前思路是暴力求出每个数因数再加起来，ai提供的思路没想到，但确实非常巧妙
6.时间长是因为思路错了，换了思路之后大概半小时到一小时做出来




