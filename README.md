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

Commands for checking in ansible if connection is working fine or not:

ansible -i hosts --list-hosts web  #Command for checking all the hosts on the web group.

ansible -i hosts --private-key=/home/centos/devops -m ping web #Command for chekcing conenction between hosts of web group.


################################################################

Running playbooks:

1) Change IP's in hosts/inventory file according to your worker nodes.

2) you can run playbooks by using below command.

    ansible-playbook --private-key=<key-file Location> -i hosts <playbook_name>
  
    Example: In my case I had key file in /home/centos/devops
  
    ansible-playbook --private-key=/home/centos/devops -i hosts 01-print-message.yml
