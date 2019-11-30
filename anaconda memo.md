# 0. add a channels by Tsinghua to speedup
* conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
* conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
* conda config --set show_channel_urls yes
* check the current config setting: conda config --show
* delete channels: conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

# 1. update anaconda
* conda update conda -> conda update anaconda

# 2. uninstall nanconda
* rm -rf anaconda
* remember to clean the anaconda path in .bashrc

# 3. create a new environment, conda creat -n your_env_name python=x.x(2.7\3.5) anaconda ,“-n"可以改为“--name”
* conda create --name python35 python=3.5

# 4. activate the enviroment after created it
* activate python34 (windows)
* source activate python34 (linux and mac)

# 5. version of python
* python -version

# 6. return the default environment
* deactivate python34 (windows)
* source deactivate python34 (linux and mac)

# 7. delete a environment
* conda remove --name python34 --all

# 8.delete a specific package in a environment
* conda remove --name &python34 $numpy (delete numpy)

# 9. search all environments, has activates env would have * or ()
* conda info -e
* or conda env list

# 10. install a package
* conda install package_name

# 11. update a package
* conda update package_name

# 12. delete a oackage
* conda remove package_name

# 13. list all installed package
* conda list

# 14. add anaconda to environment path
* modify .bashrc: add "  export PATH="/home/lishanliao/anaconda3/bin:$PATH"  " and run source ~/.bashrc

# 15. 在新环境中使用notebook
* 先在新环境中安装notebook，可以用navigator安装，之后到想用的文件夹中命令行 激活环境之后 执行jupyter notebook
* source activate --envs_name-- 之后 conda install jupyter 之后 jupyter notebook

# 16. install dlib in wi10
第一步：下载相应whl文件：

python2 和 python3.5：

https://pypi.org/project/dlib/18.17.100/#files

python3.6：

https://pypi.org/project/dlib/19.7.0/#files

第二步：

pip install xxx.whl

# 17. install scikit-learn py-version problems
If you install scikit-learn by ``` conda install scikit_learn``` with py37 when tf is py36. You can run bellow to solve it.
```shell
conda install scikit_learn
conda install python=3.6
```

# 19. uninstall the package after installing by distutils
If you run py file and get the same result, even you change the code or delete the file, the problem will be this
```shell
$ python setup.py install --record files.txt
$ cat files.txt | xargs rm -rf          # delete
```
