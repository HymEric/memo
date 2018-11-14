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
