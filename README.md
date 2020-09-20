# ansible

1) Change IP's in hosts/inventory file according to your worker nodes.

2) you can run playbooks by using below command.

    ansible-playbook --private-key=<key-file Location> -i hosts <playbook_name>
  
    Example: In my case I had key file in /root/devops
  
    ansible-playbook --private-key=/root/devops -i hosts 01-print-message.yml
