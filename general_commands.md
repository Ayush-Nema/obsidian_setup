# Curation of basic useful commands for level-0 to advanced usage
## todo: REFACTOR and RESTRUCTURE this file

1. `pip list` / `condo list` to view all the libraries installed 
2. `cat ~/.bashrc` to print the content of bashrc file (`cat` syntax is used for printing). Another example: `$ cat ~/.ssh/id_rsa.pub`
3. `conda info —envs` to list out all the conda environments
4. `conda info` to view all the details of condo version. And `conda info --envs` for listing all the environments.
5. `rm -r <dir name>` or `rmdir -p <dir name>` to delete the directory and all its content
6. `rmdir <dir name>` to delete the empty directory
7. To check what directories are in your `$PATH`, you can use either the printenv or echo command:
	`$echo $PATH`  
	-or-  
	`$printenv` (more descriptive)  
8. Adding directory to the PATH environment variable (here: `~/anaconda3/bin`)  
	`$ export PATH=~/anaconda3/bin:$PATH`
9. Use `tmux` to get into the environment such that the EC2 session doesn’t terminate automatically. And type tmux kill-session to get out of the tmux session.
10. Checking whether the GPU is being used: `nvidia-smi -h` to see all the options. For checking the GPU utilisation: `nvidia-smi -i 0 -l -q -d UTILIZATION` other way is `$ watch -n 0.1 nvidia-smi` (results update every 0.1 seconds)
11. Copying file from local machine to the ec2 instance: `scp -i an_ec2_key.pem cudnn-10.0-linux-x64-v7.5.1.10.tgz ubuntu@ec2-3-23-99-4.us-east-2.compute.amazonaws.com:~/cudnn_dir` [here, cudnn_dir is the directory in the instance where you want to copy the file]: look https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/ for more information. For sending entire directory use `scp -i key.pem -r /path/to/directory ubuntu@….:~/path/to/paste/in/ec2`
12. To download a file from ec2: `scp -i ~/Downloads/an_ec2_key.pem ubuntu@ec2-18-219-215-56.us-east-2.compute.amazonaws.com:~/output_df.csv ~/Desktop` {after <:> file in the ec2 and then the location where the file will be downloaded in the local machine}
13. The SSH keys are stored in `.ssh` directory. In order to view the content: `$ cd /.ssh` and the `ls` to view.
14. In order to find the size of file: `ls -lh <filename>` [for more info: https://stackoverflow.com/questions/11720079/how-can-i-see-the-size-of-files-and-directories-in-linux] 
	OR `$du -sh <filename>`
15. To kill the task running in any port use: `kill -9 $(sudo lsof -t -i:8888)`. `$sudo lsof -t -i:8888` lists the task running in the port specified. Better way is to run `$ ps all` and get the PID number associated with the process and then run `$ sudo kill -9 <PID>`
16. To copy the content of the ssh file to the clipboard: `$ pbcopy < ~/.ssh/id_ed25519.pub` (here the content of id_ed25519 is being copied)
17. To see the list of held packages use: `apt-mark showhold` (try `sudo`, if this doesn’t work). To un-hold the packages use: `sudo apt-mark unhold <package name>`. Another way is to use ‘`aptitude`’ package: `sudo apt-get install aptitude`, and then `sudo aptitude install myNewPackage` (for more information: https://cutt.ly/njDNDgN)
18. To create a git branch use `$ git checkout -b <new-branch-name>`
19. To delete a branch remotely and locally, follow the link: https://stackoverflow.com/questions/2003505/how-do-i-delete-a-git-branch-locally-and-remotely 
    1. `$ git push -d <remote_name> <branch_name>` (remote_name=origin, -D instead of -d for force delete)
    2. `$ git branch -d <branch_name>`
20. Task manager in the terminal: `$ top`. Better version is `$ htop`, it is not preinstalled. 
21. To check whether a git brach exists locally use: `git show-ref --verify refs/heads/<branch-name>`, also another way: `git rev-parse --verify <branch_name>`. And the shell scripting way: https://dev.to/iridiumcao/how-to-check-if-a-git-branch-exists-in-the-local-remote-repository-3gkd 
22. While installing the python libraries, sometimes we encounter `contradicting packages` error, it looks like “INFO: pip is looking at multiple versions of <package name> to determine which version is compatible with other requirements.”. Use  `—use-deprecated=legacy-resolver` to install the package. Ex.: `$ pip install --use-deprecated=legacy-resolver -i https://pypi.toyotaconnected.net/simple/ tomo==3.2.5`
23. To install a python package from custom cloud like TCIN’s use: `pip install -i https://pypi.toyotaconnected.net/simple/ <package_name>`. And to install the package from default pypi cloud use `pip install -i https://pypi.python.org/simple <package_name>`
24. To update the local master with remote master: https://stackoverflow.com/questions/36540645/updating-local-master-with-remote-master 
25. Purge clean the virtual environment: `pip freeze | xargs pip uninstall -y`
26. Installing the package based on version conditions: [Ex.] `pip install numpy<0.7.0,>=0.6`
27. Move or rename a file/ directory: `mv <existing location/name> <new location/ name>`. This command can be used to move or rename a file or directory
28. Clearing the pip cache (for installing the desired version of packages and removing the previous installations): https://stackoverflow.com/questions/9510474/removing-pips-cache 
29. To change the commit message use: `$ git commit —amend` (this open the terminal editor, make changes and save)
30. Look inside a pod: `kubectl -n kubeflow get pods | grep -i <pipeline name>`. Using (-i) for case insensitive search
31. Opening a shell in the running pod: `kubectl -n kubeflow exec -it <pod name> — /bin/bash` (OR) `— sh`
32. Find a file using terminal: https://winaero.com/find-files-linux-terminal/ , https://www.cyberciti.biz/faq/linux-how-can-i-find-a-file-on-my-system/ 
    1. `find /etc -type f -name file1.txt` [look for file1.txt in /etc dir, use `.` to check everywhere]
33. check whether a file exists using shell script: https://linuxize.com/post/bash-check-if-file-exists/ 
34. if after running `make build` we face `no space available error` then run `docker system prune` command. To remove all the images in local machine use `$ docker system prune -a`
35. For moving a file from one location to another: `import shutil` and then `shutil.move("path/to/current/file", "path/to/new/destination/for/file")`
36. Changing the default version of Python: https://dev.to/meetsohail/change-the-python3-default-version-in-ubuntu-1ekb 
37. To un-commit the changes after staging the files: `$ git rm -r —cached <filename/ or . for all files>`. 
38. To undo the one last commit with `$ git reset —soft HEAD~1`. Number of commits can be altered.
39. To pull a branch from origin/master: 
    1. if it exists in local already: `$ git switch <branch name>`
    2. if it does not exists, then: `$ git fetch <remote> <rbranch>:<lbranch>` and `$ git checkout <lbranch>`
    3. https://stackoverflow.com/questions/9537392/git-fetch-remote-branch 
40. Aggregated one shot commit (squashing all commits into one)
    1. `git checkout yourBranch`
    2. `git reset $(git merge-base master $(git rev-parse --abbrev-ref HEAD))`
    3. `git add -A`
    4. `git commit -m "one commit on yourBranch"`
    5. https://stackoverflow.com/questions/25356810/git-how-to-squash-all-commits-on-branch
41. Installing vim in pod: `$ (sudo) apt install vim`
42. To get the directory tree in the terminal: 
    1. Install tree module:`$ sudo apt-get install tree`
    2. Use this command to get the tree: `$ tree /path/to/folder`
43. To count the number of files in the current directory use: `ls -1 | wc -l`
44. To get the list of `ipykernels`:  `jupyter kernelspec list`
    1. to delete a kernel from jupyter notebook: `jupyter kernelspec uninstall <kernel-name>`
    2. to add a kernel:
        1. `pip install ipykernel`
        2. `python -m ipykernel install --prefix="/home/ubuntu/anaconda3/envs/fine-tune" —name=<name_of_virtual_env>`  [prefix: path till conda env]
45. If jupyter notebook fails to load in EC2: `conda update jupyter_core jupyter_client`
    1. Also try to update the extensions:
        1. `pip install jupyter_contrib_nbextensions`
        2. `jupyter contrib nbextension install`
        3. Link: https://www.analyticsvidhya.com/blog/2022/02/11-extensions-to-power-up-your-jupyter-notebook/ 
46. Find the version and release of Ubuntu in Ec2: `$ lsb_release -a`
47. To know about the hardware properties in Ubuntu: `$ sudo lshw -C display`
48. Find and remove all `.DS_Store` files/ dirs from project: `$ find . -name .DS_Store -print0 | xargs -0 git rm –f --ignore-unmatch`
49. Get the list of extensions installed in jupyter lab:
    1. `jupyter labextension list`
    2. full list can be found here: https://github.com/topics/jupyterlab-extension
    3. Reference official doc: https://jupyterlab.readthedocs.io/en/stable/user/extensions.html 
    4. Installing an extension: `jupyter labextension install my-extension`
    5. Uninstalling an extension: `jupyter labextension uninstall my-extension`
    6. Enabling an extension: `jupyter labextension enable my-extension`
    7. Disabling an extension: `jupyter labextension disable my-extension`
50. Like `pip freeze`, getting the `environment.yml` file for conda environment: 
    1. `conda env export -f environment.yml -n gpu-test` [where gpu-test is the name of conda env. Dumps the file in the same directory from where this command is run]
    2. to create a new conda env using environment.yml file: `conda env create --name <conda-env-name> --file=environment.yml`
    3. also check use of different flags in `conda create —help`
51. For module import error or module not found error: `$ export PYTHONPATH="${PYTHONPATH}:/path/to/your/project/“` [run this from 1 level above project root]
52. To find the details of OS and distribution: `cat /etc/*release` or `cat /etc/os-release` or `lsb_release -d`
	1. to get the kernel version: `uname -r`
	2. to get the system architecture info: `uname -m`
53. `Got permission denied while trying to connect to the Docker daemon socket at unix….. connect: permission denied` > docker error. 
    1. scenario: newly installed docker + `$ docker image ls`
    2. Resolution:
        1. `sudo groupadd docker`
        2. `sudo usermod -a -G docker [user]` (here [user] is ubuntu)
        3. `newgrp docker`
        4. for more info refer: https://docs.docker.com/engine/install/linux-postinstall
54. Copying the file from docker to local: `docker cp <containerId>:/file/path/within/container /host/path/target`
    1. https://stackoverflow.com/questions/22049212/copying-files-from-docker-container-to-host 
55. Validate JSON using Python
    1. Cereberus (https://github.com/pyeve/cerberus)
    2. Jsonschema (https://github.com/python-jsonschema/jsonschema)
    3. Schema (https://github.com/keleshev/schema)
56. In order to remove a commit from Gitlab and revert to older version:
    1. `git reset --hard <commit-id-from-git>`
    2. `git status (for checking)`
    3. `git push -f origin <name-of-branch>`
57. To check the remaining space in Ubuntu system: `df -h`
58. To get the nvidia drivers version: `cat /proc/driver/nvidia/version`
59. Use `sudo -i` to enter into the root shell. This will have all the permissions and commands will run without `sudo`. Run `exit` to exit the shell and return to base terminal.


---
## Virtual and Conda environment
### Create a conda environment
`$ conda create --no-default-packages -n <conda-env-name> python=3.7`
OR
`$ conda create -n <name of conda_env> python=3.7`
`$ conda update -n base conda` [to update the conda environment]

- Delete conda environment
`$ conda env remove -n <name of conda_env>`


### Using the jupyter notebook (tips and shortcuts)
https://gist.github.com/AdamGagorik/248bedfcccd5e9a0b6f953fa1dc87f1a
Also, do `pip install jupyter`


### Adding a virtual environment to Jupyter notebook
`pip install --user ipykernel`
`python -m ipykernel install --user --name=<name of virtual_env>`

https://medium.com/@nrk25693/how-to-add-your-conda-environment-to-your-jupyter-notebook-in-just-4-steps-abeab8b8d084  
and  
https://janakiev.com/blog/jupyter-virtual-envs/  

---

## EC2 instance related
1. Initiating the EC2 instance  
`$ ssh -v -I ~/Downloads/an_ec2_key.pem -L 8888:localhost:8888 ubuntu@ec2-3-12-83-190.us-east-2.compute.amazonaws.com`
[here, -L 8888:localhost:8888 is the port tunnelling, -v is for controlling the verbosity level , set to debug]
Format: `ssh -i abc.pem -L <remote_port>:localhost:<local_port> <remote_user>@<remote_host>`
More about port tunnelling: https://tinyurl.com/y4xhv9fo

2. Activate the condo virtual environment 
`conda activate virtual_env`

3. Getting the anaconda
`$ wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh`  
`$ bash Anaconda3-2022.10-Linux-x86_64.sh`  
Go to the virtual environment: `conda activate virtual_env` then `pip install jupyter`  
(https://repo.anaconda.com/archive/) -> stores all versions  
- more instructions here: https://docs.anaconda.com/anaconda/install/linux/   
- install jupyter notebook: `pip install notebook`  
- install jupyter lab: `pip install jupyterlab`  

4. Setting up the Jupyter notebook
`$ pip install jupyter`   
`$ jupyter notebook --no-browser --port=8888` (this command forces jupyter notebook to use port 8888)

5. Attaching environment to notebook
	conda environment :→
	`conda install nb_conda`
	`conda install -c anaconda ipykernel`
	`python -m ipykernel install --user --name=<env_name>`  

	virtual environment :→
	`pip install --user ipykernel`  
	`python -m ipykernel install --user --name=myenv`

---

## CUDA and NVIDIA drivers installation
- Purge clean CUDA from the instance:
    - `sudo apt-get purge nvidia*`
    - `sudo apt-get autoremove`
    - `sudo apt-get autoclean`
    - `sudo rm -rf /usr/local/cuda*`
    - Note: CUDA drivers are installed in `/usr/local` directory

- Installation of the drivers
    - Click on the CUDA version to install. Check backward compatibility with libs like Tensorflow before clicking. Click on the version and select OS, version etc and execute the commands.
    - https://developer.nvidia.com/cuda-toolkit-archive
    - check the installation by running `nvidia-smi`
    - to install the cuda toolkit: `$ sudo apt install nvidia-cuda-toolkit`

- Check the CUDA version using: `nvcc —version`. 
    - alternate: `dpkg -l | grep cuda`

- Once the cuda is installed based on above instructions, try `nvcc -V`, if it fails then probably automatic addition of cuda to PATH variable has failed. Add the following to `~/.bashrc`, once done source it:
    - `export CUDA_HOME=/usr/local/cuda`
    - `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64`
    - `export PATH=$PATH:$CUDA_HOME/bin`


Mandatory requirements For GPU utilisation
https://www.tensorflow.org/install/gpu

CUDA Drivers installation guide:
1. https://gist.github.com/bogdan-kulynych/f64eb148eeef9696c70d485a76e42c3a
2. https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html 
3. https://developer.nvidia.com/cuda-10.1-download-archive-base?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=debnetwork  
4. GPU utilisation test: https://www.tensorflow.org/guide/gpu 
5. Checking for compatibility: https://www.tensorflow.org/install/source#linux 

CUDA toolkit installation:
https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_local 

- Nvidia cuDNN documentation
    - https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html   
- Verify Cuda installation
    - https://xcat-docs.readthedocs.io/en/stable/advanced/gpu/nvidia/ verify_cuda_install.html 



