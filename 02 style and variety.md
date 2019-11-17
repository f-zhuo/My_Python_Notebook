# 风格

python是区分大小写的，list和List是不同的

## 注释

* 单行采用 #
* 多行可以用 """ """ 或者 ''' '''

如

```python
print('Hello World') # 打印Hello World这个句子
```

```python
def pri():
"""
这是一段注释
可以作用于多行
"""
   print('这是个打印函数')
```

## 分行

**采用`\`** 

如

```python
s = 'Hell\
o World'
print(s)
```

**()中的内容也可以分行，但要使用引号组成一个整体**

```python
print('Hell'
'o World')
```

## 缩进

表示一个代码块

如

```python
a = 1
if a % 2 == 0:
	print('a是偶数')
else:
	print('a是奇数')
```

# 输入输出函数

## 输入函数

变量名=input(提示语)

如

```python
name = input('请输入您的姓名:')
#请输入您的姓名:zf
```

函数输出的是字符串类型
```python
print(name,type(name))
#zf <class 'str'>
```

type()函数可以显示对象的数据类型
这里的'str'就是string，表示字符串类型

## 输出函数

print()

# 变量

## 变量的赋值

python不同于其他大部分语言，变量不需要声明，直接赋值即可

如

```python
a = 1
a = 'python'
a = [1,2,3]
```

## 命名规则
由数字，字母，_组成，不可以数字开头，_或__开头的变量属于私有或半私有变量，一般不采用，同时应避免关键字和保留字

<img src="./pictures/reserved words.png" style="zoom:70%" />


## 命名规范
* 下划线命名：所有字母小写，单词间以_连接
* 驼峰命名：首字母大写，每个单词首字母大写，一般用于类名

