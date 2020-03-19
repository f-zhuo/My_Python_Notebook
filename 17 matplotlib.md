# matplotlib

## 折线图plot

反应连续数据的变化趋势

```python
from matplotlib import pyplot as plt
x = range(1,8) 
y = [17, 17, 18, 15, 11, 11, 13]

# 设置图片的大小
'''
figsize:指定figure的宽和高，单位为英寸；
dpi指定绘图对象的分辨率，即每英寸多少个像素，缺省值为80      
'''
plt.figure(figsize=(20,8),dpi=80)

# 传入x和y, 通过plot画折线图
plt.plot(x,y) 
# plt.show()

# 保存(注意：plt.show()会释放figure资源，如果在这之后保存图片将只能保存空图片)
plt.savefig('./t1.png')
# 图片的格式也可以保存为svg这种矢量图格式，这种矢量图放在网页中放大后不会有锯齿
# plt.savefig('./t1.svg')
```

**plot中的参数**

|   参数    |       含义        |
| :-------: | :---------------: |
|   color   |    折线的颜色     |
|   alpha   | 折线的透明度(0-1) |
| linestyle |    折线的样式     |
| linewidth |    折线的宽度     |
|  marker   |      标记点       |

**linestyle**

| 符号 |            含义             |
| :--: | :-------------------------: |
|  -   | 实线(solid)，注意不是下划线 |
|  --  |        短线(dashed)         |
|  -.  |     短点相间线(dashdot)     |
|  ：  |       虚点线(dotted)        |

**marker**

| 符号 |  含义  |
| :--: | :----: |
|  o   | 实心圆 |
|  .   |   点   |
|  *   |   星   |
|  D   |  钻石  |
|  s   | 正方形 |

```python
from matplotlib import pyplot as plt
x = range(1,8) 
y = [17, 17, 18, 15, 11, 11, 13]

# 传入x和y, 通过plot画折线图
plt.plot(x,y,'r-o',linewidth=3,alpha=0.5) 
plt.show()
```

### 绘制x轴和y轴的刻度

```python
x_ticks_label = ["{}:00".format(i) for i in x]
y_ticks_label = ["{}℃".format(i) for i in range(min(y),max(y)+1)]
plt.xticks(x,x_ticks_label,rotation = 45) # 刻度值，刻度标签
plt.yticks(range(min(y),max(y)+1),y_ticks_label)
```

### 显示中文

matplotlib不支持中文输出，要调用其他方法

```python
from matplotlib import font_manager
my_font = font_manager.FontProperties(fname='C:/Windows/Fonts/PingFang.ttc',size=18)

# 设置x轴和y轴标题
plt.xlabel("次数",fontproperties=my_font)

# 设置图像标题
plt.title('每分钟跳动次数',fontproperties=my_font,color='red')
```

### 一图多线

```python
x = range(11,31)
y1 = [1,0,1,1,2,4,3,4,4,5,6,5,4,3,3,1,1,1,1,1]
y2 = [1,0,3,1,2,2,3,4,3,2,1,2,1,1,1,1,1,1,1,1]

plt.plot(x,y1,color='red',label='甲')
plt.plot(x,y2,color='blue',label='乙')
# 绘制网格
plt.grid(alpha=0.4)

# 添加图例(注意：只有这里显示中文添加的参数是prop，其他的都用fontproperties)
# 设置位置loc : upper left、 lower left、 center left、 upper center
plt.legend(prop=my_font,loc='upper right')
plt.show()
```

### **一个画布多张子图**

#### subplots

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(1, 100)
#划分子图
fig,axes=plt.subplots(2,2)
ax1=axes[0,0]
ax2=axes[0,1]
ax3=axes[1,0]
ax4=axes[1,1]
 
fig=plt.figure(figsize=(20,10),dpi=80)
#作图1
ax1.plot(x, x)
#作图2
ax2.plot(x, -x)
#作图3
ax3.plot(x, x ** 2)
#作图4
ax4.plot(x, np.log(x))
plt.show()
```

#### add_subplot

```python
fig=plt.figure(figsize=(20,10),dpi=80)
#新建子图1
ax1=fig.add_subplot(2,2,1)
ax1.plot(x, x)
#新建子图2
ax3=fig.add_subplot(2,2,2)
ax3.plot(x, x ** 2)
ax3.grid(color='r', linestyle='--', linewidth=1,alpha=0.3)
#新建子图3
ax4=fig.add_subplot(2,2,3)
ax4.plot(x, np.log(x))
plt.show()
```

#### subplot

```python
fig=plt.figure(figsize=(20,10),dpi=80)
#作图1
plt.subplot(2,2,1)
plt.plot(x, x)
#作图2
plt.subplot(2,2,2)
plt.plot(x, -x)
#作图3
plt.subplot(2,2,3)
plt.plot(x, x ** 2)
#作图4
plt.subplot(2,2,4)
plt.plot(x, np.log(x))
plt.show()
```

### **设置坐标轴范围**

```python
# 设置x轴的左右极限
plt.xlim([-5,5])
# 只设置一边
plt.xlim(xmin=-4)
plt.xlim(xmax=4)
plt.ylim(ymin=0)
```

### **改变坐标轴的显示方式**和位置

```python
# 获得当前图表的图像
ax = plt.gca()

# 设置图像外面的4条包围线
ax.spines['right'].set_color('none')
ax.spines['top'].set_color('none')
ax.spines['bottom'].set_color('blue')
ax.spines['left'].set_color('red')

# 设置底边线的位置，与y轴的0刻度对齐,'data':移动轴的位置到交叉轴的指定坐标
ax.spines['bottom'].set_position(('data', 0))
ax.spines['left'].set_position(('data', 2))
```

## 散点图scatter

```python
from matplotlib import pyplot as plt
from matplotlib import font_manager
y = [11,17,16,11,12,11,12,6,6,7,8,9,12,15,14,17,18,21,16,17,20,14,15,15,15,19,21,22,22,22,23]
x = range(1,32)

plt.figure(figsize=(20,8),dpi=80)
# 使用scatter绘制散点图
plt.scatter(x,y,label= '3月份')

my_font = font_manager.FontProperties(fname='C:/Windows/Fonts/PingFang.ttc',size=10)

xticks_labels = ['3月{}日'.format(i) for i in x]

plt.xticks(x[::3],xticks_labels[::3],fontproperties=my_font,rotation=45)
plt.xlabel('日期',fontproperties=my_font)
plt.ylabel('温度',fontproperties=my_font)

plt.legend(prop=my_font)
plt.show()
```

## 柱状图bar/条形图barh

#### 柱状图

```python
a = ['流浪地球','疯狂的外星人','飞驰人生','大黄蜂','熊出没·原始时代','新喜剧之王']
b = ['38.13','19.85','14.89','11.36','6.47','5.93']
'''
from matplotlib import pyplot as plt
from matplotlib import font_manager
a = ['流浪地球','疯狂的外星人','飞驰人生','大黄蜂','熊出没·原始时代','新喜剧之王']
b = ['38.13','19.85','14.89','11.36','6.47','5.93']
# b =[38.13,19.85,14.89,11.36,6.47,5.93]

my_font = font_manager.FontProperties(fname='C:/Windows/Fonts/PingFang.ttc',size=10)

plt.figure(figsize=(20,8),dpi=80)

# 绘制柱状图
rects = plt.bar(range(len(a)),[float(i) for i in b],width=0.3,color= 'red')
plt.xticks(range(len(a)),a,fontproperties=my_font)

plt.yticks(range(0,41,5),range(0,41,5))

# 在柱状图上加标注(水平居中)
for rect in rects:
    height = rect.get_height()
    plt.text(rect.get_x() + rect.get_width() / 2, height+0.3, str(height),ha="center")
plt.show()
```

#### 条形图

```python
rects = plt.barh(range(len(a)),b,height=0.5,color='r')
plt.yticks(range(len(a)),a,fontproperties=my_font,rotation=45)
# 在条形图上加标注(水平居中)
for rect in rects:
	# print(rect.get_x())
	width = rect.get_width()
	plt.text(width, rect.get_y()+0.3/2, str(width),va="center")
plt.show()
```

#### 并列柱状图

```python
import matplotlib.pyplot as plt
import numpy as np
index = np.arange(4)
BJ = [50,55,53,60]
Sh = [44,66,55,41]

plt.bar(index,BJ,width=0.3)
plt.bar(index+0.3,Sh,width=0.3,color='green')
plt.xticks(index+0.3/2,index)
plt.show()
```

#### 堆积柱状图

```python
plt.bar(index,Sh,bottom=BJ,width=0.3,color='green')
plt.show()
```

## 直方图hist

```python
time = [131, 98, 125, 131, 124, 139, 131, 117, 128, 108, 135, 138, 131, 102, 107, 114, 119, 128, 121, 142, 127, 130, 124, 101, 110, 116, 117, 110, 128, 128, 115, 99, 136, 126, 134,  95, 138, 117, 111,78, 132, 124, 113, 150, 110, 117,  86,  95, 144, 105, 126, 130,126, 130, 126, 116, 123, 106, 112, 138, 123,  86, 101,  99, 136,123, 117, 119, 105, 137, 123, 128, 125, 104, 109, 134, 125, 127,105, 120, 107, 129, 116, 108, 132, 103, 136, 118, 102, 120, 114,105, 115, 132, 145, 119, 121, 112, 139, 125, 138, 109, 132, 134,156, 106, 117, 127, 144, 139, 139, 119, 140,  83, 110, 102,123,107, 143, 115, 136, 118, 139, 123, 112, 118, 125, 109, 119, 133,112, 114, 122, 109, 106, 123, 116, 131, 127, 115, 118, 112, 135,115, 146, 137, 116, 103, 144, 83, 123, 111, 110, 111, 100, 154,136, 100, 118, 119, 133, 134, 106, 129, 126, 110, 111, 109, 141,120, 117, 106, 149, 122, 122, 110, 118, 127, 121, 114, 125, 126,114, 140, 103, 130, 141, 117, 106, 114, 121, 114, 133, 137,  92,121, 112, 146,  97, 137, 105, 98, 117, 112,  81, 97, 139, 113,134, 106, 144, 110, 137, 137, 111, 104, 117, 100, 111, 101, 110,105, 129, 137, 112, 120, 113, 133, 112,  83,  94, 146, 133, 101,131, 116, 
111,  84, 137, 115, 122, 106, 144, 109, 123, 116, 111,111, 133, 150]
my_font = font_manager.FontProperties(fname='C:/Windows/Fonts/PingFang.ttc',size=10)

plt.figure(figsize=(20, 8), dpi=100)

# 设置组距
distance = 2
# 计算组数
group_num = int((max(time) - min(time)) / distance)

plt.hist(time, bins=group_num)

plt.xticks(range(min(time), max(time))[::2])
plt.grid(linestyle="--", alpha=0.5)
plt.xlabel("电影时长大小",fontproperties=my_font)
plt.ylabel("电影的数据量",fontproperties=my_font)

plt.show()
```

## 饼状图pie

```python
label_list = ["第一部分", "第二部分", "第三部分"]    # 各部分标签
size = [55, 35, 10]    # 各部分大小
color = ["red", "green", "blue"]     # 各部分颜色
explode = [0, 0.05, 0]   # 各部分突出值
"""
绘制饼图
explode：设置各部分突出
label:设置各部分标签
labeldistance:设置标签文本距圆心位置，1.1表示1.1倍半径
autopct：设置圆里面文本
shadow：设置是否有阴影
startangle：起始角度，默认从0开始逆时针转
pctdistance：设置圆内文本距圆心距离
返回值
patches：图形对象
l_text：圆内部文本，matplotlib.text.Text object
p_text：圆外部文本
"""
patches, l_text, p_text = plt.pie(size, 
                                  explode=explode, 
                                  colors=color, 
                                  labels=label_list, 
                                  labeldistance=1.1, 
                                  autopct="%1.1f%%", 
                                  shadow=False, 
                                  startangle=90,
                                  pctdistance=0.6)

for t in l_text: 
    t.set_fontproperties(my_font)
    
plt.legend(prop=my_font)
plt.show()
```



