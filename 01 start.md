# 用户界面

我们必须要通过软件来对计算机完成各种操作，但是软件中并不是所有的功能都会对用户开放，用户需要调用软件提供的接口（Interface/交互界面）来操作计算机

用户界面分成两种：TUI（文本交互界面）和 GUI（图形化交互界面）

## 文本交互界面

* Windows：命令行/DOS窗口

* Linux：终端/Terminal


## 图形化交互界面

Windows的大部分的操作，比如双击图标打开我的电脑


# 环境变量

环境变量是给系统或应用程序设置的参数，系统变量会对整个计算机系统进行设置，用户变量只会在当前用户登陆下生效

* Windows：一个环境变量可以有多个值，值与值之间使用;（英文）隔开
* Linux：系统环境变量存储在```/etc/profile```,```/etc/bashrc```等文件里，管理员用户环境变量存储在 ```~/.bash_profile```,```~/.bashrc```等文件里。在正常的登陆命令下，首先访问```/etc/profile```，这个文件只访问一次；非正常登陆命令下，首先访问```/etc/bashrc```，每次打开新的bash shell都会访问一次


## Linux的PATH变量

是最常用的环境变量，保存的是应用程序的安装路径或者命令的存放路径。PATH可以有多个值，以:（英文）分割，形式为：```PATH=/aaa/bbb:/ccc/ddd```

* 查看Linux系统的所有环境变量：```export```

* 查看Linux系统的所有PATH变量：```echo $PATH```

  其中，echo是打印的意思，$表示后面跟着的是变量名

### 设置PATH变量

#### export

* 设置新PATH变量
  
  ```
  export PATH=/usr/local/src/test
  ```

此种方法立刻生效，但只在本次登陆的本个shell窗口有效，一旦关闭本shell窗口就失效，会覆盖原PATH变量的值

* 添加PATH变量
  
```shell
  export PATH=$PATH:/usr/local/src/test
```
  
  或
  
  ```shell
  export PATH=/usr/local/src/test:$PATH
  ```
  
  和上一种情况一样，不同之处在于，本方法在原PATH变量的值后，追加了/usr/local/src/test这个路径，系统在寻找PATH值 时，会从前往后搜索，一旦找到就会停止，所以要把同一应用程序的优先使用版本放在前面

#### 在系统配置文件里写入PATH

以```/etc/profile```为例

* 打开文件

```shell
vi /etc/profile
```

* 在文件底部追加

```shell
export PATH=/usr/local/src/test:$PATH 
```

* 为使文件生效，退出文件在终端输入

```shell
source /etc/profile
```


在系统配置文件中写入的好处在于，以后每一次登陆，不管是哪个用户都生效

#### 在用户配置文件里写入PATH

以```~/.bashrc```为例

* 打开文件

```shell
vi ~/.bashrc
```

* 在文件底部追加

 ```shell
export PATH=/usr/local/src/test:$PATH
 ```

* 为使文件生效，退出文件在终端输入

```shell
source ~/.bashrc
```


## Windows的path变量

当我们在命令行中输入一个命令（或访问一个文件时），系统会首先在当前目录下寻找，如果找到了则直接执行或打开如果没有找到，则会依次去path环境变量的路径中去寻找，直到找到为止。如果path环境变量中的路径都没有找到，则报错

将文件或程序的路径添加到path/PATH环境变量中的意义在于，可以在任意的位置访问这些文件


# 运行python

## Windows

### Windows命令行下运行python
* 输入python，进入交互模式；退出：```CTRL+z```

* 文件另存为```C:/aa/filename.py```
  ```shell
  cd C:/aa
  python filename.py
  ```
  
  或
  
  ```shell
  python C:/aa/filename.py
  ```

### Windows命令行下运行ipython

输入ipython，进入解释器，像jupyter一样可进行交互

* magic：查看魔法命令
* 退出：CTRL+d

### 运行jupyter

Windows命令行下输入jupyter notebook，默认浏览器会跳转到该网页，地址为http://localhost:8888

## Linux
系统自带了python，在shell中输入python即可，但要注意的是，系统自带的版本为python2，最好自己安装一个python3，配置PATH路径

## anaconda
第三方科学计算包管理工具，可以管理多个python版本，简单方便

# 风格

python是区分大小写的，list和List是不同的

## 注释

- 单行采用 #
- 多行可以用 """ """ 或者 ''' '''

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
    
pri()
```

## 分行

采用`\`，分行的原因是某行太长，写成多行，实际上仍为一行

如

```python
s = 'Hell\
o World'
print(s)

# Hello World
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

