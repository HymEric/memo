
## 目录
<!--TOC-->
- [1. 关于pytorch中的初始化问题](#1-关于pytorch中的初始化问题)
- [2. 构建模型的几种方法](#2-构建模型的几种方法)
- [3. pytorch中的padding策略](#3-pytorch中的padding策略)
- [4. 自定义dataset](#4-自定义dataset)
- [5. Pytorch提速指南](#5-Pytorch提速指南)
- [6. 如何设计一个好的pytorch项目框架](#6-如何设计一个好的pytorch项目框架) 
- [7. 关于保存模型与加载模型](#7-关于保存模型与加载模型)
- [8. 关于自动求导和特定tensor的导数](#8-关于自动求导和特定tensor的导数)
- [9. 关于pytorch的小知识点包括argparse,tqdm,logging等等](#9-关于pytorch的小知识点包括argparsetqdmlogging等等)
- [10. pytorch不同版本转换](#10-pytorch不同版本转换) 
- [11. 关于backward中的retain_graph的问题](#11-关于backward中的retain_graph的问题)
- [12. 一个框架中多网络训练的require_grad问题](#12-一个框架中多网络训练的requires_grad问题)
- [13. 关于tensorboardX和pytorch版本问题](#13-关于tensorboardX和pytorch版本问题)
<!--TOC-->

### 1. 关于pytorch中的初始化问题
默认状况下，nn中的conv和linear里面的weight都是kaiming初始化，bias都是unifor初始化（1.1cpu版本），可以通过源码查询。当需要自己设置的时候也可以
自己设置初始化方式
参考：https://blog.csdn.net/qq_36338754/article/details/97756378?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task  
https://blog.csdn.net/ys1305/article/details/94332007  
在模型定义的时候初始化或者在使用model的时候apply  
https://www.cnblogs.com/wanghui-garcia/p/11385160.html

### 2. 构建模型的几种方法
如何寻找适合自己的构建模型的方法，以方便后续的使用？ 比如要找到一个特定名称的层
参考：https://www.cnblogs.com/denny402/p/7593301.html  
**注意：不能在forward里面定义网络层，包括batchNorm也不行（因为BN里面有需要训练的参数），只能在里面进行运算操作，可以加入比如relu等没有参数的操作，要不然每次运行model 的forward都会初始化一遍参数，是不对的。**

### 3. pytorch中的padding策略
可以根据公式计算padding应该是什么，比如padding=[1,2]，代表在H上也就是上下各padding 1行，W上左右个padding 2行，默认padding的是数字0  
$$H_{out}=\lfloor \frac{H_{in} - kernel_size[0] + 2 \times padding}{strides[0]} +1  \rfloor$$
$$W_{out}=\lfloor \frac{W_{in} - kernel_size[0] + 2 \times padding}{strides[0]} +1  \rfloor$$    
参考：https://blog.csdn.net/g11d111/article/details/82665265?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task

### 4. 自定义dataset
在getitem中得到的数据应该是numpy array或者PILImage格式的，注意图像的RGB顺序，  
如果要使用torchvision中的数据集，要记得里面的数据集得到的是PILImage格式的，transform中一般都需要进行Tensor转化  
为了节约内存可以使用txt进行读取数据：https://blog.csdn.net/lyl771857509/article/details/84642560 ，但如果内存、显存够的话推荐还在先全部加载，这样后面的训练会更快！ 

### 5. Pytorch提速指南
https://zhuanlan.zhihu.com/p/39752167  
给训练踩踩油门 —— Pytorch 加速数据读取： https://zhuanlan.zhihu.com/p/80695364

### 6. 如何设计一个好的pytorch项目框架
https://github.com/IgorSusmelj/pytorch-styleguide ，**但是要注意使用prefetch_generator，可能会OOM，显存使用过大**
一个训练模板：https://www.ctolib.com/victoresque-pytorch-template.html

### 7. 关于保存模型与加载模型
参考：https://zhuanlan.zhihu.com/p/38056115

### 8. 关于自动求导和特定tensor的导数
参考： https://www.cnblogs.com/marsggbo/p/11549631.html

### 9. 关于pytorch的小知识点包括argparse,tqdm,logging等等
参考：https://zhuanlan.zhihu.com/p/104706637?utm_source=wechat_session

### 10. pytorch不同版本转换
pytorch不同版本之间有差别，从0.3.1转到0.4.1或更高版本等，可参考：https://heroinlin.github.io/2019/02/27/Pytorch/Pytorch_version_transform/

### 11. 关于backward中的retain_graph的问题
当训练的网络中存在多个loss的时候，并且这些loss还是相关联的，如果正常最loss1.backward()，那么后面的loss2，loss3可能会报错，因为这时候计算图已经释放了，如果有三个loss，我们需要这样写
```python
...
loss1.backward(retain_graph=True)
...
loss2.backward(retain_graph=True)
...
loss3.backward() # note here no retain_graph=True for freeing the computation graph
```
参考：https://discuss.pytorch.org/t/runtimeerror-trying-to-backward-through-the-graph-a-second-time-but-the-buffers-have-already-been-freed-specify-retain-graph-true-when-calling-backward-the-first-time/6795

### 12. 一个框架中多网络训练的requires_grad问题
有一次在训练一个包含多个模型的（有GAN）框架，但是GAN的loss怎么越来越大（一个正的大一个负的大）呢？原因是因为一个框架中有多个模型训练的时候，一个模型训练要把其他的模型的requires_grad设置为False，只把当前需要更新的模型设置为True才行，要不然loss就会变得出奇的大或者小，这个时候就感觉pytrch的动态图没有tf的静态图好用。

### 13. 关于tensorboardX和pytorch版本问题
在训练期间，遇到了tensorboardX报错，比如init() got an unexpected keyword argument 'record_shapes'和缺失参数的错误，解决办法可以调整tensorboardX或者pytorch版本，已确定tensorboardX1.8和pytorch1.1.0可以使用。
参考：https://blog.csdn.net/jzwong/article/details/104130073


