# Assignment #9: Mock Exam立冬前一天

Updated 1658 GMT+8 Nov 6, 2025

2025 fall, Complied by <mark>同学的姓名、院系</mark>



>**说明：**
>
>1. Nov⽉考： AC6<mark>（请改为同学的通过数）</mark> 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。
>
>2. 解题与记录：对于每一个题目，请提供其解题思路（可选），并附上使用Python或C++编写的源代码（确保已在OpenJudge， Codeforces，LeetCode等平台上获得Accepted）。请将这些信息连同显示“Accepted”的截图一起填写到下方的作业模板中。（推荐使用Typora https://typoraio.cn 进行编辑，当然你也可以选择Word。）无论题目是否已通过，请标明每个题目大致花费的时间。
>
>3. 提交安排：提交时，请首先上传PDF格式的文件，并将.md或.doc格式的文件作为附件上传至右侧的“作业评论”区。确保你的Canvas账户有一个清晰可见的本人头像，提交的文件为PDF格式，并且“作业评论”区包含上传的.md或.doc附件。
> 
>4. 延迟提交：如果你预计无法在截止日期前提交作业，请提前告知具体原因。这有助于我们了解情况并可能为你提供适当的延期或其他帮助。  
>
>请按照上述指导认真准备和提交作业，以保证顺利完成课程要求。





## 1. 题目

### E29982:一种等价类划分问题

hashing, http://cs101.openjudge.cn/practice/29982

思路：



代码

```python
m, n, k = map(int, input().split(","))
d = {}
for i in range(m+1,n):
    j = str(i)
    c = 0
    for _ in j:
        c += int(_)
    if c%k == 0:
        if c in d:
            d[c].append(j)
        else:
            d[c] = [j]
a = sorted(d.keys())
for i in a:
    print(",".join(d[i]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251111192446.png]]




### E30086:dance

greedy, http://cs101.openjudge.cn/practice/30086

思路：



代码

```python
N, D = map(int, input().split())
s = list(map(int, input().split()))
s.sort()
c = 1
able = True
for i in range(2*N-1):
    if s[i+1] - s[i] <= D:
        c += 1
    else:
        if c%2 == 0:
            c = 1
        else:
            able = False
            break
print('Yes' if able else 'No')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251111192524.png]]




### M25570: 洋葱

matrices, http://cs101.openjudge.cn/practice/25570

思路：



代码

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### M28906:数的划分

dfs, dp, http://cs101.openjudge.cn/practice/28906


思路：



代码

```python
def f(n, k):
    if n < k:
        return 0
    if n == k or k == 1:
        return 1
    return f(n-k, k) + f(n - 1, k - 1)

n, k = map(int, input().split())
print(f(n, k))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251111192555.png]]




### M29896:购物

greedy, http://cs101.openjudge.cn/practice/29896

思路：



代码

```python
X, N = map(int, input().split())
coins = sorted(list(map(int, input().split())))
if coins[0] != 1:
    print(-1)
else:
    r = 0
    for c in range(X+1):
        if r >= X:
            print(c)
            break
        else:
            for i in range(N):
                if coins[i] > r+1:
                    r += coins[i-1]
                    break
                if i == N-1:
                    r += coins[i]
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251111192625.png]]




### T25353:排队

greedy, http://cs101.openjudge.cn/practice/25353

思路：



代码

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。
无额外练习
AC4
第一题看错了，浪费了很多时间
第二题很快做出来
第三题没写出来，没想到好的方法，最后看了ai
第四题做过一道类似的题，所以很快
第五题想了很久才想出来大概一个小时
第六题没时间，之后自己想也想不出来，问ai也写不出来






