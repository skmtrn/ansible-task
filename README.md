
## Description
This repository contains Ansible files allowing the deployment of the Docker Getting Started Todo app on a remote server using the provided docker-compose.yml file.


https://docs.docker.com/get-started/02_our_app/

The playbook was tested on a bare Azure VM with Ubuntu 20.04 LTS OS.
The repo consists of:

 - playbook.yml - contains the playbook itself,
 - inventory.yml - contains the inventory with an app_port variable declared, which will specify the port that the app will serve on on the docker host, 
 - docker-compose.yml.j2 -  contains the jinja2 template for docker-compose
   file.

## Notes:

 - **docker_compose Ansible module limitations**
   
   As with tasks' intent, I wanted to keep the original
   docker-compose.yml config provided by docker tutorial. It has a
   hardcoded volume mount of "./:/app". In order to mount current
   directory, I have to store the docker-compose.yml there. Due to
   ansible docker_compose module limitations, I cannot keep the
   docker-compose.yml and workdir (actual pwd workdir) separate. Hence,
   docker-compose.yml unnecessary gets mounted into actual app
   container.
   
   This is unintended and would be unsafe in real life, because
   docker-compose.yml could hold protected values like passwords to DBS.
   
   A workaround would be to not use the docker_compose Ansible module
   and instead just run the shell commands, but it may defeat the
   purpose of using Ansible in the first place (the whole playbook might
   become a shell script wrapped in yaml).
   It is also worth noting that the said ansible module works only with docker_compose v1, hence the latest, non-2 version was    specified in the notebook.
   

 - **usage of the jinja2 template**

   To comply with the instructions' specification that "the port in which the
   application runs on the target virtual machine should be configurable
   via the inventory." a jinja2 template was used.
   
   Another possibility would be to use sed-like
   replace-the-line-in-a-file Ansible module, but template felt more
   elegant to me and allows further customization in the future.
                 
  - **pip modules**
	Ansible's docker_compose module requires docker and docker-compose pip packages installed.
	Also, due to the crypto.py and pyopenssl bug described [here](https://github.com/pyca/pyopenssl/issues/1143) (it renders pip3 unusuable) the pyopenssl has to be installed in the latest version.

