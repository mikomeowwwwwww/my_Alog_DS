# Assignment #D: Mock Exam下元节

Updated 1729 GMT+8 Dec 4, 2025

2025 fall, Complied by <mark>同学的姓名、院系</mark>



>**说明：**
>
>1. Dec⽉考： AC6<mark>（请改为同学的通过数）</mark> 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。
>
>2. 解题与记录：对于每一个题目，请提供其解题思路（可选），并附上使用Python或C++编写的源代码（确保已在OpenJudge， Codeforces，LeetCode等平台上获得Accepted）。请将这些信息连同显示“Accepted”的截图一起填写到下方的作业模板中。（推荐使用Typora https://typoraio.cn 进行编辑，当然你也可以选择Word。）无论题目是否已通过，请标明每个题目大致花费的时间。
>
>3. 提交安排：提交时，请首先上传PDF格式的文件，并将.md或.doc格式的文件作为附件上传至右侧的“作业评论”区。确保你的Canvas账户有一个清晰可见的本人头像，提交的文件为PDF格式，并且“作业评论”区包含上传的.md或.doc附件。
> 
>4. 延迟提交：如果你预计无法在截止日期前提交作业，请提前告知具体原因。这有助于我们了解情况并可能为你提供适当的延期或其他帮助。  
>
>请按照上述指导认真准备和提交作业，以保证顺利完成课程要求。





## 1. 题目

### E29945:神秘数字的宇宙旅行 

implementation, http://cs101.openjudge.cn/practice/29945

思路：



代码

```python
n = int(input())
while n != 1:
    if n % 2 == 0:
        print(str(n) + "/2=" + str(n//2))
        n = n // 2
    else:
        print(str(n) + "*3+1=" + str(n*3+1))
        n = n*3+1
print('End')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251209181607.png]]




### E29946:删数问题

monotonic stack, greedy, http://cs101.openjudge.cn/practice/29946

思路：



代码

```python
n = [int(i) for i in list(input().strip())]
k = int(input())
num = len(n) - k
c = []
idx = -1
while True:
    if num == 0:
        break
    mid = []
    for i in range(idx+1, len(n)-num+1):
        mid.append(n[i])
    c.append(min(mid))
    idx += mid.index(min(mid))+1
    num -= 1
c = int(''.join(map(str, c)))
print(c)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251209181625.png]]




### E30091:缺德的图书馆管理员

greedy, http://cs101.openjudge.cn/practice/30091

思路：



代码

```python
L = int(input())
N = int(input())
s = list(map(int, input().split()))
min_num = 0
max_num = 0
for i in range(N):
    min_num = max(min_num, min(s[i], L - s[i]+1))
    max_num = max(max_num, s[i], L - s[i]+1)
print(str(min_num) + ' ' + str(max_num))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251209181729.png]]




### M27371:Playfair密码

simulation，string，matrix, http://cs101.openjudge.cn/practice/27371


思路：



代码

```python
def get_matrix(keyword):
    alphabet = 'abcdefghiklmnopqrstuvwxyz'
    matrix = []
    mid = []
    marker = set()
    for letter in keyword:
        if letter not in marker:
                mid.append(letter)
                marker.add(letter)
        if len(mid) == 5:
            matrix.append(mid)
            mid = []
    for letter in alphabet:
        if letter not in marker:
            mid.append(letter)
            marker.add(letter)
        if len(mid) == 5:
            matrix.append(mid)
            mid = []
    return matrix

def trans_plaintext(plaintext):
    idx = 0
    translated = []
    while idx < len(plaintext):
        if idx < len(plaintext)-1:
            if plaintext[idx] == plaintext[idx+1]:
                if plaintext[idx] == 'x':
                    s1 = 'x'
                    s2 = 'q'
                else:
                    s1 = plaintext[idx]
                    s2 = 'x'
                idx += 1
            else:
                s1 = plaintext[idx]
                s2 = plaintext[idx+1]
                idx += 2
        else:
            if plaintext[idx] == 'x':
                s1 = 'x'
                s2 = 'q'
            else:
                s1 = plaintext[idx]
                s2 = 'x'
            idx += 1
        mid = [s1, s2]
        translated.append(mid)
    return translated

def get_x_y(matrix, pair):
    locations = []
    for i in range(5):
        for j in range(5):
            if matrix[i][j] == pair[0]:
                locations.append([i, j])
    for i in range(5):
        for j in range(5):
            if matrix[i][j] == pair[1]:
                locations.append([i, j])
    return locations

def code_text(matrix,translated):
    coded = []
    for pair in translated:
        locations = get_x_y(matrix,pair)
        x1, y1, x2, y2 = locations[0][0], locations[0][1], locations[1][0], locations[1][1]
        if x1 == x2:
            y1 += 1
            y2 += 1
            y1 %= 5
            y2 %= 5
            coded.append(matrix[x1][y1])
            coded.append(matrix[x2][y2])
        elif y1 == y2:
            x1 += 1
            x2 += 1
            x1 %= 5
            x2 %= 5
            coded.append(matrix[x1][y1])
            coded.append(matrix[x2][y2])
        else:
            coded.append(matrix[x1][y2])
            coded.append(matrix[x2][y1])
    return coded


keyword = input().strip().replace('j','i')
matrix = get_matrix(keyword)
n = int(input())
for i in range(n):
    plaintext = input().strip().replace('j','i')
    translated = trans_plaintext(plaintext)
    coded = code_text(matrix,translated)
    print(*coded,sep='')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251209181754.png]]




### T30201:旅行售货商问题

dp,dfs, http://cs101.openjudge.cn/practice/30201

思路：



代码

```python
n = int(input())
cost = [list(map(int, input().split())) for _ in range(n)]

INF = float('inf')
# dp[mask][u]: mask是已访问城市的集合，u是当前所在城市
dp = [[INF] * n for _ in range(1 << n)]
dp[1 << 0][0] = 0  # 从城市0出发

for mask in range(1 << n):
    for u in range(n):
        if not (mask & (1 << u)):
            continue  # u不在当前集合中，跳过
        if dp[mask][u] == INF:
            continue
        # 枚举未访问的城市v
        for v in range(n):
            if mask & (1 << v):
                continue
            new_mask = mask | (1 << v)
            if dp[new_mask][v] > dp[mask][u] + cost[u][v]:
                dp[new_mask][v] = dp[mask][u] + cost[u][v]

# 所有城市都访问过，返回起点0
result = INF
full_mask = (1 << n) - 1
for u in range(n):
    result = min(result, dp[full_mask][u] + cost[u][0])

print(result)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251209182140.png]]




### T30204:小P的LLM推理加速

greedy, http://cs101.openjudge.cn/practice/30204

思路：



代码

```python
n, m = map(int, input().split())
c = []
min_twice = float('inf')
for i in range(n):
    xi, yi = map(int, input().split())
    c.append(xi)
    min_twice = min(min_twice, xi+yi)
c.sort()
temp_sum = 0
max_t = 0
temp_t = 0
if sum(c) <= m:
    temp_sum = sum(c)
    max_idx = n-1
else:
    for i in range(n):
        temp_sum += c[i]
        if temp_sum > m:
            max_idx = i - 1
            temp_sum -= c[i]
            break
temp_t = max_idx+1
max_t = temp_t
for i in range(max_idx, -1, -1):
    temp_t -= 1
    temp_sum -= c[i]
    temp_t += (m-temp_sum)//min_twice*2
    temp_sum = m-(m-temp_sum)%min_twice
    max_t = max(max_t, temp_t)
print(max_t)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20251209181901.png]]




## 2. 学习总结和收获

如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。
无额外练习
1.无
2.题目未详细说明，导致我未考虑数字不合法的情况，考试时一直做不出来，结束后在微信群看了才知道
3.无
4.太长且难debug，耗费时间太久
5.不会做，交给ai了
6.感觉不是很难，想了大概半小时吧，考试时根本没时间看




