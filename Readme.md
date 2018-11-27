Ansible Primer

Step 1: Get the Vagrantfile and run the below commands:
vagrant plugin install vagrant-hostmanager - Install the plugin
vagrant up - Setup the infrastructure
vagrant ssh - Connect to the control Node

Step 2: Setup the cluster with appropriate alias names in each node's bashrc file
alias bashrc='vim ~/.bashrc'
alias sbash='source ~/.bashrc'
alias pb='cd ~/ansible/playbook'
alias ans='cd ~/ansible'
alias control='ssh 192.168.136.10'
alias lb01='ssh 192.168.136.101'
alias app01='ssh 192.168.136.111'
alias app02='ssh 192.168.136.112'
alias db01='ssh 192.168.136.121'

Step 3: Change each node to the appropriate hostname using
sudo hostname <host_name>
Eg: sudo hostname control

Step 4: Setup Ansible on control Node
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible

Sanity Check: ansible --version

Step 5: Setup Custom Ansible config and inventory details
mkdir ansible
cd ansible
Copy the ansible.cfg and dev file into this folder

Sanity Checks and few commands:
-Sanity Checking
ansible -m ping all

-List Hosts
ansible --list-hosts all
ansible --list-hosts webserver - Hosts under a group
ansible --list-hosts \!control - Everything other than group control

-Run Command on each server
ansible -m command -a 'echo Hi' all

Step 6: Setup loadbalancer, control, webservers using yaml file
Command: ansible-playbook <YAML File>
This has to be run in the folder where the ansible config file is present
