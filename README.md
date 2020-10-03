# ansible

Generating key's in master and adding publick key to worker/agent nodes.

*********************MASTER SERVER*********************

centos@Master ~$ pwd

/home/centos

centos@Master ~$ ssh-keygen -f devops  

#press enter and then enter then publick key will generate in devops.pub file and private key will generate in devops file.

#Publick key needs to share or add in worker/agent nodes.

centos@Master ~$ cat devops.pub

#Copy content in pub file

*********************WORKER/AGENT SERVER*********************

centos@Worker ~$ pwd

/home/centos

centos@Worker ~$ cd .ssh

centos@Worker ~$ vi authorized_keys

#Paste the content which you coppied from master server devops.pub file.

*********************MASTER SERVER*********************

centos@Master ~$pwd

/home/centos

centos@Master ~$ ssh -i devops <workerip>


#You should able to conenct without any password.

################################################################

Change IP's in hosts/inventory file according to your worker nodes.

Commands for checking in ansible if connection is working fine or not.

#Command for checking all the hosts on the web group:

ansible -i hosts --list-hosts web

#Command for chekcing conenction between hosts of web group:

ansible -i hosts --private-key=/home/centos/devops -m ping web


################################################################

Running playbooks:

1) Change IP's in hosts/inventory file according to your worker nodes.

2) you can run playbooks by using below command.

    ansible-playbook --private-key=<key-file Location> -i hosts <playbook_name>
  
    Example: In my case I had key file in /home/centos/devops
  
    ansible-playbook --private-key=/home/centos/devops -i hosts 01-print-message.yml
    
# Role directory structure:

roles/
    common/
        tasks/
        handlers/
        library/
        files/
        templates/
        vars/
        defaults/
        meta/
    webservers/
        tasks/
        defaults/
        meta/
        
By default Ansible will look in each directory within a role for a main.yml file for relevant content (also main.yaml and main):

1) tasks/main.yml - the main list of tasks that the role executes.

2) handlers/main.yml - handlers, which may be used within or outside this role.

3) library/my_module.py - modules, which may be used within this role (see Embedding modules and plugins in roles for more information).

4) defaults/main.yml - default variables for the role (see Using Variables for more information). These variables have the lowest priority of any variables available, and can be easily overridden by any other variable, including inventory variables.

5) vars/main.yml - other variables for the role (see Using Variables for more information).

6) files/main.yml - files that the role deploys.

7) templates/main.yml - templates that the role deploys.

8) meta/main.yml - metadata for the role, including role dependencies.
