一 用户界面
我们必须要通过软件来对计算机完成各种操作，但是软件中并不是所有的功能都会对用户开放，用户需要调用软件提供的接口（Interface交互界面）来操作计算机

用户界面分成两种：TUI（文本交互界面）和 GUI（图形化交互界面）

1.文本交互界面

* Windows：命令行/DOS窗口

* Linux：shell，终端/Terminal


2.图形化交互界面

Windows的大部分的操作，比如双击图标打开我的电脑


二 环境变量

环境变量是给系统或应用程序设置的参数，系统变量会对整个计算机系统进行设置，用户变量只会在当前用户登陆下生效

* Windows：一个环境变量可以有多个值，值与值之间使用;（英文）隔开

* Linux：系统环境变量存储在/etc/profile,/etc/bashrc等文件里，管理员用户环境变量存储在 ~/.bash_profile,~/.bashrc等文件里。在正常的登陆命令下，首先访问/etc/profile，这个文件只访问一次；非正常登陆命令下，首先访问/etc/bashrc，每次打开新的bash shell都会访问一次


2.1 Linux的PATH变量:

是最常用的环境变量，保存的是应用程序的安装路径或者命令的存放路径。

PATH可以有多个值，以:（英文）分割，形式：PATH=/aaa/bbb:/ccc/ddd

查看Linux系统的所有环境变量：export

查看Linux系统的所有PATH变量：echo $PATH
其中，echo是打印的意思，$表示后面跟着的是变量名
   
2.1.1 PATH变量的设置

1.export

* 设置新PATH变量
  export PATH=/usr/local/src/test

 此种方法立刻生效，但只在本次登陆的本个shell窗口有效，一旦关闭本shell窗口就失效，会覆盖原PATH变量的值

* 添加PATH变量
  export PATH=$PATH:/usr/local/src/test
或
  export PATH=/usr/local/src/test:$PATH

   和上一种情况一样，不同之处在于，本方法在原PATH变量的值后，追加了/usr/local/src/test这个路径，系统在寻找PATH值 时，会从前往后搜索，一旦找到就会停止，所以要把同一应用程序的优先使用版本放在前面

2.在系统配置文件里写入PATH

以/etc/profile为例
   打开文件：
     vi /etc/profile
   在文件底部追加：
     export PATH=/usr/local/src/test:$PATH 
   为使文件生效，退出文件在终端输入：
     source /etc/profile
    
在系统配置文件中写入的好处在于，以后每一次登陆，不管是哪个用户都生效，但是必须要source

3.在用户配置文件里写入PATH

以~/.bashrc为例
   打开文件：
     vi ~/.bashrc
   在文件底部追加：
     export PATH=/usr/local/src/test:$PATH
   为使文件生效，退出文件在终端输入：
     source ~/.bashrc

2.2 Windows的path变量

  当我们在命令行中输入一个命令（或访问一个文件时），系统会首先在当前目录下寻找，如果找到了则直接执行或打开如果没有找到，则会依次去path环境变量的路径中去寻找，直到找到为止。如果path环境变量中的路径都没有找到，则报错
  
将文件或程序的路径添加到path/PATH环境变量中的意义在于，可以在任意的位置访问这些文件


三 运行python

3.1 Windows

1.Windows命令行下运行python：
* 输入python，进入交互模式，退出：CTRL+z
* 文件另存为C:/aa/filename.py:
  * cd C:/aa
    python filename.py
  * python C:/aa/filename.py

 
2.Windows命令行下输入ipython，进入ipython解释器，像jupyter一样可进行交互
* 使用[函数名?/??]的方法查看帮助
* magic：查看魔法命令
* 退出：CTRL+d

3.Windows命令行下输入jupyter notebook,地址为http://localhost:8888

3.2 Linux
系统自带了python，在shell中输入python即可，但要注意的是，系统自带的版本为python2，最好自己安装一个python3，配置PATH路径

3.3 anaconda
第三方科学计算包管理工具，可以管理多个python版本，简单方便