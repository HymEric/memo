# 1. python -m
* run library module as a script (terminates option list)意思是将库中的python模块用作脚本去运行。
* python -m SimpleHTTPServer    #python2中启动一个简单的http服务器
* python -m http.server    #python3中启动一个简单的http服务器
# 2.use __future__
* 简单说可以是在2.7中使用3.x的特性，比如
* 如果你想在Python 2.7的代码中直接使用Python 3.x的除法，可以通过__future__模块的division实现：
```python
from __future__ import division
print '10 / 3 =', 10 / 3
print '10.0 / 3 =', 10.0 / 3
print '10 // 3 =', 10 // 3
```
results:
```
10 / 3 = 3.33333333333
10.0 / 3 = 3.33333333333
10 // 3 = 3
```
# 3. numpy :mnp.lib.pad
* 填补一个数组。

pad（array，pad_width，mode，**kwars）

其中array为要填补的数组（input）

pad_width是在各维度的各个方向上想要填补的长度,如（（2，3），（4，5）），如果直接输入一个整数，则说明各个维度和各个方向所填补的长度都一样。

mode为填补类型，即怎样去填补，有“constant”，“edge”等模式，如果为constant模式，就得指定填补的值。

剩下的都是一些可选参数.返回值为填补好的ndarray。

二维数组的时候先上下后左右，也就是数组中的第一个[]表示的先行，再后面的[]增加列。（从外向内）

```python
>>> a = [1, 2, 3, 4, 5]
>>> np.lib.pad(a, (2,3), 'constant', constant_values=(4, 6))
array([4, 4, 1, 2, 3, 4, 5, 6, 6, 6])


>>> a = [[1, 2], [3, 4]]
>>> np.lib.pad(a, ((3, 2), (2, 3)), 'minimum')
array([[1, 1, 1, 2, 1, 1, 1],
  	 [1, 1, 1, 2, 1, 1, 1],
 	  [1, 1, 1, 2, 1, 1, 1],
 	  [1, 1, 1, 2, 1, 1, 1],
 	  [3, 3, 3, 4, 3, 3, 3],
 	  [1, 1, 1, 2, 1, 1, 1],
 	  [1, 1, 1, 2, 1, 1, 1]])

>>> a = [[0,1, 2], [3, 4,5]]
>>> np.lib.pad(a, 2, padwithtens)
array([[10, 10, 10, 10, 10, 10, 10],
     [10, 10, 10, 10, 10, 10, 10],
  	 [10, 10,  0,  1,  2, 10, 10],
  	 [10, 10,  3,  4,  5, 10, 10],
  	 [10, 10, 10, 10, 10, 10, 10],
 	 [10, 10, 10, 10, 10, 10, 10]])
```
# 4. argparse
* argparse is a Command line parsing module(命令行解析)
* 位置参数
```python
import argparse
# argparse是命令行解析模块
parse=argparse.ArgumentParser()
#位置参数
# 指定位置参数后，程序必须输入该参数值才能运行
# 指定程序将要去接受的命令行选项，在这里我们命名为echo
parse.add_argument('echo',help="echo the string you use here")
# argoarse将输入的参数都看作strings类型，用int时候 可以在计算过程中转化为int，或者在add_argument中指定type
parse.add_argument("square",help="display the square of a given number",type=int)
args=parse.parse_args()
print(args.echo)
print(args.square**2)

E:\Workspace\PycharmProjects\VSR-DUF>python hymtest.py hym 6
hym
36

# 也可以使用help查看输入要求
E:\Workspace\PycharmProjects\VSR-DUF>python hymtest.py -h
usage: hymtest.py [-h] echo square

positional arguments:
  echo        echo the string you use here
  square      display the square of a given number

optional arguments:
  -h, --help  show this help message and exit

```
* 可选参数
```python
# 第二种，可选参数
import argparse

parser = argparse.ArgumentParser()
# 默认可选参数赋值为str
parser.add_argument("--verbosity", help="increase output verbosity")
args = parser.parse_args()
if args.verbosity:
    print("verbosity turned on")
    
E:\Workspace\PycharmProjects\VSR-DUF>python hymtest.py --verbosity hym
verbosity turned on

```

```python
# 很多时候，可选参数是作为一个标识而不是一个确切的值，仅需要确定是true或false即可，可以指定关键字action，赋值为"store_true"：
parser = argparse.ArgumentParser()
# 默认可选参数赋值为str
parser.add_argument("--verbosity", help="increase output verbosity",action="store_true") # 输入赋值给verbosity
args = parser.parse_args()
if args.verbosity:
    print("verbosity turned on")
    
E:\Workspace\PycharmProjects\VSR-DUF>python hymtest.py --verbosity
verbosity turned on

```

* 短选项，类似命令行用法，长选项总会有相应的短选项，只需在相应的add_argument()方法中加上即可:
```python
parser.add_argument("-v",--verbosity", help="increase output verbosity",action="store_true") # 输入赋值给verbosity

E:\Workspace\PycharmProjects\VSR-DUF>python hymtest.py -v
verbosity turned on

```

* 指定输入参数范围，关键字choices
```python
parser.add_argument("-v", "--verbosity", type=int, choices=[0,1,2], help="increase output verbosity")
```

* 结合使用
```python
import argparse
 
parser = argparse.ArgumentParser()
parser.add_argument("square", type=int, help="display a square of a given number")
parser.add_argument("-v", "--verbosity", type=int, help="increase output verbosity")
args = parser.parse_args()
answer = args.square**2
if args.verbosity == 2:
    print("the square of {} equals {}".format(args.square, answer))
elif args.verbosity == 1:
    print("{}^2 == {}".format(args.square, answer))
else:
    print(answer)
    
E:\Workspace\PycharmProjects\VSR-DUF>python hymtest.py 2 -v 1
2^2 == 4

E:\Workspace\PycharmProjects\VSR-DUF>python hymtest.py 2 -v 2
the square of 2 equals 4

E:\Workspace\PycharmProjects\VSR-DUF>python hymtest.py -v 2 5
the square of 5 equals 25

```
* default 增加默认值
* 参考：https://blog.csdn.net/u012005313/article/details/50111455
* 详细： http://kuanghy.github.io/2016/06/30/python-argparse
# 5. glob.glob和排序
```python
#imgs存放图片,相当于名字路径
imgs=glob.glob('*.png')
print(imgs)
# 图片文件最后的数字名字排序
imgs=sorted(imgs, key=lambda name: int(name[:-4]))
print(imgs)

>>>['0.png', '1.png', '10.png', '100.png', '101.png', '102.png', '103.png', '104.png',....]
>>>['0.png', '1.png', '2.png', '3.png', '4.png', '5.png', '6.png', '7.png', '8.png',.....]
```
