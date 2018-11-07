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
