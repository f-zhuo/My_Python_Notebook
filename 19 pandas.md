# pandas

## pandas的两种数据结构

* series
* dataframe
## Series
带索引的一维数组，可以自定义索引
### 创建Series对象

pd.Series(arr,[index])

index可以省略，默认从0开始，属于位置索引；自定义index可以是数字，也可以是字符串

```python
import pandas as pd
# from pandas import Series,DataFrame
import numpy as np
se1=pd.Series([1,2,3,4])
se1
se2=pd.Series([1,2,3,4],['a','b','c','d'])
se2
```

创建值相同的Series对象

```python
pd.Series(2,index=['a','b','c'])
```

用字典创建Series

```python
dic={'a':1,'b':2,'c':3}
se=pd.Series(dic)
se
```

通过ndarray创建

```python
pd.Series(np.arange(4))
```

### 获取Series索引及内容

```python
print(se.values)
print(se.index)

print(se.items())
print(list(se.items()))

print(se.iteritems())
print(list(se.iteritems()))
```

### 给Series及索引设置名字

```python
s = pd.Series([1,2,3,4],index=list('abcd'))
# print(s)
# print(s.name)
# print(s.index.name)

s.name = 'Series对象'
s.index.name = '索引'
print(s)
```

### Series索引取值

```python
print(se[2]) # 位置索引
print(se['c']) # 自定义索引
```

获取多个数据

```python
print(se[[0,2]]) # 位置索引
print(se[['a','c']]) # 自定义索引
```

切片

```python
print(se[0:2]) # 位置索引左闭右开
print(se['a':'c']) # 自定义索引，左闭右闭
```

get方法：

获取索引值，若索引不存在设置默认值

```python
print(se.get('d',4))
```

修改索引值

```python
se.index=['1','2','3']
se
```

reindex()：

对Index重新排序，index若不存在，用缺失值NaN填补，返回新数组，原数组不受影响
还可设置参数，fill_value=num,使NaN值变为num值

```python
print(se.reindex(list('2314')))
print(se)
print(se.reindex(list('2314'),fill_value=0))

s = pd.Series({'a':1,'b':2,'c':3},index=['b','a','d'])
s
```

### 布尔条件取值

```python
se=pd.Series([1,2,3,4],['a','b','c','d'])
print(se[se>2])
```

### 删除数组元素

返回新数组，原数组不变。  若数组没有自定义索引，则使用位置索引；若数组自定义了索引，则必须使用自定义索引，不可用位置索引

```python
print(se.drop(['1','2']))
# se.drop([1,2]) # KeyError: '[1 2] not found in axis'
print(se)
```

### 排序

* s.sort_index()

按索引排

* s.sort_values()

按值排

```python
s = pd.Series(np.arange(5),index=list('agetk'))
s.sort_index()
s.sort_values(ascending=False)
```

### 算术计算

基于索引进行运算，两个数组基于对应的索引运算，如果没有对应的索引，就返回空值NaN，计算结果为浮点型，以避免丢失精度

```python
se1=pd.Series([1,2,3,4],['Beijing','Shanghai','Guangzhou','Shenzhen'])
se2=pd.Series([4,3,3,2],['Beijing','HongKong','Shanghai','Taiwan'])
print(se1+se2)
print(se1-se2)
print(se1*se2)
print(se1/se2)
print(se1//se2)
print(se1%se2)
print(se1**se2)
```

```python
se=pd.Series([1,2,3,4],['a','b','c','d'])
print(se*2)
print(se**2)
print(np.square(se))
```

### 统计函数集合

* 描述series数值

```python
s = pd.Series(np.arange(5),index=list('agetk'))
s1 = s.describe() 

#count    5.000000
#mean     2.000000
#std      1.581139
#min      0.000000
#25%      1.000000
#50%      2.000000
#75%      3.000000
#max      4.000000
#dtype: float64

s1['count']
```

* 判断相关性

  `corr()
  0.8-1 强相关
  0.5-0.8 弱相关`

```python
s1 = pd.Series([1,2,3,4],index=list('abcd'))
s2 = pd.Series([2,2,6,4],index=list('abcd'))
s1.corr(s2)
```

## DataFrame
二维表结构，可以存储不同的数据类型，每个轴都有自己的标签，水平轴为行索引(index)，竖直轴为列索引(columns)

```python
df=pd.DataFrame(np.random.randint(1,40,(4,4)),list('abcd'),['bj','sh','gz','sz'])
df
```

* 通过字典创建DataFrame

  字典的值就是data，键就是columns，只需指定行索引(index)

```python
dic={'bj':[6,1,3,37],'sh':[24,18,4,16],'gz':[35,18,38,30],'sz':[3,22,6,5]}
df1=pd.DataFrame(dic,list('abcd'))
df1
```

* 用字典和Series创建DataFrame

DataFrame的每列column可分别指定index，values数量也可不相等，以最多values的index为标准，缺失就为NaN

```python
dic={'bj':pd.Series([6,1,3,37],list('abcd')),'sh':pd.Series([24,18,4,16,7],list('abcde')),'gz':pd.Series([35,18,38,30],list('bcad')),'sz':pd.Series([3,22,6,5],list('cabd'))}
pd.DataFrame(dic)
```

**创建DataFrame指定index和columns**

```python
dic={'bj':pd.Series([6,1,3,37],list('abcd')),'sh':pd.Series([24,18,4,16,7],list('abcde')),'gz':pd.Series([35,18,38,30],list('bcad')),'sz':pd.Series([3,22,6,5],list('cabd'))}
pd.DataFrame(dic,index=['b','d','f'],columns=['sh','gz','xz'])
```

* from_dict()

```python
df2=pd.DataFrame.from_dict(dic,orient='index', columns=list('abcd'))
df2
```

**把DataFrame转化为dict**

```python
df2.to_dict()
```

### DataFrame的属性

#### 获取形状

```python
df2.shape
```

#### 获取行索引index

```python
print(df2.index)
print(df2.index.tolist())
```

#### 获取列索引columns

```python
print(df2.columns)
print(df2.columns.tolist())
```

#### DataFrame修改index，columns

```python
df1=pd.DataFrame(np.arange(9).reshape(3,3),['bj','sh','gz'],['a','b','c'])
print(df1)
df1.index=['Beijing','Shanghai','Guangzhou']
print(df1)

print(df1.reindex(['Beijing','Guangzhou','Shenzhen']))
print(df1.reindex(['Beijing','Guangzhou','Shenzhen'],fill_value=0))

print(df1.reindex(columns=['a','c','d']))

df1.columns=list('123')
df1

'''rename(index=dic1,columns=dic2)
修改index和columns，dic={old_index:new_index}
返回新数组，原数组不变'''
print(df1.rename(index={'Guangzhou':'HK'},columns={'2':'4'}))
print(df1)

'''用rename和函数修改index，columns'''
def modify(x):
    return x+'_abc'

df1.rename(index=modify,columns=modify) # 调用函数名即可，不需带参数
```

#### 添加，修改和删除

对index和columns的添加删除，不影响原数组

**删除**

```python
df1=pd.DataFrame(np.arange(9).reshape(3,3),['bj','sh','gz'],['a','b','c'])
new_columns = df1.columns.delete(1)
df2 = df1.reindex(columns=new_columns)
print(df1,'\n',df2)
```

```python
df1.drop(index='bj',columns='b',inplace=True)
df1

print(df.drop([0],axis=0,inplace=False))
print(df.drop(['a'],axis=1,inplace=False))
```

**修改**

```python
df1 = pd.DataFrame([['Snow', 'M', 22], ['Tyrion', 'M', 32], ['Sansa', 'F', 18],
                    ['Aray', 'F', 14]],
                   columns=['name', 'gender', 'age'])
print(df1)
df1['score'] = [80, 98, 67, 90]
print(df1)
df1.iloc[1]=['Kongming','M',27,99]
df1
```

**添加**

```python
df2=pd.DataFrame([['Liu Bei','M',29,60],['Guan Yu','M',27,75],
                  ['ZhangFei','F',26,90]],
                 columns=['name','gender','age','score'])
print(df1.append(df2,ignore_index=False)) #ignore_index默认是False,按两个数组原来的index
print(df1.append(df2,ignore_index=True)) # gnore_index=True，不按原来索引，从0递增
print(df1)
```

任意位置插入一列

```python
df1.insert(2,'city',['sh','bj','sz','gz'])
df1
```

df.assign

```python
df = pd.DataFrame({'temp_c': [17.0, 25.0]},
                index=['Portland', 'Berkeley'])
df
df.assign(temp_f=lambda x: x['temp_c'] * 9 / 5 + 32,
   temp_k=lambda x: (x['temp_f'] +  459.67) * 5 / 9)
```



#### 指定列为index，行为columns

```python
df1=pd.DataFrame({'x':range(5),'s':list('abcde'),'z':[1,1,2,2,3]})
print(df1)
print(df1.set_index('s',drop=True)) # 默认，删除设置为index的那一列
print(df1.set_index('s',drop=False)) # 不删除设置为index的那一列
print(df1)

#df2=df1.set_index('s',drop=False)
#df2.index.name=None
#df2

df2=df1.set_axis(df1.iloc[2],inplace=False,axis=1)
df2
```

#### 数据类型

```python
df2.dtypes
```

#### 数据维度

```python
df2.ndim
```

#### 数据值

```python
df2.values
```

#### 概览信息

```python
df2.info()
```

#### 数值型列的统计信息

```python
df2.describe()
```

#### 显示前几行数据

```python
df2.head(3)
```

#### 显示后几行的数据

```python
df2.tail(3)
```

### 获取元素

* `df[index][columns]`
   * index可以用切片，可以是自定义索引或位置索引，columns不可切片。也就是说`df[c]`必取列，`df[i1:i2]`必取行；取一个值用`df[i1:i2][c]`；行index的切片可以叠加，若用`df[i1:i2][c1:c2]`,则取`[i1:i2]`中[c1:c2]的行
* `df.columns[index]`
   * index可以是自定义或者位置的索引，返回具体的元素值
* `df.loc[index,columns]`
   * index，columns是实际定义的index
* `df.iloc[index,columns]`
   * index，columns是位置索引（0，1，2……）

```python
dic={'bj':[6,1,3,37],'sh':[24,18,4,16],'gz':[35,18,38,30],'sz':[3,22,6,5]}
df1=pd.DataFrame(dic,list('abcd'))
print(df1)
print(df1[0:2])
print(df1['a':'c'])
print(df1['bj'])
print(df1['a':'c'][1:])
print(df1['bj'][0])

print(df1.loc[:,'sh'])
df1.loc['a',['sh','sz']]
print(df1.iloc[:,0])
print(df1.iloc[1])
```

获取多个列/行

```python
print(df1[['bj','sh']])
print(type(df1[['bj','sh']]))

print(df2.loc[['a','c']])
print(df2.iloc[[0,2]])
```

修改值

```python
df1.iloc[1,1]=97
df1
```

### DataFrame的排序

* 对索引排序
  
  * df.sort_index(axis=0,ascending=True)
  
  axis=0是对行index排序，axis=1是对column排序
* 对数据排序
  
  * df.sort_values(by=columns/index,axis=0/1,ascending=True)

```python
df=pd.DataFrame(np.arange(9).reshape(3,3),index=list('bac'), columns=list('djf'))
df
df.sort_index()
df.sort_index(axis=1)

df.sort_values('a',axis=1) # 默认升序
```

### 数据处理

#### 删除Series空值

```python
se=pd.Series([2,np.nan,7,np.nan,9])
# se=np.array([4,np.nan,8,np.nan,5])
print(se)

'''判断是否空值，返回布尔型'''
print(se.isnull())
print(se.notnull())

print(se.dropna())
print(se[se.notnull()])    # 条件索引
print(se)                  # 原数组不变

```

#### 删除DataFrame空值

* 只要是包含空值的行就删除

```python
df=pd.DataFrame([[1,2,3],[np.nan,np.nan,2],[np.nan,np.nan,np.nan],[8,8,np.nan]])
print(df)
print(df.dropna(axis=0,how='any')) # axis默认是0,how默认是any
# df.dropna(axis=1) 
```

* 删除全部为空值的行

```python
print(df.dropna(how='all'))
```

* 只要是包含空值的列就删除

```python
print(df.dropna(axis=1))
print(df.dropna(axis=1,thresh=1)) # thresh=n 每列保留至少n个非空值
```

#### 填充缺失数据

* 填充常数

```python
df=pd.DataFrame([[1,2,3],[np.nan,np.nan,2],[np.nan,np.nan,np.nan],[8,8,np.nan]])
print(df)
print(df.fillna(0))
print(df)
print(df.fillna(0,inplace=True))
print(df)
```

* 用字典填充

```python
df=pd.DataFrame([[1,2,3],[np.nan,np.nan,2],[np.nan,np.nan,np.nan],[8,8,np.nan]])
print(df)
print(df.fillna({0:10,1:20,2:30})) # {column:value}
```

* 统计函数填充

```python
'''平均值填充
np中的统计函数数的值中不能有nan，否则ndarray的计算结果为nan
pd的dataframe会自动忽略nan值
'''
df.fillna(df.mean())
# 只填充一列
df.iloc[:,1].fillna(df.iloc[:,1].mean())
```

* 指定填充方式和填充行数

````python
print(df)
print(df.fillna(method='ffill')) # 以该列最靠近NaN值，位置在其上面的非NaN值填充
print(df.fillna(method='bfill')) # 以该列最靠近NaN值，位置在其下面的非NaN值填充
print(df.fillna(method='ffill',axis=1)) # 以该列最靠近NaN值，位置在其左面的非NaN值填充
print(df.fillna(method='bfill',axis=1)) # 以该列最靠近NaN值，位置在其右面的非NaN值填充
print(df.fillna(method='bfill',limit=1))
print(df.fillna(method='bfill',limit=1,axis=1))
print(df.fillna(method='bfill',limit=2,axis=1))
````

* df1.add(df2,fill_value=num)

可以设置空值时的填充值num替代NaN值，但两个df的原行/列数据不能都为空

```python
df1 = pd.DataFrame(np.arange(9).reshape(3,3),index=list('abc'),columns=list('qwe'))
df2 = pd.DataFrame(np.arange(9,18).reshape(3,3),index=list('bdc'),columns=list('qye'))
print(df1,'\n',df2)
print(df1.add(df2,fill_value=10))
df1.sub(df2,axis=0)
```

#### 删除重复行

默认从0行开始，保留靠前的行

```python
df=pd.DataFrame({'A':[1,1,1,2,2,3,1],'B':list('aabbbca')})
print(df)
# 数据是否重复，布尔型
print(df.duplicated()) 
# 删除重复项,原数组不变
print(df.drop_duplicates())
```

* 指定列去重

```python
print(df.loc[:,'B'].drop_duplicates())
print(df.drop_duplicates(['B']))
pd.unique(df['B'])
df.drop_duplicates(['B'],inplace=True)

#取重复行的最后一行
df.drop_duplicates(['B'],keep='last')
```

#### 数据合并

```python
df1=pd.DataFrame({'Red':[1,3,5],'Green':[5,0,3]},index=list('abc'))
df2=pd.DataFrame({'Blue':[1,9,8],'Yellow':[6,6,7]},index=list('cde'))
print(df1,'\n',df2)
# 以df1为基准，默认左连接
print(df1.join(df2,how='left'))
# 以df2为基准
print(df1.join(df2,how='right'))
# 外连接，连接所有数据
print(df1.join(df2,how='outer'))
```

##### 多个数组连接

```python
df3=pd.DataFrame({'Brown':[3,4,5],'White':[1,1,2]},index=list('aed'))
df1.join([df2,df3])
```

* merge()

把含有相同columns和index的数组连接起来

```python
df1=pd.DataFrame({'名字':list('ABCDE'),'性别':['男','女','男','男','女'],
                 '职称':['副教授','讲师','助教','教授','助教']},index=range(1001,1006))
df1.columns.name='老师'
df1.index.name='编号'
df2=pd.DataFrame({'名字':list('ABDAX'),'课程':['C++','计算机导论','汇编','数据结构','马克思原理'],
                 '职称':['副教授','讲师','教授','副教授','讲师']},index=[1001,1002,1004,1001,3001])
df2.columns.name='课程'
df2.index.name='编号'
print(df1,'\n',df2)
print(pd.merge(df1,df2))

# 合并‘名字’这一列，其他重复的列分别加后缀_1,_2
print(pd.merge(df1,df2,on='名字',suffixes=['_1','_2']))
print(pd.merge(df1,df2,how='left'))
print(pd.merge(df1,df2,how='right'))
print(pd.merge(df1,df2,how='outer'))
print(pd.merge(df1,df2,on=['职称','名字']))
```

* concat()

Series对象

```python
'''不改变Series对象'''
s1=pd.Series([1,2],list('ab'))
s2=pd.Series([3,4,5],index=list('bde'))
print(s1)
print(s2)
print(pd.concat([s1,s2],ignore_index=True))
print(pd.concat([s1,s2]))

'''改变Series为DataFrame'''
print(pd.concat([s1,s2],axis=1,sort=True))
print(type(pd.concat([s1,s2],axis=1,sort=True)))
```

改变连接方式,inner表示内连接，完全匹配;outer表示外连接，求并集

```python
print(pd.concat([s1,s2],axis=1,join='inner'))
print(pd.concat([s1,s2],axis=1,join='outer',sort=True)) # 连接方式默认是outer
```

指定索引进行连接

```python
pd.concat([s1,s2],axis=1,join_axes=[list('abc')])
```

创建层次化索引

```python
pd.concat([s1,s2],keys=['A','B'])
```

指定列名连接两个Series为DataFrame

```python
pd.concat([s1,s2],keys=['A','B'],axis=1,sort=True)
```

DataFrame对象
axis=0时，添加columns项，合并的另一个数组所有index对应的columns值都为NaN，可理解为无交集的合并
axis=1时，添加columns项，根据两个数组的index补全columns值，缺省为NaN，可理解为有交集的合并

```python
df1=pd.DataFrame(np.random.randint(2,28,(2,3)),index=[1,0],columns=list('abc'))
df2=pd.DataFrame(np.random.randint(10,80,(3,2)),index=[0,2,1],columns=list('de'))
print(df1,'\n',df2)
print(pd.concat([df1,df2],sort=True)) # axis默认0
# 忽略原有index，自动递增生成
print(pd.concat([df1,df2],axis=0,ignore_index=True,sort=True))

print(pd.concat([df1,df2],axis=1,sort=True))
```

层次化列索引

```python
print(pd.concat({'A':df1,'B':df2},axis=1))
print(pd.concat([df1,df2],axis=1,sort=True,keys=['A','B']))
```

DataFrame的相关性分析

```python
df.corr()
```

### 多层索引

* Series对象

```python
'''单层索引'''
# s=pd.Series(np.random.randint(0,150,size=6),list('abcdef'))
# s=pd.Series(np.random.randint(0,150,(6,)),list('abcdef'))
# print(s)
'''多层索引，最外层索引去重'''
s1=pd.Series(np.random.randint(0,150,size=6),[list('aabbcc'),['期中','期末','期末','期中','期中','期末']])
print(s1)
s2=pd.Series(np.random.randint(0,150,size=6),[['期中','期末','期末','期中','期中','期末'],list('aabbcc')])
print(s2)
```

* DataFrame对象

```python
df1=pd.DataFrame(np.random.randint(0,150,(6,4)),columns=['zs','ls','ww','zl'],
                index=[['python','python','math','math','En','En'],['期中','期末','期末','期中','期中','期末']])
df1
```

**MultiIndex.from_arrays()创建多层索引**

```python
class1=['python','python','math','math','En','En']
class2=['期中','期末','期中','期末','期中','期末']
my_index=pd.MultiIndex.from_arrays([class1,class2])
pd.DataFrame(np.random.randint(0,150,(6,4)),index=my_index)
```

**MultiIndex.from_product()创建多层索引**

```python
class1=['python','math','En']
class2=['期中','期末']
my_index=pd.MultiIndex.from_product([class1,class2])
pd.DataFrame(np.random.randint(0,150,(6,4)),index=my_index)
```

#### 多层索引对象的索引

series

```python
'''取第一级索引'''
s1=pd.Series(np.random.randint(0,150,size=6),[list('aabbcc'),['期中','期末','期末','期中','期中','期末']])
print(s1)
# 单个
print(s1['a'])
print(s1.loc['a'])
print(s1.iloc[1])
# 多个
print(s1[['a','c']])
print(s1.loc[['a','c']])
print(s1.iloc[1:4])

'''获取两级索引'''
s1['a','期末']
print(s1.loc['a','期末'])
```

dataframe

```python
class1=['python','math','En']
class2=['期中','期末']
my_index=pd.MultiIndex.from_product([class1,class2])
df=pd.DataFrame(np.random.randint(0,150,(6,4)),index=my_index)
print(df)

# 取一列
print(df[0])

'''一级索引'''
# 单个
print(df.loc['python'])
# 多个
print(df.loc[['python','math']])

'''取两级索引'''
df.loc['python','期末']

'''取一个值'''
df.loc['python','期末'][0]

df.iloc[0]
```

## 时间序列

`pd.date_range(start,periods,end,freq)`
start，periods(个数)，end三个参数至少要赋值两个，freq默认取'D'

|  freq  |       含义       |
| :----: | :--------------: |
|   D    |   日历日的每天   |
|   B    |   工作日的每天   |
|   H    |      每小时      |
| T或min |      每分钟      |
|   S    |       每秒       |
| L或ms  |      每毫秒      |
|   U    |      每微秒      |
|   M    | 日历日的月底日期 |
|   BM   | 工作日的月底日期 |
|   MS   | 日历日的月初日期 |
|  BMS   | 工作日的月初日期 |

*日历日：一周7天*

*工作日：一周5天*

```python
date_index1=pd.date_range(start='20190501',end='20190930')
print(date_index1)
date_index2=pd.date_range(start='20190501',periods=153)
print(date_index2)
date_index3=pd.date_range(periods=153,end='20190930')
print(date_index3)
date_index4=pd.date_range(start='20190501',periods=153,freq='10D')
print(date_index4)
date_index5=pd.date_range(start='20190501',periods=10,freq='1H30min')
print(date_index5)
```

时间序列生成np数组

```python
# index = pd.date_range(start='20190101',periods=10)
# index = pd.date_range(start='2019/1/1',periods=10)
index = pd.date_range(start='2019-01-01',periods=10)
df = pd.Series(np.random.randint(0,10,10),index=index)
df
```

通过时间序列取数组值

```python
ts = pd.Series(np.random.randn(1000),index=pd.date_range('2019-01-01',periods=1000))
# print(ts)
# print(ts['2019'])
# print(ts['2019-5'])
# print(ts['2019/5':'2019-7'])
print(ts.loc['2019/4'])
```

between_time函数

```python
index=pd.date_range("2018-03-17","2018-03-30",freq="2H")
ts = pd.Series(np.random.randn(157),index=index)
ts
ts.between_time("6:00","18:00")
```

* 日期索引的移位

```python
ts = pd.Series(np.random.randn(10),index=pd.date_range('1/1/2019',periods=10))
print(ts)
```

移动数据

```python
print(ts.shift(periods=2))
print(ts.shift(periods=-3,fill_value=0))
```

移动时间序列索引

```python
print(ts.tshift(2))
print(ts.tshift(-2))
print(ts.shift(periods=2,freq='D'))
```

### 转换时区

处理单个时间戳

```python
import time
u_time=pd.to_datetime(time.time(),unit='s')
print(u_time)
s_time=u_time.tz_localize('UTC') # 格林尼治时间
print(s_time)
sh_time=s_time.tz_convert('Asia/Shanghai')
print(sh_time)
```

处理多个时间戳

```python
df = pd.DataFrame([1554970740000, 1554970800000, 1554970860000],columns = ['time_stamp'])
pd.to_datetime(df['time_stamp'],unit='ms').dt.tz_localize('UTC').dt.tz_convert('Asia/Shanghai')
```

格式化时间

```python
print(pd.to_datetime('2019年10月10日',format='%Y年%m月%d日'))
print(pd.to_datetime('2019/10/10',format='%Y/%m/%d'))
```

## 分组

```python
df=pd.DataFrame({
    'name':['BOSS','Lilei','Lilei','Han','BOSS','BOSS','Han','BOSS'],
    'Year':[2016,2016,2016,2016,2017,2017,2017,2017],
    'Salary':[999999,20000,25000,3000,9999999,999999,3500,999999],
    'Bonus':[100000,20000,20000,5000,200000,300000,3000,400000]
    })
print(df)
df_group=df.groupby('name')
# print(df_group)
# print(type(df_group))
# 查看分组结果
# print(df_group.groups)
# 查看分组数量
# print(df_group.count())
# 查看分组的具体内容
#for name,group in df_group:
    #print(name,'\n',group)
# 查看某组内容
# print(df_group.get_group('BOSS'))
```

对一列进行分组

```python
group_by_name=df['Year'].groupby(df['name'])
# print(group_by_name.count())
print(group_by_name.get_group('BOSS'))
```

对多列进行分组

```python
group_by_name_year=df.groupby(['name','Year'])
# print(group_by_name_year.groups)
# for name,group in group_by_name_year:
#     print(name,'\n',group)
    
print(group_by_name_year.get_group(('BOSS',2016)))
```

## 聚合函数

|     聚合函数     |                  说明                   |
| :--------------: | :-------------------------------------: |
|       mean       |               分组平均值                |
|      count       |         分组中**非NaN值**的个数         |
|       sum        |            分组中非NaN值的和            |
|      median      |           非NaN值的算术中位数           |
|       std        |                 标准差                  |
|       var        |                  方差                   |
|       min        |             非NaN值的最小值             |
|       max        |             非NaN值的最大值             |
|       prod       |               非NaN值的积               |
|      first       |              第一个非NaN值              |
|       last       |             最后一个非NaN值             |
|       mad        |              平均绝对偏差               |
|       mode       |                   模                    |
|       abs        |                 绝对值                  |
|       sem        |            平均值的标准误差             |
|       skew       |          样品偏斜度（三阶矩）           |
|       kurt       |           样品峰度（四阶矩）            |
|     quantile     |       样本分位数（百分位上的值）        |
|      cumsum      |            前面所有数据求和             |
|     cumprod      |            前面所有数据乘积             |
|      cummax      |           前面所有数据最大值            |
|      cummin      |           前面所有数据最小值            |
|    rolling(n)    | window.rolling文件，前n个数据聚合在一起 |
| rolling(n).sum() |              前n个数据之和              |

```python
df1=pd.DataFrame({'Data1':np.random.randint(0,10,5),
                  'Data2':np.random.randint(10,20,5)
                 })
print(df1)
print(df1.cumsum())
print(df1.rolling(2).sum())
```

```python
df1=pd.DataFrame({'Data1':np.random.randint(0,10,5),
                  'Data2':np.random.randint(10,20,5),
                  'key1':list('aabba'),
                  'key2':list('xyyxy')})
print(df1)
```

* 按key1分组，进行聚合计算
    当分组后进行数值计算时，不是数值类的列（即麻烦列）不会参与

```python
df1.groupby('key1').sum()
```

只算data1

```python
print(df1['Data1'].groupby(df1['key1']).sum())
print(df1.groupby('key1')['Data1'].sum())
```

* 使用agg()函数做聚合运算
  `agg(['func_name1','func_name2'])`
  只能用于DataFrame

```python
print(df1.groupby('key1').agg('sum'))
print(df1.groupby('key1').agg(['sum','mean','std']))
```

可自定义函数，传入agg方法中

```python
def peak_range(df):
    return df.max() - df.min()
# 同时应用多个聚合函数，自定义函数可重命名，用元组表示
df1.groupby('key1').agg(['sum','mean','std',('range', peak_range)])
```

* apply函数

​       可以用于DataFrame和Series

```python
df1=pd.DataFrame({'gender':list('FFMFMMF'),'smoker':list('YNYYNYY'),'age':[21,30,17,37,40,18,26],'weight':[120,100,132,140,94,89,123]})
print(df1)

def bin_age(age):
    if age >=18:
        return 1
    else:
        return 0

'''年龄大于等于18'''
print(df1['age'].apply(bin_age))
df1['age'] = df1['age'].apply(bin_age)
print(df1)
```

取出抽烟和不抽烟的体重前二名

```python
def top(df,smoker,weight):
    for name,group in df1.groupby(smoker):
        return group.sort_values(by=weight)[weight][-1:-3:-1]

df1.apply(top,smoker='smoker',weight='weight')


def top(smoker,col,n=5):
        return smoker.sort_values(by=col)[-n:]
df1.groupby('smoker').apply(top,col='weight',n=2)
```

## 数据读取和处理
### csv文件

读取

```python
data=pd.read_csv('../movie_metadata.csv')
print(data.shape)
print(data.head(10))
```

处理缺失值

```python
data = data.dropna()
print(data.head())
```

查看票房收入统计，各导演的总票房

```python
group_director = data.groupby(by='director_name')['gross'].sum()
result=group_director.sort_values(ascending=False)
result
```

```python
import matplotlib.pyplot as plt
from matplotlib import font_manager as fm
res=data['title_year'].groupby(data['title_year']).count()
year=res.index.tolist()
counts=res.values.tolist()
plt.figure(figsize=(20,8),dpi=80)
my_font=fm.FontProperties(fname='C:\\Windows\\Font\\SourceHanMono.ttc',size=18)
plt.plot(year,counts,linestyle='--',marker='D')
plt.xlabel('年份',fontproperties=my_font)
plt.ylabel('电影数量',fontproperties=my_font)
plt.show()
```

## Excel文件

创建文件

```python
df = pd.DataFrame({'id':[1,2,3],'name':['zs','ls','ww']})

'''默认会有索引，将ID列设置成索引,
添加参数inplace=True,修改原来的df''' 
df = df.set_index('id')
df.to_excel('./test_create.xlsx')
```

读取文件

```python
people = pd.read_excel('./data/People.xlsx')
print('获取文件中的行数和列数：',people.shape)
print('获取文件中的列名：',people.columns)
print('获取文件中的前5行数据信息：',people.head())
print('获取文件中的后5行数据信息：',people.tail())
```

指定index_col作为index

```python
people1 = pd.read_excel('./data/People_u.xlsx',index_col = "Type1")
print(people1.head())
```

读取的时候，默认会将第一行作为列名，修改第二行作为列名

```python
people = pd.read_excel('./data/People1.xlsx',header = 2)
print(people.columns)
```

`header=None`使用默认的0，1，2……作为列名

```python
people = pd.read_excel('./data/People.xlsx',header = None)
print(people.columns)
print(people.head())
```

自定义列名

```python
people.columns = ['ID1','Type1','Title1','FirstName1','MiddleName1','LastName1']
print(people.columns)
print(people.head())
```

工作簿中存在多个表时，指定读取表

```python
sheet = pd.read_excel('./data/sheet.xlsx',sheet_name='sheet2')
print(sheet.head())
```

数据在表中没有顶格时
 skiprows : 跳过几行
 usecols: 读取几列，C:F（读取区间[C,F）,C,指的就是Excel上的ABCD....）

```python
book = pd.read_excel('./data/Books.xlsx',skiprows=3,usecols ="C:F")
print(book.head())
```

修改ID的值
`at[]`：通过索引选择值
`iat[]`：通过索引位置选择值
类似于loc,iloc,一般用在取一个行列确定的具体的值上

```python
print(book['ID'])
book["ID"].at[0] = 1
print(book['ID'])
```

重新存储数据

```python
peole=people.set_index('ID1')
print(peole.head())
people.to_excel('./data/People_u.xlsx')
```

## 连接MySQL数据库

* pandas

```python
import pandas as pd
import pymysql

conn =pymysql.connect(host='localhost',user='root',passwd='123456',db='mysql2019',port=3306,charset='utf8mb4')

query = 'SELECT area,name FROM manager'

df = pd.read_sql_query(query,conn)
print(df)
```

* python

```python
def create_phone():
    pass

import pymysql
# 连接数据库
conn=pymysql.connect(host='localhost',user='root',passwd='123456',db='telephone')

# 创建游标
cursor=conn.cursor()

# 执行事务

for i in range(10):
    tel=create_phone()
    
    cursor.execute('insert into tel(tel) values("{}")'.format(tel)) # {}外的引号不可丢
    conn.commit()
# 关闭游标
cursor.close()

# 关闭数据库
conn.close()

```

