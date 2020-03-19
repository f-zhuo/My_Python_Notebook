# numpy
* 优点
  快速处理任意维度的数组
  
## ndarray对象
* 一般存放同类型元素（同质）的多维数组，若元素类型不一致或某轴上元素个数不一致（非同质），则每个元素都会被视为一个对象(Object)
* 由实际数据（数组元素）和描述实际数据的元数据（数组类型，维度等）组成
* 轴/axis：存储数据的维度，可以理解为方向，用0，1，2表示。一维数组0轴，二维0，1轴，三维0，1，2轴
* 秩/rank：轴的数量/维度

* 列表，数组(array)，字典都可以形成ndarray对象
* 列表与数组的区别
   列表的元素类型可以是不同的，数组的元素类型必须是相同的

### 创建一维数组

**把list/tuple转化为array**

```python
import numpy as np
list1=[1,2,3]
onearray=np.array(list1)
# onearray=np.array([1,2,3])
# onearray=np.array((1,2,3))
print(type(onearray))
print(onearray)

#<class 'numpy.ndarray'>
#[1 2 3]
```

**array直接创建**

```python
import numpy as np
onearray=np.array(range(5))
print(type(onearray))
print(onearray)
```

**np.arange()创建**

```python
onearray==np.arange(1,5,0.5)
print(type(onearray))
print(onearray)
```

**创建ndarray对象的函数**

|        函数         |                  说明                  |
| :-----------------: | :------------------------------------: |
|   np.ones(shape)    |              全为1的数组               |
|   np.zeros(shape)   |              全为0的数组               |
| np.full(shape,val)  |             全为val的数组              |
|      np.eye(n)      |               n维单位阵                |
|  np.zeros_like(a)   |      根据a的shape生成全为0的数组       |
|   np.ones_like(a)   |      根据a的shape生成全为1的数组       |
| np.full_like(a,val) |     根据a的shape生成全为val的数组      |
|    np.linspace()    | 根据起止数据等间距填充数据，形成新数组 |
|  np.concatenate()   |          合并多数组为一个数组          |

```python
'''np.linspace(n1,n2,count,endpoint=True/False)
   n1:开始点
   n2:结束点
   count:元素个数
   endpoint:是否包含结束点，默认包含
'''
a = np.linspace(2,10,5)
print(a)
b = np.linspace(2,10,5,endpoint=False)
print(b)
```

### 创建二维数组

#### array

```python
twoarray=np.array([[1,2],[3,4]])
print(twoarray)
print(type(twoarray))
```

#### np.ones

```python
tarray = np.ones((3,4),dtype=np.int32)
tarray
```

**只有一行/一列的二维**

```python
# 一维
onearray=np.ones((6,))
print(onearray)
# 二维
twoarray=np.ones((1,6))
print(twoarray)
```

**秩/维度**

```python
print(twoarray.ndim)
```

**形状**

```python
print(twoarray.shape)
```

**元素个数**

```python
print(twoarray.size)
```

#### 改变数组形状

* shape：改变原数组的shape

```python
twoarray=np.array([[1,2,3,4],[3,4,5,6]])
twoarray.shape=(4,2)
twoarray
```

* reshape：产生新数组，不改变原数组

```python
twoarray=np.array([[1,2,3,4],[3,4,5,6]])
twoarray.reshape((4,2),order='F')
print(twoarray)
st=twoarray.reshape((4,2),order='F') # 以列展开，Fortran风格
rd=twoarray.reshape((4,2),order='C') # 默认，以行展开
print(st,'\n')
print(rd,'\n')
print(twoarray)
```

```python
t=np.arange(24)
t.shape
t1=t.reshape((2,3,4))
t1
```

* resize：改变原数组

```python
twoarray=np.array([[1,2,3,4],[3,4,5,6]])
twoarray.resize((4,2))
twoarray
```

* flatten：不改变原数组

```python
'多维数组变一维'
twoarray=np.array([[1,2,3,4],[3,4,5,6]])
one_st=twoarray.reshape(8,)
one_rd=twoarray.reshape((8,),order='F')

print(twoarray.flatten()) # flatten()
print(twoarray.flatten(order='F'))
print(one_st)
print(one_rd)
```

#### ndarray转换为列表

```python
l=np.arange(24).reshape((4,6)).tolist()
print(l)
print(type(l))
```

## numpy的数据类型

|   数组类型    |                    描述                     | 简写 |
| :-----------: | :-----------------------------------------: | :--: |
|    np.bool    |            布尔类型，占一个字节             |  b   |
|    np.int8    |          1个字节的整数，-2^7~2^7-1          |  i   |
|   np.int16    |         2个字节的整数，-2^15~2^15-1         |  i2  |
|   np.int32    |         4个字节的整数，-2^31~2^31-1         |  i4  |
|   np.int64    |         8个字节的整数，-2^63~2^63-1         |  i8  |
|   np.uint8    |        1个字节的无符号整数，0~2^8-1         |  u   |
|   np.uint16   |        2个字节的无符号整数，0~2^16-1        |  u2  |
|   np.uint32   |        4个字节的无符号整数，0~2^32-1        |  u4  |
|   np.uint64   |        8个字节的无符号整数，0~2^64-1        |  u8  |
|  np.float16   | 半精度浮点数，正负号1位，指数5位，精度10位  |  f2  |
|  np.float32   | 单精度浮点数，正负号1位，指数8位，精度23位  |  f4  |
|  np.float64   | 双精度浮点数，正负号1位，指数11位，精度52位 |  f8  |
| np.complex64  |    复数，分别用32位浮点数表示实部与虚部     |  c8  |
| np.complex128 |    复数，分别用64位浮点数表示实部与虚部     | c16  |
|  np.object_   |                 python对象                  |  O   |
|  np.string_   |                   字符串                    |  S   |
|  np.unicode_  |                 unicode类型                 |  U   |

```python
t=np.array([1,2,3,4],dtype=np.int16)
print(t.dtype) # 元素数据类型
print(t.itemsize) # 数组每个元素所占字节大小
```

### 更改数据类型

```python
t1=t.astype(np.int32)
print(t.dtype) # 原数组的数据类型不会变
print(t1.dtype)
print(t)
print(t1)
```

## 数组的计算

### 数组和数字计算

采用broadcast的机制，每个数组元素都和数字进行相应的计算

```python
t=np.arange(24).reshape((6,4))
print(t)
print(t+1) 
```

### 数组和数组间的计算

* 相同shape的数组：对应位置的元素计算

```python
t1=np.arange(24,48).reshape(6,4)
print(t1)
print(t1+t)
```

不同shape的**多维数组**不能相互计算

**行/列形状相同的一维数组与多维数组可以计算**

* 行形状相同

```python
t1=np.arange(24).reshape((6,4))
t2=np.arange(4)
print(t1)
print(t2)
print(t1+t2)
```

* 列形状相同

```python
t1=np.arange(24).reshape((6,4))
t2=np.arange(6).reshape(6,1)
print(t1)
print(t2)
print(t1+t2)
```

## 数组的计算函数

### sum函数

#### 二维数组

* 求所有元素的和
   np.sum(array)

```python
import numpy as np
a=np.array([[1,2,3],[4,5,6]])
print(np.sum(a))
```

* 求0轴方向（水平向）的和
     np.sum(array,axis=0)

```python
a=np.array([[1,2,3],[4,5,6]])
print(np.sum(a,axis=0))
```

* 求1轴方向（竖直向）的和
  np.sum(array,axis=1)

```python
a=np.array([[1,2,3],[4,5,6]])
print(np.sum(a,axis=1))
```

#### 三维数组

* 求所有元素的和
   np.sum(array)

```python
a=np.arange(24).reshape((2,3,4)) # 0，1，2轴分别是2，3，4
print(a)
print(np.sum(a))
```

* 求0轴方向（二维堆积的方向）的和
   np.sum(array,axis=0)

```python
a=np.arange(24).reshape((2,3,4))
print(np.sum(a,axis=0))
```

* 求1轴方向（水平向）的和
   np.sum(array,axis=1)

```python
a=np.arange(24).reshape((2,3,4))
print(np.sum(a,axis=1))
```

* 求2轴方向（竖直向）的和
   np.sum(array,axis=2)

```python
a=np.arange(24).reshape((2,3,4))
print(np.sum(a,axis=2))
```

### average函数

* 所有元素平均值

```python
t=np.array([[1,3,4,5],[-2,5,3,2],[-4,6,-2,0]])
np.average(t) # 结果和np.mean(t)一样
# np.mean(t)
```

* 求0轴方向（水平向）的平均值

```python
np.average(t,axis=0)
# np.mean(t,axis=0)
```

* 求1轴方向（竖直向）的平均值

```python
np.average(t,axis=1)
# np.mean(t,axis=1)
```

* 加权平均值

```python
# mean没有该参数
np.average(t,axis=0,weights=[1,2,3]) # -2.5=(1*1-2*2-4*3)/(1+2+3)

# array([-2.5,5.16666667,0.66666667,1.5])
```

### median函数

```python
t=np.array([[1,3,4],[-2,5,3],[-4,6,-2]])
np.median(t)
np.median(t,axis=0)
np.median(t,axis=1)
```

### max函数

```python
a=np.array([[[80,88],[82,81]],[[75,81],[78,89]]])
print(a)
print(np.max(a))
print(np.max(a,axis=0))
print(np.max(a,axis=1))
print(np.max(a,axis=2))
```

### min函数

```python
a=np.array([[80,88],[82,81],[75,81]])
print(a)
print(np.min(a))
print(np.min(a,axis=0))
print(np.min(a,axis=1))
```

### maximum和minimum函数

数组和数字/同样形状的数组取最大/最小值

```python
np.maximum([[1,3,4],[-2,5,6]],3)
np.maximum([1,3,4,-2,5],[3,5,-4,6,-2])
np.minimum([1,3,4,-2,5],3)
```

### cumsum函数

* arr.cumsum(0) 

  0轴方向上，arr前一行与本行之和

```python
t=np.array([[1,3,4],[-2,5,3],[-4,6,-2]])
print(t)
print(t.cumsum(0))
```

* arr.cumsum(1) 

  1轴方向上，arr前一列与本列之和

```python
t=np.array([[1,3,4],[-2,5,3],[-4,6,-2]])
print(t)
print(t.cumsum(1))
```

### argmin和argmax函数

* np.argmin(arr,[axis])：最小值的索引，不指定轴时，输出是降维为一维的索引值

```python
t=np.array([[1,3,4],[-2,5,3],[-4,6,-2]])
np.argmin(t,axis=0)
np.argmin(t,axis=1)

np.argmin(t) # 6
```

* np.argmax(arr,[axis])：最大值的索引

```python
np.argmax(t) # 7
```

### unravel_index(onearray_index,narray_shape)

一维数组的某索引位置在narray_shape形状的多维数组中的索引值

```python
np.unravel_index(0,(3,3))
np.unravel_index(1,(3,3))
np.unravel_index(6,(3,3))
```

#### np.var(）

方差

```python
t=np.array([[1,3,4],[-2,5,3],[-4,6,-2]])
np.var(t)
np.var(t,axis=1)
```

#### np.cov()

协方差

```python
t=np.array([[1,3,4],[-2,5,3],[-4,6,-2]])
np.cov(t)
np.cov(t,axis=1)
```

#### np.std()

标准差

```python
t=np.array([[1,3,4],[-2,5,3],[-4,6,-2]])
np.std(t,axis=0)
```

#### np.ptp()

极差

```python
t=np.array([[1,3,4],[-2,5,3],[-4,6,-2]])
np.ptp(t,axis=0)
```

### 其他通用函数

|                           通用函数                           |                        说明                        |
| :----------------------------------------------------------: | :------------------------------------------------: |
|                         numpy.sqrt()                         |                       平方根                       |
|                         numpy.exp()                          |                   e^arr[i]的数组                   |
|                       numpy.abs/fabs()                       |                       绝对值                       |
|                        numpy.square()                        |                       平方值                       |
|                       numpy.log/log10                        |                        对数                        |
|                         numpy.sign()                         |                     计算正负号                     |
|                        numpy.isnan()                         |                   判断是否为nan                    |
|                        numpy.isinf()                         |                   判断是否为inf                    |
|   numpy.cos/cosh/arccos/sin/sinh/arcsin/tan/tanh/arctan()    |                      三角函数                      |
|                         numpy.modf()                         | 分离小数和整数部分，以整数和小数的形式返回两个数组 |
|                         numpy.ceil()                         |                      向上取整                      |
|                        numpy.floor()                         |                      向下取整                      |
|                         numpy.rint()                         |                      四舍五入                      |
|                        numpy.trunc()                         |                      向0取整                       |
|               numpy.add(arr1,arr2)/arr1+ arr2                |                    两个数组求和                    |
|             numpy.subtract(arr1,arr2)/arr1- arr2             |                    两个数组相减                    |
|             numpy.multiply(arr1,arr2)/arr1* arr2             |                    两个数组相乘                    |
|             numpy.divide(arr1,arr2)/ arr1/ arr2              |              两个数组相除 arr1./arr2               |
|              numpy.power(arr1,arr2)/arr1** arr2              |                数组间乘方arr1.^arr2                |
|    numpy.fmin/minimum(arr1,arr2)/fmax/maximum(arr1,arr2)     |           两个数组同级元素的最小/最大值            |
|               numpy.mod(arr1,arr2)/arr1% arr2                |                    两个数组取模                    |
|                  numpy.copysign(arr1,arr2)                   |          把arr2元素符号复制给arr1对应元素          |
| numpy.greater/greater_equal/less/less_equal/equal/not_equal(arr1,arr2)/arr1>= arr2 |             两个数组比较，返回布尔数组             |
| numpy.logical_and/logical_or/logical_xor(arr1,arr2)/logical_not(arr) |      两个数组逻辑运算，0表示False,非0表示True      |

**np.random函数**

|                 函数                 |                             说明                             |
| :----------------------------------: | :----------------------------------------------------------: |
|        np.random.rand(shape)         |          生成形状为shape的`[0,1)`之间的随机小数数组          |
|        np.random.randn(shape)        |                生成形状为shape的随机小数数组                 |
|     np.random.randint(a,b,shape)     |          生成形状为shape的`[a,b)`之间的随机整数数组          |
|         np.random.shuffle(a)         |             由a数组的最外层随机排列，改变原数组              |
|       np.random.permutation(a)       |            由a数组的最外层随机排列，不改变原数组             |
| np.random.choice(a,[size,replace,p]) | 从一维数组a中以概率p抽取元素，形成size形状的新数组，replace默认False，表是否可以重用元素 |
|     np.random.uniform(a,b,shape)     |          生成形状为shape的`[a,b]`之间的随机小数数组          |

```python
import random
d=np.random.choice(np.arange(40),(3,2,5),True)
print(d)
np.random.shuffle(d)
print(d)
e = np.random.uniform(1,10,(2,3))
print(e)
```

#### np.gradient(f)

梯度函数，计算f的元素的梯度。f若为n维，返回每个维度的梯度，结果是n个n维数组

梯度计算：
     f:[a,b,c]
     
    gradient:
    [(b-a)/(index(b)-index(a)),(c-a)/(index(c)-index(a)),(c-b)/(index(c)-index(b))]
```python
# a = np.random.randint(1,15,(8,))
# print(a)
# np.gradient(a)
a = np.random.randint(1,15,(4,3))
print(a)
np.gradient(a)
```

## 数组的索引和切片

### 取值

#### 一维数组

```python
a=np.arange(10)
a[2]
a[2:8:2]
a[2:]
```

#### 二维数组

```python
t=np.arange(24).reshape(4,6)

'''取第二行'''
print(t[1])
print(t[1,:])

'''取连续多行'''
print(t[1:3])
print(t[1:3,:])

'''取不连续多行'''
print(t[[1,3]])
print(t[[1,3],:])

'''取一列'''
print(t[:,1])

'''取连续多列'''
print(t[:,0:2])

'''取不连续多列'''
print(t[:,[0,2]])

'''取某值'''
print(t[1,2])

'''取多值'''
print(t[[1,3],[2,4]])
```

### 修改值

```python
'''修改某行的值'''
t=np.arange(24).reshape(4,6)
t[1]=0
t

'''修改某列的值'''
t=np.arange(24).reshape(4,6)
t[:,1]=0
t
```

##### 条件赋值

```python
t=np.arange(24).reshape(4,6)
t[t<10]=-1
t
```

##### 逻辑判断赋值

* 与

```python
t1=np.arange(24).reshape(4,6)
t1[(t1<10)&(t1>2)]=-1
print(t1,'\n')

t2=np.arange(24).reshape(4,6)
t2[np.logical_and(t2<10,t2>2)]=-1
print(t2)
```

* 或

```python
t1=np.arange(24).reshape(4,6)
t1[(t1<2)|(t1>10)]=-1
print(t1)
print()

t2=np.arange(24).reshape(4,6)
t2[np.logical_or(t2<2,t2>10)]=-1
print(t2)
```

* 非

```python
t1=np.arange(24).reshape(4,6)
t1[~(t1<2)]=-1
print(t1)
print()

t2=np.arange(24).reshape(4,6)
t2[np.logical_not(t2<2)]=-1
print(t2)
```

* 三目条件运算式

   np.where(condition,if,else)

```python
t=np.arange(24).reshape(4,6)
t=np.where(t<10,0,1)
t
```

## 数组的添加，删除与去重

*  np.append(arr,values,axis)
  无axis时，生成新的一维数组，values(可以是任意形状)添加在末尾，原数组不变
  有axis时，生成新的多维数组，按照axis排列，values在对应axis上形状一致

```python
t=np.arange(6).reshape(2,3)
t
print(np.append(t,6))
print(t)

print(np.append(t,[6,7,8]))
print(t)

print(np.append(t,[[6,7],[5,7]],axis=1))
print(t)

print(np.append(t,[[6,7,8],[5,7,9]],axis=0))
print(t)
```

* np.insert(arr,values,axis)
  指定axis时，插入values可以是同形状的数组，也可以是数字。如果是数字，将按照broadcast机制插入，其余用法与np.append一致

```python
t=np.arange(6).reshape(2,3)
t
print(np.insert(t,3,6))
print(t)

print(np.insert(t,3,[6,7]))
print(t)

print(np.insert(t,2,[6],axis=0))

print(np.insert(t,2,6,axis=0))
print(t)

print(np.insert(t,2,[6,7,8],axis=0))
print(t)

print(np.insert(t,2,6,axis=1))
print(np.insert(t,2,[6],axis=1))
print(t)

print(np.insert(t,2,[6,7],axis=1))
print(t)
```

* np.delete(arr,index/arr,axis)
   删除，原数组不变，不指定axis时返回的是一维数组；指定时删除对应索引的行/列

```python
t=np.arange(6).reshape(2,3)
t
print(np.delete(t,5))
print(t)

print(np.delete(t,[5,4]))
print(t)

print(np.delete(t,1,axis=0))
print(t)

print(np.delete(t,1,axis=1))
print(t)
```

* 数组的去重 
    * np.unique(arr) 去重后的数组
    * arr,index=np.unique(arr,return_index=True) ：arr是去重后的数组，index是去重后的数组在原数组中第一次出现位置的索引值
    * arr,inverse=np.unique(arr,return_inverse=True) arr是去重后的数组，inverse是原数组在去重后的数组中的索引值
    * arr,counts=np.unique(arr,return_counts=True) arr是去重后的数组，counts是去重的数组元素在原数组中重复的次数

```python
t=np.array([2,1,1,3,3,5,2,5])
t
print(np.unique(t))
print(t)

u,index=np.unique(t,return_index=True)
print(u,index,t)

u,inverse=np.unique(t,return_inverse=True)
print(u,inverse,t)

u,counts=np.unique(t,return_counts=True)
print(u,counts,t)
```

## 数组的拼接

* np.concatenate((arr1,arr2),[axis])
   按现有轴拼接，此方法两数组axis方向上的形状必须一致，axis不写，则默认为按轴0拼接

```python
a=np.array([[1,2],[3,4]])
b=np.array([[5,6],[7,8]])
np.concatenate((a,b))
np.concatenate((a,b),axis=0)
np.concatenate((a,b),axis=1)

a=np.array([[1,2],[3,4]])
b=np.array([[5,6,5],[7,8,9]])
np.concatenate((a,b),axis=1)
```

* np.stack((arr1,arr2),[axis])

   沿新的轴拼接

```python
a=np.array([[1,2],[3,4]])
b=np.array([[5,6],[7,8]])
np.stack((a,b),axis=0)
np.stack((a,b))
np.stack((a,b),axis=1)
```

* hstack((arr1,arr2)) 

  水平方向堆叠

```python
a=np.array([[1,2],[3,4]])
b=np.array([[5,6],[7,8]])
np.hstack((a,b))
```

* vstack((arr1,arr2)) 

  竖直方向堆叠

```python
a=np.array([[1,2],[3,4]])
b=np.array([[5,6],[7,8]])
np.vstack((a,b))
```

**concatenate()与vstack()的比较**

vstack是单纯的堆叠，不改变原来数组维度，concatenate会降维

```python
a=np.array([[[1,2],[3,4]],[[5,8],[0,9]]])
b=np.array([[[5,6],[7,8]],[[7,0],[8,4]]])
np.vstack((a,b))

np.concatenate((a,b),axis=1)
```

## 数组的分割

* np.split(arr_origin,num/arr_index,axis)
  * num：均分为num份，按axis切分，默认0轴
  * arr_index：按数组中的axis向的索引分割

```python
a=np.random.randint(1,10,(7,3))
np.split(a,[3,6])
np.split(a,2,axis=0)

a=np.array([[1,2],[3,4],[5,6],[7,8]])
np.split(a,2)
a=np.array([[1,2],[3,4],[5,6],[7,8]])
np.split(a,2,axis=0)
a=np.array([[1,2],[3,4],[5,6],[7,8]])
np.split(a,2,axis=1)
np.split(a,[1,3],axis=0)
np.split(a,[1],axis=1)
```

* np.vsplit和np.hsplit

```python
a=np.floor(10*np.random.random((2,6)))
print(a)
print(np.hsplit(a,3))

a=np.floor(10*np.random.random((3,6)))
print(a)
print(np.vsplit(a,3))
```

## nan和inf

* nan表示缺失值，float类型，和其他任意值的计算结果都是nan，任意nan值都不相同，即np.nan!=np.nan
* inf表示无穷大，float类型

创建nan值和inf值

```python
a=np.nan
b=np.inf
print(type(a))
print(type(b))
```

数值修改为nan

*nan值是float类型，也只能赋值给float类型的元素*

```python
t=np.arange(24,dtype=float).reshape(4,6) 
# t=np.arange(24).reshape(4,6).astype('float')
print(t)
t[3,4]=np.nan
print(t)
```

计算数组中有多少nan值

```python
a=np.isnan(t)
print(a)
print(np.count_nonzero(a))

print(t!=t) # np.nan!=np.nan,t!=t等价于np.isnan(t)
print(np.count_nonzero(t!=t))
```

nan值与任意值计算都是nan

```python
np.sum(t,axis=0)
```

用条件索引修改nan值为0

```python
t[np.isnan(t)]=0
t
```

nan值替换为该列上的平均值

```python
t=np.arange(24).reshape(4,6).astype('float')
t[1,3:]=np.nan
print(t)
for i in range(t.shape[1]):
    col=t[:,i]
    if np.count_nonzero(col!=col):
        col_nonzero=col[col==col] 
        col[col!=col]=np.mean(col_nonzero)
print(t)
```

inf同nan

## 数组转置

* np.transpose(arr)
* arr.T

```python
t=np.arange(24).reshape(4,6)
print(t)
print(np.transpose(t))
print(t.T)
```

* arr.swapaxes()
  交换轴，二维数组时相当于转置

二维数组

```python
t=np.arange(24).reshape(4,6)
print(t)
print(t.swapaxes(1,0))
print(t.swapaxes(0,1)) # 轴的顺序无所谓
```

三维数组

```python
t=np.arange(24).reshape(2,2,6)
print(t)
print(t.swapaxes(1,2))
print(t.swapaxes(0,1))
```

## numpy文件处理

### CSV文件

只能存取一维和二维数组

* 存入CSV文件

```
np.savetxt(fname,array,fmt='%.18e',delimiter=None)
fname:文件、字符串或产生器，可以是.gz或.bz2压缩文件
array:写入文件的数组
fmt(format):格式，如'%d','%.2f'
delimiter:分割字符串，默认为空格
```

```python
a = np.arange(20).reshape((4,5))
np.savetxt('./a.csv',a,fmt='%.1f',delimiter=',')
```

* 读取CSV文件

```
np.loadtxt(fname,dtype=np.float,delimiter=None,unpack=False)
fname:文件、字符串或产生器，可以是.gz或.bz2压缩文件
dtype:数据类型
delimiter:分割字符串，默认为空格
unpack:默认False,写入同一个数组；True:写入不同数组变量
```

```python
b1 = np.loadtxt('./a.csv',delimiter=',')
print(b1)
b2 = np.loadtxt('./a.csv',dtype=np.int,delimiter=',')
print(b2)
```

#### 多维数组存取

* 存入

```
a.tofile(fname,sep='',format=='%s')
fname:文件
sep:分隔符，设为''时文件变为二进制文件
format:格式化
```

```python
a = np.arange(100).reshape(2,5,10)
a.tofile('./a.dat',sep=',',format='%d')
b = np.arange(100).reshape(2,5,10)
b.tofile('./b.dat',format='%d') # 二进制文件
```

* 读取

```
np.fromfile(fname,dtype=np.float,count=-1,sep='')
fname:文件名，字符串
dtype:读取的数据类型
count:读取元素个数，-1表示全部读入
sep:分割符，为空表示要读取的文件是二进制

np.fromfile需要知道tofile时的数组类型和维度，两者应配合使用，可把数组类型和维度写入另一个文件
```

```python
c=np.fromfile('./a.dat',dtype=np.int,sep=',')
print(c)
print(c.reshape(2,5,10))

d = np.fromfile('./b.dat',dtype=np.int)
print(d)
print(d.reshape(2,5,10))
```

### npy和npz文件

* 存储
  * np.save(fname,arr) 
     文件拓展名：.npy
  * np.savez(fname,arr)
     文件拓展名：.npz
* 读取
  * np.load(fname)

```python
a = np.arange(100).reshape(2,5,10)
np.save('./a.npy',a)
b = np.load('./a.npy')
b
```

