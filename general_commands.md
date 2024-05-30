# Curation of basic useful commands for level-0 to advanced usage
## todo: REFACTOR and RESTRUCTURE this file

1. `pip list` / `condo list` to view all the libraries installed 
2. `cat ~/.bashrc` to print the content of bashrc file (`cat` syntax is used for printing). Another example: `$ cat ~/.ssh/id_rsa.pub`
3. `conda info —envs` to list out all the conda environments
4. conda info to view all the details of condo version
5. rm -r <dir name> or rmdir -p <dir name> to delete the directory and all its content
6. rmdir <dir name> to delete the empty directory
7. cd .. to go one level up in the directory
8. To check what directories are in your $PATH, you can use either the printenv or echo command:
	$echo $PATH 
	-or-
	$printenv (more descriptive)
9. Adding directory to the PATH environment variable (here: ~/anaconda3/bin)
	$ export PATH=~/anaconda3/bin:$PATH
10. Use tmux to get into the environment such that the EC2 session doesn’t terminate automatically. And type tmux kill-session to get out of the tmux session.
11. Checking whether the GPU is being used: nvidia-smi -h to see all the options. For checking the GPU utilisation: nvidia-smi -i 0 -l -q -d UTILIZATION other way is $ watch -n 0.1 nvidia-smi (results update every 0.1 seconds)
12. Copying file from local machine to the ec2 instance: scp -i an_ec2_key.pem cudnn-10.0-linux-x64-v7.5.1.10.tgz ubuntu@ec2-3-23-99-4.us-east-2.compute.amazonaws.com:~/cudnn_dir [here, cudnn_dir is the directory in the instance where you want to copy the file]: look https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/ for more information. For sending entire directory use scp -i key.pem -r /path/to/directory ubuntu@….:~/path/to/paste/in/ec2
13. To download a file from ec2: scp -i ~/Downloads/an_ec2_key.pem ubuntu@ec2-18-219-215-56.us-east-2.compute.amazonaws.com:~/output_df.csv ~/Desktop {after <:> file in the ec2 and then the location where the file will be downloaded in the local machine}
14. The SSH keys are stored in .ssh directory. In order to view the content: $ cd /.ssh and the ls to view.
15. In order to find the size of file: ls -lh <filename> [for more info: https://stackoverflow.com/questions/11720079/how-can-i-see-the-size-of-files-and-directories-in-linux] 
	OR $du -sh <filename>
16. To kill the task running in any port use: kill -9 $(sudo lsof -t -i:8888). $sudo lsof -t -i:8888 lists the task running in the port specified. Better way is to run `$ ps all` and get the PID number associated with the process and then run $ sudo kill -9 <PID>
17. To copy the content of the ssh file to the clipboard: $ pbcopy < ~/.ssh/id_ed25519.pub (here the content of id_ed25519 is being copied)
18. To see the list of held packages use: apt-mark showhold (try sudo, if this doesn’t work). To un-hold the packages use: sudo apt-mark unhold <package name>. Another way is to use ‘aptitude’ package: sudo apt-get install aptitude, and then sudo aptitude install myNewPackage (for more information: https://cutt.ly/njDNDgN)
19. To create a git branch use `$ git checkout -b <new-branch-name>`
20. To delete a branch remotely and locally, follow the link: https://stackoverflow.com/questions/2003505/how-do-i-delete-a-git-branch-locally-and-remotely 
    1. $ git push -d <remote_name> <branch_name> (remote_name=origin, -D instead of -d for force delete)
    2. $ git branch -d <branch_name>
21. To check whether a branch exists already, use the command: git rev-parse --verify <branch_name>
22. Task manager in the terminal: $ top. Better version is $ htop, it is not preinstalled. 
23. To check whether a git brach exists locally use: git show-ref --verify refs/heads/<branch-name>, also another way: git rev-parse --verify <branch_name>. And the shell scripting way: https://dev.to/iridiumcao/how-to-check-if-a-git-branch-exists-in-the-local-remote-repository-3gkd 
24. While installing the python libraries, sometimes we encounter `contradicting packages` error, it looks like “INFO: pip is looking at multiple versions of <package name> to determine which version is compatible with other requirements.”. Use  `—use-deprecated=legacy-resolver` to install the package. Ex.: $ pip install --use-deprecated=legacy-resolver -i https://pypi.toyotaconnected.net/simple/ tomo==3.2.5
25. To install a python package from custom cloud like TCIN’s use: pip install -i https://pypi.toyotaconnected.net/simple/ <package_name>. And to install the package from default pypi cloud use pip install -i https://pypi.python.org/simple <package_name> 
26. To update the local master with remote master: https://stackoverflow.com/questions/36540645/updating-local-master-with-remote-master 
27. Purge clean the virtual environment: pip freeze | xargs pip uninstall -y
28. Installing the package based on version conditions: [Ex.] pip install numpy<0.7.0,>=0.6.
29. Move or rename a file/ directory: mv <existing location/name> <new location/ name>. This command can be used to move or rename a file or directory
30. Clearing the pip cache (for installing the desired version of packages and removing the previous installations): https://stackoverflow.com/questions/9510474/removing-pips-cache 
31. To change the commit message use: $ git commit —amend (this open the terminal editor, make changes and save)
32. Look inside a pod: kubectl -n kubeflow get pods | grep -i <pipeline name>. Using (-i) for case insensitive search
33. Opening a shell in the running pod: kubectl -n kubeflow exec -it <pod name> — /bin/bash (OR) — sh
34. Find a file using terminal: https://winaero.com/find-files-linux-terminal/ , https://www.cyberciti.biz/faq/linux-how-can-i-find-a-file-on-my-system/ 
    1. find /etc -type f -name file1.txt [look for file1.txt in /etc dir, use `.` to check everywhere]
35. check whether a file exists using shell script: https://linuxize.com/post/bash-check-if-file-exists/ 
36. if after running `make build` we face `no space available error` then run `docker system prune` command. To remove all the images in local machine use `$ docker system prune -a`
37. For moving a file from one location to another: import shutil and then shutil.move("path/to/current/file", "path/to/new/destination/for/file")
38. Changing the default version of Python: https://dev.to/meetsohail/change-the-python3-default-version-in-ubuntu-1ekb 
39. To un-commit the changes after staging the files: `$ git rm -r —cached <filename/ or . for all files>`. 
40. To undo the one last commit with `$ git reset —soft HEAD~1`. Number of commits can be altered.
41. To pull a branch from origin/master: 
    1. if it exists in local already: `$ git switch <branch name>`
    2. if it does not exists, then: `$ git fetch <remote> <rbranch>:<lbranch>` and `$ git checkout <lbranch>`
    3. https://stackoverflow.com/questions/9537392/git-fetch-remote-branch 
42. Aggregated one shot commit (squashing all commits into one)
    1. git checkout yourBranch
    2. git reset $(git merge-base master $(git rev-parse --abbrev-ref HEAD))
    3. git add -A
    4. git commit -m "one commit on yourBranch"
    5. https://stackoverflow.com/questions/25356810/git-how-to-squash-all-commits-on-branch
43. Installing vim in pod: $ (sudo) apt install vim
44. To get the directory tree in the terminal: 
    1. Install tree module:`$ sudo apt-get install tree`
    2. Use this command to get the tree: `$ tree /path/to/folder`
45. To count the number of files in the current directory use: ls -1 | wc -l
46. To get the list of ipykernels:  jupyter kernelspec list
    1. to delete a kernel from jupyter notebook: jupyter kernelspec uninstall <kernel-name>
    2. to add a kernel:
        1. pip install ipykernel
        2. python -m ipykernel install --prefix="/home/ubuntu/anaconda3/envs/fine-tune" —name=<name_of_virtual_env>  [prefix: path till conda env]
47. If jupyter notebook fails to load in EC2: `conda update jupyter_core jupyter_client`
    1. Also try to update the extensions:
        1. pip install jupyter_contrib_nbextensions
        2. jupyter contrib nbextension install
        3. Link: https://www.analyticsvidhya.com/blog/2022/02/11-extensions-to-power-up-your-jupyter-notebook/ 
48. Find the version and release of Ubuntu in Ec2: `$ lsb_release -a`
49. To know about the hardware properties in Ubuntu: `$ sudo lshw -C display`
50. Find and remove all .DS_Store files/ dirs from project: `$ find . -name .DS_Store -print0 | xargs -0 git rm –f --ignore-unmatch`
51. Get the list of extensions installed in jupyter lab:
    1. jupyter labextension list
    2. full list can be found here: https://github.com/topics/jupyterlab-extension
    3. Reference official doc: https://jupyterlab.readthedocs.io/en/stable/user/extensions.html 
    4. Installing an extension: jupyter labextension install my-extension
    5. Uninstalling an extension: jupyter labextension uninstall my-extension
    6. Enabling an extension: jupyter labextension enable my-extension
    7. Disabling an extension: jupyter labextension disable my-extension
52. Like `pip freeze`, getting the environment.yml file for conda environment: 
    1. `conda env export -f environment.yml -n gpu-test` [where gpu-test is the name of conda env. Dumps the file in the same directory from where this command is run]
    2. to create a new conda env using environment.yml file: `conda env create --name <conda-env-name> --file=environment.yml`
    3. also check use of different flags in `conda create —help`
53. For module import error or module not found error: $ export PYTHONPATH="${PYTHONPATH}:/path/to/your/project/“ [run this from 1 level above project root]
54. To find the details of OS and distribution: `cat /etc/*release` or `cat /etc/os-release` or `lsb_release -d`
	1. to get the kernel version: `uname -r`
	2. to get the system architecture info: `uname -m`
54. `Got permission denied while trying to connect to the Docker daemon socket at unix….. connect: permission denied` > docker error. 
    1. scenario: newly installed docker + $ docker image ls
    2. Resolution:
        1. sudo groupadd docker
        2. sudo usermod -a -G docker [user] (here [user] is ubuntu)
        3. newgrp docker
        4. for more info refer: https://docs.docker.com/engine/install/linux-postinstall
55. Copying the file from docker to local: docker cp <containerId>:/file/path/within/container /host/path/target
    1. https://stackoverflow.com/questions/22049212/copying-files-from-docker-container-to-host 
56. Validate JSON using Python
    1. Cereberus (https://github.com/pyeve/cerberus)
    2. Jsonschema (https://github.com/python-jsonschema/jsonschema)
    3. Schema (https://github.com/keleshev/schema)
57. In order to remove a commit from Gitlab and revert to older version:
    1. git reset --hard <commit-id-from-git>
    2. git status (for checking)
    3. git push -f origin <name-of-branch> 
58. To check the remaining space in Ubuntu system: `df -h`