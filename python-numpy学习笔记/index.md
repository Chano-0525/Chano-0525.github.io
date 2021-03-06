# Python-Numpy


# Numpy库介绍

`NumPy`是一个功能强大的`Python`库，主要用于对多维数组执行计算。`NumPy`这个词来源于两个单词-- `Numerical`和`Python`。`NumPy`提供了大量的库函数和操作，可以帮助程序员轻松地进行数值计算。在数据分析和机器学习领域被广泛使用。他有以下几个特点：  
1. numpy内置了并行运算功能，当系统有多个核心时，做某种计算时，numpy会自动做并行计算。  
2. Numpy底层使用C语言编写，内部解除了GIL（全局解释器锁），其对数组的操作速度不受Python解释器的限制，效率远高于纯Python代码。  
3. 有一个强大的N维数组对象Array（一种类似于列表的东西）。  
4. 实用的线性代数、傅里叶变换和随机数生成函数。

总而言之，他是一个非常高效的用于处理数值型运算的包。

## 安装：

通过`pip install numpy`即可安装。

## 教程地址：
1. 官网：`https://docs.scipy.org/doc/numpy/user/quickstart.html`。
2. 中文文档：`https://www.numpy.org.cn/user_guide/quickstart_tutorial/index.html`。


## Numpy数组和Python列表性能对比：

比如我们想要对一个Numpy数组和Python列表中的每个素进行求平方。那么代码如下：

```python
# Python列表的方式
t1 = time.time()
a = []
for x in range(100000):
    a.append(x**2)
t2 = time.time()
t = t2 - t1
print(t)
```

花费的时间大约是`0.07180`左右。而如果使用`numpy`的数组来做，那速度就要快很多了：

```python
t3 = time.time()
b = np.arange(100000)**2
t4 = time.time()
print(t4-t3)
```



# NumPy数组基本用法

1. `Numpy`是`Python`科学计算库，用于快速处理任意维度的数组。
2. `NumPy`提供一个**N维数组类型ndarray**，它描述了**相同类型**的“items”的集合。
3. `numpy.ndarray`支持向量化运算。
4. `NumPy`使用c语言写的，底部解除了`GIL`，其对数组的操作速度不在受`python`解释器限制。

## numpy中的数组：

`Numpy`中的数组的使用跟`Python`中的列表非常类似。他们之间的区别如下：  

1. 一个列表中可以存储多种数据类型。比如`a = [1,'a']`是允许的，而数组只能存储同种数据类型。  
2. 数组可以是多维的，当多维数组中所有的数据都是数值类型的时候，相当于线性代数中的矩阵，是可以进行相互间的运算的。

## 创建数组（np.ndarray对象）：

`Numpy`经常和数组打交道，因此首先第一步是要学会创建数组。在`Numpy`中的数组的数据类型叫做`ndarray`。以下是两种创建的方式：

1. 根据`Python`中的列表生成：

   ```python
   import numpy as np
   a1 = np.array([1,2,3,4])
   print(a1)
   print(type(a1))
   ```

2. 使用`np.arange`生成，`np.arange`的用法类似于`Python`中的`range`：

   ```python
   import numpy as np
   a2 = np.arange(2,21,2)
   print(a2)
   ```

3. 使用`np.random`生成随机数的数组：

   ```python
   a1 = np.random.random(2,2) # 生成2行2列的随机数的数组
   a2 = np.random.randint(0,10,size=(3,3)) # 元素是从0-10之间随机的3行3列的数组
   ```

4. 使用函数生成特殊的数组：

   ```python
   import numpy as np
   a1 = np.zeros((2,2)) #生成一个所有元素都是0的2行2列的数组
   a2 = np.ones((3,2)) #生成一个所有元素都是1的3行2列的数组
   a3 = np.full((2,2),8) #生成一个所有元素都是8的2行2列的数组
   a4 = np.eye(3) #生成一个在斜方形上元素为1，其他元素都为0的3x3的矩阵
   ```

## ndarray常用属性：

### `ndarray.dtype`：

因为数组中只能存储同一种数据类型，因此可以通过`dtype`获取数组中的元素的数据类型。以下是`ndarray.dtype`的常用的数据类型：

| 数据类型   | 描述                                                         | 唯一标识符 |
| ---------- | ------------------------------------------------------------ | ---------- |
| bool       | 用一个字节存储的布尔类型（True或False）                      | 'b'        |
| int8       | 一个字节大小，-128 至 127                                    | 'i1'       |
| int16      | 整数，16 位整数\(-32768 ~ 32767\)                            | 'i2'       |
| int32      | 整数，32 位整数\(-2147483648 ~ 2147483647\)                  | 'i4'       |
| int64      | 整数，64 位整数\(-9223372036854775808 ~ 9223372036854775807\) | 'i8'       |
| uint8      | 无符号整数，0 至 255                                         | 'u1'       |
| uint16     | 无符号整数，0 至 65535                                       | 'u2'       |
| uint32     | 无符号整数，0 至 2 \*\* 32 - 1                               | 'u4'       |
| uint64     | 无符号整数，0 至 2 \*\* 64 - 1                               | 'u8'       |
| float16    | 半精度浮点数：16位，正负号1位，指数5位，精度10位             | 'f2'       |
| float32    | 单精度浮点数：32位，正负号1位，指数8位，精度23位             | 'f4'       |
| float64    | 双精度浮点数：64位，正负号1位，指数11位，精度52位            | 'f8'       |
| complex64  | 复数，分别用两个32位浮点数表示实部和虚部                     | 'c8'       |
| complex128 | 复数，分别用两个64位浮点数表示实部和虚部                     | 'c16'      |
| object\_   | python对象                                                   | 'O'        |
| string\_   | 字符串                                                       | 'S'        |
| unicode\_  | unicode类型                                                  | 'U'        |

我们可以看到，`Numpy`中关于数值的类型比`Python`内置的多得多，这是因为`Numpy`为了能高效处理处理海量数据而设计的。举个例子，比如现在想要存储上百亿的数字，并且这些数字都不超过254（一个字节内），我们就可以将`dtype`设置为`int8`，这样就比默认使用`int64`更能节省内存空间了。类型相关的操作如下：

1. 默认的数据类型：

   ```python
   import numpy as np
   a1 = np.array([1,2,3])
   print(a1.dtype) 
   # 如果是windows系统，默认是int32
   # 如果是mac或者linux系统，则根据系统来
   ```

2. 指定`dtype`：

   ```python
   import numpy as np
   a1 = np.array([1,2,3],dtype=np.int64)
   # 或者 a1 = np.array([1,2,3],dtype="i8")
   print(a1.dtype)
   ```

3. 修改`dtype`：

   ```python
   import numpy as np
   a1 = np.array([1,2,3])
   print(a1.dtype) # window系统下默认是int32
   # 以下修改dtype
   a2 = a1.astype(np.int64) # astype不会修改数组本身，而是会将修改后的结果返回
   print(a2.dtype)
   ```

### `ndarray.size`：

获取数组中总的元素的个数。比如有个二维数组：

```python
   import numpy as np
   a1 = np.array([[1,2,3],[4,5,6]])
   print(a1.size) #打印的是6，因为总共有6个元素
```

### `ndarray.ndim`：

数组的维数。比如：

```python
   a1 = np.array([1,2,3])
   print(a1.ndim) # 维度为1
   a2 = np.array([[1,2,3],[4,5,6]])
   print(a2.ndim) # 维度为2
   a3 = np.array([[[1,2,3],[4,5,6]],[[7,8,9],[10,11,12]]])
   print(a3.ndim) # 维度为3
```

### `ndarray.shape`：

数组的维度的元组。比如以下代码：

```python
   a1 = np.array([1,2,3])
   print(a1.shape) # 输出(3,)，意思是一维数组，有3个数据

   a2 = np.array([[1,2,3],[4,5,6]])
   print(a2.shape) # 输出(2,3)，意思是二位数组，2行3列

   a3 = np.array([
       [
           [1,2,3],
           [4,5,6]
       ],
       [
           [7,8,9],
           [10,11,12]
       ]
   ])
   print(a3.shape) # 输出(2,2,3)，意思是三维数组，总共有2个元素，每个元素是2行3列的

   a44 = np.array([1,2,3],[4,5])
   print(a4.shape) # 输出(2,)，意思是a4是一个一维数组，总共有2列
   print(a4) # 输出[list([1, 2, 3]) list([4, 5])]，其中最外面层是数组，里面是Python列表
```

另外，我们还可以通过`ndarray.reshape`来重新修改数组的维数。示例代码如下：

```python
   a1 = np.arange(12) #生成一个有12个数据的一维数组
   print(a1) 

   a2 = a1.reshape((3,4)) #变成一个2维数组，是3行4列的
   print(a2)

   a3 = a1.reshape((2,3,2)) #变成一个3维数组，总共有2块，每一块是2行2列的
   print(a3)

   a4 = a2.reshape((12,)) # 将a2的二维数组重新变成一个12列的1维数组
   print(a4)

   a5 = a2.flatten() # 不管a2是几维数组，都将他变成一个一维数组
   print(a5)
```

注意，`reshape`并不会修改原来数组本身，而是会将修改后的结果返回。如果想要直接修改数组本身，那么可以使用`resize`来替代`reshape`。

### `ndarray.itemsize`：

数组中每个元素占的大小，单位是字节。比如以下代码：

```python
   a1 = np.array([1,2,3],dtype=np.int32)
   print(a1.itemsize) # 打印4，因为每个字节是8位，32位/8=4个字节
```

# Numpy数组操作(1)

## 数组广播机制：

### 数组与数的计算：

在`Python`列表中，想要对列表中所有的元素都加一个数，要么采用`map`函数，要么循环整个列表进行操作。但是`NumPy`中的数组可以直接在数组上进行操作。示例代码如下：

```python
import numpy as np
a1 = np.random.random((3,4))
print(a1)
# 如果想要在a1数组上所有元素都乘以10，那么可以通过以下来实现
a2 = a1*10
print(a2)
# 也可以使用round让所有的元素只保留2位小数
a3 = a2.round(2)
```

以上例子是相乘，其实相加、相减、相除也都是类似的。

### 数组与数组的计算：

1. 结构相同的数组之间的运算：

   ```python
   a1 = np.arange(0,24).reshape((3,8))
   a2 = np.random.randint(1,10,size=(3,8))
   a3 = a1 + a2 #相减/相除/相乘都是可以的
   print(a1)
   print(a2)
   print(a3)
   ```

2. 与行数相同并且只有1列的数组之间的运算：

   ```python
   a1 = np.random.randint(10,20,size=(3,8)) #3行8列
   a2 = np.random.randint(1,10,size=(3,1)) #3行1列
   a3 = a1 - a2 #行数相同，且a2只有1列，能互相运算
   print(a3)
   ```

3. 与列数相同并且只有1行的数组之间的运算：

   ```python
   a1 = np.random.randint(10,20,size=(3,8)) #3行8列
   a2 = np.random.randint(1,10,size=(1,8))
   a3 = a1 - a2
   print(a3)
   ```

### 广播原则：

**如果两个数组的后缘维度（trailing dimension，即从末尾开始算起的维度）的轴长度相符或其中一方的长度为1，则认为他们是广播兼容的。广播会在缺失和（或）长度为1的维度上进行。**。看以下案例分析：

1. `shape`为`(3,8,2)`的数组能和`(8,3)`的数组进行运算吗？  
   分析：不能，因为按照广播原则，从后面往前面数，`(3,8,2)`和`(8,3)`中的`2`和`3`不相等，所以不能进行运算。

2. `shape`为`(3,8,2)`的数组能和`(8,1)`的数组进行运算吗？  
   分析：能，因为按照广播原则，从后面往前面数，`(3,8,2)`和`(8,1)`中的`2`和`1`虽然不相等，但是因为有一方的长度为`1`，所以能参与运算。

3. `shape`为`(3,1,8)`的数组能和`(8,1)`的数组进行运算吗？  
   分析：能，因为按照广播原则，从后面往前面数，`(3,1,4)`和`(8,1)`中的`4`和`1`虽然不相等且`1`和`8`不相等，但是因为这两项中有一方的长度为`1`，所以能参与运算。

---

## 数组形状的操作：

可以通过一些函数，非常方便的操作数组的形状。

### reshape和resize方法：

两个方法都是用来修改数组形状的，但是有一些不同。

1. `reshape`是将数组转换成指定的形状，然后返回转换后的结果，对于原数组的形状是不会发生改变的。调用方式：

   ```python
   a1 = np.random.randint(0,10,size=(3,4))
   a2 = a1.reshape((2,6)) #将修改后的结果返回，不会影响原数组本身
   ```

2. `resize`是将数组转换成指定的形状，会直接修改数组本身。并不会返回任何值。调用方式：

   ```python
   a1 = np.random.randint(0,10,size=(3,4))
   a1.resize((2,6)) #a1本身发生了改变
   ```

### flatten和ravel方法：

两个方法都是将多维数组转换为一维数组，但是有以下不同：  

1. `flatten`是将数组转换为一维数组后，然后将这个拷贝返回回去，所以后续对这个返回值进行修改不会影响之前的数组。  
2. `ravel`是将数组转换为一维数组后，将这个视图（可以理解为引用）返回回去，所以后续对这个返回值进行修改会影响之前的数组。  
   比如以下代码：

```python
x = np.array([[1, 2], [3, 4]])
x.flatten()[1] = 100 #此时的x[0]的位置元素还是1
x.ravel()[1] = 100 #此时x[0]的位置元素是100
```

### 不同数组的组合：

如果有多个数组想要组合在一起，也可以通过其中的一些函数来实现。

1. `vstack`：将数组按垂直方向进行叠加。数组的列数必须相同才能叠加。示例代码如下：

   ```python
   a1 = np.random.randint(0,10,size=(3,5))
   a2 = np.random.randint(0,10,size=(1,5))
   a3 = np.vstack([a1,a2])
   ```

2. `hstack`：将数组按水平方向进行叠加。数组的行必须相同才能叠加。示例代码如下：

   ```python
   a1 = np.random.randint(0,10,size=(3,2))
   a2 = np.random.randint(0,10,size=(3,1))
   a3 = np.hstack([a1,a2])
   ```

3. `concatenate([],axis)`：将两个数组进行叠加，但是具体是按水平方向还是按垂直方向。则要看`axis`的参数，如果`axis=0`，那么代表的是往垂直方向（行）叠加，如果`axis=1`，那么代表的是往水平方向（列）上叠加，如果`axis=None`，那么会将两个数组组合成一个一维数组。需要注意的是，如果往水平方向上叠加，那么行必须相同，如果是往垂直方向叠加，那么列必须相同。示例代码如下：

   ```python
   a = np.array([[1, 2], [3, 4]])
   b = np.array([[5, 6]])
   np.concatenate((a, b), axis=0)
   # 结果：
   array([[1, 2],
       [3, 4],
       [5, 6]])
   
   np.concatenate((a, b.T), axis=1)
   # 结果：
   array([[1, 2, 5],
       [3, 4, 6]])
   
   np.concatenate((a, b), axis=None)
   # 结果：
   array([1, 2, 3, 4, 5, 6])
   ```

### 数组的切割：

通过`hsplit`和`vsplit`以及`array_split`可以将一个数组进行切割。

1. `hsplit`：按照水平方向进行切割。用于指定分割成几列，可以使用数字来代表分成几部分，也可以使用数组来代表分割的地方。示例代码如下：

   ```python
   a1 = np.arange(16.0).reshape(4, 4)
   np.hsplit(a1,2) #分割成两部分
   >>> array([[ 0.,  1.],
        [ 4.,  5.],
        [ 8.,  9.],
        [12., 13.]]), array([[ 2.,  3.],
        [ 6.,  7.],
        [10., 11.],
        [14., 15.]])]
   
   np.hsplit(a1,[1,2]) #代表在下标为1的地方切一刀，下标为2的地方切一刀，分成三部分
   >>> [array([[ 0.],
        [ 4.],
        [ 8.],
        [12.]]), array([[ 1.],
        [ 5.],
        [ 9.],
        [13.]]), array([[ 2.,  3.],
        [ 6.,  7.],
        [10., 11.],
        [14., 15.]])]
   ```

2. `vsplit`：按照垂直方向进行切割。用于指定分割成几行，可以使用数字来代表分成几部分，也可以使用数组来代表分割的地方。示例代码如下：

   ```python
   np.vsplit(x,2) #代表按照行总共分成2个数组
   >>> [array([[0., 1., 2., 3.],
        [4., 5., 6., 7.]]), array([[ 8.,  9., 10., 11.],
        [12., 13., 14., 15.]])]
   
   np.vsplit(x,(1,2)) #代表按照行进行划分，在下标为1的地方和下标为2的地方分割
   >>> [array([[0., 1., 2., 3.]]),
       array([[4., 5., 6., 7.]]),
       array([[ 8.,  9., 10., 11.],
              [12., 13., 14., 15.]])]
   ```

3. `split/array_split(array,indicate_or_seciont,axis)`：用于指定切割方式，在切割的时候需要指定是按照行还是按照列，`axis=1`代表按照列，`axis=0`代表按照行。示例代码如下：

   ```python
   np.array_split(x,2,axis=0) #按照垂直方向切割成2部分
   >>> [array([[0., 1., 2., 3.],
        [4., 5., 6., 7.]]), array([[ 8.,  9., 10., 11.],
        [12., 13., 14., 15.]])]
   ```

---

## 数组（矩阵）转置和轴对换：

`numpy`中的数组其实就是线性代数中的矩阵。矩阵是可以进行转置的。`ndarray`有一个`T`属性，可以返回这个数组的转置的结果。示例代码如下：

```python
a1 = np.arange(0,24).reshape((4,6))
a2 = a1.T
print(a2)
```

另外还有一个方法叫做`transpose`，这个方法返回的是一个View，也即修改返回值，会影响到原来数组。示例代码如下：

```python
a1 = np.arange(0,24).reshape((4,6))
a2 = a1.transpose()
```

为什么要进行矩阵转置呢，有时候在做一些计算的时候需要用到。比如做矩阵的内积的时候。就必须将矩阵进行转置后再乘以之前的矩阵：

```python
a1 = np.arange(0,24).reshape((4,6))
a2 = a1.T
print(a1.dot(a2))
```



# Numpy数组操作(2)

## 数组广播机制：

### 数组与数的计算：

在`Python`列表中，想要对列表中所有的元素都加一个数，要么采用`map`函数，要么循环整个列表进行操作。但是`NumPy`中的数组可以直接在数组上进行操作。示例代码如下：

```python
import numpy as np
a1 = np.random.random((3,4))
print(a1)
# 如果想要在a1数组上所有元素都乘以10，那么可以通过以下来实现
a2 = a1*10
print(a2)
# 也可以使用round让所有的元素只保留2位小数
a3 = a2.round(2)
```

以上例子是相乘，其实相加、相减、相除也都是类似的。

### 数组与数组的计算：

1. 结构相同的数组之间的运算：

   ```python
   a1 = np.arange(0,24).reshape((3,8))
   a2 = np.random.randint(1,10,size=(3,8))
   a3 = a1 + a2 #相减/相除/相乘都是可以的
   print(a1)
   print(a2)
   print(a3)
   ```

2. 与行数相同并且只有1列的数组之间的运算：

   ```python
   a1 = np.random.randint(10,20,size=(3,8)) #3行8列
   a2 = np.random.randint(1,10,size=(3,1)) #3行1列
   a3 = a1 - a2 #行数相同，且a2只有1列，能互相运算
   print(a3)
   ```

3. 与列数相同并且只有1行的数组之间的运算：

   ```python
   a1 = np.random.randint(10,20,size=(3,8)) #3行8列
   a2 = np.random.randint(1,10,size=(1,8))
   a3 = a1 - a2
   print(a3)
   ```

### 广播原则：

**如果两个数组的后缘维度（trailing dimension，即从末尾开始算起的维度）的轴长度相符或其中一方的长度为1，则认为他们是广播兼容的。广播会在缺失和（或）长度为1的维度上进行。**。看以下案例分析：

1. `shape`为`(3,8,2)`的数组能和`(8,3)`的数组进行运算吗？  
   分析：不能，因为按照广播原则，从后面往前面数，`(3,8,2)`和`(8,3)`中的`2`和`3`不相等，所以不能进行运算。

2. `shape`为`(3,8,2)`的数组能和`(8,1)`的数组进行运算吗？  
   分析：能，因为按照广播原则，从后面往前面数，`(3,8,2)`和`(8,1)`中的`2`和`1`虽然不相等，但是因为有一方的长度为`1`，所以能参与运算。

3. `shape`为`(3,1,8)`的数组能和`(8,1)`的数组进行运算吗？  
   分析：能，因为按照广播原则，从后面往前面数，`(3,1,4)`和`(8,1)`中的`4`和`1`虽然不相等且`1`和`8`不相等，但是因为这两项中有一方的长度为`1`，所以能参与运算。

---

## 数组形状的操作：

可以通过一些函数，非常方便的操作数组的形状。

### reshape和resize方法：

两个方法都是用来修改数组形状的，但是有一些不同。

1. `reshape`是将数组转换成指定的形状，然后返回转换后的结果，对于原数组的形状是不会发生改变的。调用方式：

   ```python
   a1 = np.random.randint(0,10,size=(3,4))
   a2 = a1.reshape((2,6)) #将修改后的结果返回，不会影响原数组本身
   ```

2. `resize`是将数组转换成指定的形状，会直接修改数组本身。并不会返回任何值。调用方式：

   ```python
   a1 = np.random.randint(0,10,size=(3,4))
   a1.resize((2,6)) #a1本身发生了改变
   ```

### flatten和ravel方法：

两个方法都是将多维数组转换为一维数组，但是有以下不同：  

1. `flatten`是将数组转换为一维数组后，然后将这个拷贝返回回去，所以后续对这个返回值进行修改不会影响之前的数组。  
2. `ravel`是将数组转换为一维数组后，将这个视图（可以理解为引用）返回回去，所以后续对这个返回值进行修改会影响之前的数组。  
   比如以下代码：

```python
x = np.array([[1, 2], [3, 4]])
x.flatten()[1] = 100 #此时的x[0]的位置元素还是1
x.ravel()[1] = 100 #此时x[0]的位置元素是100
```

### 不同数组的组合：

如果有多个数组想要组合在一起，也可以通过其中的一些函数来实现。

1. `vstack`：将数组按垂直方向进行叠加。数组的列数必须相同才能叠加。示例代码如下：

   ```python
   a1 = np.random.randint(0,10,size=(3,5))
   a2 = np.random.randint(0,10,size=(1,5))
   a3 = np.vstack([a1,a2])
   ```

2. `hstack`：将数组按水平方向进行叠加。数组的行必须相同才能叠加。示例代码如下：

   ```python
   a1 = np.random.randint(0,10,size=(3,2))a2 = np.random.randint(0,10,size=(3,1))a3 = np.hstack([a1,a2])
   ```

3. `concatenate([],axis)`：将两个数组进行叠加，但是具体是按水平方向还是按垂直方向。则要看`axis`的参数，如果`axis=0`，那么代表的是往垂直方向（行）叠加，如果`axis=1`，那么代表的是往水平方向（列）上叠加，如果`axis=None`，那么会将两个数组组合成一个一维数组。需要注意的是，如果往水平方向上叠加，那么行必须相同，如果是往垂直方向叠加，那么列必须相同。示例代码如下：

   ```python
   a = np.array([[1, 2], [3, 4]])b = np.array([[5, 6]])np.concatenate((a, b), axis=0)# 结果：array([[1, 2],    [3, 4],    [5, 6]])np.concatenate((a, b.T), axis=1)# 结果：array([[1, 2, 5],    [3, 4, 6]])np.concatenate((a, b), axis=None)# 结果：array([1, 2, 3, 4, 5, 6])
   ```

### 数组的切割：

通过`hsplit`和`vsplit`以及`array_split`可以将一个数组进行切割。

1. `hsplit`：按照水平方向进行切割。用于指定分割成几列，可以使用数字来代表分成几部分，也可以使用数组来代表分割的地方。示例代码如下：

   ```python
   a1 = np.arange(16.0).reshape(4, 4)np.hsplit(a1,2) #分割成两部分>>> array([[ 0.,  1.],     [ 4.,  5.],     [ 8.,  9.],     [12., 13.]]), array([[ 2.,  3.],     [ 6.,  7.],     [10., 11.],     [14., 15.]])]np.hsplit(a1,[1,2]) #代表在下标为1的地方切一刀，下标为2的地方切一刀，分成三部分>>> [array([[ 0.],     [ 4.],     [ 8.],     [12.]]), array([[ 1.],     [ 5.],     [ 9.],     [13.]]), array([[ 2.,  3.],     [ 6.,  7.],     [10., 11.],     [14., 15.]])]
   ```

2. `vsplit`：按照垂直方向进行切割。用于指定分割成几行，可以使用数字来代表分成几部分，也可以使用数组来代表分割的地方。示例代码如下：

   ```python
   np.vsplit(x,2) #代表按照行总共分成2个数组>>> [array([[0., 1., 2., 3.],     [4., 5., 6., 7.]]), array([[ 8.,  9., 10., 11.],     [12., 13., 14., 15.]])]np.vsplit(x,(1,2)) #代表按照行进行划分，在下标为1的地方和下标为2的地方分割>>> [array([[0., 1., 2., 3.]]),    array([[4., 5., 6., 7.]]),    array([[ 8.,  9., 10., 11.],           [12., 13., 14., 15.]])]
   ```

3. `split/array_split(array,indicate_or_seciont,axis)`：用于指定切割方式，在切割的时候需要指定是按照行还是按照列，`axis=1`代表按照列，`axis=0`代表按照行。示例代码如下：

   ```python
   np.array_split(x,2,axis=0) #按照垂直方向切割成2部分>>> [array([[0., 1., 2., 3.],     [4., 5., 6., 7.]]), array([[ 8.,  9., 10., 11.],     [12., 13., 14., 15.]])]
   ```

---

## 数组（矩阵）转置和轴对换：

`numpy`中的数组其实就是线性代数中的矩阵。矩阵是可以进行转置的。`ndarray`有一个`T`属性，可以返回这个数组的转置的结果。示例代码如下：

```python
a1 = np.arange(0,24).reshape((4,6))a2 = a1.Tprint(a2)
```

另外还有一个方法叫做`transpose`，这个方法返回的是一个View，也即修改返回值，会影响到原来数组。示例代码如下：

```python
a1 = np.arange(0,24).reshape((4,6))a2 = a1.transpose()
```

为什么要进行矩阵转置呢，有时候在做一些计算的时候需要用到。比如做矩阵的内积的时候。就必须将矩阵进行转置后再乘以之前的矩阵：

```python
a1 = np.arange(0,24).reshape((4,6))a2 = a1.Tprint(a1.dot(a2))
```



# 深拷贝和浅拷贝

在操作数组的时候，它们的数据有时候拷贝进一个新的数组，有时候又不是。这经常是初学者感到困惑。下面有三种情况：

### 不拷贝：

如果只是简单的赋值，那么不会进行拷贝。示例代码如下：

```python
a = np.arange(12)
b = a #这种情况不会进行拷贝
print(b is a) #返回True，说明b和a是相同的
```

### View或者浅拷贝：

有些情况，会进行变量的拷贝，但是他们所指向的内存空间都是一样的，那么这种情况叫做浅拷贝，或者叫做`View(视图)`。比如以下代码：

```python
a = np.arange(12)
c = a.view()
print(c is a) #返回False，说明c和a是两个不同的变量
c[0] = 100
print(a[0]) #打印100，说明对c上的改变，会影响a上面的值，说明他们指向的内存空间还是一样的，这种叫做浅拷贝，或者说是view
```

### 深拷贝：

将之前数据完完整整的拷贝一份放到另外一块内存空间中，这样就是两个完全不同的值了。示例代码如下：

```python
a = np.arange(12)
d = a.copy()
print(d is a) #返回False，说明d和a是两个不同的变量
d[0] = 100
print(a[0]) #打印0，说明d和a指向的内存空间完全不同了。
```

### 例子：

像之前讲到的`flatten`和`ravel`就是这种情况，`ravel`返回的就是View，而`flatten`返回的就是深拷贝。

# 文件操作

## 操作CSV文件：

### 文件保存：

有时候我们有了一个数组，需要保存到文件中，那么可以使用`np.savetxt`来实现。相关的函数描述如下：

```python
np.savetxt(frame, array, fmt='%.18e', delimiter=None)
* frame : 文件、字符串或产生器，可以是.gz或.bz2的压缩文件
* array : 存入文件的数组
* fmt : 写入文件的格式，例如：%d %.2f %.18e
* delimiter : 分割字符串，默认是任何空格
```

以下是使用的例子：

```python
a = np.arange(100).reshape(5,20)
np.savetxt("a.csv",a,fmt="%d",delimiter=",")
```

### 读取文件：

有时候我们的数据是需要从文件中读取出来的，那么可以使用`np.loadtxt`来实现。相关的函数描述如下：

```python
np.loadtxt(frame, dtype=np.float, delimiter=None, unpack=False)
* frame：文件、字符串或产生器，可以是.gz或.bz2的压缩文件。
* dtype：数据类型，可选。
* delimiter：分割字符串，默认是任何空格。
* skiprows：跳过前面x行。
* usecols：读取指定的列，用元组组合。
* unpack：如果True，读取出来的数组是转置后的。
```

## np独有的存储解决方案：

`numpy`中还有一种独有的存储解决方案。文件名是以`.npy`或者`npz`结尾的。以下是存储和加载的函数。  

1. 存储：`np.save(fname,array)`或`np.savez(fname,array)`。其中，前者函数的扩展名是`.npy`，后者的扩展名是`.npz`，后者是经过压缩的。  
2. 加载：`np.load(fname)`。


---

# CSV文件操作：

## 读取csv文件：

```python
import csv

with open('stock.csv','r') as fp:
    reader = csv.reader(fp)
    titles = next(reader)
    for x in reader:
        print(x)
```

这样操作，以后获取数据的时候，就要通过下表来获取数据。如果想要在获取数据的时候通过标题来获取。那么可以使用`DictReader`。示例代码如下：

```python
import csv

with open('stock.csv','r') as fp:
    reader = csv.DictReader(fp)
    for x in reader:
        print(x['turnoverVol'])
```

## 写入数据到csv文件：

写入数据到csv文件，需要创建一个`writer`对象，主要用到两个方法。一个是`writerow`，这个是写入一行。一个是`writerows`，这个是写入多行。示例代码如下：

```python
import csv

headers = ['name','age','classroom']
values = [
    ('zhiliao',18,'111'),
    ('wena',20,'222'),
    ('bbc',21,'111')
]
with open('test.csv','w',newline='') as fp:
    writer = csv.writer(fp)
    writer.writerow(headers)
    writer.writerows(values)
```

也可以使用字典的方式把数据写入进去。这时候就需要使用`DictWriter`了。示例代码如下：

```python
import csv

headers = ['name','age','classroom']
values = [
    {"name":'wenn',"age":20,"classroom":'222'},
    {"name":'abc',"age":30,"classroom":'333'}
]
with open('test.csv','w',newline='') as fp:
    writer = csv.DictWriter(fp,headers)
    writer.writerow({'name':'zhiliao',"age":18,"classroom":'111'})
    writer.writerows(values)
```



# NAN和INF值处理

首先我们要知道这两个英文单词代表的什么意思：  

1. `NAN`：`Not A number`，不是一个数字的意思，但是他是属于浮点类型的，所以想要进行数据操作的时候需要注意他的类型。  
2. `INF`：`Infinity`，代表的是无穷大的意思，也是属于浮点类型。`np.inf`表示正无穷大，`-np.inf`表示负无穷大，一般在出现除数为0的时候为无穷大。比如`2/0`。

## NAN一些特点：

1. NAN和NAN不相等。比如`np.NAN != np.NAN`这个条件是成立的。
2. NAN和任何值做运算，结果都是NAN。

有些时候，特别是从文件中读取数据的时候，经常会出现一些缺失值。缺失值的出现会影响数据的处理。因此我们在做数据分析之前，先要对缺失值进行一些处理。处理的方式有多种，需要根据实际情况来做。一般有两种处理方式：删除缺失值，用其他值进行填充。

## 删除缺失值：

有时候，我们想要将数组中的`NAN`删掉，那么我们可以换一种思路，就是只提取不为`NAN`的值。示例代码如下：

```python
# 1. 删除所有NAN的值，因为删除了值后数组将不知道该怎么变化，所以会被变成一维数组
data = np.random.randint(0,10,size=(3,5)).astype(np.float)
data[0,1] = np.nan
data = data[~np.isnan(data)] # 此时的data会没有nan，并且变成一个1维数组

# 2. 删除NAN所在的行
data = np.random.randint(0,10,size=(3,5)).astype(np.float)
# 将第(0,1)和(1,2)两个值设置为NAN
data[[0,1],[1,2]] = np.NAN
# 获取哪些行有NAN
lines = np.where(np.isnan(data))[0]
# 使用delete方法删除指定的行,axis=0表示删除行，lines表示删除的行号
data1 = np.delete(data,lines,axis=0)
```

## 用其他值进行替代：

有些时候我们不想直接删掉，比如有一个成绩表，分别是数学和英语，但是因为某个人在某个科目上没有成绩，那么此时就会出现NAN的情况，这时候就不能直接删掉了，就可以使用某些值进行替代。假如有以下表格：

| 数学 | 英语 |
| ---- | ---- |
| 59   | 89   |
| 90   | 32   |
| 78   | 45   |
| 34   | NAN  |
| NAN  | 56   |
| 23   | 56   |

如果想要求每门成绩的总分，以及每门成绩的平均分，那么就可以采用某些值替代。比如求总分，那么就可以把NAN替换成0，如果想要求平均分，那么就可以把NAN替换成其他值的平均值。示例代码如下：

```python
scores = np.loadtxt("nan_scores.csv",skiprows=1,delimiter=",",encoding="utf-8",dtype=np.str)
scores[scores == ""] = np.NAN
scores = scores.astype(np.float)
# 1. 求出学生成绩的总分
scores1 = scores.copy()
socres1.sum(axis=1)

# 2. 求出每门成绩的平均分
scores2 = scores.copy()
for x in range(scores2.shape[1]):
    score = scores2[:,x]
    non_nan_score = score[score == score]
    score[score != score] = non_nan_score.mean()
print(scores2.mean(axis=0))
```



# np.random模块

`np.random`为我们提供了许多获取随机数的函数。这里统一来学习一下。

## np.random.seed：

用于指定随机数生成时所用算法开始的整数值，如果使用相同的`seed()`值，则每次生成的随即数都相同，如果不设置这个值，则系统根据时间来自己选择这个值，此时每次生成的随机数因时间差异而不同。一般没有特殊要求不用设置。以下代码：

```python
np.random.seed(1)
print(np.random.rand()) # 打印0.417022004702574
print(np.random.rand()) # 打印其他的值，因为随机数种子只对下一次随机数的产生会有影响。
```

## np.random.rand：

生成一个值为`[0,1)`之间的数组，形状由参数指定，如果没有参数，那么将返回一个随机值。示例代码如下：

```python
data1 = np.random.rand(2,3,4) # 生成2块3行4列的数组，值从0-1之间
data2 = np.random.rand() #生成一个0-1之间的随机数
```

## np.random.randn：

生成均值\(μ\)为0，标准差（σ）为1的标准正态分布的值。示例代码如下： 

```python
data = np.random.randn(2,3) #生成一个2行3列的数组，数组中的值都满足标准正太分布
```

## np.random.randint：

生成指定范围内的随机数，并且可以通过`size`参数指定维度。示例代码如下：

```python
data1 = np.random.randint(10,size=(3,5)) #生成值在0-10之间，3行5列的数组
data2 = np.random.randint(1,20,size=(3,6)) #生成值在1-20之间，3行6列的数组
```

## np.random.choice：

从一个列表或者数组中，随机进行采样。或者是从指定的区间中进行采样，采样个数可以通过参数指定：

```python
data = [4,65,6,3,5,73,23,5,6]
result1 = np.random.choice(data,size=(2,3)) #从data中随机采样，生成2行3列的数组
result2 = np.random.choice(data,3) #从data中随机采样3个数据形成一个一维数组
result3 = np.random.choice(10,3) #从0-10之间随机取3个值
```

## np.random.shuffle：

把原来数组的元素的位置打乱。示例代码如下：

```python
a = np.arange(10)
np.random.shuffle(a) #将a的元素的位置都会进行随机更换
```

## 更多：

更多的random模块的文档，请参考`Numpy`的官方文档：[https://docs.scipy.org/doc/numpy/reference/routines.random.html](https://docs.scipy.org/doc/numpy/reference/routines.random.html)

# Axis理解

之前的课程中，为了方便大家理解，我们说`axis=0`代表的是行，`axis=1`代表的是列。但其实不是这么简单理解的。这里我们专门用一节来解释一下这个`axis`轴的概念。

简单来说， **最外面的括号代表着 axis=0，依次往里的括号对应的 axis 的计数就依次加 1**。什么意思呢？下面再来解释一下。 
![](../../static/images/axis1.png)

最外面的括号就是`axis=0`，里面两个子括号`axis=1`。
**操作方式：如果指定轴进行相关的操作，那么他会使用轴下的每个直接子元素的第0个，第1个，第2个...分别进行相关的操作。**

现在我们用刚刚理解的方式来做几个操作。比如现在有一个二维的数组：

```python
x = np.array([[0,1],[2,3]])
```

1. 求`x`数组在`axis=0`和`axis=1`两种情况下的和：

   ```python
    >>> x.sum(axis=0)
    array([2, 4])
   ```

   为什么得到的是\[2,4\]呢，原因是我们按照`axis=0`的方式进行相加，那么就会把**最外面轴下的所有直接子元素中的第0个位置进行相加，第1个位置进行相加...依此类推**，得到的就是`0+2`以及`2+3`，然后进行相加，得到的结果就是`[2,4]`。

   ```python
    >>> x.sum(axis=1)
    array([1, 5])
   ```

   因为我们按照`axis=1`的方式进行相加，那么就会把**轴为1里面的元素拿出来进行求和**，得到的就是`0,1`，进行相加为`1`，以及`2,3`进行相加为`5`，所以最终结果就是`[1,5]`了。

2. 用`np.max`求`axis=0`和`axis=1`两种情况下的最大值：

 ```python
>>> np.random.seed(100)
>>> x = np.random.randint(0,10,size=(3,5))
>>> x.max(axis=0)
array([8, 8, 3, 7, 8])
 ```

因为我们是按照`axis=0`进行求最大值，那么就会在最外面轴里面找直接子元素，然后将每个子元素的第0个值放在一起求最大值，将第1个值放在一起求最大值，以此类推。而如果`axis=1`，那么就是拿到每个直接子元素，然后求每个子元素中的最大值：

 ```python
>>> x.max(axis=1)
array([8, 5, 8])
 ```

3. 用`np.delete`在`axis=0`和`axis=1`两种情况下删除元素：

   ```python
    >>> np.delete(x,0,axis=0)
    array([[2, 3]])
   ```

   `np.delete`是个例外。我们按照`axis=0`的方式进行删除，那么他会首先找到最外面的括号下的直接子元素中的第0个，然后删掉，剩下最后一行的数据。

   ```python
    >>> np.delete(x,0,axis=1)
    array([[1],
           [3]])
   ```

   同理，如果我们按照`axis=1`进行删除，那么会把第一列的数据删掉。



## 三维以上数组：

![](../../static/images/axis2.png)
按照之前的理论，如果以上数组按照`axis=0`的方式进行相加，得到的结果如下：
![](../../static/images/axis3.png)
如果是按照`axis=1`的方式进行相加，得到的结果如下：
![](../../static/images/axis4.png)



# 通用函数

## 一元函数：

| 函数                                              | 描述                                                         |
| ------------------------------------------------- | ------------------------------------------------------------ |
| np.abs                                            | 绝对值                                                       |
| np.sqrt                                           | 开根                                                         |
| np.square                                         | 平方                                                         |
| np.exp                                            | 计算指数\(e^x\)                                              |
| np.log，np.log10，np.log2，np.log1p               | 求以e为底，以10为低，以2为低，以\(1+x\)为底的对数            |
| np.sign                                           | 将数组中的值标签化，大于0的变成1，等于0的变成0，小于0的变成-1 |
| np.ceil                                           | 朝着无穷大的方向取整，比如5.1会变成6，-6.3会变成-6           |
| np.floor                                          | 朝着负无穷大方向取证，比如5.1会变成5，-6.3会变成-7           |
| np.rint，np.round                                 | 返回四舍五入后的值                                           |
| np.modf                                           | 将整数和小数分隔开来形成两个数组                             |
| np.isnan                                          | 判断是否是nan                                                |
| np.isinf                                          | 判断是否是inf                                                |
| np.cos，np.cosh，np.sin，np.sinh，np.tan，np.tanh | 三角函数                                                     |
| np.arccos，np.arcsin，np.arctan                   | 反三角函数                                                   |

## 二元函数：

| 函数                                                     | 描述                                   |
| -------------------------------------------------------- | -------------------------------------- |
| np.add                                                   | 加法运算（即1+1=2），相当于+           |
| np.subtract                                              | 减法运算（即3-2=1），相当于-           |
| np.negative                                              | 负数运算（即-2），相当于加个负号       |
| np.multiply                                              | 乘法运算（即2\*3=6），相当于\*         |
| np.divide                                                | 除法运算（即3/2=1.5），相当于/         |
| np.floor\_divide                                         | 取整运算，相当于//                     |
| np.mod                                                   | 取余运算，相当于%                      |
| greater,greater\_equal,less,less\_equal,equal,not\_equal | &gt;,&gt;=,&lt;,&lt;=,=,!=的函数表达式 |
| logical\_and                                             | &的函数表达式                          |
| logical\_or                                              | \|的函数表达式                         |

### 聚合函数：

| 函数名称  | NAN安全版本  | 描述             |
| --------- | ------------ | ---------------- |
| np.sum    | np.nansum    | 计算元素的和     |
| np.prod   | np.nanprod   | 计算元素的积     |
| np.mean   | np.nanmean   | 计算元素的平均值 |
| np.std    | np.nanstd    | 计算元素的标准差 |
| np.var    | np.nanvar    | 计算元素的方差   |
| np.min    | np.nanmin    | 计算元素的最小值 |
| np.max    | np.nanmax    | 计算元素的最大值 |
| np.argmin | np.nanargmin | 找出最小值的索引 |
| np.argmax | np.nanargmax | 找出最大值的索引 |
| np.median | np.nanmedian | 计算元素的中位数 |

使用`np.sum`或者是`a.sum`即可实现。并且在使用的时候，可以指定具体哪个轴。同样`Python`中也内置了`sum`函数，但是Python内置的`sum`函数执行效率没有`np.sum`那么高，可以通过以下代码测试了解到：

```python
a = np.random.rand(1000000)
%timeit sum(a) #使用Python内置的sum函数求总和，看下所花费的时间
%timeit np.sum(a) #使用Numpy的sum函数求和，看下所花费的时间
```

### 布尔数组的函数：

| 函数名称 | 描述                     |
| :------- | :----------------------- |
| np.any   | 验证任何一个元素是否为真 |
| np.all   | 验证所有元素是否为真     |

比如想看下数组中是不是所有元素都为0，那么可以通过以下代码来实现：

```python
np.all(a==0) 
# 或者是
(a==0).all()
```

比如我们想要看数组中是否有等于0的数，那么可以通过以下代码来实现：

```python
np.any(a==0)
# 或者是
(a==0).any()
```

### 排序：

1. `np.sort`：指定轴进行排序。默认是使用数组的最后一个轴进行排序。

   ```python
    a = np.random.randint(0,10,size=(3,5))
    b = np.sort(a) #按照行进行排序，因为最后一个轴是1，那么就是将最里面的元素进行排序。
    c = np.sort(a,axis=0) #按照列进行排序，因为指定了axis=0
   ```

   还有`ndarray.sort()`，这个方法会直接影响到原来的数组，而不是返回一个新的排序后的数组。

2. `np.argsort`：返回排序后的下标值。示例代码如下：

   ```python
    np.argsort(a) #默认也是使用最后的一个轴来进行排序。
   ```

3. 降序排序：`np.sort`默认会采用升序排序。如果我们想采用降序排序。那么可以采用以下方案来实现：

   ```python
    # 1. 使用负号
    -np.sort(-a)
   
    # 2. 使用sort和argsort以及take
    indexes = np.argsort(-a) #排序后的结果就是降序的
    np.take(a,indexes) #从a中根据下标提取相应的元素
   ```

### 其他函数补充：

1. `np.apply_along_axis`：沿着某个轴执行指定的函数。示例代码如下：

   ```python
    # 求数组a按行求均值，并且要去掉最大值和最小值。
    np.apply_along_axis(lambda x:x[(x != x.max()) & (x != x.min())].mean(),axis=1,arr=a)
   ```

2. `np.linspace`：用来将指定区间内的值平均分成多少份。示例代码如下：

   ```python
    # 将0-1分成12分，生成一个数组
    np.linspace(0,1,12)
   ```

3. `np.unique`：返回数组中的唯一值。

   ```python
    # 返回数组a中的唯一值，并且会返回每个唯一值出现的次数。
    np.unique(a,return_counts=True)
   ```

## 更多：

[https://docs.scipy.org/doc/numpy/reference/index.html](https://docs.scipy.org/doc/numpy/reference/index.html)


