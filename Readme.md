# Ansible Primer

# Day 1

## Step 1: Get the Vagrantfile and run the below commands:
vagrant plugin install vagrant-hostmanager - Install the plugin
vagrant up - Setup the infrastructure
vagrant ssh - Connect to the control Node

## Step 2: Setup the cluster with appropriate alias names in each node's bashrc file
alias bashrc='vim ~/.bashrc'
alias sbash='source ~/.bashrc'
alias pb='cd ~/ansible/playbook'
alias ans='cd ~/ansible'
alias control='ssh 192.168.136.10'
alias lb01='ssh 192.168.136.101'
alias app01='ssh 192.168.136.111'
alias app02='ssh 192.168.136.112'
alias db01='ssh 192.168.136.121'

## Step 3: Change each node to the appropriate hostname using
Edit the /etc/hostname file in each node
Then vagrant halt --> vagrant up

## Step 4: Setup Ansible on control Node
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible

Sanity Check: ansible --version

## Step 5: Setup Custom Ansible config and inventory details
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

## Step 6: Setup loadbalancer, control, webservers using yaml file
Command: ansible-playbook <YAML File>
This has to be run in the folder where the ansible config file is present

## Step 7: Prepare the maintainence yamls
maintainence yamls - help us perform sanity checks and perform some pre and post deployment actions
stop_stack.yml - Stops all the services running in the nodes
restart_stack.yml - Restarts the services in the nodes

## Step 8: Create the Python Demo Application
Copy the demo folder to the ansible folder of the control node

## Step 9: Configure the WebServer for the demo Application
1. Install the packages required for the demo Application
2. Modify the config and default site of the apache2 Server

## Step 10: Configure the loadbalancer for the demo application
1. Modify the config and the default site of the apache2 Server

## Step 11: Configure the database server for the demo application
1. Add db_user and demo database
2. Install python-mysqldb on WebServer and Database Server
3. Set the Listener ports

# Day 2
## Optimized Code and Refactoring to roles
### Roles - Group tasks according to functionality

## Step 1: Create a roles directory under the ansible folder
mkdir roles

## Step 2: Under the roles directory, run the below command

ansible-galaxy init <role_name>
For our demo application, we need 5 roles:
* nginx
* mysql
* apache2
* control
* demo_app

## Step 3: Restructure the yml files
Example:
Take all tasks from database-server-setup.yml and put them in mysql/tasks/main.yml
Take all handlers from database-server-setup.yml and put them in mysql/handlers/main.yml

## Step 4: Create a sites.yml file to include all the other yml files

## Step 5: Further optimize and refactor the code
1. Use defaults module in mysql
2. Using Variables

## Step 6: Install Ansible Tower
new folder - mkdir ansible-tower/
vagrant init ansible/tower
vagrant up -- provider virtualbox
vagrant ssh

# Day 3
## Other Optimizations
1. gather_facts
We will gather facts only when we need it. In this example, we use the gather facts data only for the mysql module. Load Balancer and Web Server do not need fact gathering. Hence we can set gather_facts: false

2. update_cache
Cache Update happens every time we run the playbook. We either use the cache_valid_time parameter to update the cache at periodic intervals

3. Tags
We can tag each task with a tag and then apply parameters at a tag level or run only specific tags. Eg: ansible-playbook sites.xml --tags "packages"

## Get only active sites
### Shell module
It will run a shell command and store the output in a register variable
