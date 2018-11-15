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
