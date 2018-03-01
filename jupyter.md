#### Jupyter setup instruction on CentOS 7 VirtualBox

###### I. Create CentOS 7 virtualbox VM

a). Create a CentOS 7 virtualbox VM with two network interface(NAT and Host only Adapter).

b). Setup SSH server on the VM.

c). Login to VM from host machine to VM via ssh

###### II. Install package dependencies

a). Install epel repo

\# yum install -y https://dl.fedoraproject.org/pup/epel/x86_64/e/epel-release-7.8.noarch.rpm

\# yum install python-pip python-devel python-virtualenv

\# yum groupinstall 'Development Tools'

###### III. Install jupyter notebook

\# pip install jupyter

###### IV. Setup and Configure jupyter notebook

a). Gerenate a configuration file

\# jupyter notebook --generate-config

b). Generate a hashed password:

\# python -c 'from notebook.auth import passwd ; password = passwd() ; print password'

c). Configure hashed password in jupyter configuration file

\# vim /root/.jupter/jupyter_notebook_config.py

c.NotebookApp.password = u''

d). Generate self-signed certificate to use HTTPS

\# openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mykey.key -out mycert.pem

e). Configure Key and bind ip

\# vim /root/.jupter/jupyter_notebook_config.py

c.NotebookApp.ip = ''
c.NotebookApp.certfile = u''
c.NotebookApp.keyfile = u''
c.NotebookApp.open_browser = False

###### V. Confire firewall 

\# firewall-cmd --zone=public --add-port=8888/tcp --permanent

\# systemctl restart firewalld

###### VI. Start jupyter

\# jupyter notebook

