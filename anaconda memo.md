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
