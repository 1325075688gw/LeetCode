## 找出数值中前k大

#### 1.题目

#### 2.分析

- 通过分析，最大的前三个数比数值中其其它数都大，因此可以采用类似求最大值的方法来求前三名。初始化前三名为最小整数：r1,r2,r3。
- 然后遍历数组
- 如果当前值tmp > r1:r3=r2,r2=r1,r1=tmp
- 如果当前值tmp>r2且不等于r1：r3=r2,r2=tmp
- 如果当前值tmp大于r3且不等于r2,r3 = tmp

#### 3.代码1

- ```python
  def findTop3(li):
      if li == None or len(li) < 3:
          return 
      r1 = r2 = r3 = -2**31
      i = 0 
      while i < len(li):
          if li[i]>r1:
              r3,r2,r1 = r2,r1,li[i]
  		elif li[i]>r2:
              r3,r2 = r2,li[i]
          else:
              r3 = li[i]
          i += 1
  	print("前三名："+str(r1)+","+str(r2)+","+str(r3))
  findTop([2,3,4,45,5,5])

  ```

####  代码2（堆排序）

- ```python
  import heapq
  li = list(range(10))
  random.shuffle(li)
  def topk(li, k):
      tmp = li[:k]
      heapq.heapify(tmp)
      for i in li[k:]:
          if i < tmp[0]:
              pass
          else:
  #             heapq.heappop(tmp)
  #             tmp.append(i)
  #             heapq.heapify(tmp)

              heapq.heapreplace(tmp, i) # 小根堆,先加进去，再把最小的输出去丢掉
      print(tmp)
      for i in range(k):
          print(heapq.heappop(tmp))
  #     print(tmp)
  topk(li,5)
  ```

  ​

