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
