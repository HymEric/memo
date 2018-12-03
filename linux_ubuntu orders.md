# 1.Linux查看Nvidia显卡信息及使用情况，Nvidia自带一个命令行工具可以查看显存的使用情况：
* nvidia-smi

# 2.实时地对系统处理器的状态进行监视。可以查看PID、USER、CPU使用率等等信息
* top
# 3. 移动文件或文件夹到指定位置
* mv dir1 dir2
* mv path1 path2
* 移动当前文件夹下所有文件到指定位置 mv * path
# 4. unzip命令
* unzip -o -d /home/sunny myfile.zip
把myfile.zip文件解压到 /home/sunny/

-o:不提示的情况下覆盖文件；

-d:-d /home/sunny 指明将文件解压缩到/home/sunny目录下；
# 5. 查看磁盘占用的情况
* df -h
# 6. 压缩.tar.gz文件. 
* 将当前路径下的VSR-DUF_Youku文件夹中的东西都打包成VSR-DUF_Youku.tar.gz
* tar -czvf VSR-DUF_Youku.tar.gz VSR-DUF_Youku
# 7. 正确执行.sh文件的方法
* dao .sh 所在目录 cd xxx
* 给.sh文件添加x执行权限  chmod u+x hello.sh
* 执行.sh文件 ./hello.sh
# 8. 解压.tar.gz文件
* tar -zxf XXX.tar.gz （可选-C 解压位置）
# 9. 查看linux 内核版本
* uname -r
# 10. 查看linux正在运行的版本
* cat /etc/issue
* 或者 sudo lsb_release -a 需要管理员相应权限
# 11. 查看cuda版本
* nvcc-V
