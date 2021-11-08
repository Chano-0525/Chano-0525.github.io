# Python可视化


此笔记记载通过使用python matplotlib等数据可视化工具的方法。

### Python matplotlib

#### marplotlib的总体概念
最大的概念是figure，每个figure可以有多个axes，每个axes有两个或者三个（3D）axis，可以通过以下代码进行创建：

```python
fig = plt.figure() # 创建一个figure
fig, ax = plt.subplots() # 创建一个figure并返回figure和一个Axes
fig, axs = plt.subplots(2,2) # 创建一个带有2行2列（共4个）Axes的figure
axs[0,0].plot(x,y)
axs[1,1].scatter(x,y)
......
```

subplots()返回Axes对象的数组，每个axes都是一个单独的子图，可以通过axes.Axes.set_xlim()和axes.Axes.set_ylim()方法控制x轴和y轴的长度，同时可以通过set_xlabel()和set_ylabel()来设置两个轴的标题，通过legend()方法显示该axes的图注。通过set_title()设置axes的大标题。注意，plot()函数的输入必须是numpy的array类型。

建议通过以下的格式来抽象出一个绘图函数：

```python
def my_plotter(ax, data1, data2, param_dict):
    """
    A helper function to make a graph
    Parameters
    -----------
    ax : Axes
    	The axes to draw to
    data1 : array
    	The x data
    data2 : array
    	The y data
    param_dict : dict
    	Dictionary of kwargs to pass to ax.plot
    Returns
    ------
    out : list
    	list of artists added
    """
    out = ax.plot(data1,data2,**param_dict)
    return out
```

#### plot函数的使用
一般是：
```python
plot(x,y,...)
```

后面的参数有以下：

| 参数名 | 描述      |
| ------ | --------- |
| color  | color颜色 |
| linestyle | 线形，{'-','--','-.',':'} |
| linewidth | 线的宽度,float |
|marker | 点的标记，具体见下 |

可以通过format string控制，format string的格式为
```python
fmt = '[marker][line][color]'
...
fmt = 'o-r'
plot(x,y,fmt)
```
点的标记有以下格式

| character | description           |
| --------- | --------------------- |
| '.'       | point marker          |
| ','       | pixel marker          |
| 'o'       | circle marker         |
| 'v'       | triangle_down marker  |
| '^'       | triangle_up marker    |
| '<'       | triangle_left marker  |
| '>'       | triangle_right marker |
| '1'       | tri_down marker       |
| '2'       | tri_up marker         |
| '3'       | tri_left marker       |
| '4'       | tri_right marker      |
| 's'       | square marker         |
| 'p'       | pentagon marker       |
| '*'       | star marker           |
| 'h'       | hexagon1 marker       |
| 'H'       | hexagon2 marker       |
| '+'       | plus marker           |
| 'x'       | x marker              |
| 'D'       | diamond marker        |
| 'd'       | thin_diamond marker   |
| '\|'      | vline marker          |
| '-'       | hline marker          |

颜色的分类有以下：

| character | color   |
| --------- | ------- |
| 'b'       | blue    |
| 'g'       | green   |
| 'r'       | red     |
| 'c'       | cyan    |
| 'm'       | magenta |
| 'y'       | yellow  |
| 'k'       | black   |
| 'w'       | white   |

如果format string ***只设定了*** 颜色，可以使用16进制串如‘#008000’.

#### 分层设色地形图/等高线图相关
##### 需要用到的函数
```python
contour([X,Y,]Z,[levels], **kwargs) # 只能绘制线
contourf([X,Y,]Z,[levels], **kwargs) # 只能绘制色块
```
X,Y都是坐标，Z是高度，levels是高度的分级（必须是递增）重要参数有：
* colors : 指定每个level的颜色，如果是contour则指定了线的颜色，如果是contourf则指定了色块的颜色
* extend : 取值有{'neither', 'both', 'min', 'max'}, 这个指定了超出等级范围的色块的显示，如果设置neither，超出范围都是空白，如果选min则对低于最低level的有效，如果选max则对高于最高level的有效，选both对所有范围都有效，一般选both。可以通过cmap的set_over()和set_under()来设定超过上限和下限的颜色，更换颜色以后需要使用cs.changed()来调整（注：cs是contour或者contourf的返回，是QuadContourSet类型，大概是代表了所有等高线的一个集合set）
* linewidths: 线的宽度，只适用于contour
* linestyles:线的类型，可选的值有{None, 'solid', 'dashed', 'dashdot', 'dotted'}，只适用于contour
* extend : 一个四元组如（-3,4,-4,3）,指定了图片的左上角和右下角，即划分了范围

一个简单的例子如下：
```python
import numpy as np
import matplotlib.pyplot as plt
x = np.arange(1,10)
y = x.reshape(-1,1)

h = x * y
cs = plt.contourf(h, levels=[10,30,50], 
	colors=['#808080','#A0A0A0','#C0C0C0'],extend='both')
plt.show()
```
##### 在等高线上绘制值

通过

```python
clabel(CS, inline=True, fontsize=10) 
```

绘制值，其中inline指定这个值是否被登高线遮住，一般是选择True，让值遮住线，fontsize则是选择值的字体大小。

例子如下：

```python
import numpy as np
import matplotlib.pyplot as plt

delta = 0.025
x = np.arange(-3.0, 3.0, delta)
y = np.arange(-2.0, 2.0, delta)
X, Y = np.meshgrid(x,y)
Z1 = np.exp(-X**2 - Y**2)
Z2 = np.exp(-(X-1)**2 - (Y-1)**2)
Z = (Z1 - Z2) * 2
fig, ax = plt.subplots()
CS = ax.contour(X,Y,Z)
ax.clabel(CS, inline=True, fontsize=10)
ax.set_title('Simplest default with labels')
plt.show()
```

#### 绘制直方图

使用

```python
hist()
```

进行绘制，主要的参数有

| 参数        | 值                                                           |
| ----------- | ------------------------------------------------------------ |
| x           | 输入，可以是一维或者多维数组（多维数组不要求等长）           |
| bins        | 区间，一个一维数组如[1,2,3,4]，代表了1到2，2到3，3到4这三个区间，将会统计每个区间的个数并显示 |
| histtype    | 绘制的柱的类型，可选的值有{'bar','barstacked','step','stepfilled'}，step指只画线 |
| align       | 可选的值有{'left', 'mid', 'right'}，指柱子是在一个bin中的位置 |
| orientation | 可选的值有{'vertical', 'horizontal'}，指定了图的方向         |
| stacked     | 多维数据的显示方式，正常是放在柱子的旁边，如果是True，将堆叠在上方 |
| rwidth      | 柱子宽度，**感觉**是按（0，1）的百分比来的                   |

例子如下：

```python
import numpy as np
import matplotlib.pyplot as plt

x = [[1.2,1.2,2.2,-2.2,-1.2],[2.2,-0.2]]   # 一个二维的数据
fig, axs = plt.subplots(2,2)
axs[0,0].hist(x,bins=[-3,-2,-1,0,1,2,3], rwidth=0.5)
axs[0,0].set_title('stacked=False')

axs[0,1].hist(x,bins=[-3,-2,-1,0,1,2,3], rwidth=0.5, stacked=True)
axs[0,1].set_title('stacked=True')

axs[1,0].hist(x,bins=[-3,-2,-1,0,1,2,3], rwidth=0.5, orientation='horizontal')
axs[1,0].set_title('orientation=\'horizontal\'')

axs[1,1].hist(x,bins=[-3,-2,-1,0,1,2,3], rwidth=0.5, histtype='step')
axs[1,1].set_title('histtype=\'step\'')
plt.show()
```

结果如下

![图3](/images/figure3.png)

####  矢量图

```python
ax.streamplot(X,Y,U,V,...)
```

绘制矢量图首先需要一个X,Y网格，可以使用np.mgrid来绘制，X是一个二维矩阵，里面每个元素是每个点的X值，Y是一个二维矩阵，里面每个元素是每个点的Y值，对于每个点（X，Y）需要给出这一点的矢量（U，V）。满足X,Y,U,V已经可以绘制简单的矢量图，有以下参数可以对图片进行调整，比如density（用于调整图片矢量的疏密），linewidth（用于调整，图上矢量线的宽度），color（调整图上矢量的颜色），linewidth和color都可以是二维变量，猜测是表示每个矢量的颜色。除此之外，可以设定图中矢量经过的点...以下是例子

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.gridspec as gridspec

w = 3
Y, X = np.mgrid[-w:w:100j, -w:w:100j]
U = -1 - X**2 + Y
V = 1 + X - Y**2
speed = np.sqrt(U**2 + V**2)            # 矢量的大小，这里表示这个矢量的快慢速度
fig, axs = plt.subplots(2,2)

axs[0,0].streamplot(X,Y,U,V,density=[0.5,1])
axs[0,0].set_title('Varying Density')

axs[0,1].streamplot(X,Y,U,V,color=U,linewidth=2,cmap='autumn')
axs[0,1].set_title('Varying Color')

lw = 5 * speed / speed.max()
axs[1,0].streamplot(X, Y, U, V, density=0.6, color='k', linewidth=lw)   # 某点矢量越大，线条越粗
axs[1,0].set_title('Varying Line Width')

# seed_points 是设定矢量图需要经过的点
seed_points = np.array([[-2,-1,0,1,2,-1],[-2,-1,0,1,2,2]])
axs[1,1].streamplot(X,Y,U,V,color=U,linewidth=2,cmap='autumn', start_points=seed_points.T)
axs[1,1].set_title("Controlling Strating Points")
axs[1,1].plot(seed_points[0],seed_points[1],'bo')

plt.show()
```




### 参考文献

* [Matplotlib Usage Guide](https://matplotlib.org/tutorials/introductory/usage.html#sphx-glr-tutorials-introductory-usage-py)
