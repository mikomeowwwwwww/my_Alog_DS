# Assignment #3: 语法练习

Updated 1440 GMT+8 Sep 23, 2025

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

### E28674:《黑神话：悟空》之加密

http://cs101.openjudge.cn/pctbook/E28674/



思路：



代码

```python
# 
k = int(input())%26
s = input()
upper_c = {}
lower_c = {}
for i in range(ord("A"), ord("Z")+1):
    upper_c[chr(i)] = i%26
for i in range(ord("a"), ord("z")+1):
    lower_c[chr(i)] = i%26
upper_d = {}
lower_d = {}
for i in range(ord('A'), ord('Z')+1):
    upper_d[i%26] = chr(i)
for i in range(ord('a'), ord('z')+1):
    lower_d[i%26] = chr(i)
a = []
for c in s:
    if c.isupper():
        a.append(upper_d[(upper_c[c]-k)%26])
    else:
        a.append(lower_d[(lower_c[c]-k)%26])
print(''.join(a))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-07 172942.png]]




### E28691: 字符串中的整数求和

http://cs101.openjudge.cn/pctbook/E28691/



思路：



代码

```python
a, b = input().split()
print(int(a[0])*10+int(a[1])+int(b[0])*10+int(b[1]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-07 173026.png]]




### M28664: 验证身份证号 

http://cs101.openjudge.cn/pctbook/M28664/



思路：



代码

```python
n = int(input())
m = [7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2]
a = ['1','0','X','9','8','7','6','5','4','3','2']
for i in range(n):
    k = input()
    l = 0
    for j in range(0,17):
        l += int(k[j])*m[j]
    if k.endswith(str(a[l%11])):
        print("YES")
    else:
        print("NO")
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-07 173141.png]]




### M28678: 角谷猜想

http://cs101.openjudge.cn/pctbook/M28678/


思路：



代码

```python
# 
n = int(input())
while n != 1:
    if n % 2 == 0:
        print(str(n) + "/2=" + str(int(n/2)), end="\n")
        n = int(n/2)
    else:
        print(str(n) + "*3+1=" + str(int(n*3+1)), end="\n")
        n = int(n*3+1)
print("End")
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-07 173220.png]]




### M28700: 罗马数字与整数的转换

http://cs101.openjudge.cn/pctbook/M28700/



思路：



代码

```python
def roman_to_int(s):
    roman_map = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
    total = 0
    n = len(s)
    for i in range(n):
        if i < n - 1 and roman_map[s[i]] < roman_map[s[i+1]]:
            total -= roman_map[s[i]]
        else:
            total += roman_map[s[i]]
    return total
def int_to_roman(num):
    roman_list = [(1000, 'M'), (900, 'CM'), (500, 'D'), (400, 'CD'),
                  (100, 'C'), (90, 'XC'), (50, 'L'), (40, 'XL'),
                  (10, 'X'), (9, 'IX'), (5, 'V'), (4, 'IV'), (1, 'I')]
    roman_str = ''
    for value, symbol in roman_list:
        while num >= value:
            roman_str += symbol
            num -= value
    return roman_str
s = input().strip()
if s.isnumeric():
    num = int(s)
    print(int_to_roman(num))
else:
    print(roman_to_int(s))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-07 173351.png]]




### 158B. Taxi

*special problem, greedy, implementation, 1100,  https://codeforces.com/problemset/problem/158/B



思路：



代码

```python
import math
n = int(input())
s = input()
s1 = s.count('1')
s2 = s.count('2')
s3 = s.count('3')
s4 = s.count('4')
if s1 > s3:
    if s2%2 == 0:
        print(s4+s3+int(s2/2)+int(math.ceil((s1-s3)/4)))
    elif s1 - s3 > 2:
        print(s4+s3+int(math.ceil(s2/2))+int(math.ceil((s1-s3-2)/4)))
    else :
        print(s4+s3+int(math.ceil(s2/2)))
else:
    print(s4+s3+int(math.ceil(s2/2)))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Screenshot 2025-10-07 173441.png]]




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
无额外练习题
1.用ord()得到字符对应的ascii码，用isupper()判断大小写
2.无
3.用endswith()判断字符串结尾
4.无
5.了解罗马数字与阿拉伯数字的转换方法
6.无




