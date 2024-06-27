# Subject

we want to setup a `controller node`, and 2 `managed nodes`, and configure our `controller node` to be able to connect to `managed nodes` by ssh key;

the we want to install `nginx` in managed nodes from `controller_node` with the help of playbook. so we will do the following steps:

1. setup 2 `managed nodes`.
2. setup `controller node`.
3. setup ssh key in `controller node`.
4. create a host file in `controllel node`.
5. test the ping of `controller node` to `managed nodes`.
6. uninstall `nginx` from managed nodes.
7. create a playbook named `package-nginx.yaml`.
8. install `nginx` in managed nodes.



**Caution:** for steps 1 to 5 refer to link `https://github.com/hamedvalizadeh/ansible-tutorial/blob/master/Sample-Scenarios/01_Setup_A_Simple_Inventory.md`.



# Uninstall Nginx

to be sure that managed `nginx` is installed or not in maned nodes, execute the following command in each of them:

```powershell
sudo apt-cache policy nginx
```



if it was installed, execute the following command to uninstall it:

```powershell
sudo apt purge nginx
```



# Create Playbook

first create a directory named `ansible_nginx_prj` and navigate to it by executing following command:

```powershell
sudo mkdir ansible_nginx_prj
sudo cd ansible_nginx_prj
```

 

then create a file file named `package-nginx.yaml` and paste the following content to it:

```powershell
---
- name: installing unzip package
  hosts: all
  tasks:
    - name: Install package
      yum:
        name: nginx
        state: latest
```



**HINT:** value of `hosts` refers to the `all` group declared inside `hosts` file in `inventory` directory inside `ansible_nginx_prj`. if this file does not exists, it refers to the default path `/etc/ansible/hosts`.



# Install Nginx

now we can install `nginx` in our managed nodes from controller node; but before installing, it is good idea to check the syntax of our playbook to find if there is any error inside it. so execute the following command:

```powershell
sudo ansible-playbook package-nginx.yaml --syntax-check
```

 

if there is no syntax error in the file, we should see the following message:

```powershell
playbook: package-nginx.yaml
```



after checking the syntax we can run our playbook to install `nginx` in managed nodes, as follow:

```powershell
sudo ansible-playbook package-nginx.yaml -u hamed --become --ask-become-pass
```



the above command will prompt to ask the password of the the user `hamed`, and then will install the `nginx` package in managed nodes.



**HINT:** the option `--become` means to run this command on managed nodes as `root` user. it will do the job if the user `hamed` is member of `sudoers` group.

