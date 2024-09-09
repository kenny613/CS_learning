## Coding
---
https://www.studocu.com/row/document/university-of-central-punjab/safe-agile-software-engineer-ase/pc-question-asfasf/88383726
-  [Prime factor visitation](https://stackoverflow.com/questions/70935535/prime-factor-visitation-flipping-states-based-on-prime-factors)
	- https://www.1point3acres.com/bbs/thread-796294-1-1.html
	- 刚刚写完就来发帖了，第一题是portfolio balance，本质上就是刷题网叁柒壹，只需要注意他是1-index开始的就可以了，-1就能搞定了，网上很多解法。
第二题是prime factors visitation，花了我超多时间。截止到我发帖为止，网上现存的任何一种解法都无法直接全pass，剩下的全部timeout，包括某个chegg的答案，和地里很多的优化后答案集。我全部试了一遍，最好的也就只能pass一半而已。一直试错导致我浪费了很多时间，到只剩20分钟才开始自己优化，不过还是要感谢这些前辈们的贡献。
下面是我的解法：首先用一个map来记录下<prime factor, occurance>。比如[2,4,6,8]就会记录下<2, 4>和<3,1>。注意在找每一个数的prime factor的时候不要重复记录了，比如8虽然有三个2，但是在map里只加一次。然
	- start to divide by 2, 3 .... (Prime factoriazstion)

assume 最多只可以有一個prime factor > sqrt(n) 
```python
b  = [1,1,1,1,1,11,1,1,11,1,1,1,1...]


nums = [2,6]
primes_freq = {2 : 2, 3 : 1}

def solution(states, nums)
	for i in range(len(states)) # 
	    
	    total_flips = 0
	    
	    primes = genereate_primes_lst(i + 1) # 6 -> 2,3
	    # get total flip by getting occurance of all prime factoers of b[i+1]
	    for prime in primes:
	        total_flips += primes_freq.get(prime, 0)
	    if total_flips % 2 == 1:
	        b[i] = 1 - b[i]
        
i == 5
primes = genereate_primes_lst(2) = 2, 3
for i in [2,3]:
    # i = 2
    flips += primes_freq.get(prime, 0) = 2
```

[547. Number of Provinces](https://leetcode.com/problems/number-of-provinces/)
DFS



网投之后给了个DATA ENGINEER岗位的OA，要求3小时4道题，不过比较简单，一个小时就写完了。
1. 给两个array nums和queries，对于queries里面的每个值q，要求找到nums里面从第q个element开始到结束的subarry的最大的element的出现次数，把结果放在array里面返回。
    e.g. nums = [4,3,3,1,2], queries = [1,2,3,4,5]
    q = 1的时候，subarray就是[4,3,3,1,2]，最大的数字是4，出现了1次，所以第一个结果是1；
    q = 2的时候，subarray就是[3,3,1,2]，最大的数字是3，出现了2次，所以第二个结果是2；
    q = 3的时候，subarray就是[3,1,2]，最大的数字是3，出现了1次，所以第三个结果是1；
   以此类推，最后的结果就是[1,2,1,...]
    从后往前traverse，遇到新的数字如果大于之前的最大值就更新最大值，出现次数reset到1，把1加到结果里；如果等于之前最大值就把出现次数+1，同样把次数加到结果里；如果小于最大值，就不更新次数，直接加到结果里。
2. SQL题目。给了一个table，里面四个column: client, protocol, input_cnt, output_cnt, 要求结果是每个client一行，把每个client用到的protocol组成一个string，用逗号隔开。同一个client的不同Protocol按in
https://www.1point3acres.com/bbs/thread-859534-1-1.html
https://www.geeksforgeeks.org/queries-to-count-occurrences-of-maximum-array-element-in-subarrays-starting-from-given-indices/
```python
```

DP题：假设某股票未来T个时间点的价格变化为（P1P2P3PT）每次咱要么1）买1股2）卖n股n小于等于持仓3）啥也不做算最优盈利我直接用迭代也过了所有的测试用例所以题目没有space的要求记得用哈希表就行了

## Knoewldege
---
线性回归，如果数据重复了什么会变化，什么不会变化?
ridge&lasso的区别，有没有解析解?
Tree模型原理是什么，如果选fea‍
[‌‌‌‌‌‍̴https://www.1point3acres.com/bbs/thread-989081-1-1.html]

1. 问我CTE是什么。为啥要问我缩写啊？？common table expression，就是SQL里的WITH （SQL query to create a table）。只会写，从来不知道他叫这个名字-baidu 1point3acres
2. 问我为什么relational databases要用SQL不用Python…咱就是说那些data warehouse也只支持SQL啊AWS Athena Microsoft Azure GCP big query也没允许我用python查数据…原因就是multi spreading/scalability，能
[https://www.1point3acres.com/bbs/thread-988464-1-1.html]



![[Pasted image 20240827024614.png|500]]

![[Pasted image 20240827024643.png|500]]
1. What are hash tables and how are they implemented in Python?
2. What is the advantage of a hash table vs. a list?
3. What's the complexity of insertion into a hash table?
4. How to derive black scholes equation and what
https://www.1point3acres.com/bbs/thread-982809-1-1.html

一个千禧年的OA，面的是developer的职位，猎头联系的，OA一共两个小时，五道题，其他四题都很简单，包括一个sql的基础题，一道python题写一个decorator，不过最后一道题我只过了80%的test case，题目是这样，请教大家这题咋做：
There are m jobs to schedule on n processors. A schedule is balanced if the difference between the number of jobs scheduled on any two neighboring processors does not exceed 1. The kth processor is the most efficient and thus, the maximum number of jobs should be scheduled on that process

https://www.1point3acres.com/bbs/thread-1079245-1-1.html