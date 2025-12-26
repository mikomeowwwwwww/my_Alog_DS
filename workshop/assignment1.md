# Assignment #1: 自主学习

Updated 1306 GMT+8 Sep 14, 2025

2025 fall, Complied by 李鑫，医学部



**作业的各项评分细则及对应的得分**

| 标准                  | 等级                                                                       | 得分  |
| ------------------- | ------------------------------------------------------------------------ | --- |
| 按时提交                | 完全按时提交：1分<br/>提交有请假说明：0.5分<br/>未提交：0分                                    | 1 分 |
| 源码、耗时（可选）、解题思路（可选）  | 提交了4个或更多题目且包含所有必要信息：1分<br/>提交了2个或以上题目但不足4个：0.5分<br/>少于2个：0分              | 1 分 |
| AC代码截图              | 提交了4个或更多题目且包含所有必要信息：1分<br/>提交了2个或以上题目但不足4个：0.5分<br/>少于：0分                | 1 分 |
| 清晰头像、PDF文件、MD/DOC附件 | 包含清晰的Canvas头像、PDF文件以及MD或DOC格式的附件：1分<br/>缺少上述三项中的任意一项：0.5分<br/>缺失两项或以上：0分 | 1 分 |
| 学习总结和个人收获           | 提交了学习总结和个人收获：1分<br/>未提交学习总结或内容不详：0分                                      | 1 分 |
| 总得分： 5              | 总分满分：5分                                                                  |     |

>
>
>
>**说明：**
>
>1. **解题与记录：**
>
>   对于每一个题目，请提供其解题思路（可选），并附上使用Python或C++编写的源代码（确保已在OpenJudge， Codeforces，LeetCode等平台上获得Accepted）。请将这些信息连同显示“Accepted”的截图一起填写到下方的作业模板中。（推荐使用Typora https://typoraio.cn 进行编辑，当然你也可以选择Word。）无论题目是否已通过，请标明每个题目大致花费的时间。
>
>2. **课程平台：**课程网站位于Canvas平台（https://pku.instructure.com ）。该平台将在<mark>第2周</mark>选课结束后正式启用。在平台启用前，请先完成作业并将作业妥善保存。待Canvas平台激活后，再上传你的作业。
>
>3. **提交安排：**提交时，请首先上传PDF格式的文件，并将.md或.doc格式的文件作为附件上传至右侧的“作业评论”区。确保你的Canvas账户有一个清晰可见的本人头像，提交的文件为PDF格式，并且“作业评论”区包含上传的.md或.doc附件。
>
>4. **延迟提交：**如果你预计无法在截止日期前提交作业，请提前告知具体原因。这有助于我们了解情况并可能为你提供适当的延期或其他帮助。  
>
>请按照上述指导认真准备和提交作业，以保证顺利完成课程要求。





## 1. 题目

### E02733: 判断闰年

http://cs101.openjudge.cn/pctbook/E02733/



思路：



代码

```python
a = int(input())
if a%4 != 0 :
    print("N")
elif a%100 != 0 :
    print("Y")
elif a%400 != 0 :
    print("N")
elif a%3200 != 0 :
    print("Y")
else :
    print("N")
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>


![[QQ20250910-220625.png]]


### E02750: 鸡兔同笼

http://cs101.openjudge.cn/pctbook/E02750/



思路：



代码

```python
a = int(input())
if a==0:
    print("0 0")
elif a%2!=0 :
    print("0 0")
else :
    print(int(a%4/2+a//4),int(a/2))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[QQ20250910-222825.png]]




### 50A. Domino piling

greedy, math, 800, http://codeforces.com/problemset/problem/50/A



思路：



代码

```python
M,N = (input().split())
M = int(M)
N = int(N)
if M*N==1 :
    print(0)
elif M%2==0 or N%2==0:
    print(int(M*N/2))
else:
    print(int((M*N-1)/2))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-09-21 162804.png]]




### 1A. Theatre Square

math, 1000, https://codeforces.com/problemset/problem/1/A



思路：



代码

```python
import math
n,m,a = input().split()
n = int(n)
m = int(m)
a = int(a)
print(math.ceil(n/a)*math.ceil(m/a))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-09-21 162830.png]]




### 112A. Petya and Strings

implementation, strings, 1000, http://codeforces.com/problemset/problem/112/A



思路：



代码

```python
str1 = input().lower()
str2 = input().lower()
if str1 == str2:
    print(0)
else:
    for i in range(0, len(str1)):
        if str1[i]  < str2[i]:
            print(-1)
            break
        elif str1[i] > str2[i]:
            print(1)
            break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-09-21 162916.png]]




### 231A. Team

bruteforce, greedy, 800, http://codeforces.com/problemset/problem/231/A



思路：



代码

```python
n = int(input())
answer = 0
for i in range(0,n):
    a,b,c = input().split()
    a,b,c = int(a),int(b),int(c)
    if a+b+c >= 2 :
        answer += 1
print(answer)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-09-21 162944.png]]




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
无额外练习题
1.if,elif,else的运用
2.涉及 /的运算结果均为float型，输出时需要强制类型转换
3.无
4.import的使用方法，以及math中ceil方法的使用(向上取整)
5.字符串lower方法的使用(所有字母转换为小写),以及字符串可直接用\==比较
6.无



[^1]: 
