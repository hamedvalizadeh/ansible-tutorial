# What is it?

Ansible is an open source IT automation engine that automates provisioning, configuration management, application deployment, orchestration, and many other IT processes. 



for example it is possible to install applications, copy files, change configurations of some servers that are called `managed nodes`, from a server that is called `controller node`.



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