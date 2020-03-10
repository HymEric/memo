### 1. 关于pytorch中的初始化问题
默认状况下，nn中的conv和linear里面的weight都是kaiming初始化，bias都是unifor初始化（1.1cpu版本），可以通过源码查询。当需要自己设置的时候也可以
自己设置初始化方式
参考：https://blog.csdn.net/qq_36338754/article/details/97756378?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task  
https://blog.csdn.net/ys1305/article/details/94332007

### 2. 构建模型的几种方法
如何寻找适合自己的构建模型的方法，以方便后续的使用？ 比如要找到一个特定名称的层
参考：https://www.cnblogs.com/denny402/p/7593301.html  
https://www.cnblogs.com/denny402/p/7593301.html
