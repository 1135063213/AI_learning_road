# Python基础

## 1.表达

```python
# 寻求帮助
a=[5]
dir(a)         # 简单的列出对象a所包含的方法名称，返回一个字符串列表
help(a.__add__)   # 查询a.func的具体介绍和用法
#----------------------------------------------------------------------------------------
#数字的表达式操作符
    # yield x                                      # 生成器函数发送协议
def myplus(a):
    print("starting...")
    while(True):
        yield 4     #第一次next执行到return 4停止，第二次输出1 4
        print('a',a)
g=myplus(2)
print(next(g))
print(next(g))
print(g.send(5))
#----------------------------------------------------------------------------------------
    # lambda args: expression                      # 生成匿名函数
    # 匿名函数lambda：是指一类无需定义标识符（函数名）的函数或子程序。所谓匿名函数，
    # 通俗地说就是没有名字的函数，lambda函数没有名字，是一种简单的、在同一行中定义函数的方法。
f=lambda a,b,c,d:a*b*c*d
print(f(1,2,3,4))  #相当于下面这个函数
def test01(a,b,c,d):
    return a*b*c*d
print(test01(1,2,3,4))

g=[lambda a:a*2,lambda b:b*3]
print(g[0](5))  #调用
print(g[1](6))
    # x if y else z                                # 三元选择表达式
    # 这个用法的效果是，如果y真，返回x，否则返回z。而且这个用法是表达式，不是语句
f = lambda a,b:a+b if a>1 else a-b
print(f(2,3))
print(f(1,2))
#----------------------------------------------------------------------------------------
    # x and y, x or y, not x                       # 逻辑与、逻辑或、逻辑非   
    # x in y, x not in y                           # 成员对象测试
    # x is y, x is not y                           # 对象实体测试
    # x<y, x<=y, x>y, x>=y, x==y, x!=y             # 大小比较，集合子集或超集值相等性操作符
    # 1 < a < 3                                    # Python中允许连续比较
    # x|y, x&y, x^y, ~x                            # 位或、位与、位异或、位翻转
    # x<<y, x>>y                                   # 位操作：x左移、右移y位
    # 简单来说，按位运算就把数字转换为机器语言——二进制的数字来运算的一种运算形式
# 3&5                        
# 解法：3的二进制补码是 11,  5的是101, 3&5也就是011&101,先看百位(其实不是百位,这样做只是便于
# 理解)一个0一个1,根据(1&1=1，1&0=0，0&0=0，0&1=0)可知百位应该是1,同样十位上的数字1&0=0,个位
# 上的数字1&1=1,因此最后的结果是1.(这之后本来应该还有一步,因为我们现在得到的数值只是所求答案的
# 补码,但是因为正数的补码即是它本身,所以就省略了。不过,下面的例子就不能省略最后这一步了). 
# 3<<2
# 解法:11向左移动两位变为1100,即12 
# ~3
# 将二进制数+1之后乘以-1,3的二进制是11, -(11+1)=-100B=-4D. (注:B和D分别表示二进制和十进制).
# 10^15
# 对位相加,特别要注意的是不进位(1+1=0).1111^1010=0101,二进制0101得到十进制的结果是5.
    # +, -, *, /, //, %, **                        # 真除法、floor除法：返回不大于真除法结果
                                                   # 的整数值、取余、幂运算
    # -x, +x, ~x                                   # 一元减法、识别、按位求补（取反）
    # x[i], x[i:j:k], x(……)                        # 索引、分片、调用
    # int(3.14),  float(3)                         # 强制类型转换
#----------------------------------------------------------------------------------------
# 数字相关的模块
  # math模块
  # Decimal模块：小数模块
import decimal
from decimal import Decimal
decimal.getcontext().prec = 4            # 设置全局精度为4 即有效数字为4位
Decimal("0.01") + Decimal("0.02")        # 返回Decimal("0.03")  
  # Fraction模块：分数模块
from fractions import Fraction
x=Fraction(4,6)
y=Fraction(0.25)
```

## 2.变量和数据类型

```python
#python数据类型:哈希类型、不可哈希类型
   #哈希类型：不可变类型，可以用hash函数查看hash值，也可作为字典的key
     #"数字类型：int, float, decimal.Decimal, fractions.Fraction, complex"
     #"字符串类型:str, bytes"
     #"元组:tuple"
     #"冻结集合:frozenset"
     #"布尔类型:True, Flase"
     #"None"
   #不可哈希类型：可变类型，dictionary, list, set,不可作为字典的key
   #                    dictionary,set不能用下标访问，list可以
   #                   可变类型只能存储不可变类型,但dictionary可以存储dictionary
   #                   tuple\list可以存储任何数据
```

## 3.数据结构和算法

![](..\images\1601952372557.jpeg)

## 4.函数

```python
def functionname( parameters ):
   "函数_文档字符串"
   function_suite
   return [expression]
```

## 5.安装包

虚拟环境中再详细介绍

```python
pip install 
conda install
```

## 6.代码样式

PEP8