# What is it?

Ansible is an open source IT automation engine that automates provisioning, configuration management, application deployment, orchestration, and many other IT processes. 



for example it is possible to install applications, copy files, change configurations of some servers that are called `managed nodes`, from a server that is called `controller node`.



# Workflow

![](ansible-works.png)





# Key Terms in Ansible

- **Controller Machine** 
  - A task is a section that consists of a single procedure to be completed
  - This is where Ansible gets installed. The controller machine helps in enabling provisioning on servers we manage.
- **Inventory** 
  - This is basically an initializing file that contains information about the servers that we are managing.
- **Playbook** 
  - It is an organized unit of scripts defining an automated work for the configuration management of our server.
- **Task** 
  - A task block defines a single procedure to be executed on the server like installing packages.
- **Tag**
  - Name set to a task which can be used later on to issue just that specific task or group of tasks.
- **Handlers** 
  - Task which is called only if a notifier is present.
  - Handlers in Ansible are event-driven actions that execute specific tasks when triggered, ensuring precise and efficient responses within your automation workflows.

- **Notifier**
  - Section attributed to a task which calls a handler if the output is changed.

- **Roles** 
  - A way of organizing tasks and related files to be later called in a playbook
  - Roles in Ansible are like pre-packaged sets of instructions and configurations, simplifying complex automation tasks and ensuring consistency across projects.
- **Variables** 
  - In Ansible, variables act as dynamic substitutes, allowing you to customize automation by storing and manipulating data within playbooks and roles, enhancing adaptability to different system configurations.
- **Modules** 
  - Basically, a module is a command or set of similar Ansible commands meant to be executed on the client-side.
  - Modules in Ansible are task-specific tools that help automate various actions on remote servers, simplifying the execution of tasks like software installation, file management, and more.



# Ansible ad-hoc commands

One of the simplest ways Ansible can be used is by using ad-hoc commands. These can be used when you want to issue some commands on a server or a bunch of servers. Ad-hoc commands are not stored for future uses but represent a fast way to interact with the desired servers.



# Inventory

this is a file in which the connection information of the managed nodes are defined, and also this connections info are grouped and categorized.

by default ansible read this file from path `/etc/ansible/host`, but you can have your inventory file in each project directory separately. 

for example if you execute the following `ad-hoc` command, the default inventory is read:  

```powershell
sudo ansible all -m ping
```



but the following `ad-hoc` command read inventory from the path `/my-anisble-prj/hosts.yaml`:

```powershell
sudo ansible all -i /my-anisble-prj/hosts.yaml -m ping
```



# Facts

these are some meta data about managed nodes machines that are retrieved by controller node and saved as variables in controller node to be used in writing better playbooks.

for example when we know the OS, Architecture, and so many info about our managed nodes, we can use this info to have some roles and tasks based on them.

before running a playbook, by default`gether-fact` module runs and retrieve these information, that we can disable this behavior.  

also we can manually call the `setup` module to gather facts about our nodes. 

for example following `ad-hoc` command will retrieve facts of managed nodes of group `all` declared inside host file `inventory/hosts.yaml`:

```powershell
sudo ansible all -i inventory/hosts.yaml -m setup
```



following `ad-hoc` command will retrieve facts of managed nodes of group `hamed_group` declared inside host file `inventory/hosts.yaml`:

```powershell
sudo ansible hamed_group -i inventory/hosts.yaml -m setup
```



following `ad-hoc` command will retrieve facts about OS of managed nodes of group `hamed_group` declared inside host file `inventory/hosts.yaml`:

```powershell
sudo ansible hamed_group -i inventory/hosts.yaml -m setup -a "filter=ansible_os_family"
```

