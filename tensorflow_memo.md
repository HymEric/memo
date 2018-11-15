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
