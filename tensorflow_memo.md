# 1. tf.depth_to_space
```
depth_to_space （ 
    input ， 
    block_size ， 
    name = None
 ）
```
* 假设输入的形状是:[batch, height, width, depth]，输出的形状为:[batch, height*block_size, width*block_size, depth/(block_size*block_size)]；

如：输入[1,1,1,4] block_size=2 ->输出[1,2,2,1]
```
x = [[[[1, 2, 3, 4]]]]
to: [[[[1], [2]],
     [[3], [4]]]]
```
对于以下输入的形状 [1, 1, 1, 12]，并且块大小为2,输出[1,2,2,3]
```
x = [[[[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]]]]
to: x = [[ [1],   [2],  [5],  [6]],
     [ [3],   [4],  [7],  [8]],
     [ [9],  [10], [13],  [14]],
     [ [11], [12], [15],  [16]]]
```
# 2. 检查GPU是否在干活
```python
import tensorflow as tf
tf.test.gpu_device_name()

'/device:GPU:0' #代表GPU在干活
```
# 3. 运行时使用特定GPU
* CUDA_VISIBLE_DEVICES=1 python your_python_file.py some_parameter_maybe_
# 4. tf.clip_by_value(A, min, max)
* 输入一个张量A，把A中的每一个元素的值都压缩在min和max之间。小于min的让它等于min，大于max的元素的值等于max。
```python

import tensorflow as tf;
import numpy as np;
 
A = np.array([[1,1,2,4], [3,4,8,5]])
 
with tf.Session() as sess:
	print sess.run(tf.clip_by_value(A, 2, 5))

输出：
[[2 2 2 4]
 [3 4 5 5]]
```
