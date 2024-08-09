# 7. High Performance Computing   
## High Performance Computing (HPC) Cluster Login   

on Mac, open Terminal:

~~~
## ex) ssh janedoe@ssh.eri.ucsb.edu  
ssh {your_username}@ssh.{host}
{your_pwd}   
## ex) ssh janedoe@bellows.eri.ucsb.edu  
ssh {your_username}@{hpc_machine}.{host}
{your_pwd}   
~~~

Windows Applications:  
* Putty  
* MobaXterm (*personal preference: nice GUI*)  


## Linux Commands   

- Press tab-tab following a command (such as ```cd```: change directory , ```ls```: list files, or ```vim```: to launch text editor) will list all possible files/folders and autofill if there's only one match   
- Enter ```pwd```: print working directory to have that path in the terminal to easily copy + paste it later    
- ```|```   : pipe that takes first command's output and feeds it into the command after the pipe    
- ```*``` : wildcard matching any character    

<b>List</b> ```-l``` long list, sorted by last modified time ```- t```, reversed ```- r``` --  so the last edited file is printed in the terminal last:  
> ls -ltr  

<b>List</b> two last modified files:  
> ls -ltr | tail -2

<b>Size</b> of current directory:  
> du -sh .

<b>Files sorted based on size</b>:  
> du -sh -- * | sort -rh  

<b>Count</b> number of files in current directory:  
> ls | wc -l  

<b>Count</b> number of files in directory (that start with ```004```):   
> ls -dq 004* | wc -l 

<b>Move </b> files that contain ```filterstring``` (in current dir) and move them into out_dir:  
> mv * filterstring * out_dir  

<b>Zip</b> files in ```in_dir```:     
> zip -r out_file.zip in_dir*

<b>Delete</b> files in current directory that start with ```S1_```:  
> find . -type f -name 'S1_*' -delete  
> find . -name gee -exec ls {} \;
> find . -name gee -exec rm -rf {} \;  

<b>Delete</b> files <i>recursively</i> in current directory that start with ```L3A_LC```):   
> find . -name 'L3A_LC*' -type f -exec rm -r {} +

<b>Delete</b> folders in current directory that match string (contain the string ```landsat```):  
> find . -name '* landsat *' -type d -exec rm -r {} +

---




## SLURM Workload Manager
SLURM handles which bash scripts, tasks, or jobs submitted by all users connected to a HPC cluster get sent to which nodes, and when.

These bash scripts must be located in a user's ```~/code/bash``` directory, and they may contain lines to activate virtual environments and run python scripts.  

Submit a bash script to SLURM: 
~~~
cd ~/code/bash 
sbatch {bash_script_name}.sh
~~~

Check on bash script progress from ```~/code/bash```:
~~~
squeue ## to make sure it's running and see how busy the cluster is    
ls -ltr ## print most recently edited file at the bottom, to copy last.err filename then paste after cat command in the following line      
cat last.err ## prints the contents of the last edited file, last.err, in the terminal   
~~~
  

---

