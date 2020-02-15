# python 笔记



```python
print（'''
打印多行内容
'''）
```

```python
print('你叫{}，今年{}岁了'.format(name,age))
```

input（'输入'）

如果字符串中还有引号,记得在单引号后加入转义符\

print('he said "today \ 's weather is good"')

索引也可以是负数，最后一个字符的索引是-1倒数第二个就是-2

注释为#

%	取模	    返回除法的余数
**	幂	       返回 x 的 y 次幂
//	取整除	 返回商的整数部分（向下取整）

```python
if ss:
	elif xx：
	else xx：
```

```python
for ... in...:
while ... :   #循环
```

```python
# range(x) 生成一个从0~x-1的整数序列  
for i in range(10):
    print(i)	#结果是0~9
    
for a in range(1,11):
    print(a)	#结果是1~10
#range(a,b)  从a开始向后b-a个数
```

for循环适合一直循环次数的循环，所有后面跟的是次数或区间。

如果不知道要循环多少次才能达成目标，用while。

break 表示停止当前循环

```python
for a in range(10):
    if a == 5:
        break
    print(a)
```

continue 表示跳过当前循环轮次，去执行下一轮循环。

```python
a = 0
while a < 10:
    a = a + 1
    if a == 5:
        continue
    print(a)
```

