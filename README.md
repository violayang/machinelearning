# machinelearning###**Install Jupyter Notebook on Oracle VM compute**

Check python version on the OCI compute:
'''
$ python -V
'''
Install pip on vm compute: 
'''
$ sudo yum install python-pip
$ sudo pip install --upgrade pip
'''
Install Anaconda and Jupyter Notebook on vm compute, follow the steps in the blog:
https://blogs.oracle.com/securityde/oci-mit-jupyter
'''
$ mkdir anaconda
$ cd anaconda
$ wget https://repo.anaconda.com/archive/Anaconda3-5.3.0-Linux-x86_64.sh
$ bash ~/anaconda/Anaconda3-5.3.0-Linux-x86_64.sh
'''
> Follow the instructions

After finish config anaconda, source the .bashrc
'''
$ source ~/.bashrc
'''
Then finish config Jupyter Notebook
'''
$ jupyter notebook --generate-config
$ vi /home/opc/.jupyter/jupyter_notebook_config.py
'''
add the following lines at the beginning of jupyter_notebook_config.py
'''
   c = get_config()
   c.NotebookApp.ip = '*'
   c.NotebookApp.open_browser = False
   c.NotebookApp.port = xxxx
'''

Generate password for Jupyter Notebook 
'''
$ jupyter notebook password
'''
> Follow the instructions

Open port on firewall rules:
'''
$ sudo firewall-cmd --state
$ sudo firewall-cmd --list-all
$ sudo firewall-cmd --permanent --add-port=xxxx/tcp
$ sudo firewall-cmd --reload
$ sudo firewall-cmd --state
$ sudo firewall-cmd --list-all
'''

Be default, Jupyter Notebook uses port 8888, user can also launch Jupyter Notebook at a different port by define the port: 
'''
$ jupyter notebook --port=xxxx
'''
Make sure on the security list for the subnet, the port you're using has stateful engress rule allows traffic to come in.

